# MyAssistant
import datetime
import pyttsx3
import speech_recognition as sr
import wikipedia
import webbrowser
import os

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voices',voices[0].id)


def speak(audio):   #speak function
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour=int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning")
    elif hour>=0 and hour<18:
        speak("Good Afternoon")
    else:
        speak("Good Evening")

    speak(" I am Assistant Sir. Please tell me how may i help you")
def takeCommand():
    # it takes microphone input from user and returns string output
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        sr.pause_threshold = 1
        audio = r.listen(source)

    try:
    
        print("Recognizing...")
        query = r.recognize_google(audio,Language='en-in')
        print(f"user said:{query}\n")   
    except Exception as e:
        print("Say that again please...")
        return"None"
    return query
if __name__ == "__main__":
    wishMe()
    takeCommand()
    #while True:
    if 1:
        query=takeCommand().lower() #query converted into lower case so can be matched easily

        #logic for executing task
        if 'wikipedia' in query:
           query = query.replace("wikipedia","")
           results = wikipedia.summary(query, sentence=2)
           speak("according to Wikipiedia")
           speak(results)
        elif 'open youtube ' in query:
            webbrowser.open("youtube.com")
        elif 'open google ' in query:
            webbrowser.open("google.com")
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Sir, the time is (strTime)")
