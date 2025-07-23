import speech_recognition as sr
import pyttsx3
import datetime

# Initialize speech engine
engine = pyttsx3.init()
recognizer = sr.Recognizer()

def speak(text):
    print("Assistant:", text)
    engine.say(text)
    engine.runAndWait()

def get_command():
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
        try:
            command = recognizer.recognize_google(audio)
            print("You said:", command)
            return command.lower()
        except:
            speak("Sorry, I didn't catch that.")
            return ""

def run_assistant():
    speak("Hello! I am your assistant. Say 'time' to know the time or 'exit' to quit.")
    while True:
        command = get_command()
        if "time" in command:
            time = datetime.datetime.now().strftime('%I:%M %p')
            speak(f"The current time is {time}")
        elif "exit" in command or "stop" in command:
            speak("Goodbye!")
            break
        else:
            speak("Please say a valid command.")

if __name__ == "__main__":
    print("Script started...")
    run_assistant()
