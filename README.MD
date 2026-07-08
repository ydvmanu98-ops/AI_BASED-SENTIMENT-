from flask import Flask, request, jsonify
from transformers import pipeline

app = Flask(__name__)
# Load sentiment analysis pipeline
sentiment_analyzer = pipeline("sentiment-analysis")

@app.route('/analyze', methods=['POST'])
def analyze():
    user_text = request.json.get("text")
    result = sentiment_analyzer(user_text)
    return jsonify(result)

if __name__ == '__main__':
    app.run(debug=True)
