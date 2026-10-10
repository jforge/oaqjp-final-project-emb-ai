from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")

def format_emotion_response(emotions: dict) -> str:
    dominant = emotions.get("dominant_emotion", "unknown")
    
    # Keep only the numeric emotion scores
    pairs = [(k, v) for k, v in emotions.items() if k != "dominant_emotion"]
    formatted = [f"'{k}': {v}" for k, v in pairs]
    
    if len(formatted) > 1:
        scores = ", ".join(formatted[:-1]) + " and " + formatted[-1]
    else:
        scores = formatted[0] if formatted else ""
    
    return (
        f"For the given statement, the system response is {scores}. "
        f"The dominant emotion is {dominant}."
    )

@app.route("/emotionDetector")
def emo_detector():
    text_to_analyze = request.args.get('textToAnalyze')

    response = emotion_detector(text_to_analyze)

    return format_emotion_response(response)

@app.route("/")
def render_index_page():
    return render_template('index.html')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
