# Echo

Imagine this: you’re 75, retired, and living alone. The phone doesn’t ring as often. Friends move away. Days stretch endlessly with no one to talk to. You miss the small things, morning chats over tea, laughing at old jokes, or simply having someone remember your stories.
This is not a rare occurrence, it’s a global health crisis:
- nearly 1 in 3 seniors worldwide experiences chronic loneliness.
- 40% of elderly people report feeling socially isolated, leading to higher rates of depression and anxiety.
- Cognitive decline accelerates when the brain lacks stimulation, beginning years before dementia symptoms appear.
- Alzheimer’s cases are expected to triple by 2050, with inactivity and isolation as major risk factors.
Loneliness isn't merely an emotional issue; it shrinks key memory regions, accelerates neuronal loss, and shortens lifespans.

**Echo explores how everyday conversation can become both an opportunity for cognitive engagement and a way to observe changes in speech and language over time.**

Through an AI conversational companion, speech analysis, and supporting tools for everyday care, Echo aims to make cognitive engagement more accessible while helping caregivers gain a clearer picture of an older adult's well-being.

## What Echo Does

### Conversational AI and Speech Analysis

Conversation is at the heart of Echo. Beyond responding to what a person says, Echo analyses features of their speech and language to explore patterns that may become more meaningful when observed over time.

- **Acoustic analysis:** Examines characteristics such as pitch, pauses, and speech timing.
- **Lexical and linguistic analysis:** Extracts features including vocabulary diversity, filler-word frequency, and sentence length.
- **Narrative analysis:** Explores aspects of coherence, repetition, and how thoughts are expressed.
- **Longitudinal tracking:** Stores session-level results to support comparisons across interactions.

The goal is to explore whether everyday communication can offer useful signals of changes that might otherwise go unnoticed.

### Cognitive Exercises

Echo includes cognitive activities designed to encourage regular mental engagement across several domains. These exercises complement the conversational experience rather than replacing it.

| Brain Region| Cognitive Domain | Example Activities |
|---|---|---|
| Hippocampus | Memory & learning | Story recall, memory games |
| Prefrontal Cortex | Focus & decision-making | Logic puzzles, problem-solving tasks |
| Temporal Lobe | Language & retrieval | Word games, conversation drills |
| Parietal Lobe | Spatial & mathematical reasoning | Math challenges, visual puzzles |

The aim is to make cognitive activities accessible and engaging as part of a broader everyday routine. These exercises are not a clinically validated treatment, and their inclusion does not establish that Echo can prevent or reverse cognitive decline.


### Caregiver Dashboard

The caregiver dashboard provides a way to review information from a user's sessions and follow their progress over time, helping connect individual interactions to a broader picture of their engagement and communication, and allowing caretakers to review their progress, medication intake & status.

### Medication Reminders

Medication reminders support everyday routines by helping users keep track of scheduled medications.

> **Note:** Echo is an experimental project, not a clinically validated diagnostic tool. Its outputs should not be used to diagnose or rule out cognitive impairment.

---

## Screenshots
The project brings together an Android application, a Python backend, and a feature-extraction pipeline to analyze audio and transcript data across sessions.

<img width="960" height="540" alt="I see it I like it I want it I got it (1)" src="https://github.com/user-attachments/assets/51cfdb9c-57c9-48c0-a882-6713f12d4be9" />
<img width="960" height="540" alt="I see it I like it I want it I got it (2)" src="https://github.com/user-attachments/assets/6f21b811-7d96-4be2-89b4-43fa838b5f3a" />
<img width="960" height="540" alt="I see it I like it I want it I got it (3)" src="https://github.com/user-attachments/assets/4cde3fa5-dce1-4862-b1c9-5b82426dd5d8" />
<img width="960" height="540" alt="I see it I like it I want it I got it (4)" src="https://github.com/user-attachments/assets/d9eb513c-59a2-4633-ab69-015edbc52668" />



## Features

