# LiveCaptioning

import speech_recognition as sr

recognizer = sr.Recognizer()

with sr.Microphone() as source:
    print("Live Captioning Started... Speak Now")
    recognizer.adjust_for_ambient_noise(source)

    while True:
        try:
            audio = recognizer.listen(source, phrase_time_limit=3)
            text = recognizer.recognize_google(audio)
            print("Caption:", text)

        except sr.UnknownValueError:
            print("...")
        except KeyboardInterrupt:
            print("Captioning Stopped")
            break
