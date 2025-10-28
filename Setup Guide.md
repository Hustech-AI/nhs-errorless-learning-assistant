# SETUP GUIDE — NHS Errorless Learning Voice Assistant

This document shows how to install **everything from scratch** and run the project locally:
- Install Python
- (Optional) Install VS Code
- Create a virtual environment
- Install all libraries
- Download the Vosk English model
- Verify audio devices
- Run the assistant
- Troubleshoot common issues

> If you’re using **Jupyter/Colab**, prefix `pip` commands with `!` (e.g., `!pip install ...`).

---

## 1) Install Python 3.10+

### Windows
1. Download **Python 3.10+ (64-bit)**: https://www.python.org/downloads/
2. Run the installer and **check “Add Python to PATH.”**
3. Verify:
   ```powershell
   python --version
   pip --version

### macOS
# (Optional) Install Homebrew first: https://brew.sh
    brew install python
    python3 --version
    pip3 --version

### Ubuntu / Debian Linux
    sudo apt update
    sudo apt install -y python3 python3-pip python3-venv
    python3 --version
    pip3 --version


- If your system uses python instead of python3, substitute accordingly in later commands.

### 2) (Optional) Install VS Code

* Download: https://code.visualstudio.com/
Recommended extensions: Python, Pylance
(You can also use PyCharm or just the terminal.)

### 3) Get the Project Code
# Using HTTPS
git clone https://github.com/yourusername/nhs-fsm-voice-assistant.git
cd nhs-fsm-voice-assistant

No Git? Click Code → Download ZIP on GitHub, extract, then open the folder.

### 4) Create & Activate a Virtual Environment
|OS |	Commands|
|Windows |	python -m venv venv|
|| venv\Scripts\activate|
|macOS/Linux|	python3 -m venv venv|
||- source venv/bin/activate|


| OS | Commands|
| :--- | :--- |
| **Windows** | python -m venv venv      |
|             | venv\Scripts\activate    |
|macOS/Linux  | python3 -m venv venv     |
|             | source venv/bin/activate |


#### To deactivate later:
- deactivate

### 5) Install OS Audio Prerequisites (for sounddevice + TTS)

#### Windows
- No additional system packages required.

#### macOS
    brew install portaudio

#### Ubuntu / Debian
    sudo apt update
    sudo apt install -y portaudio19-dev libasound2-dev
    sudo apt install -y espeak-ng   # recommended for TTS on Linux

### 6) Install Python Libraries
- You can install from a requirements file (recommended) or one by one.

#### A) Using requirements.txt (recommended)
- Create a file named requirements.txt with this content:

      vosk==0.3.45
      pyttsx3==2.90
      pygame==2.5.2
      sounddevice==0.4.6
      numpy>=1.24

> Then install:

    pip install -r requirements.txt

#### B) Install packages individually
    pip install vosk==0.3.45
    pip install pyttsx3==2.90
    pip install pygame==2.5.2
    pip install sounddevice==0.4.6
    pip install numpy

#### C) Jupyter / Colab users
    !pip install vosk==0.3.45 pyttsx3==2.90 pygame==2.5.2 sounddevice==0.4.6 numpy
#### If pip errs, try python -m pip install ... (or python3 -m pip install ...).


### 7) Download the Vosk English Model (Large, not in repo)

- Go to: https://alphacephei.com/vosk/models

- Download an English model (example: vosk-model-en-us-0.42-gigaspeech).

- Extract it to the models/ folder so the path looks like:


      nhs-fsm-voice-assistant/
          └─ models/
            └─ vosk-model-en-us-0.42-gigaspeech/
              ├─ am
              ├─ conf
              ├─ graph
              └─ ...

- Do not commit the model folder to GitHub. Keep it local.

### 8) Ensure Project Structure
- Create folders if missing:

      nhs-fsm-voice-assistant/
      │
      ├─ src/
      │  ├─ main.py
      │  ├─ fsm_logic.py
      │  ├─ speech_module.py
      │  └─ utils.py
      │
      ├─ models/
      │  └─ vosk-model-en-us-0.42-gigaspeech/
      │
      ├─ assets/
      │  └─ start_beep.wav
      │
      ├─ logs/
      │  └─ nhs_errorless_log.txt
      │
      ├─ requirements.txt
      ├─ README.md
      └─ .gitignore

Suggested .gitignore:

    # Large models
    models/*
    !models/.gitkeep
    
    # Logs (keep folder)
    logs/*
    !logs/.gitkeep
    
    # Python cache
    __pycache__/
    *.pyc
    
    # OS cruft
    .DS_Store
    Thumbs.db

(Use empty .gitkeep files so Git tracks empty folders.)

### 9) Verify Audio Devices (optional but helpful)

    python -c "import sounddevice as sd; print(sd.query_devices())"
If you see a device list, your microphone and speaker are detected.

### 10) Run the Assistant

- Make sure your virtual environment is active, then:

      python src/main.py
      # or
      python3 src/main.py

### Expected behaviour:
- Starts in S0 Passive Listening
- Plays beep cues
- Proceeds through Alignment → Consent → Warm-up → Errorless Learning protocols
- Writes logs to logs/nhs_errorless_log.txt

### 11) Troubleshooting (Quick Fixes)

| Error                                      | Likely Cause                        | Fix                                      |
|--------------------------------------------|--------------------------------------|-------------------------------------------|
| `ModuleNotFoundError: No module named 'vosk'` | Wrong environment or not installed   | `pip install vosk==0.3.45`                |
| `sounddevice.PortAudioError`              | Microphone busy / PortAudio missing | Close Zoom/Teams, install PortAudio (Step 5) |
| `pyttsx3` silent on Linux                 | TTS engine missing                  | `sudo apt install -y espeak-ng`           |
| `PermissionError` writing logs           | Missing logs folder / no permission | `mkdir -p logs`                           |
| Jupyter issues with `pip`                | Forgot `!` in notebooks             | Use `!pip install ...`                    |


### 12) One-Shot Installation
- Windows (PowerShell)
  
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

### 13) Library Reference (What each package does)

| Library        | Purpose                                   | Install Command                                    |
|--------------- |-------------------------------------------|----------------------------------------------------|
| `vosk`         | Offline speech recognition (ASR)          | `pip install vosk==0.3.45`                          |
| `pyttsx3`      | Offline text-to-speech                    | `pip install pyttsx3==2.90`                         |
| `pygame`       | Audio playback (beeps/cues)               | `pip install pygame==2.5.2`                         |
| `sounddevice`  | Microphone input (PortAudio wrapper)      | `pip install sounddevice==0.4.6`                    |
| `numpy`        | Arrays/buffers used by audio libraries    | `pip install numpy`                                 |


### Colab shortcut:

    !pip install vosk==0.3.45 pyttsx3==2.90 pygame==2.5.2 sounddevice==0.4.6 numpy

##  Technical Support

If you run into any issues during installation or setup, feel free to reach out for support:

**Email:** [hustech.ai@hotmail.com](mailto:hustech.ai@hotmail.com)

Please include:
- Your operating system (Windows / macOS / Linux)  
- Python version (`python --version`)  
- A brief description of the issue or error message  

I’ll do my best to help you resolve it quickly.
