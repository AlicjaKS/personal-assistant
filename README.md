### SMALL INTELLIGENT PERSONAL ASSISTANT

### 
_ _ _ _ _ _ _

In this file I wrote all steps that I made creating this little program with explanation and some
theoretical knowledge.

If you are beginner and learning this topic I’m recommending reading this file because I also
answered some questions that comes to my mind while learning this topic.

I used Python 3.7, PyCharm 2020.1 on MacOS so tutorial is most suitable for this system but of
course it is possible to use it with Windows or Linux.

_ _ _ _ _ _ _

#### GOALS:

- speech recognition - we will talk to our program^
- converting text to speech^
- opening other applications with our assistant^
- getting answers from assistant - give ability to think^

#### Installing Homebrew and Python (MacOS / Linux):

1. Open terminal
2. Paste this in terminal and run:
"/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/
       install/master/install.sh)"
3. Type in terminal:
    ```brew install python```
4. I will use Python 3.7, if you want to check your version type in terminal:
    ```python --version```

Homebrew is package manager. Other ways to install it here -> https://brew.sh

#### Starting with PyCharm:

* requires Java, if you don’t have —> https://www.java.com/

1. Download a Pycharm here, I’m using free community version:
https://www.jetbrains.com/pycharm/download/#section=mac
2. Create a directory for PyCharm files, type in terminal:
   ``` mkdir PycharmProjects```
3. Go to this directory:
    ```cd PycharmProjects```
4. Open PyCharm
5. Create New Project:
We will use: virualenv, choose newest version of Python as interpreter and name your project then
click “Create”.
6. To open file in PyCharm just right click on the directory —> New —> Python file and name it.
* if its possible name in in different way than directory because it may leads to some difficulties
when it comes to describing the path


Q: Why we need IDE (integrated development environment)?
If you want you can open up basic text editor (like notepad on Windows) and write a script there
and then go over to the terminal to run it but it’s not efficient way for a variety of reasons.

#### Installing Python packages:

1. Go to the terminal and type:
    pip3 install pyaudio

```
pip3 install speechrecognition
```
More about packages:
—> https://pypi.org/project/PyAudio/
—> https://pypi.org/project/SpeechRecognition/

Since both packages are from Python Package Index (pypi) we can install them using ‘pip3’ or
‘pip’. More about The Python Package Installer
—> https://pip.pypa.io/en/stable

#### Getting notifications sound from program:

1. Import packages:

```
import pyaudio
import wave
```
* Wave reads and writes *.wav files.

2. Defining a function play_audio:

```
def play_audio(filename):
chunk = 1024
wf = wave.open(filename, 'rb')
pa = pyaudio.PyAudio()
```
- Chunk is the number of frames in the buffer. Often used values are 1024, 2048 or 4096.

- ‘rb’ is a mode of opening files which means ‘read only mode’, other mode is ‘wb’ which means ‘write only mode’
3. Opening stream:

```
stream = pa.open(
format=pa.get_format_from_width(wf.getsampwidth()),
channels=wf.getnchannels(),
rate=wf.getframerate(),
output=True
)
```
- stream is used to stream the audio ;) —> opening the file through PyAudio (pa.open)

- Defining format, channels, frame rate


4. Playing stream:
```   
 while data_stream:
stream.write(data_stream)
data_stream = wf.readframes(chunk)
```
- Creating variable data stream wf.readframes(chunk). Initial chunk = 1024 bytes.

5. Stopping stream and closing PyAudio

```
stream.close()
pa.terminate()
```
More about used functions here:
—> https://docs.python.org/3/library/wave.html
—> https://people.csail.mit.edu/hubert/pyaudio/docs/

6. Download a two notification sounds in *.wav format which will tell us when recording is starting
and when ends.
For example from here:
—> https://notificationsounds.com (here are in *.mp3 so you have to convert them into wav.)
And keep them in directory called ‘audio’ where you have your python file
7. Checking if its working:
play_audio(“.yourdirectory/audio.wav”) for example:

```
play_audio("./audio/clearly.wav")
```
If you run this code you should get notification sound.

