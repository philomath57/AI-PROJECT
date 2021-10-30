# AI-PROJECT
The program consists of lines of code to perform AI operations such as wishing, opening Wikipedia, opening YouTube and many more
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
print(voices[1].id)
engine.setProperty('voice',voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>0 and hour<12:
        speak("Good Morning")
    elif hour<=12 and hour<18:
        speak("Good Afternoon")
    else:
        speak("Good Evening")
    speak("I am Zira, speed 1 terabyte robo, how may I help you sir")
def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognizing....")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}")
    except Exception as e:
        print(e)

        print("I did not recognized you, please say that again")
        return "None"
    return query
if __name__ == '__main__':
    wishMe()
while True:

    query = takeCommand().lower()
    
    
    if 'wikipedia' in query:
      speak ('Searching....)
      query = query.replace('wikipedia','')
      result = wikipedia.summary(query,sentences = 2)
      speak = ("As per the wikipedia")
      speak (result)
    elif 'open youtube' in query:
      webbrowser.open("youtube.com")
