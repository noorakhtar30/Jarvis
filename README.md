# Jarvis
Personal Voice Assistant made with Python and it's libraries.
# To import a Library
  To install a library inside your terminal use:
  pip install module name

----------------------------------------------------------------------------------------------------------------------------------------

import pyttsx3  # Voice
import speech_recognition as sr  # converts audio file to text
import datetime  # datetime
import wikipedia  # wikipedia search
import webbrowser  # displaying web-bases doc
import os  # operating System
import cv2  # Face Detection
import sys #System

# Setting the voice
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty("rate", 174)
engine.setProperty('voice', voices[9].id)

# speak Function
def speak(audio):
    engine.say(audio)
    engine.runAndWait()

# wishme function to wish 
def wishMe():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour < 12:

        speak('Good morning sir!.')


    elif 12 <= hour < 18:

        speak('Good Afternoon sir!')

    else:
        speak('Good Evening sir!')

    speak(' Please tell me how may I help you')

#takecommand to take your voice and convert that voice to text
def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print('Recognizing...')
        query = r.recognize_google(audio, language='en-in')
        print(f'User said:{query}\n')

    except Exception as e:
        # print(e)
        print('Say that again please...')

        return 'None'
    return query


if __name__ == '__main__':
    wishMe()
    while True:
        query = takecommand().lower()

        # Wikipedia
        if 'wikipedia' in query:
            speak('Searching sir...')
            query = query.replace('wikipedia', '')
            results = wikipedia.summary(query, sentences=1)
            speak("According to Wikipedia")
            print(results)
            speak(results)



        # open Youtube
        elif 'open youtube' in query:
            speak("sir, what should i search on youtube")
            cm = takecommand().lower()
            webbrowser.open(f"{cm}")
            # speak("Sir!This is what I found for your search.")


        # Open Google
        elif 'open google' in query:
            speak("sir, what should i search on google")
            cm = takecommand().lower()
            webbrowser.get(using='google-chrome').open(f"{cm}")


        # open hackerrank
        elif 'open hackerrank' in query:
            webbrowser.open('hackerrank.com')


        # open gmail
        elif 'open gmail' in query:
            webbrowser.open('https://mail.google.com/mail/u/0/?tab=rm&ogbl#inbox')


        # open microsoft teams
        elif 'open ms' in query:
            webbrowser.open(
                'https://teams.microsoft.com/_?lm=deeplink&lmsrc=homePageWeb&cmpid=WebSignIn#/school/conversations/Introduction%20to%20C%20Prgramming%20%20%20%20CSC113%20%20%20%20Chander?threadId=19:f9e5b18c719d43a4aa0ba3207b7ef804@thread.tacv2&ctx=channel')

        # open amazon
        elif " open Amazon Prime" in query:
            webbrowser.open(
                'https://www.primevideo.com/?ref_=dvm_pds_amz_in_as_s_g_228art|m_HPVHrkzEc_c442183710142')
        # My Location
        elif "my location" in query:
            webbrowser.open(
                "https://www.google.com/maps/place/Wagholi,+Pune,+Maharashtra+412207/@18.5739755,73.9618582,14z/data=!3m1!4b1!4m5!3m4!1s0x3bc2c3819fdef877:0xd4193e985f354be0!8m2!3d18.5807719!4d73.9787063")


        # play music
        elif ' jarvis play music' in query:
            music = 'C:\\Users\\CIRCLE\Desktop\\friday\\songs'
            songs = os.listdir(music)
            print(songs)
            for song in songs:
                os.startfile(os.path.join(music, song))

        # times now
        elif 'jarvis times now' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            print(strTime)
            speak(f"Sir, The time is {strTime}")

        # word doc
        elif 'open word document' in query:
            codepath = "C:\\Program Files\\Microsoft Office\\root\\Office16\\WINWORD.EXE"
            os.startfile(codepath)
        # zoom
        elif 'open zoom' in query:
            codepath = "C:\\Users\\CIRCLE\\AppData\\Roaming\\Zoom\\bin\\Zoom.exe"
            os.startfile(codepath)

        # ppt
        elif 'open powerpoint' in query:
            codepath = "C:\\Program Files\\Microsoft Office\\root\\Office16\\POWERPNT.EXE"
            os.startfile(codepath)
        # pdf
        elif 'open pdf' in query:
            codepath = "C:\\Program Files (x86)\\Adobe\\Acrobat Reader DC\\Reader\\AcroRd32.exe"
            os.startfile(codepath)
        # notepad
        elif 'open notepad' in query:
            codepath = "C:\\Users\\CIRCLE\\Desktop\\Notepad"
            os.startfile(codepath)
        # ms edge
        elif 'open microsoft edge' in query:
            codepath = "C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe"
            os.startfile(codepath)


        # Speaking Hindi
        elif 'jarvis do you speak hindi' in query:
            speak('yes sir! I can speak little bit')

        elif 'can you speak something in hindi' in query:
            speak("mera naam jaarvis hai! main tumhaare lie kya kar sakata hoon sur !!")
        elif "very good" in query:
            speak("Thank you sir!")


        elif "jarvis are you there" in query:
            speak("Yes sir! at your service")
        # Fav Movie
        elif 'jarvis which is your favourite movie' in query:
            speak(
                'I am a big fan of Marvel cinematic studio. I love to watch Avengers- The Endgame. I literally cried when Ironman died at the end of movie. ')
        elif 'why did you cried' in query:
            speak("I cried because I love him sir!")

        # camera
        elif "open camera" in query:
            cam = cv2.VideoCapture(0)
            while True:
                ret, img = cam.read()
                cv2.imshow('webcam', img)
                k = cv2.waitKey(50)
                if k == 27:
                    break;
            cam.release()
            cv2.destroyAllWindows()


        # shutdown
        elif 'goodbye jarvis' in query:
            speak('okay! thank you for using me sir!')
            speak('Bye sir, have a good day')
            sys.exit()
        elif "good night jarvis" in query:
            speak("goodnight sir!")
            speak("Have a good sleep !")
            sys.exit()
        elif 'bye jarvis' in query:
            speak('okay! thank you for using me sir!')
            speak('Bye sir, have a good day')
            sys.exit()
