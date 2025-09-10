# AutoBrief-(AB)-Agentic-AI

AutoBriefing Agentic AI
This project implements an Agentic AI system that provides automated morning briefings. It fetches real-time data for weather, air quality, and AI tech news for a specified location, summarizes it using a Generative AI model, and converts the summary into spoken audio. The project includes components for wake word detection and speech recognition to potentially integrate voice activation.

Prerequisites
To run this project, you will need:
Python 3.7+

Libraries:
  google-search-results
  geocoder
  requests
  google-generativeai
  gTTS
  IPython.display
  pvporcupine (requires a Porcupine AccessKey)
  pyaudio
  speech_recognition
  
API Keys:
  SerpAPI Key
  WAQI API Token
  Google API Key (for Google Generative AI)
  
1. Installation
Copy the code into your Colab notebook.
Install the required libraries using pip

2. Data Fetching Functions
get_weather(location): This function uses SerpAPI to fetch current weather data for the specified location. It extracts key information like temperature, condition, precipitation, humidity, and wind from the search results.
get_air_quality(location): This function first attempts to get air quality data from the WAQI API. If that fails, it uses SerpAPI to search for AQI data and extracts relevant information from the search results.
get_tech_news(): This function uses SerpAPI to fetch the top 5 news headlines related to "Today's top AI tech company news". It formats the headlines as a bulleted list with links.

3. Summarization and Text-to-Speech
summarize_with_gemini(briefing_json): This function takes the fetched data (weather, air quality, news) in JSON format. It constructs a detailed prompt for the Gemini 2.5 Flash model, instructing it to generate a friendly, structured morning briefing that includes the date, weather details (with rain warning if applicable), air quality information (including AQI category and suggested actions), and a summary of the top AI tech news headlines.
text_to_speech(summary_text, filename="morning_briefing.mp3"): This function uses the gTTS library to convert the generated text summary into an audio file (MP3 format) and saves it. It then returns an IPython audio object for playback in the notebook environment.

4. MorningBriefingAgent Class
MorningBriefingAgent: This class encapsulates the briefing logic.
__init__(): Initializes the agent with a memory dictionary to store fetched data.
run(): This is the main method that orchestrates the briefing process. It detects the location (currently hardcoded), calls the data fetching functions, stores the results in self.memory, structures the data into a JSON-like format, calls summarize_with_gemini to get the briefing text, prints the text, calls text_to_speech to generate the audio, and displays the audio.

5. Wake Word Detection (Optional Integration)
This section includes code snippets for wake word detection using the pvporcupine library. This part is intended for integrating voice activation, allowing the system to start listening for commands when a specific wake word ("hey ab" in this example) is spoken. Note: Full integration requires additional code to continuously listen for the wake word and trigger the subsequent steps.

6. Speech Recognition (Optional Integration)
This section includes a code snippet using the speech_recognition library to convert spoken audio captured from a microphone into text commands. This is another component for enabling voice interaction with the agent. Note: Full integration requires capturing audio after the wake word is detected and then processing it with this code.

7. Response Generation and Playback (Optional Integration)
This section demonstrates how to summarize the briefing and play the generated audio using gTTS and the os.system command (specifically afplay for macOS). This part would be triggered after a command is recognized via speech recognition. Note: The os.system command might need to be adjusted based on your operating system.

How to Run
Ensure you have installed all prerequisites and set up your API keys.
Replace the placeholder API keys in the code with your actual keys.
You can run the notebook cells sequentially to execute the briefing agent and generate the audio.
To implement the wake word detection and speech recognition for voice activation, you will need to integrate the provided code snippets into a continuous listening loop, which is not fully implemented in the current sequential notebook structure.

Future Improvements
Implement a continuous listening loop for wake word detection and speech recognition.
Allow the user to specify the location via voice command.
Add support for more news categories or data sources.
Improve error handling and provide more user-friendly feedback.
Package the project as a standalone application.
