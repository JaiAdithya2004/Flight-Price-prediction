## Flight Price Prediction Web Application

This project implements a web application for predicting flight prices using a pre-trained machine learning model. The application is built with Flask, containerized using Docker, and deployed on Render for public access.

## Project Structure

- `app.py`: Flask application script handling routing, preprocessing, model inference, and UI rendering
- `model.pkl`: Serialized pre-trained machine learning model
- `templates/home.html`: HTML template providing the user interface
- `Dockerfile`: Defines the Docker image for containerizing the app
- `requirements.txt`: Python dependencies for the application

## Dependencies

The application uses:

- `Flask`: Web framework
- `pickle`: For loading the trained ML model
- `pandas`: Feature extraction and preprocessing
- `numpy`: Handling numerical arrays

Install dependencies locally:
```bash
pip install -r requirements.txt
```

## Workflow Details

### Data Preprocessing

- Extracts date & time features (Journey_day, Dep_hour, Arrival_hour, etc.)
- Extracts duration features (Duration_hours, Duration_minutes)
- Converts stops into integers
- Encodes categorical features (Airline, Source, Destination) via one-hot encoding

### Model Loading & Prediction

- Loads `model.pkl` at application startup
- Transforms user inputs → numerical features → passes into model’s `predict()`
- Returns predicted price (rounded to 2 decimals)

### Web Interface

- Home (`/`) → Displays form for input
- Predict (`/predict`) → Accepts form submission, runs prediction, and displays result

## How to Run Locally

1.  **Clone the repository** and ensure files are present (`app.py`, `model.pkl`, `templates/`, `Dockerfile`, `requirements.txt`)
2.  **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the Flask app**:
    ```bash
    python app.py
    ```
4.  **Access in browser**:
    `http://127.0.0.1:5000/`

## Docker Setup

The project is containerized for easy deployment.

### Build Docker Image
```bash
docker build -t flight-price-prediction .
```

### Run Docker Container
```bash
docker run -p 5000:5000 flight-price-prediction
```

### Access Application
`http://localhost:5000/`

(You can also manage containers and logs with Docker Desktop.)

## Deployment on Render

The project is deployed on Render for public access.

### Steps to Deploy

1.  **Push your Docker image to Docker Hub**:
    ```bash
    docker tag flight-price-prediction username/flight-price-prediction
    docker push username/flight-price-prediction
    ```
2.  **On Render Dashboard, create a Web Service**
3.  **Select Docker environment** and provide your Docker Hub image
4.  **Set Start Command**:
    ```bash
    gunicorn app:app -b 0.0.0.0:$PORT
    ```
    Render builds & deploys automatically.

### Live Demo

🔗 Access the deployed app here:

Flight Price Prediction on Render:


https://flightpriceprediction-latest.onrender.com


