# Automated Hotel Check-in System with Face Authentication and Anti-spoofing

> [!NOTE]  
> This is an automated hotel check-in system integrated with Face Recognition and Biometric Liveness Detection (Anti-spoofing). The project is developed to optimize the check-in workflow at hotels, enhance security, and deliver a seamless, contactless self-service experience for guests.

---

## 📖 Project Overview

The system provides an end-to-end solution from online room booking and room management to automated self-service check-in using facial recognition. The core of the system is real-time dual-layer biometric authentication:
1. **Liveness Detection (Anti-spoofing):** Utilizes a custom-trained **ResNet-18** Deep Learning model to detect presentation attacks (spoofing attempts) such as printed photos, replay attacks via screens (mobiles/tablets), or masks.
2. **Face Matching (Recognition):** Utilizes the state-of-the-art **InsightFace (buffalo_l model)** to extract highly accurate face embeddings and verify them against the face profile registered during booking.

### Key Features:
* **Guest Portal (Client facing):**
  * Search, view details, and book hotel rooms online.
  * Register guest details and capture a portrait photo (extract and save high-quality face embeddings as a biometric key).
  * Self-service contactless check-in at hotel Kiosks using real-time camera feeds to generate a digital room key.
* **Admin Dashboard (Employee/Management facing):**
  * Manage rooms, room availability, and live status (Available, Booked, Occupied).
  * Oversee booking transactions, check-in logs, and room keys.
  * System configurations, user role authorization, and logs.

---

## 🏗️ System Architecture

The project is built on a **Microservices** architecture, cleanly separating core services:

```text
┌────────────────┐        HTTP Requests        ┌───────────────────────┐
│                ├────────────────────────────>│  Node.js Express API  │
│ React Frontend │                             │  (Main Backend & DB)  │
│  (Port 5173)   │<────────────────────────────┤      (Port 3000)      │
└───────┬────────┘        Response Json        └───────────┬───────────┘
        │                                                  │
        │ Send Base64 Face Image                           │ Query / Match Embeddings
        │ (Liveness & Authenticate)                        │
        ▼                                                  ▼
┌──────────────────────────────────────────────────────────────────────┐
│                  Python AI Authentication Microservice               │
│                  (Flask + PyTorch + InsightFace)                     │
│                            (Port 5000)                               │
└──────────────────────────────────────────────────────────────────────┘
```

* **Frontend:** React, Vite, TailwindCSS v4, HeadlessUI, MediaPipe Tasks-Vision.
* **Main Backend:** Node.js, Express, MongoDB (Mongoose ODM).
* **AI Microservice:** Python 3.9+, Flask, PyTorch (ResNet-18 FAS), InsightFace, OpenCV.

> [!TIP]  
> A detailed overview of the project structure can be found in the [FOLDER_STRUCTURE.md](file:///c:/Users/vinhp/OneDrive/M%C3%A1y%20t%C3%ADnh/Hotel_Check-in_System/FOLDER_STRUCTURE.md) file.

---

## 🛠️ Installation & Setup

### 📋 Prerequisites
* **Node.js** (Recommended: v18 or higher)
* **Python** (Recommended: 3.9 - 3.11)
* **MongoDB** (The project currently connects directly to a MongoDB Atlas cluster; ensure your machine is connected to the Internet).

---

### Step 1: Clone the Repository
Open your terminal and clone the project:
```bash
git clone https://github.com/chauquocvinh2234/Automated_Hotel_Check-in_System_with_Face_Authentication_and_Anti-spoofing.git
cd Automated_Hotel_Check-in_System_with_Face_Authentication_and_Anti-spoofing
```

---

### Step 2: Set up the Python AI Authentication Microservice
This microservice processes heavy AI tasks like liveness detection and face embedding extraction.

1. **Navigate to the microservice directory:**
   ```bash
   cd FinalProject_CV/FaceAuthorizationSystem/FaceAuthorization_MicroService
   ```

2. **Create and activate a virtual environment (Recommended):**
   ```bash
   python -m venv venv
   # On Windows (PowerShell)
   .\venv\Scripts\Activate.ps1
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Launch the Flask Server:**
   ```bash
   python BackendServer.py
   ```
   > [!IMPORTANT]  
   > Upon the first launch, the InsightFace library will automatically download the `buffalo_l` face analysis models. Please ensure a stable internet connection. The AI microservice server will run on `http://localhost:5000`.

---

### Step 3: Set up the Node.js Backend Server
This backend orchestrates the main hotel business logic and communicates with the MongoDB database.

1. **Open a new terminal window and navigate to the backend folder:**
   ```bash
   cd FinalProject_CV/FaceAuthorizationSystem/backend
   ```

2. **Install Node modules:**
   ```bash
   npm install
   ```

3. **Configure environment variables (`.env`):**
   Create a `.env` file in the backend root directory (next to `app.js`) and define the JWT secret key:
   ```env
   JWT_KEY=THI_GIAC_MAY_TINH_SECRET_KEY
   ```

4. **Launch the Backend Server:**
   ```bash
   npm start
   ```
   *The main backend server will start on `http://localhost:3000` and automatically connect to the MongoDB Atlas cluster.*

---

### Step 4: Set up the React Frontend (Vite)
This is the interactive client-side user interface.

1. **Open a new terminal window and navigate to the frontend folder:**
   ```bash
   cd FinalProject_CV/FaceAuthorizationSystem/frontend
   ```

2. **Install frontend dependencies:**
   ```bash
   npm install
   ```

3. **Launch the development server:**
   ```bash
   npm run dev
   ```
   *Open your browser and navigate to `http://localhost:5173` to explore the system!*

---

## 🏆 Contributors
This project was developed by **Chau Quoc Vinh** (Group 2) as a practical application for the Computer Vision (CV) course. For any issues or feature requests, feel free to open a Pull Request or file an Issue on the official repository.
