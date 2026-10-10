from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")

@app.route("/emotionDetector")
def emotion_detector_route():
    # Get the text (supports both query param and JSON body)
    text_to_analyze = request.args.get("textToAnalyze", "")

    # Call the detector (it should return the emotions dict)
    emotions = emotion_detector(text_to_analyze)

    # Error handling: blank / invalid input
    if emotions.get("dominant_emotion") is None:
        return "Invalid text! Please try again!"

    # Build the normal response sentence
    dominant = emotions["dominant_emotion"]
    pairs = [(k, v) for k, v in emotions.items() if k != "dominant_emotion"]
    formatted = [f"'{k}': {v}" for k, v in pairs]

    if len(formatted) > 1:
        scores = ", ".join(formatted[:-1]) + " and " + formatted[-1]
    else:
        scores = formatted[0] if formatted else ""

    response_text = (
        f"For the given statement, the system response is {scores}. "
        f"The dominant emotion is {dominant}."
    )

    return response_text


@app.route("/")
def render_index_page():
    return render_template('index.html')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