- **Conversational interaction:** Speech-based interactions designed around memory and recall.
- **Speech transcription:** Converts recorded audio into text while attempting to preserve hesitations, filler words, and repetitions.
- **Acoustic analysis:** Extracts features such as speech duration, pauses, pitch, and pitch variability.
- **Lexical and syntactic analysis:** Examines vocabulary diversity, filler-word frequency, sentence length, and pronoun-to-noun ratios.
- **Narrative analysis:** Uses an LLM to estimate discourse coherence, ambiguous references, and repetition.
- **Session-based tracking:** Stores session-level results to support longitudinal analysis.

## How It Works

1. **Record:** The Android application captures a user's speech during an interaction.
2. **Store:** Audio recordings are stored using Firebase Storage.
3. **Process:** The backend retrieves recordings and normalizes audio into mono, 16 kHz WAV files.
4. **Analyze:** Speech is transcribed and passed through acoustic, lexical, syntactic, and narrative analysis modules.
5. **Persist:** Session results are stored in Cloud Firestore for subsequent retrieval and longitudinal tracking.

## Architecture

```text
Android Application
(Kotlin + Jetpack Compose)
          |
          v
Firebase Authentication
Firebase Storage
Cloud Firestore
          |
          v
Python Backend
(FastAPI)
          |
          v
Audio Preprocessing
(FFmpeg)
          |
          v
Speech Transcription
(Groq Whisper)
          |
          v
Feature Extraction
  ├── Acoustic
  ├── Lexical & Syntactic
  └── Narrative
          |
          v
Cloud Firestore
(Session-level results)
```

## Tech Stack

| Component | Technologies |
|---|---|
| Android app | Kotlin, Jetpack Compose |
| Backend API | Python, FastAPI |
| Authentication | Firebase Authentication |
| Data storage | Cloud Firestore, Firebase Storage |
| Audio processing | FFmpeg, Librosa, NumPy |
| Speech transcription | Groq Whisper API |
| Narrative analysis | Groq API, LLM-based analysis |
| Language processing | spaCy |


## Getting Started

#### For a quick test, download the APK file on an android device through https://drive.google.com/file/d/1mO8jtwOHAm8t3p0RkoGG9YRlNgprmb65/view?usp=sharing & log-in to the caretaker dashboard here https://echo-caretaker-dashboard.onrender.com/

### Prerequisites

- Android Studio and a compatible Android SDK
- Python 3.10 or a version compatible with the project's dependencies
- A Firebase project with Authentication, Cloud Firestore, and Cloud Storage configured
- A Groq API key
- FFmpeg installed and available on your system

### Android Application

1. Clone the repository:

   ```bash
   git clone https://github.com/MyraArora/echo.git
   cd echo
   ```

2. Open the project in Android Studio.

3. Configure your local Firebase setup and required API credentials.

4. Build and run the application on a compatible Android device or emulator.

### Backend

1. Navigate to the backend directory:

   ```bash
   cd backend
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

3. Install the backend dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Configure the required environment variables and Firebase credentials.

5. Start the development server:

   ```bash
   uvicorn main:app --reload
   ```

   The API documentation is available at `http://127.0.0.1:8000/docs` when the server is running.

> **Setup note:** The dependency list, credentials, environment variables, and backend deployment configuration must be complete for a fresh installation. See the project configuration before running the pipeline.

## Limitations

- The extracted features are exploratory measurements, not validated clinical indicators.
- Speech characteristics vary with language, accent, age, environment, and individual speaking style.
- LLM-generated narrative assessments may be inconsistent or incorrect.
- Longitudinal changes require repeated observations and careful interpretation.
- Echo has not been established as a substitute for professional clinical assessment.

## Future Directions

Potential areas for further development include validating feature extraction against appropriate datasets, evaluating longitudinal trends, improving robustness across speakers, and studying how conversational design affects the quality of collected data.

## Recognitions

Echo was the winner of the India AI Tinkerpreneur competition, by Intel & Niti Aayog (govt of India). The developers were invited to showcase my work at the  India-AI Impact Summit, the first-ever global AI summit hosted in the Global South, in front of various dignitaries & industry leaders.

## Authors

**Myra Arora, Kriday Moudgil**

