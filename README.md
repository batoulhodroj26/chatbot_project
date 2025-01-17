# chatbot_project
#main
# main.py
import gradio as gr
from data_loader import load_data  # Import the load_data function from data_loader.py
from chatbot import generate_response  # Import the generate_response function from chatbot.py

def process_data(file_path):
    """Load and process the data from the provided file path."""
    data = load_data(file_path)
    if data is None:
        return "No data loaded. Please check the file path."
    return data

def chatbot_interface():
    """Create a Gradio interface for the chatbot."""
    # Load your data file (adjust the path to your actual file location)
    data = process_data("C:/Users/admin/OneDrive - Beirut Arab University/Documents/chatbot_project/chatbot_data.txt")  # Adjust path if needed

    # Gradio interface setup
    interface = gr.Interface(
        fn=lambda query: generate_response(query, data),  # Function to handle queries
        inputs=gr.Textbox(label="Ask a question"),  # User's query input
        outputs=gr.Textbox(label="Chatbot Response")  # The chatbot's response
    )

    # Launch the interface
    interface.launch(share=True)  # This will create a public link

# Run the chatbot interface when the script is executed
if __name__ == "__main__":
    chatbot_interface()


------------------------------------------------------
# data_loader.py

def load_data(file_path):
    """Load data from the provided file path."""
    try:
        with open(file_path, 'r', encoding='utf-8') as file:
            data = file.read()
        return data
    except FileNotFoundError:
        print(f"Error: The file {file_path} was not found.")
        return None
    except Exception as e:
        print(f"Error: An error occurred while loading the file. {e}")
        return None

        -------------------------------------------------------------------------
  #chatbot.py
  def generate_response(query, data):
    """Generate a response based on the user's query and loaded data."""
    
    # Simple matching logic: if the query contains any word found in the data, respond with relevant info
    query = query.lower()

    # Check for keywords in the data and provide the corresponding answer
    if 'ai' in query or 'artificial intelligence' in query:
        return "AI stands for Artificial Intelligence, which refers to the simulation of human intelligence in machines."

    elif 'machine learning' in query:
        return "Machine learning is a subset of AI that involves training machines to recognize patterns in data."

    elif 'natural language processing' in query or 'nlp' in query:
        return "Natural language processing (NLP) enables machines to understand, interpret, and respond to human language."

    elif 'robotics' in query:
        return "Robotics involves the design, construction, and use of robots."

    elif 'reinforcement learning' in query:
        return "Reinforcement learning is a type of machine learning where agents learn to make decisions by receiving rewards or penalties."

    else:
        return "I'm sorry, I couldn't find relevant information in the data."
