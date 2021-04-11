# buzzer_music
Play thousands of songs on your Raspberry Pi Pico with a buzzer

Micropython library to play music through a buzzer, automatically replaces chords with fast arpeggios to simulate polyphony. Music can be easily taken from onlinesequencer.net

Also supports playing music through multiple buzzers, dividing the currently playing notes across them for polyphony

<br>

### Usage
1) Connect your buzzer to a ground pin and pin 0 on your Pico
2) Install micropython on your Pico and copy the files in this repository to it
3) Find some music on onlinesequencer.net, click edit, select all notes with CTRL + A and then copy them with CTRL + C
4) Paste the string in place of the one in the example file, making sure to remove the "Online Sequencer:120233:" from the start and the ";:" from the end
