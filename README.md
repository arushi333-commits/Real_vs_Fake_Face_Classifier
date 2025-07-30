# Real_vs_Fake_Face_Classifier
# Real vs. Fake Face Classification API

This project builds, trains, and deploys a deep learning model that can distinguish between real human faces and synthetically generated fake faces. The final trained model is exposed as a web API using FastAPI and made publicly accessible using ngrok.

---

## 🧠 Project Overview

* **Data Sources:**

  * [140k Real and Fake Faces](https://www.kaggle.com/datasets/xhlulu/140k-real-and-fake-faces)
  * [ThisPersonDoesNotExist.com](https://thispersondoesnotexist.com) (TPDNE) for additional synthetic fake faces

* **Data Preparation:**

  * Downloads and extracts the Kaggle dataset
  * Augments it with fake face images from TPDNE
  * Organizes data into train/test/validation splits

* **Modeling:**

  * Uses **ResNet-18** pretrained architecture
  * Final classification layer modified for binary classification (real vs. fake)
  * Model trained using **transfer learning**

* **Evaluation:**

  * Accuracy: `94.7%`
  * Precision: `94.3%`
  * Recall: `95.2%`
  * F1 Score: `94.75%`
  * Confusion Matrix: Included in notebook visualizations

* **Deployment:**

  * Trained model is saved as a `.pth` file
  * Model is loaded and served with FastAPI
  * Publicly accessible using `ngrok`

---

## 🛠 Setup and Installation

> 💡 Recommended Environment: [Google Colab](https://colab.research.google.com/)

### ✅ Prerequisites

* **Kaggle Account:** For dataset download
* **Kaggle API Token:** Upload `kaggle.json` during runtime
* The **ngrok authtoken is provided ** and already included in the notebook cell. No additional setup is required for this.
⚠️ Important: Due to security concerns, the kaggle.json file is not included in this repository.

To run the notebook, the reviewer must:

Create a Kaggle account (https://www.kaggle.com/)

Navigate to "My Account" > "Create New API Token"

This downloads the kaggle.json file

Upload it in the appropriate cell when prompted in the notebook

---

## 🚀 Running the Notebook

1. **Install Libraries:**

   * Run the first cell to install all required libraries: `fastapi`, `torch`, `kaggle`, `pyngrok`, etc.

2. **Upload Kaggle Token:**

   * Upload the `kaggle.json` when prompted

3. **Download and Prepare Data:**

   * The notebook handles data download, extraction, and splitting

4. **Download TPDNE Fake Faces:**

   * Synthetic fake face images from TPDNE are downloaded (code included)

5. **Train the Model:**

   * Trains ResNet-18 on the dataset
   * Final model is saved to disk

6. **Run the API:**

   * Load the saved model
   * Start FastAPI server
   * Expose it using ngrok

---

## 🤖 About the Trained Model

* The model is saved as a `.pth` file after training
* **IMPORTANT:** The model file (e.g., `face_classifier_20250729_194456.pth`) **must be in the same directory** as the deployment code to run correctly
* Alternatively, store it in a known path and update `model_path` in the code accordingly

---

## 🔌 API Usage

Once deployed, the model can be accessed via the `/predict` endpoint:

### POST `/predict`

* Accepts multiple images as input using `multipart/form-data`
* Returns a list of predictions: `real` or `fake`

### Example `curl` Request:

```bash
curl -X POST \
  -F "files=@image1.jpg" \
  -F "files=@image2.jpg" \
  https://YOUR_NGROK_URL/predict
```

### Sample Response:

```json
{
  "predictions": ["real", "fake"]
}
```

---

## 📂 Files in This Repository

| File/folder                                | Purpose                                     |
| ------------------------------------------ | ------------------------------------------- |
| `Final_Real_vs_Fake_Face_Classifier.ipynb` | Main training + deployment notebook         |
| `face_classifier_*.pth`                    | Trained model file (required for inference) |
| `README.md`                                | Documentation                               |


---






