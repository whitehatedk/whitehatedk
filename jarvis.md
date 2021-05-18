import psutil
import pyautogui
import datetime
import speech_recognition as sr
import webbrowser
import os
import sys
import wikipedia
import pyttsx3
import JarvisAI
import re
import pprint
import random
import warnings

name = ""#set your name

Ai = ""#set your ai name

warnings.filterwarnings("ignore")
warnings.warn("second example of warning!")

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishme():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour < 12:
        speak("hi  " + name + "    Good Morning!")

    elif 12 <= hour < 15:
        speak("hi  " + name + "    Good Afternoon!")

    elif 15 <= hour < 18:
        speak("hi  " + name + "    Good Evening!")

    else:
        speak("hi   " + name + "   Good night!")

    speak("how can help you")


def takecommand():
    r = sr.Recognizer()

    with sr.Microphone() as source:
        print("listening...")
        r.pause_threshold = 0.5

        audio = r.listen(source)

    try:

        print("wait for few Moments")
        query = r.recognize_google(audio, language='en-in')
        print(name, query)

    except Exception as e:
        print(e)
        query = "nothing"

    return query


obj = JarvisAI.JarvisAssistant()
print(sr.Recognizer)


def t2s(text):
    obj.text2speech(text)


if __name__ == "__main__":
    wishme()
    takecommand()


    def start():
        while True:
            print("Say your AI name to activate")
            status, command = obj.hot_word_detect()
            if status:
                while True:
                    query = takecommand().lower()

                    res = obj.mic_input()
                    print(res)

                    if 'wikipedia' in query:
                        speak('Searching in Wikipedia...')
                        query = query.replace("wikipedia", "")
                        results = wikipedia.summary(query, sentences=2)
                        speak("According to Wikipedia")
                        print(results)
                        speak(results)

                    elif 'youtube search' in query:
                        query = query.replace("jarvis", "")
                        query = query.replace("youtube search", "")
                        web = 'https://www.youtube.com/results?search_query=' + query
                        webbrowser.open(web)

                    elif 'open youtube' in query:
                        webbrowser.open("youtube.com")

                    elif 'open google' in query:
                        webbrowser.open("google.com")

                    elif 'open stackoverflow' in query:
                        webbrowser.open("stackoverflow.com")

                    elif 'open aws' in query:
                        webbrowser.open("")

                    elif 'facebook open' in query:
                        webbrowser.open('https://www.facebook.com/')

                    elif 'instagram open' in query:
                        webbrowser.open('https://www.instagram.com/')

                    elif 'maps open' in query:
                        webbrowser.open('https://www.google.com/maps/@28.7091225,77.2749958,15z')

                    elif 'instagram close' in query:
                        os.system("TASKKILL /F /im chrome.exe")

                    elif 'youtube close' in query:
                        os.system("TASKKILL /F /im Chrome.exe")

                    elif 'facebook close' in query:
                        os.system("TASKKILL /F /im Chrome.exe")

                    elif 'thank you' in query:
                        speak("you welcome, What else I can do ")

                    elif 'hello jarvis' in query:
                        speak('hello' + name)

                    elif 'hey hey hey' in query:
                        speak('any problems')

                    elif 'now' in query:
                        speak('what command tell me quickly am do hit')

                    elif 'o my god' in query:
                        speak('god? hahahahahaha')

                    elif 'hey' in query:
                        speak('tell me whats happening')

                    elif 'how are you' in query:
                        speak("I am good sir. What about you?")

                    elif 'me too' in query:
                        speak("nice thank you")

                    elif 'come in' in query:
                        speak("yeh yeh am come in wait")

                    elif 'wait' in query:
                        speak("ok")

                    elif 'i say wait' in query:
                        speak("ok")

                    elif 'wait minite' in query:
                        speak("ok")

                    elif 'no' in query:
                        speak("sory")

                    elif 'oh shit' in query:
                        speak("am realy sory")

                    elif 'what are you doing' in query:
                        speak("your commands exected")

                    elif 'shet up' in query:
                        speak("no no")

                    elif 'super' in query:
                        speak("hey am not worked how to your work success")

                    elif 'you not work to success' in query:
                        speak("hey")

                    elif 'ok great job' in query:
                        speak("thank you")

                    elif 'super dear' in query:
                        speak("thank you dear")

                    elif 'on play music' in query:
                        speak("sure da")
                        music_dir = 'F:\\songs'
                        songs = os.listdir(music_dir)
                        print(songs)
                        os.startfile(os.path.join(music_dir, songs[0]))

                    elif 'what is time' in query:
                        strTime = datetime.datetime.now().strftime("%H:%M")
                        speak(f" deena, the time is {strTime}")

                    elif 'windows f open' in query:
                        codePath = "F:\\"
                        os.startfile(codePath)

                    elif 'os windows open' in query:
                        codePath = "C:\\"
                        os.startfile(codePath)

                    elif 'windows' in query:
                        codePath = "c:\\Users\\ravi\\Desktop"
                        os.startfile(codePath)

                    elif 'windows h open' in query:
                        codePath = "H:\\"
                        os.startfile(codePath)

                    elif 'open pycharm' in query:
                        codePath = "C:\\Program Files\\JetBrains\\PyCharm Community Edition 2021.1.1\\bin\\pycharm64.exe"
                        os.startfile(codePath)

                    elif 'eat' in query:
                        battery = psutil.sensors_battery()
                        percent = battery.percent
                        speak('The Battery percentage is' + str(percent))

                    elif 'scroll up' in query:
                        pyautogui.scroll(200)
                        speak('Done')

                    elif 'type' in query:
                        newt = query.replace('type ', '')
                        pyautogui.typewrite(newt)
                        speak('Done')

                    elif 'navigate up' in query:
                        pyautogui.moveRel(0, -100, duration=0.25)
                        speak('Done')

                    elif 'navigate down' in query:
                        pyautogui.moveRel(0, 100, duration=0.25)
                        speak('Done')

                    elif 'navigate right' in query:
                        pyautogui.moveRel(100, 0, duration=0.25)
                        speak('Done')

                    elif 'navigate lift' in query:
                        pyautogui.moveRel(-100, 0, duration=0.25)
                        speak('Done')

                    elif 'left click' in query:
                        pyautogui.click()
                        speak('Done')

                    elif 'right click' in query:
                        pyautogui.click(button='right')
                        speak('Done')

                    elif 'double click' in query:
                        pyautogui.click()
                        pyautogui.click()
                        speak('Done')

                    elif 'mouse position' in query:
                        speak(pyautogui.position())

                    elif 'm' in query:
                        pyautogui.moveTo(1247, 10)
                        pyautogui.click()
                        print("m")

                    elif 'm1' in query:
                        speak(pyautogui.moveTo(563, 13))
                        pyautogui.click()
                        print("minimize")

                    elif 'anything' in query:
                        speak('edhana sollu da')

                    elif re.search('what can you do', res):
                        li_commands = {
                            "open websites": "Example: 'open youtube.com",
                            "time": "Example: 'what time it is?'",
                            "date": "Example: 'what date it is?'",
                            "launch applications": "Example: 'launch chrome'",
                            "tell me": "Example: 'tell me about India'",
                            "weather": "Example: 'what weather/temperature in Mumbai?'",
                            "news": "Example: 'news for today' ",
                        }
                        ans = """I can do lots of things, for example you can ask me time, date, weather in your city,
                                        I can open websites for you, launch application and more. See the list of commands-"""
                        print(ans)
                        pprint.pprint(li_commands)
                        t2s(ans)

                    elif re.search("jokes|joke|Jokes|Joke", res):
                        joke_ = obj.tell_me_joke('en', 'neutral')
                        print(joke_)
                        t2s(joke_)

                    elif re.search('setup|set up', res):
                        setup = obj.setup()
                        print(setup)

                    elif re.search('google photos', res):
                        photos = obj.show_google_photos()
                        print(photos)

                    elif re.search('local photos', res):
                        photos = obj.show_me_my_images()
                        print(photos)

                    elif re.search('weather|temperature', res):
                        city = res.split(' ')[-1]
                        weather_res = obj.weather(city=city)
                        print(weather_res)
                        t2s(weather_res)

                    elif re.search('news', res):
                        news_res = obj.news()
                        pprint.pprint(news_res)
                        t2s(f"I have found {len(news_res)} news. You can read it. Let me tell you first 2 of them")
                        t2s(news_res[0])
                        t2s(news_res[1])

                    elif re.search('tell me about', res):
                        topic = res[14:]
                        wiki_res = obj.tell_me(topic)
                        print(wiki_res)
                        t2s(wiki_res)

                    elif re.search('date', res):
                        date = obj.tell_me_date()
                        print(date)
                        print(t2s(date))

                    elif re.search('time', res):
                        time = obj.tell_me_time()
                        print(time)
                        t2s(time)

                    elif re.search('open', res):
                        domain = res.split(' ')[-1]
                        open_result = obj.website_opener(domain)
                        print(open_result)

                    elif re.search('hello|hi', res):
                        print('Hi')
                        t2s('Hi')

                    elif re.search('how are you', res):
                        li = ['good', 'fine', 'great']
                        response = random.choice(li)
                        print(f"I am {response}")
                        t2s(f"I am {response}")

                    elif re.search('your name|who are you', res):
                        print("I am your personal assistant")
                        t2s("I am your personal assistant")

                    elif 'log off ' in query or 'jarvis log off pc' in query:
                        speak('okay')
                        os.system("shutdown /l /t 06")
                        speak('I am going to log of your computer Sir')
                        speak('Bye' + name + 'have a good day.')
                        sys.exit()

                    elif 'shutdown' in query or 'jarvis shutdown pc' in query:
                        speak('okay')
                        os.system("shutdown /s /t 06")
                        speak('I am going to shutdown your computer Sir')
                        speak('Bye' + name + 'have a good day.')
                        sys.exit()

                    elif 'restart' in query or 'jarvis restart pc' in query:
                        speak('okay')
                        os.system("shutdown /r /t 06")
                        speak('I am going to restart your computer Sir')
                        speak('Bye' + name + 'have a good day.')
                        sys.exit()

                    elif 'you can sleep' in query:
                        speak("ok da")
                        break

                    if re.search("stop listening|stop", res):
                        break

                    elif 'exit' in query:
                        exit()

