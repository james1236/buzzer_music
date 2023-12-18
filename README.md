# buzzer_music
Play thousands of songs on your Raspberry Pi Pico with a buzzer

Micropython library to play music through a buzzer, automatically replaces chords with fast arpeggios to simulate polyphony. Music can be easily taken from [onlinesequencer.net](https://onlinesequencer.net/)

Also supports playing music through multiple buzzers, dividing the currently playing notes across them for polyphony

### Online Simulator
See it working or test it out using this online simulator! [One Buzzer](https://wokwi.com/projects/384484222930823169) | [Multiple Buzzers](https://wokwi.com/projects/384484055755294721) <br><br>
![buzzers](https://github.com/james1236/buzzer_music/assets/32351696/87245a5d-99e1-4d9d-a607-87499c3d1e27)

<video src="https://user-images.githubusercontent.com/32351696/215248051-8b161d79-5e79-405d-bb80-717d03b9edb8.mp4](https://user-images.githubusercontent.com/32351696/215248120-8da75442-0793-4c2a-8c1f-44bfb2d84262.mp4)"></video>

<br>

### Usage with RPi Pico / Other Micropython Board 
1) Connect your buzzer to a ground pin and pin 0 on your Pico
2) Install micropython on your Pico and copy the files in this repository to it
3) Find some music on onlinesequencer.net, click edit, select all notes with CTRL + A and then copy them with CTRL + C
4) Paste the string in place of the one in the example file, making sure to remove the "Online Sequencer:120233:" from the start and the ";:" from the end
<br>

### Board Compatibility
| Board | Compatible? |
|-------|-------------|
| Raspberry Pi Pico | Yes |
| Wemos D1 mini (ESP8266) | Yes [i8](/../../issues/8)|
| Raspberry Pi 3, 4 | Follow steps below |
<br>

### Raspberry Pi 3, 4 Compatibility
The following code was contributed by [@Miniontoby](https://github.com/Miniontoby) in [i10](/../../issues/10), simply create a file called `machine.py` in the same folder as the other files and put this code in it:
```python3
import RPi.GPIO as GPIO
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)

class PWMchanged(GPIO.PWM):
    def __init__(self, chan, freq):
        super().__init__(chan, freq)
        self.start(freq)
    def duty(self,dutycycle): self.ChangeDutyCycle(dutycycle/65535)
    def freq(self, value): self.ChangeFrequency(value)
    def deinit(self): self.stop()
    pass

def PWM(pin):
    GPIO.setup(pin, GPIO.OUT) # Just to make sure
    return PWMchanged(pin, 50)

def Pin(pin):
    GPIO.setup(pin, GPIO.OUT)
    return pin
```
