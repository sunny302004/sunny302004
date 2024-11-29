import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import pywhatkit as wk
import os
import random
import pyautogui
import time
import wolframalpha
import requests
import sys
import pygame
import json
import speedtest
from pygame import mixer
from bs4 import BeautifulSoup

from emma import play_gif 

engine=pyttsx3.init('sapi5') 
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)
engine.setProperty('rate',190)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()
    
            
def wishMe(): 
    hour=int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
           print("Good Morning Sir!")
           speak("Good Morning Sir!")
           
           
    elif hour>=12 and hour<18:
        print("Good Afternoon Sir! ")
        speak("Good Afternoon Sir! ")
        
        
    else:
        print("Good Evening Sir!")
        speak("Good Evening Sir!")
    print("Hello,I am Bixby!")
    speak("Hello,I am Bixby!")
    print("How can I assist you today,Sir!?")
    speak("How can I assist you today,Sir!?")
    
def takeCommand():
    r=sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)
        
    try:
        print("Recognizing...")
        query=r.recognize_google(audio,language='en-in')
        print(f"User said: {query}\n")
            
    except Exception as e:
        print("Say that again please...")
        speak("Say that again please...")
        return "None"
    return query

def alarm(query):
    print("input time example:- 10 and 10 and 10")
    speak("Set the time")
    a = input("Please tell the time :- ")
    alarm(a)
    speak("Done,sir")
        
