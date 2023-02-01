import tkinter
from tkinter import *
import tkinter as tk
import speech_recognition
import webbrowser as wb
import pyttsx3


engine = pyttsx3.init()
engine.setProperty('rate', 150) # скорость речи
engine.setProperty('volume', 8.9) # громкость речи
engine.say('Привет я голосовой помошник чем могу помочь')
engine.runAndWait()

def str_to_sort_list(event):
    sr = speech_recognition.Recognizer()
    sr.pause_threshold = 0.5

    with speech_recognition.Microphone() as mic:
        sr.adjust_for_ambient_noise(source=mic, duration=0.5)
        audio = sr.listen(source=mic)
        query = sr.recognize_google(audio_data=audio, language='ru-RU').lower()


# функция для прослушивание команд через микрофон
    def listen_command():
        try:
            with speech_recognition.Microphone() as mic:
                sr.adjust_for_ambient_noise(source=mic, duration=0.5)
                audio = sr.listen(source=mic)
                query = sr.recognize_google(audio_data=audio, language='ru-RU').lower()
            return query
        except speech_recognition.UnknownValueError:
            return 'не понял'
        

    if query == 'музыка':
        engine = pyttsx3.init()
        engine.setProperty('rate', 150) # скорость речи
        engine.setProperty('volume', 8.9) # громкость речи
        engine.say('Вы хотите открыть музыку?')
        engine.runAndWait()
        query = listen_command()
        if query =='да':
            wb.open(f'https://zvuk.com/')

    elif query == 'youtube':
        engine = pyttsx3.init()
        engine.setProperty('rate', 150) # скорость речи
        engine.setProperty('volume', 8.9) # громкость речи
        engine.say('Что вы хотите посмотреть на ютуб')
        engine.runAndWait()
        query = listen_command()
        wb.open(f"https://www.youtube.com/results?search_query={query}")

    elif query == 'википедия':
        engine = pyttsx3.init()
        engine.setProperty('rate', 150) # скорость речи
        engine.setProperty('volume', 8.9) # громкость речи
        engine.say('что ходите найти в википедии')
        engine.runAndWait()
        query = listen_command()
        wb.open(f"https://ru.wikipedia.org/wiki/{query}")

    elif query == 'telegram':
        engine = pyttsx3.init()
        engine.setProperty('rate', 150) # скорость речи
        engine.setProperty('volume', 8.9) # громкость речи
        engine.say('вы хотите открыть телеграмм')
        engine.runAndWait()
        query = listen_command()
        if query =='да':
            wb.open(f"https://web.telegram.org/k/")

    elif query == 'вконтакте': 
        engine = pyttsx3.init()
        engine.setProperty('rate', 150) # скорость речи
        engine.setProperty('volume', 8.9) # громкость речи
        engine.say('вы хотите открыть вконтакте')
        engine.runAndWait()
        query = listen_command()
        if query =='да':
            wb.open(f"https://vk.com/im?peers=550436840")


root = Tk()
root.title("голосовой помошник")
root.geometry("400x200+700+500")
root.resizable(width=False, height=False)
but = Button(text="начать")
but.bind('<Button-1>', str_to_sort_list)
but.pack()
root.mainloop()
