
# NHS-errorless-learning- voice assistant

<div align="justify">
The NHS Errorless Learning Voice Assistant is a deterministic, offline conversational AI system designed to support cognitive rehabilitation for patients recovering from neurological conditions such as post-brain surgery.

The project implements NHS-aligned rehabilitation protocols using a Deterministic Finite State Machine (FSM) to deliver structured, predictable, and auditable patient interactions. By following Errorless Learning (EL) principles — including modeling correct responses, guided recall, distraction, and delayed recall — the system helps patients practice orientation and memory exercises while minimizing cognitive frustration and error reinforcement.

Unlike cloud-based solutions, this assistant operates fully offline, ensuring strict privacy and data security. It uses real-time speech recognition powered by Vosk and text-to-speech (TTS) feedback via pyttsx3, enabling natural, low-latency interaction. All interactions are recorded in structured anonymised logs, supporting clinical auditing and future outcome analysis.

The envisioned deployment scenario involves a bedside conversational healthcare robot that listens passively during rest periods, initiates structured orientation and memory tasks, and adapts its flow deterministically based on patient responses. This design ensures a safe, explainable, and ethically compliant digital rehabilitation experience, aligned with NHS clinical standards.
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/c656f321-cac8-455f-a5a0-a3ec3bab33cc" 
       alt="NHS-errorless-learning-voice-assistant" 
       width="600">
  <p><em>Concept rendering of the bedside healthcare assistant robot supporting NHS-aligned cognitive rehabilitation.</em></p>
</div>



## Project Overview

This MSc project presents an **AI-powered Healthcare Robot Assistant** designed to support **cognitive rehabilitation** for patients recovering from neurological events (e.g., post-brain surgery).


The system is built on principles of safety, privacy, and clinical auditability:

- **Deterministic Finite State Machine (FSM):** Provides a structured, predictable, and auditable flow for patient interactions.
- **Errorless Learning (EL):** Implements protocols aligned with NHS rehabilitation guidelines to guide memory and orientation exercises (e.g., date, address recall) and prevent error reinforcement.
- **Strict Privacy Measures:** Operates **100% offline** (no cloud) and stores only anonymised interaction logs, with no raw audio recording.

This prototype was developed to meet the need for safe, reproducible, and privacy-preserving AI tools in cognitive care.

## Clinical & Technical Objectives

|Icon                     | Objective Details |
| :---                    | :--- |
| Structured Exercises | Deliver orientation and memory recall exercises (e.g., date, address). |
| Errorless Learning | Strictly adhere to EL principles (model, recall, distractor, delayed recall). |
| Deterministic Classification | Classify patient speech into auditable categories (A\*, Ā, S, C, FT). |
| Offline Operation | Ensure complete operation without an internet connection for patient privacy and safety. |
| Auditable Logging | Log every state transition and response deterministically for clinical review.

## Repository Structure

nhs-errorless-learning-assistant
- main.py # Entry point
- Vosk-model-en-us-0.42-gigspeech
- nhs-errorless-log
- start_beep

## Tech Stack

- **Programming Language:** Python 3.10+
- **STT (Offline):** [Vosk](https://alphacephei.com/vosk)
- **TTS (Offline):** `pyttsx3`
- **Audio Handling:** `pygame` / `sounddevice`
- **Architecture:** Custom Deterministic Finite State Machine (FSM)

---

## Setup Instructions

##### 1. Follow the Setup Instructions below
##### 2. Install Dependencies as Shown in the instructions
##### 3. Check Audio Devices
##### 5. Run the Assistant

## FSM State Flow & Response Categories
### FSM State Flow
### The session is guided by a deterministic sequence of states, with EL steps embedded in S4 and S5.

| State         | Description                              |
| ------------- | ---------------------------------------  |
| S0            | Passive Listening (Awaits presence)      |
| S1	          | Alignment (Initial check)                |
| S2            | Consent (Confirms willingness to start)  |
| S3            | Warm-up (Simple orientation checks)      |
| S4            | Date Protocol (Errorless Learning)       |
| S5	          | Address Memory (Errorless Learning)      |
| S6            |	Closure (Session end)                    |


### Response Categories
Patient responses are deterministically classified to drive the FSM transitions and capture auditable clinical data.

| Label | Meaning        | Example / System Action                                               |
|-------|--------------- |-----------------------------------------------------------------------|
| A*    | Correct        | Advance to the next state/step.                                       |
| Ā     | Incorrect      | Re-model the answer, then re-ask the question.                         |
| S     | Silence        | Repeat or rephrase the question.                                      |
| C     | Critical       | Pause session, log event, and prompt for assurance (safety protocol).  |
| FT    | Free Talking   | Reset to S0 (passive listening), wait for an idle period to resume.    |

### Logging & Privacy
Logging Format
All session interactions are logged in a structured, pipe-separated format:

[Timestamp] | State | Prompt | Patient Response | Label | Confidence | Next State

Logs are stored locally in logs/nhs_errorless_log.txt.

### Privacy & Ethics
100% Offline: The system runs without any reliance on cloud services or external APIs.

Data Minimisation: No personal identifying information (PII) is collected, and no raw audio is stored.

Auditable Design: The deterministic FSM ensures predictable, transparent, and auditable interactions, aligning with NHS guidelines and ethical research standards.

### Recommended Environment
| Component | Specification                       |
|-----------|--------------------------------------|
| OS        | Windows 11 / macOS / Ubuntu Linux    |
| Python    | 3.10+                                |
| RAM       | 4 GB+                                |
| Audio     | Working microphone and speaker      |

### Contributing
Contributions are welcome! Potential areas for extension include:

Adding new FSM states for additional rehabilitation tasks (e.g., object recall).

Improving ASR robustness or extending language support (by integrating other Vosk models).

Enhancing response classification logic.

Please fork the repository, create a feature branch, and submit a Pull Request.\

### License
This project is licensed under the MIT License. See the LICENSE file for details.

### Author & Acknowledgments
Author: Hussnain Khalid

Supervisor: Prof. Mario Gianni

Institution: University of Liverpool, Department of Computer Science

Project: AI-powered Healthcare Robot Assistant

Grade: A

<div align="center">
  <img src="https://github.com/user-attachments/assets/bde51e81-723f-4934-b69d-949c20d1f0d9" 
       alt="Hustech AI Logo" 
       width="300">
  <p><em>Project designed by <strong>hustech.ai</strong></em></p>
</div>


</div>
