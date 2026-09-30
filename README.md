# Insurance Premium Prediction API

A lightweight machine learning-backed web service built with **FastAPI** to predict insurance premiums based on individual user parameters. Developed strictly for **learning and educational purposes** to explore backend API development, data preprocessing, and model serving.

---

## Features
- **FastAPI Backend:** High-performance, asynchronous API endpoints with automatic interactive documentation (Swagger UI).
- **Input Validation:** Pydantic models ensuring incoming request payloads are rigorously validated.
- **Learning Implementation:** Built to understand the end-to-end lifecycle of training a predictive model and serving it via a production-style microservice framework.

---

## Tech Stack
- **Python**
- **FastAPI**
- **Uvicorn**
- **Scikit-Learn** / Machine Learning libraries
- **Pydantic**

---

## Project Structure
```text
model/
│
├── main.py            # FastAPI application entry point
├── model.pkl          # Trained machine learning model (or artifact directory)
├── requirements.txt   # Project dependencies
└── README.md          # Project documentation
