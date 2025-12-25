# LiveCaptioning
import json
import queue
import sounddevice as sd
from vosk import Model, KaldiRecognizer
import sys

# Ensure you have the model folder named "model" in the current directory
model = Model("model")
recognizer = KaldiRecognizer(model, 16000)

q = queue.Queue()

def callback(indata, frames, time, status):
    """This is called (from a separate thread) for each audio block."""
    if status:
        print(status, file=sys.stderr)
    q.put(bytes(indata))

print("Listening continuously... (Press Ctrl+C to stop)")

try:
    with sd.RawInputStream(samplerate=16000, blocksize=8000, dtype='int16',
                           channels=1, callback=callback):
        while True:
            data = q.get()
            
           
                    
except KeyboardInterrupt:
    print("\nStopping...")
