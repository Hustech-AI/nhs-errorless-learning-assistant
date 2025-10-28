# Setup & Technical Guide — NHS Errorless Learning Voice Assistant

This guide covers everything needed to install, configure, and run the project — starting from a bare machine with no Python, no VS Code, and no Anaconda.

---

## 0) What You Will Install

| Tool / Component         | Purpose                                            |
|--------------------------|----------------------------------------------------|
| Python 3.10+             | Programming language for the project               |
| VS Code (Optional)       | Code editor for development                        |
| Project dependencies     | vosk, pyttsx3, pygame, sounddevice, etc.           |
| Vosk English Model       | Offline speech recognition model                   |
| Project Folder Structure | Organised repo for code, models, logs, assets      |

 If you're using Jupyter Notebook or Google Colab, prefix pip commands with `!` (e.g., `!pip install ...`).

---

## 1) Install Python

### Windows
1. Download Python 3.10+ (64-bit) from https://www.python.org/downloads/
2. Run the installer and check “Add Python to PATH.”
3. Verify installation:
   python --version
   pip --version

### macOS
(Optional) Install Homebrew first: https://brew.sh
brew install python
python3 --version
pip3 --version

### Ubuntu / Debian Linux
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
python3 --version
pip3 --version

 If your system uses `python` instead of `python3`, adjust commands accordingly.

---

## 2) (Optional) Install VS Code

Download: https://code.visualstudio.com/

Recommended extensions:
- Python
- Pylance

(You can also use PyCharm, or just the terminal — VS Code is optional.)

---

## 3) Get the Project Code

If you already have the repo, skip to Step 4.

Using HTTPS:
git clone https://github.com/yourusername/nhs-fsm-voice-assistant.git
cd nhs-fsm-voice-assistant

If you don’t have Git, click Code → Download ZIP on GitHub, extract it, and open the folder.

---

## 4) Create a Virtual Environment (Recommended)

Windows:
python -m venv venv
venv\Scripts\activate

macOS/Linux:
python3 -m venv venv
source venv/bin/activate

To deactivate later:
deactivate

---

## 5) OS Prerequisites (Audio + TTS)

These ensure sounddevice and pyttsx3 work properly.

Windows:
No extra system packages required.

macOS:
brew install portaudio

Ubuntu / Debian:
sudo apt update
sudo apt install -y portaudio19-dev libasound2-dev
sudo apt install -y espeak-ng   # recommended for TTS on Linux

---

## 6) Install Python Libraries

A) Install from requirements.txt (Recommended)
pip install -r requirements.txt

Sample requirements.txt:
vosk==0.3.45
pyttsx3==2.90
pygame==2.5.2
sounddevice==0.4.6
numpy>=1.24

B) Install one-by-one (Terminal)
pip install vosk==0.3.45
pip install pyttsx3==2.90
pip install pygame==2.5.2
pip install sounddevice==0.4.6
pip install numpy

C) Install inside Jupyter/Colab
!pip install vosk==0.3.45
!pip install pyttsx3==2.90
!pip install pygame==2.5.2
!pip install sounddevice==0.4.6
!pip install numpy

If pip errors, try:
python -m pip install ...  (or python3 -m pip install ...)

---

## 7) Download the Vosk English Model

1. Go to https://alphacephei.com/vosk/models
2. Download vosk-model-en-us-0.42-gigaspeech (example)
3. Extract it in the codes directory:

<img width="645" height="214" alt="image" src="https://github.com/user-attachments/assets/31b74a02-efc0-481f-8f58-b68dcc865aeb" />

The structure of the folder should look like this 

Do not commit the model to GitHub — keep it local.

---

## 8) Folder Structure

nhs-errorless-learning-assistant/
│
├─ vosk-Model-en-us-0.42.gigaspeech/
├─ ConvAICode.ipynb/
├─ nhs_errorless_logs/
├─ start_beep
├─ requirements.txt
├─ .gitignore
└─ README.md

## 9) Verify Audio Devices (Optional)

python -c "import sounddevice as sd; print(sd.query_devices())"

If you see a list, your microphone/speaker are detected.

---

## 10) Run the Assistant

Make sure your virtual environment is activated:

python src/main.py
# or
python3 src/main.py

Expected behaviour:
- Starts in S0 Passive Listening
- Plays beep cues
- Proceeds through Alignment → Consent → Warm-up → EL Protocols
- Logs written to logs/nhs_errorless_log.txt

---

## 11) Troubleshooting

Error:
ModuleNotFoundError: No module named 'vosk'
Reason:
Library not installed or wrong environment
Fix:
pip install vosk==0.3.45

Error:
sounddevice.PortAudioError
Reason:
Mic in use or PortAudio missing
Fix:
Close Zoom/Teams; install PortAudio

Error:
pyttsx3 not speaking (Linux)
Reason:
TTS backend missing
Fix:
sudo apt install -y espeak-ng

Error:
PermissionError writing logs
Reason:
Logs folder missing or no permission
Fix:
mkdir -p logs

Error:
Issues in Jupyter
Reason:
Forgot ! before pip
Fix:
Use !pip install ...

---

## 12) Quick “All-in-One” Install

### Windows
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
# Place Vosk model under: models/
python src/main.py

### macOS / Linux
python3 -m venv venv
source venv/bin/activate
# macOS: brew install portaudio
# Ubuntu: sudo apt install -y portaudio19-dev libasound2-dev espeak-ng
pip install -r requirements.txt
# Place Vosk model under: models/
python3 src/main.py

---

## 13) Library Reference

vosk         — Offline speech recognition         — pip install vosk==0.3.45
pyttsx3      — Offline text-to-speech            — pip install pyttsx3==2.90
pygame       — Audio cues / beep sounds         — pip install pygame==2.5.2
sounddevice  — Microphone input (PortAudio)     — pip install sounddevice==0.4.6
numpy        — Math / audio buffer utilities    — pip install numpy

Colab shortcut:
!pip install vosk==0.3.45 pyttsx3==2.90 pygame==2.5.2 sounddevice==0.4.6 numpy

---

## You’re Ready!

Following this guide gives you a fully working, offline NHS-aligned conversational assistant:

-  Speech input via Vosk
-  Offline TTS via pyttsx3
-  Deterministic FSM for NHS rehab interactions
-  Anonymised logging
-  No cloud or data sharing

Author: Hussnain Khalid  
Supervisor: Prof. Mario Gianni  
Institution: University of Liverpool — Department of Computer Science  
Project: MSc — AI-powered Healthcare Robot Assistant
