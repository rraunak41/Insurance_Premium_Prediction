# Insurance Premium Prediction

A machine learning web application that predicts an **insurance premium category** from user-provided demographic, lifestyle, income, city, and occupation information.

The project uses a **FastAPI backend** for model inference and a **Streamlit frontend** for the user interface. The application is containerized with **Docker** and deployed on **AWS EC2**.

## 🚀 Live Demo

**AWS Live Application:**  
http://13.233.131.56:8501

> The live application is hosted on an AWS EC2 instance. Availability depends on the EC2 instance being running and its current public IP address.

## ✨ Features

- Machine-learning based insurance premium category prediction
- FastAPI REST API for model inference
- Pydantic-based request/response validation
- Interactive Streamlit frontend
- Prediction confidence and class probabilities
- Dockerized backend and frontend
- Docker Compose support for local multi-container deployment
- Deployed on AWS EC2
- Docker images published to Docker Hub

## 🏗️ Architecture

```text
                    User
                     |
                     v
          +----------------------+
          |  Streamlit Frontend  |
          |      Port 8501       |
          +----------+-----------+
                     |
                     | HTTP
                     v
          +----------------------+
          |    FastAPI Backend   |
          |      Port 8000       |
          +----------+-----------+
                     |
                     v
          +----------------------+
          |  ML Model (model.pkl)|
          +----------------------+

AWS EC2
└── Docker
    ├── frontend container : 8501
    └── backend container  : 8000 (internal)
```

The backend is kept private inside the Docker network. Only the Streamlit frontend port (**8501**) is exposed publicly.

## 🛠️ Tech Stack

- **Python**
- **FastAPI**
- **Uvicorn**
- **Streamlit**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- **Pydantic**
- **Docker**
- **Docker Compose**
- **AWS EC2**
- **Docker Hub**

## 📁 Project Structure

```text
Insurance_Premium_Prediction/
│
├── config/
│   └── city_tier.py
│
├── schema/
│   ├── prediction_response.py
│   └── user_input.py
│
├── app.py
├── frontend.py
├── predict.py
├── model.pkl
│
├── Dockerfile
├── Dockerfile.frontend
├── docker-compose.yml
│
├── requirements-backend.txt
├── requirements-frontend.txt
├── requirements.txt
├── .dockerignore
├── .gitignore
└── README.md
```

## 🔌 API Endpoints

### Home

`GET /`

Returns a basic API status message.

### Health Check

`GET /health`

Example response:

```json
{
  "status": "OK",
  "version": "1.0.0",
  "model_loaded": true
}
```

### Prediction

`POST /predict`

The endpoint accepts the validated user input and returns:

- Predicted insurance premium category
- Prediction confidence
- Class probabilities

Interactive API documentation is available through FastAPI Swagger UI at:

`/docs`

When running locally:

http://localhost:8000/docs

## 🐳 Docker

The application is split into two containers:

- **Backend:** FastAPI + ML model
- **Frontend:** Streamlit UI

### Docker Hub Images

- Backend: https://hub.docker.com/r/rraunak41/insurance-backend
- Frontend: https://hub.docker.com/r/rraunak41/insurance-frontend

### Run with Docker Compose

```bash
docker compose up --build
```

Then open:

http://localhost:8501

## ☁️ AWS EC2 Deployment

The application is deployed on an **AWS EC2 Ubuntu 24.04 LTS** instance in the **Asia Pacific (Mumbai) / ap-south-1** region.

Deployment flow:

```text
Docker Hub
   |
   | docker pull
   v
AWS EC2
   |
   +--> backend container
   |
   +--> frontend container
           |
           v
       Port 8501
           |
           v
      Public Internet
```

The backend is accessible only through the Docker network, while port **8501** is exposed through the EC2 security group for the Streamlit application.

### Current deployment

- **Frontend:** Port 8501
- **Backend:** Port 8000 internally
- **Hosting:** AWS EC2
- **Containerization:** Docker
- **Registry:** Docker Hub

## 💻 Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/rraunak41/Insurance_Premium_Prediction.git
cd Insurance_Premium_Prediction
```

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv myenv
.\myenv\Scripts\Activate.ps1
```

### 3. Install backend dependencies

```bash
pip install -r requirements-backend.txt
```

### 4. Start FastAPI

```bash
uvicorn app:app --reload
```

The API will be available at:

http://localhost:8000

### 5. Start Streamlit

Open another terminal and run:

```bash
pip install -r requirements-frontend.txt
streamlit run frontend.py
```

The frontend will be available at:

http://localhost:8501

## 🤖 Model

The application loads the trained model from:

```text
model.pkl
```

The model is loaded by `predict.py` and used by the FastAPI `/predict` endpoint.

If `model.pkl` is not included in a fresh clone, place the trained model artifact in the project root before running the backend or building the Docker image.

## ⚠️ Deployment Note

The AWS demo currently uses the EC2 instance's public IPv4 address. If the EC2 instance is stopped and started again, AWS may assign a different public IP unless an Elastic IP is configured.

Therefore, the Live Demo URL may need to be updated in this README after an EC2 public IP change.

## 📌 Project Purpose

This project was built to understand the complete workflow of taking a machine-learning model and exposing it as a web application:

```text
ML Model
   ↓
FastAPI API
   ↓
Streamlit UI
   ↓
Docker
   ↓
Docker Hub
   ↓
AWS EC2
   ↓
Live Application
```

