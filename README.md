# 🚀 Urban Sound Denoiser — Complete Project Workflow

This README provides a **step-by-step guide** for running the **Urban Sound Denoiser Project**, covering both **training** and **testing phases** using Kaggle notebooks.

---

## 🧠 PHASE 1: Train the Model

**File:** `Train/train.ipynb`

The goal of this phase is to train a **CNN model** using the **UrbanSound8K dataset** and generate the output file `model.h5`.

### 🔧 Setup (Kaggle Notebook)

1. Open a new **Kaggle Notebook**.
2. Click on **+ Add Data** → search for **UrbanSound8K** dataset → add it.
3. Copy all the code from `Train/train.ipynb` and paste it into the new notebook.

### ▶️ Run the Training

1. Execute all cells **sequentially**.
2. The notebook will:

   * Load UrbanSound8K data
   * Extract MFCC and Melspectrogram features
   * Train a CNN model
3. The final cell should save the model:

   ```python
   model.save('model.h5')
   ```

### 📥 Download the Output

1. After training completes, click **Save Version → Save & Run All**.
2. Go to the **Output** tab → download `model.h5`.

📦 **Result of Phase 1:** You now have one file — `model.h5`.

---

## 🎧 PHASE 2: Test the Model

**File:** `Test/test_model.ipynb`

This phase uses the `model.h5` file to clean noisy audio files.

### 🧩 Setup (New Kaggle Notebook)

Create a **new notebook** and add **3 inputs**:

#### Input 1️⃣: Trained Model

* Go to **Create → New Dataset**.
* Upload your `model.h5` (downloaded from Phase 1).
* Name it for example: `model-h5`.
* Add it to the notebook.

#### Input 2️⃣: Test Audio File

* Create another dataset and upload your audio file (e.g. `project explanation.mp3`).
* Name it `audio-mp3`.
* Add it to the notebook.

#### Input 3️⃣: Noise Profiles

* Add the **UrbanSound8K** dataset again as the third input.

### 📂 Path Configuration Example

```python
model_path = '/kaggle/input/model-h5/model.h5'
filename = '/kaggle/input/audio-mp3/project explanation.mp3'
urbansound_path = '/kaggle/input/urbansound8k/'
```

### ▶️ Run Testing

1. Run all notebook cells sequentially.
2. The script will:

   * Load your trained model
   * Analyze your audio for noise (e.g., siren, horn, street music)
   * Use UrbanSound8K noise profiles to clean the sound
3. You’ll get both **Original Audio** and **Cleaned Audio** players.

### 📤 Download Cleaned Audio

1. Click **Save Version** after execution.
2. Go to the **Output** tab.
3. Download the generated file — `clean.wav`.

---

## 🔄 Summary Workflow

```
Train/train.ipynb → model.h5 → upload as Kaggle dataset
                    ↓
Test/test_model.ipynb → use model.h5 + audio + UrbanSound8K → clean.wav
```

| Step    | Input                           | Output    |
| ------- | ------------------------------- | --------- |
| Phase 1 | UrbanSound8K                    | model.h5  |
| Phase 2 | model.h5 + audio + UrbanSound8K | clean.wav |

---

## 🧩 TRAINING CODE EXPLANATION

### 🧹 Preprocessing (UrbanSound8K)

* Loads all folds from UrbanSound8K
* Extracts **MFCCs** and **Melspectrograms**
* Converts them into `(40, 2)` features
* Saves `train_data.csv`, `test_data.csv`, and labels.

### 🧱 CNN Model Training

* Loads preprocessed CSVs
* Reshapes input to `(40, 2, 1)`
* Builds a CNN with **Conv2D → Pool → Dense → Dropout**
* Uses **EarlyStopping** for efficient training
* Saves model as `model.h5`

---

## 🎧 TESTING CODE EXPLANATION

### 1️⃣ Install Dependencies

```python
!pip install noisereduce -q
!pip install soundfile -q
```

### 2️⃣ Import Libraries

Imports `librosa`, `tensorflow`, `noisereduce`, `soundfile`, and `IPython.display`.

### 3️⃣ Define Paths

Verifies paths for model, test audio, and UrbanSound8K dataset.

### 4️⃣ Load Model

```python
model = load_model(model_path)
```

Displays summary of CNN model.

### 5️⃣ Define Denoising Function

Uses **noisereduce** with matched UrbanSound8K noise profiles.

### 6️⃣ Audio Classification

* Extracts MFCC + Melspectrogram from test audio
* Predicts noise categories using trained CNN

### 7️⃣ Apply Noise Reduction

* Fetches matching noise files from UrbanSound8K
* Reduces them iteratively

### 8️⃣ Save and Play Output

Saves the denoised file as `clean.wav` and plays both original and cleaned audio within notebook.

---

## 🧑‍🏫 Guided By

# **MR. SUSHIL KUMAR**
