 MediBot: AI-Powered Symptom Diagnosis

MediBot is a full-stack application designed to provide preliminary diagnosis based on user-described symptoms using a Machine Learning model. The system intelligently handles natural language input, corrects minor typos, and provides top-3 disease predictions with confidence scores.

 Features

AI Symptom Analysis: Predicts the top 3 most likely diseases based on input symptoms using a trained Random Forest Classifier.

Natural Language Processing (NLP): Processes full sentences (e.g., "I have a high fever and a sore throat") and extracts relevant symptom keywords.

Fuzzy Matching & Correction: Uses Python's built-in difflib to identify and match misspelled symptoms to the dataset's official column names (e.g., matching "headach" to "headache").

Safe API Design (FastAPI): Ensures the frontend receives a standardized response (predictions + error status) even when input is invalid, preventing client-side crashes.

Modern Frontend: Built with React/TypeScript for a responsive, single-page application experience.

🛠️ Technology Stack

Component

Technology

Role

Frontend (Client)

React (with TypeScript)

UI/UX, Chat Interface, Displays Diagnosis Reports.

Backend (API)

FastAPI

High-performance Python API endpoint for receiving symptom data and serving predictions.

Machine Learning

Python, Scikit-learn (Random Forest)

Trained model used for calculating disease probability.

Data Processing

Pandas, NumPy, difflib

Data vectorization, model input prep, and intelligent symptom extraction/correction.

Styling

Tailwind CSS (inferred)

Utility-first CSS framework for responsive and modern aesthetics.

 Getting Started

Follow these steps to set up and run the MediBot application locally.

Prerequisites

You need Python 3.8+ and Node.js (for the React frontend) installed on your machine.

Clone the Repository:

git clone [YOUR_REPOSITORY_URL]
cd MediBot


Install Python Dependencies:
It is highly recommended to use a virtual environment.

python -m venv venv
.\venv\Scripts\activate  # On Windows
source venv/bin/activate # On Linux/macOS

pip install -r requirements.txt


(Reference requirements.txt)

fastapi
uvicorn[standard]
scikit-learn
pandas
numpy
joblib
python-multipart


Prepare the ML Model:
(Assuming you have a script named ml/train.py that generates the necessary random_forest_model.joblib, label_encoder.joblib, and symptom_columns.joblib files in the ml/saved_model directory.)

# Run your training script once to generate model artifacts
python ml/train.py 


Running the Application

Start the Backend API (Terminal 1):
Navigate to the root directory and start the Uvicorn server.

uvicorn app.main:app --reload


The API should now be running at http://127.0.0.1:8000.

Start the Frontend (Terminal 2):
(Note: This step assumes standard React project setup. Replace with your actual frontend start command, e.g., npm start or npm run dev.)

cd frontend # Change to your frontend directory (if applicable)
npm install
npm start # Or your specific start command


The application will open in your browser, connecting to the FastAPI server at port 8000 for diagnosis predictions.

 Usage and Error Handling

Input Examples

The model is designed to accept symptoms in natural language:

Input

Symptoms Recognized

"I have high fever and a slight headache."

high_fever, headache

"vomiting, fatigue, dizziness"

vomiting, fatigue, dizziness

"bodyayche"

body_ache (Corrected via fuzzy matching)

Error Messages

The frontend is specifically configured to display helpful messages when the input is insufficient:

API Connection Error: If the server is offline.

"I couldn't identify any specific symptoms...": If the AI model cannot recognize any valid keywords or typos from the input text.

"Please write correct symptoms and send again.": If keywords were recognized but resulted in zero predictions from the ML model (e.g., if the user enters only one vague symptom not strongly tied to any disease).

 File Structure Overview

MediBot/
├── app/
│   ├── main.py       # FastAPI application, defines /predict endpoint
│   └── model.py      # ML wrapper, handles symptom cleaning, validation, and prediction
├── ml/
│   ├── train.py      # Script to train the ML model (assumed)
│   └── saved_model/  # Directory for model artifacts (.joblib files)
├── frontend/         # Your React/TSX files
│   └── index.tsx     # Main application/component file
└── requirements.txt  # Python dependencies