if __name__=='__main__':
    play_gif() 
    wishMe()
    while True:
        query=takeCommand().lower()
                  
        if 'bixby' in query:
            print("yes sir")     
            speak("yes sir")
            
        elif 'type' in query:
            query = query.replace("type","")
            query = query.replace("bixby","")
            pyautogui.typewrite(f"{query}",0.1)
                
        elif'how are you' in query  or 'good' in query:
            speak("it's good tp know that you are fine.")    
        
        elif'who i am'in query:
            print("if you can talk then surely, you are aa human")
            speak("if you can talk then surely, you are aa human")
            
        elif 'love' in query:
            print("It's not really called for, but the feeling is mutual")
            speak("It's not really called for, but the feeling is mutual")
            
        elif 'where are you' in query:
            print("I am in your system,sir!")
            speak("I am in your system,sir!")
            
            
        elif 'i love you' in query:
            print("Oh my God, thankyou.I love you too. Anything i can help you with?")
            speak("Oh my God, thankyou.I love you too. Anything i can help you with?")
            
        elif 'will you be my girlfriend' in query:
            print("I'm flattered but i'm afraid i'm already taken")
            speak("I'm flattered but i'm afraid i'm already taken")
            
        elif 'what ise your name' in query:
            print("Hii,My name is bixby")
            speak("Hii,My name is bixby")
            
        elif 'what is' in query:
            query = query.replace("what is","")
            results=wikipedia.summary(query,sentences=1)
            print(results) 
            speak("According to wikipedia")
            speak(results)  
            
            
        elif 'who is' in query:
            speak('Searching Wikipedia....')
            query = query.replace("who is","")
            results=wikipedia.summary(query,sentences=1)
            print(results)  
            speak("According to wikipedia")
            speak(results)
            
        elif 'where is' in query:
            speak('Searching,please wait....')
            query = query.replace("where is","")
            query = query.replace("bixby","")
            results=wikipedia.summary(query,sentences=1)
            print(results)  
            speak("According to place")
            print(results) 
            speak(results)           
            
        elif 'just open google' in query:
            speak("here you go to google sir")
            webbrowser.open("google.com")
            
        elif 'open google' in query:
            speak("what should I search ?,Sir")
            qry = takeCommand().lower()
            webbrowser.open(f"{qry}")
            results = wikipedia.summary(qry,sentences=1)
            speak(results)
             
        elif 'just open youtube' in query:
            speak("here you go to youtube sir")
            webbrowser.open("youtube.com")
            
        elif 'open youtube' in query:
            speak("what you will like to watch ?,Sir")
            qrry = takeCommand().lower()
            wk.playonyt("{qrry}")
            
        elif "pause video" in query:
            pyautogui.press("k")
            speak("video paused")
            
        elif "play video" in query:
            pyautogui.press("k")
            speak("video played")
                      
        elif 'play song on youtube' in query:
            query = query.replace("play song on youtube","")
            webbrowser.open(f"www.youtube.com/watch?v=vJQMhj6WYZA&list=RDMMvJQMhj6WYZA&start_radio=1{query}")
            
        elif 'close browser' in query:
            os.system("taskkill /f /im msedge.exe")
            
        elif 'close chrome' in query:
            os.system("taskkill /f /im chrome.exe")    
                           
        elif 'open myntra' in query:
            speak("here you go to myntra sir. Happy shopping,sir")
            webbrowser.open("myntra.com")
         
        elif 'open amazon' in query:
            speak("here you go to amazon sir. Happy shopping,sir")
            webbrowser.open("amazon.com")
        
        elif "open command prompt" in query:
            os.system("start cmd")
            
        elif "close command prompt" in query:
            os.system("taskkill /f /im cmd.exe")
                    
        elif "translate" in query:
            from Translator import translategl
            query = query.replace("bixby","")
            query = query.replace("translate","")
            translategl(query)
            
        elif "open" in query:
            query = query.replace("open","")
            query = query.replace("bixby","")
            pyautogui.press("super")
            pyautogui.typewrite(query)
            pyautogui.sleep(1)
            pyautogui.press("enter")
            
        elif "internet speed" in query:
            wifi = speedtest.Speedtest()
            upload_net = wifi.upload()/1048576
            download_net = wifi.download()/1048576
            print("Wifi Upload Speed is",upload_net)
            print("Wifi Download Speed is",download_net)
            speak("Wifi Upload Speed is {upload_net}")
            speak("Wifi Download Speed is {download_net}")
                            
        elif 'tell me current time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Sir, the time is {strTime}")
        
        elif "set alarm" in query:
            print("input time example:- 10 and 10 and 10")
            speak("Set the time")
            a = input("Please tell the time :- ")
            alarm(a)
            speak("Done,sir")
        
        elif "shutdown the system" in query:
            speak("shutdown your system!")
            os.system("shutdown /s /t 5")
        
        elif "restart the system" in query:
            speak("restart your system sir!")
            os.system("shutdown /r /t 5")
            
        elif "lock the system" in query:
            speak("locked your system sir!")
            os.system("rundll32.exe user32.dll,LockWorkStation")
        
        elif "click my photo" in query:
            speak("OK SIR!")
            pyautogui.press("super")
            pyautogui.typewrite("camera")
            pyautogui.press("enter")
            pyautogui.sleep(3)
            speak("SMILE")
            pyautogui.press("enter")
              
        elif "stop talking" in query:
            speak('alright then, I am going to silence mode!')
            sys.exit()
        
        elif "take a screenshot" in query:
            speak("please tell me the name for file!")
            name = takeCommand().lower()
            time.sleep(3)
            img = pyautogui.screenshot()
            img.save(f"{name}.png")
            speak("screenshot saved")
            
        elif "calculate" in query:
             from calculatenumber import wolfRamAlpha
             from calculatenumber import calc
             query = query.replace("calculate","")
             query = query.replace("bixby","")
             calc(query)    
            
        elif "my ip address" in query:
            speak("checking")
            try:
                ip = requests.get('https://api.ipify.org').text
                print(ip)
                speak(f"your ip address is {ip}")
                speak(ip)
            except Exception as e:
                speak("network is weak, please try again after sometime later!")
                print("network is weak, please try again after sometime later!")
                
                
        elif "volume up" in query:
            speak("turning volume up,sir")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            pyautogui.press("volumeup")
            
        elif "volume down" in query:
            speak("turning volume down,sir!") 
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")   
            pyautogui.press("volumedown")      
            
        elif "please mute" in query:
            pyautogui.press("volumemute")
            speak("muted")
            
        elif "please unmute" in query:
            pyautogui.press("volumemute")
            speak("unmuted")
            
        elif 'maximize this window' in query:
            pyautogui.hotkey('alt','space')
            time.sleep(1)
            pyautogui.press('x')
        
        elif 'youtube search' in query:
            query = query.replace("youtube search","")
            pyautogui.hotkey('alt','d')
            time.sleep(1)
            pyautogui.press('tab')
            pyautogui.press('tab')
            pyautogui.press('tab')
            pyautogui.press('tab')
            time.sleep(1)
            pyautogui.write(f"{query}",0.1)
            pyautogui.press("enter")
            
        elif 'open new window' in query:
            pyautogui.hotkey('ctrl','n')
            
        elif 'minimise this window' in query:
            pyautogui.hotkey('alt','space')
            time.sleep(1)
            pyautogui.press('n')
                                
        elif 'open the history' in query:
            pyautogui.hotkey('ctrl','h')
            
        elif 'open the download' in query:
            pyautogui.hotkey('ctrl','j')
            
        elif 'previous tab' in query:
             pyautogui.hotkey('ctrl','shift','tab')
        
        elif 'next tab' in query:
            pyautogui.hotkey('ctrl','tab')
            
        elif 'close this tab' in query:
            pyautogui.hotkey('ctrl','w')
            
        elif 'close this window' in query:
            pyautogui.hotkey('ctrl', 'shift', 'w')
            
        elif 'clear browsing history' in query:
            pyautogui.hotkey('ctrl','shift','del')

        elif "top 10 headlines" in query:
            speak("here is today,top 10 headlines,sir")
            query_ = {"source": "the-times-of-india",
                      "sortBy":"top",
                      "apiKey": "206ca32213e94b92ae4458cf1cf0c957"}
            main_url = "https://newsapi.org/v2/top-headlines?country=in"
            res = requests.get(main_url, params=query_)
            open_TheTimesofIndia_page = res.json()
            article = open_TheTimesofIndia_page['articles']
            results = []
            
            for ar in article:
                results.append(ar["title"])
                
            for i in range(min(10,len(results))):
                print(i + 1, results[i])  
                speak(results[i])
                
        elif "current temperature" in query:
            search = "tempreture in malout"
            url = f"https://www.google.com/search?q={search}"
            r = requests.get(url)
            data = BeautifulSoup(r.text,"html.parser")
            temp = data.find("div",class_ = "BNeawe").text
            speak(f"current{search} is {temp}")
            
        elif "current weather" in query:
            search = "weather in malout"
            url = f"https://www.google.com/search?q={search}"
            r = requests.get(url)
            data = BeautifulSoup(r.text,"html.parser")
            temp = data.find("div",class_ = "BNeawe").text
            speak(f"current{search} is {temp}")
                  
