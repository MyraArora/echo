# Echo

**A conversational cognitive monitoring app exploring how speech and language can help track changes in cognitive function over time.**

Echo combines everyday conversational interaction with audio processing and linguistic analysis to explore patterns in speech, memory, and narrative coherence.

> **Note:** Echo is an experimental project, not a clinically validated diagnostic tool. Its outputs should not be used to diagnose or rule out cognitive impairment.

---

## Overview

Cognitive changes can be difficult to recognize from a single interaction. Echo explores whether repeated speech and memory exercises, combined with longitudinal analysis, can help surface patterns that may otherwise go unnoticed.

The project brings together an Android application, a Python backend, and a feature-extraction pipeline to analyze audio and transcript data across sessions.

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

## Project Structure

```text
echo/
├── app/                       # Android application
│   └── src/main/
│       └── java/com/example/echov2/
├── backend/
│   ├── main.py                # FastAPI application
│   ├── requirements.txt       # Python dependencies
│   └── app/pipeline/
│       ├── audio_fetcher.py   # Audio retrieval
│       ├── transcription.py   # Speech transcription
│       ├── acoustic.py        # Acoustic feature extraction
│       ├── syntax_lexical.py  # Linguistic feature extraction
│       └── narrative.py      # Narrative analysis
└── README.md
```

## Getting Started

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

## Author

**Myra Arora, Kriday Moudgil**

[GitHub Repository](https://github.com/MyraArora/echo)
