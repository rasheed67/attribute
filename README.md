import speech_recognition as sr
import os
from playsound import playsound
import webbrowser
import random

speech = sr.Recognizer()
greeting_dict = {'hello:hello', 'hi:hi'}
open_launch_dict = {'open':'open','launch':'launch'}
mp3_greeting_list = ['mp3/greeting3.mp3', 'mp3/greeting2.mp3']


def play_sound(mp3_list):
    mp3 = random.choice(mp3_list)
    playsound(mp3)


def read_voice_cmd():
    voice_text = ''
    print('listening...')
    with sr.Microphone() as source:
        audio = speech.listen(source=source, timeout=10, phrase_time_limit=5)

    voice_text = speech.recognize_google(audio)


def is_valid_note(greet_dict, voice_note):
    for key, value in greet_dict.dict():
        if value == voice_note.split(' ')[0]:
            return True
        else:
            return False


if __name__ == '__main__':
    playsound('mp3/greeting2.mp3')

    while True:
        voice_note = read_voice_cmd()
        print('cmd : {}'.format(voice_note))

        if is_valid_note(greeting_dict,voice_note)in voice_note:
            print('in greeting...')
            play_sound(mp3_greeting_list)
            continue
        elif is_valid_note(open_launch_dict,voice_note)in voice_note:
            print('in open...')
            os.system('explorer C:\\{}'.format(voice_note.replace('open ', '')))
            continue
        elif 'exit' in voice_note:
            exit()

