# create_a_chatbot_using_python

# Install ChatterBot and its dependencies:
# pip install chatterbot chatterbot_corpus flask

from chatterbot import ChatBot
from chatterbot.trainers import ChatterBotCorpusTrainer
from flask import Flask, request, jsonify

# Create a Flask web application
app = Flask(__name__)

# Initialize the chatbot
chatbot = ChatBot('CustomerServiceBot')

# Create a new trainer for the chatbot
trainer = ChatterBotCorpusTrainer(chatbot)

# Train the chatbot on the English language
trainer.train('chatterbot.corpus.english')

# Define a route for handling user queries
@app.route('/chat', methods=['POST'])
def chat():
    user_input = request.json['user_input']
   
    # Get a response from the chatbot
    response = chatbot.get_response(user_input)
   
    return jsonify({'response': str(response)})

if __name__ == '__main__':
    app.run(debug=True)
