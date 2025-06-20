# 🎙️ AI-Powered Speech Therapy Assistant

**A comprehensive, AI-driven mobile application designed to provide real-time analysis and personalized therapy for individuals with speech disfluencies. This project serves as a Final Year Project, demonstrating a complete client-server system with an advanced machine learning model.**

![Kotlin](https://img.shields.io/badge/Kotlin-100%25-7F52FF?style=for-the-badge&logo=kotlin)
![Python](https://img.shields.io/badge/Python-3.9-3776AB?style=for-the-badge&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-AI%20Model-EE4C2C?style=for-the-badge&logo=pytorch)
![Firebase](https://img.shields.io/badge/Firebase-Full%20Suite-FFCA28?style=for-the-badge&logo=firebase)
![Android](https://img.shields.io/badge/Android-MVVM-3DDC84?style=for-the-badge&logo=android)

---

### ✨ **Live Dashboard & Technical Overview**

A live, interactive web dashboard detailing the project's architecture, components, and features has been deployed.

**[➡️ View the Live Project Dashboard](https://speech-therapy-dashboard1.onrender.com/)**

---

## 🎯 **Core Features**

* 🧠 **Real-time AI Stutter Detection:** Utilizes a custom-trained Audio Spectrogram Transformer (AST) model to classify speech into four distinct categories (`Block`, `Prolongation`, `Interjection`, `Fluent`) from a live audio stream.
* 📊 **Interactive Visualization:** Provides users with a real-time waveform display and a color-coded timeline that visualizes detected speech patterns, offering immediate and intuitive feedback.
* 🏋️ **Personalized Exercise Regimen:** An adaptive planner (`AdaptivePlanner`) analyzes session results to recommend targeted exercises from a comprehensive library (`exercises.json`), focusing on areas like breathing, vocal control, and fluency.
* 📈 **Advanced Progress Analytics:** A dedicated progress screen (`ProgressFragment`) with multiple charts showing fluency trends over time, stutter pattern breakdowns, and weekly improvement metrics.
* 🏥 **Clinical & Therapist Dashboard:** A secure, role-based dashboard for therapists to view patient progress, create assessments, and manage therapy plans, demonstrating the app's potential for professional use.
* 🔒 **Secure User Authentication:** A complete authentication system using Firebase for email/password sign-in, user registration, and secure profile management with role separation (`patient` vs. `therapist`).
* 🌐 **Multi-Language Support:** The UI is architected with full support for localization, with string resources provided for over 11 languages.

---

## 🛠️ **Technology Stack**

### **📱 Android Application (Client)**

| Component        | Technology & Libraries                                                                     |
| :--------------- | :----------------------------------------------------------------------------------------- |
| **Language** | [**Kotlin**](https://kotlinlang.org/) (100%)                                               |
| **Architecture** | **MVVM** (Model-View-ViewModel), Single-Activity, Repository Pattern                       |
| **UI** | **XML**, Material Design 3, `ConstraintLayout`, `CoordinatorLayout`, `RecyclerView`          |
| **Asynchronicity**| **Kotlin Coroutines** & `StateFlow` for reactive UI updates                                  |
| **Navigation** | **Jetpack Navigation Component** with Safe Args                                            |
| **Networking** | **Retrofit2** & **OkHttp3** for type-safe communication with the AI server                   |
| **Database** | **Firebase Firestore** for user data, session history, and clinical assessments          |
| **Authentication**| **Firebase Authentication** (Email/Password & Google Sign-In)                              |
| **Visualization**| **MPAndroidChart** for progress graphs, Custom `View` for real-time waveform               |
| **Audio** | **`AudioRecord` API** for low-level audio capture, **TarsosDSP** for on-device processing    |

### **🤖 AI Backend (Server)**

| Component          | Technology & Libraries                                        |
| :----------------- | :------------------------------------------------------------ |
| **Framework** | **Flask** (Python)                                            |
| **ML Inference** | **PyTorch** & **TorchScript** for running the quantized AST model |
| **Audio Processing** | **Librosa** for converting raw PCM audio to mel-spectrograms  |
| **Data Handling** | **NumPy** for numerical operations                            |

---

## 🏗️ **Architecture & Data Flow**

The application employs a robust, scalable architecture combining a modern Android client with a powerful Python backend for AI inference.

1.  **Client-Side (MVVM):** The Android app uses the Model-View-ViewModel pattern to separate UI (`Fragments`/`XML`) from business logic (`ViewModels`) and data operations (`Repositories`). This ensures a maintainable and testable codebase.

2.  **Server-Side (AI Inference):** The computationally expensive AST model is hosted on a Python Flask server. The Android client streams 3-second chunks of audio data; the server performs preprocessing, runs model inference, and returns a JSON object with the 4-class probabilities.

### **End-to-End Data Flow**

| Step | Action                      | Location        | Key Technology                                   |
| :--: | :-------------------------- | :-------------- | :----------------------------------------------- |
|  1   | **User Speaks** | Android App     | `AudioRecord` API                                |
|  2   | **Audio is Buffered** | Android App     | `RealTimeStutterDetector` (Kotlin Ring Buffer)   |
|  3   | **Data Sent to Server** | Network         | `Retrofit2` HTTP POST Request                    |
|  4   | **Audio Processed** | Python Server   | `Librosa` (Mel-Spectrogram)                      |
|  5   | **AI Prediction** | Python Server   | `PyTorch` (AST Model)                            |
|  6   | **Results Returned** | Network         | `Flask` JSON Response                            |
|  7   | **App State Updated** | Android App     | `ViewModel` with `StateFlow`                     |
|  8   | **UI Reacts to State** | Android App     | `Fragments`, `SpeechFlowVisualizationView`       |
|  9   | **Session Data Persisted** | Cloud           | `Firebase Firestore`                             |

---

## 🔬 **The 4-Class AI Detection System**

A key innovation of this project is the custom 4-class AI model, which distinguishes between clinically significant stuttering events and normal speech disfluencies. This allows for more precise and effective therapeutic intervention.

### **Class Definitions**

| Class               | Category            | Clinical Significance                                     |
| :------------------ | :------------------ | :-------------------------------------------------------- |
| 🔴 **Block** | Clinical Stutter    | Complete blockage of airflow; a primary therapy target.   |
| 🟣 **Prolongation** | Clinical Stutter    | Unnatural stretching of sounds; requires intervention.    |
| 🟠 **Interjection** | Normal Disfluency   | Fillers like "um" or "uh"; less clinically significant.   |
| 🟢 **No_Stutter** | Fluent Speech       | The target goal; used as a baseline for fluency score.    |

This distinction allows the **`AdaptivePlanner`** to recommend targeted therapeutic exercises for clinical patterns while providing gentler, more encouraging feedback for normal disfluencies.

---

## 🚀 **Project Status: Complete & Deployed**

This project has successfully implemented and integrated all core components, resulting in a fully functional, end-to-end system. The progress achieved has significantly surpassed initial project milestones, with all major systems at or near 100% completion.

| Component                       | Status                                                                    |
| :------------------------------ | :------------------------------------------------------------------------ |
| **Core Architecture** | ✅ **100%** - Modern, scalable MVVM architecture is fully implemented.    |
| **AI Model & Server** | ✅ **100%** - 4-class PyTorch model deployed and serving real-time requests.|
| **User Authentication** | ✅ **100%** - Secure user registration/login with role management is complete.  |
| **Real-time Detection** | ✅ **100%** - The core feature of the app is fully functional.             |
| **Exercise & Feedback System** | ✅ **95%** - Framework is complete; correctly recommends exercises.      |
| **Progress & Clinical Dashboards** | ✅ **95%** - All charts are implemented; data is correctly visualized.     |

---

## 🎯 **Final Steps for Project Completion**

The remaining work is focused on final testing, refinement, and academic documentation to prepare the project for its official launch and defense.

-   [ ] **Final UI/UX Refinements:** Minor adjustments and polish across all screens to ensure a professional and seamless user experience.
-   [ ] **User Acceptance Testing (UAT):** Conduct testing sessions with a small group of users to gather qualitative feedback on usability, app flow, and the effectiveness of the feedback.
-   [ ] **Prepare Final Presentation:** Create the slide deck and presentation materials for the final project defense, including a live demonstration of the complete system.
-   [ ] **Write Final Report:** Complete the comprehensive academic report detailing the project's research, methodology, implementation, results, and future work.

---

## 🧑‍💻 Author & Contact

* **Pedro Fabian Mange Owono Ondo**
* **GitHub:** [Owono2001](https://github.com/Owono2001) 
* **Email:** [owonoondomangue@gmail.com](mailto:owonoondomangue@gmail.com)
* **Portfolio:** [View My Website](https://myportfolio-b-type.onrender.com/)

---
