# Project Folder Structure: Hotel Check-in System

This document outlines the folder structure and components of the **Hotel Check-in System with Face Authentication and Anti-Spoofing**.

```text
Hotel_Check-in_System/
├── FOLDER_STRUCTURE.md                             # Project folder structure description (this file)
├── .gitignore                                      # Root Git ignore rules
├── 422001503101_Nhom2_UngDungXacThucKhuonMat...pdf # Project documentation report (PDF)
├── 422001503101_Nhom2_UngDungXacThucKhuonMat...pptx# Project presentation slide (PPTX)
└── FinalProject_CV/                                # Main Computer Vision & Web Application folder
    ├── FaceAntiSpoofing/                           # Jupyter Notebook for Face Anti-Spoofing Model training
    │   └── FAS_Model.ipynb                         # Model development, EDA and training pipeline
    └── FaceAuthorizationSystem/                    # Face Authorization Web Application
        ├── .gitattributes                          # Git attributes for LFS / line endings
        ├── .gitignore                              # Main application gitignore
        ├── FaceAuthorization_MicroService/         # Python Flask/FastAPI Microservice for AI Face Authentication
        │   ├── BackendServer.py                    # Python Server routing for Face Anti-Spoofing & Verification
        │   ├── Face_Anti_Spoofing_Model_...pth    # Trained PyTorch Model weights (.pth)
        │   └── requirements.txt                    # Python dependencies
        ├── backend/                                # Node.js Express Backend
        │   ├── app.js                              # Main server entrypoint
        │   ├── hash.js                             # Hashing utility for passwords/keys
        │   ├── package.json                        # Node dependencies and scripts
        │   ├── controllers/                        # Controller logic (handles requests)
        │   │   ├── auths-controllers.js            # User/Guest face & password auth
        │   │   ├── booking-controllers.js          # Room booking handling
        │   │   ├── management-controllers.js       # Employee & hotel system management
        │   │   └── rooms-controllers.js            # Room status management
        │   ├── middleware/                         # Custom express middleware (auth, cors, file-upload)
        │   ├── models/                             # Mongoose Database Models (MongoDB schemas)
        │   │   ├── Booking.js                      # Booking Schema
        │   │   ├── Employee.js                     # Employee Schema
        │   │   ├── Guest.js                        # Guest / Customer Schema
        │   │   ├── Room.js                         # Room Schema
        │   │   ├── RoomKey.js                      # Generated Digital Room Keys
        │   │   └── http-error.js                   # Custom HTTP Error handler model
        │   ├── routes/                             # API Routes definition
        │   │   ├── auths-routes.js
        │   │   ├── booking-routes.js
        │   │   ├── management-routes.js
        │   │   └── rooms-routes.js
        │   └── validators/                         # Input request validators
        └── frontend/                               # React + Vite Frontend
            ├── index.html                          # Entry HTML
            ├── vite.config.js                      # Vite bundle configuration
            ├── package.json                        # Frontend packages and scripts
            ├── public/                             # Public static assets
            └── src/                                # React application source code
                ├── main.jsx                        # React app entry point
                ├── App.jsx                         # Main app router & component tree
                ├── index.css                       # Global styles
                ├── assets/                         # UI images and icons
                ├── components/                     # Reusable UI React Components
                ├── data/                           # Mock data or constant values
                ├── pages/                          # Page components (Login, Booking, Admin Dashboard)
                └── util/                           # Utility and helper functions
```

---

## Component Summaries

### 1. `FaceAntiSpoofing`
* **Technology**: Python, PyTorch, Jupyter Notebook.
* **Role**: Model research and development. It contains the logic to train the deep learning model capable of distinguishing between real human faces and spoofing attempts (e.g., photos, videos, masks).

### 2. `FaceAuthorization_MicroService`
* **Technology**: Python, Flask, PyTorch.
* **Role**: A lightweight microservice that loads the trained PyTorch anti-spoofing model (`.pth`) and serves an API endpoint. When the main backend receives a check-in image, it queries this microservice to verify face authenticity before checking the user in.

### 3. `backend`
* **Technology**: Node.js, Express, MongoDB/Mongoose.
* **Role**: The main application server. It orchestrates user registration, booking flow, room key generation, and coordinates authentication checks with the Face Authorization Microservice.

### 4. `frontend`
* **Technology**: React, Vite, CSS.
* **Role**: The interactive client-side user interface. Provides dashboards for guests to check in using their camera, and administration screens for hotel employees to monitor room occupancy and booking logs.