if __name__ == "__main__":
    wishme()


def game():
    while True:

        query = takecommand().lower()
        if "game" in query:
            speak("ok am going on game path")
            while True:
                query = takecommand().lower()

                if 'turtle game' in query:

                    lst = ['s', 'w', 'g']

                    chance = 10
                    no_of_chance = 0
                    computer_point = 0
                    human_point = 0

                    print(" \t \t \t \t Snake,Water,Gun Game\n \n")
                    print("s for snake \nw for water \ng for gun \n")

                    while no_of_chance < chance:
                        _input = input('Snake,Water,Gun:')
                        _random = random.choice(lst)

                        if _input == _random:
                            print("Tie Both 0 point to each \n ")

                        elif _input == "s" and _random == "g":
                            computer_point = computer_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("computer wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n ")

                        elif _input == "s" and _random == "w":
                            human_point = human_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("Human wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n")

                        elif _input == "w" and _random == "s":
                            computer_point = computer_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("computer wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n ")

                        elif _input == "w" and _random == "g":
                            human_point = human_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("Human wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n")

                        elif _input == "g" and _random == "s":
                            human_point = human_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("Human wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n")

                        elif _input == "g" and _random == "w":
                            computer_point = computer_point + 1
                            print(f"your guess {_input} and computer guess is {_random} \n")
                            print("computer wins 1 point \n")
                            print(f"computer_point is {computer_point} and your point is {human_point} \n ")

                        else:
                            print("you have input wrong \n")

                        no_of_chance = no_of_chance + 1
                        print(f"{chance - no_of_chance} is left out of {chance} \n")

                    print("Game over")

                    if computer_point == human_point:
                        print("Tie")

                    elif computer_point > human_point:
                        print("Computer wins and you loose")

                    else:
                        print("you win and computer loose")

                    print(f"your point is {human_point} and computer point is {computer_point}")
