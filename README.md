# ✨ Face Recognition System

A Streamlit-based web application that performs face recognition using the `face_recognition` library. The app supports two modes: real-time detection via webcam and static detection via image upload.

## 📋 Features
* **Live Camera Mode:** Detects and recognizes faces in real-time using your computer's webcam.
* **Upload Image Mode:** Allows users to upload `.jpg`, `.jpeg`, or `.png` files for analysis.
* **Visual Annotation:** Draws bounding boxes and labels around detected faces.

## 🛠️ Prerequisites

Before installing the requirements, ensure you have the necessary build tools installed, as `face-recognition` depends on `dlib`.

* **Windows:** Install [Visual Studio C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) and [CMake](https://cmake.org/download/).
* **macOS:** `brew install cmake`
* **Linux:** `sudo apt-get install cmake build-essential`

## 📦 Installation

1.  **Clone the repository (or download the files):**
    ```bash
    git clone <your-repo-url>
    cd <your-repo-folder>
    ```

2.  **Create a virtual environment (Optional but recommended):**
    ```bash
    python -m venv venv
    # On Windows:
    venv\Scripts\activate
    # On Mac/Linux:
    source venv/bin/activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## ⚙️ Setup: The Model File

The application requires a file named `face_model.pkl` in the root directory. This file must contain the known face encodings and names.

**File Structure:**
The `.pkl` file must be a serialized Python dictionary with the following keys:
* `"encodings"`: A list of face encodings (numpy arrays).
* `"names"`: A list of strings corresponding to the names of the people in the encodings list.

**Example script to generate `face_model.pkl`:**
If you don't have the model file yet, run a script like this once:

```python
import face_recognition
import pickle

# 1. Load your reference images
img_person1 = face_recognition.load_image_file("person1.jpg")
img_person2 = face_recognition.load_image_file("person2.jpg")

# 2. Get encodings (assuming one face per image)
encoding1 = face_recognition.face_encodings(img_person1)[0]
encoding2 = face_recognition.face_encodings(img_person2)[0]

# 3. Create the data structure
data = {
    "encodings": [encoding1, encoding2],
    "names": ["Person One", "Person Two"]
}

# 4. Save to pickle
with open("face_model.pkl", "wb") as f:
    pickle.dump(data, f)
