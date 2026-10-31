# Network Intrusion Detection System Using Deep Learning

## Project Overview

This project implements a **Network Intrusion Detection System (NIDS)** using the NSL-KDD dataset and neural networks to classify network connections as either **Normal** or **Attack**.

The project uses data preprocessing, feature encoding, feature scaling, and deep learning techniques to identify potentially malicious network activity.

Two neural network architectures are implemented and compared:

1. Deep Neural Network (DNN)
2. Single-Layer Perceptron

An interactive web application is also developed using Flask, allowing users to enter network connection details and receive a prediction.

## Project Objectives

- Analyze network traffic data using the NSL-KDD dataset.
- Preprocess network connection features for machine learning.
- Convert categorical features into numerical representations.
- Apply feature scaling using StandardScaler.
- Build and train neural network models.
- Classify network connections as Normal or Attack.
- Evaluate model performance using accuracy, precision, recall, F1-score, and confusion matrices.
- Develop an interactive Flask application for network intrusion prediction.

## Dataset

This project uses the **NSL-KDD dataset**, a benchmark dataset commonly used for network intrusion detection research.

The dataset contains network connection records with features describing connection behavior and attack labels.

### Dataset Files

The following files are included in the `datasets/` directory:

- `KDDTrain+.txt` – Training dataset.
- `KDDTest+.txt` – Testing dataset.

### Dataset Information

| Description | Value |
|---|---:|
| Training records | 125,973 |
| Testing records | 22,544 |
| Original columns | 43 |
| Processed input features | 123 |
| Classification classes | Normal and Attack |

The original attack labels are converted into two categories:

- `0` – Normal
- `1` – Attack

## Technologies and Libraries

The project uses the following technologies:

- Python
- Google Colab
- Pandas
- NumPy
- Scikit-learn
- TensorFlow / Keras
- Flask
- HTML
- CSS

## Data Preprocessing

The following preprocessing operations are performed:

1. Load the training and testing datasets using Pandas.
2. Assign column names to the dataset.
3. Convert the original labels into binary attack labels.
4. Combine the training and testing data temporarily to ensure consistent categorical feature columns.
5. Apply One-Hot Encoding to:
   - `protocol_type`
   - `service`
   - `flag`
6. Remove unnecessary columns, including the original label and difficulty level.
7. Separate the training and testing datasets.
8. Split the data into input features (`X`) and target labels (`y`).
9. Apply StandardScaler to normalize numerical features.

After preprocessing, the model uses **123 input features** for each network connection.

## Neural Network Models

### 1. Deep Neural Network

A deep neural network is implemented using TensorFlow and Keras.

**Architecture:**

- Input layer: 123 features
- Hidden layer 1: 32 neurons, ReLU activation
- Hidden layer 2: 16 neurons, ReLU activation
- Output layer: 1 neuron, Sigmoid activation

**Model Configuration:**

| Parameter | Value |
|---|---|
| Optimizer | Adam |
| Loss function | Binary Crossentropy |
| Evaluation metric | Accuracy |
| Epochs | 10 |
| Batch size | 64 |
| Validation split | 20% |

The sigmoid output produces a value between 0 and 1, which is used to classify a connection as Normal or Attack using a threshold of 0.5.

### 2. Single-Layer Perceptron

A single-layer neural network is implemented as a baseline model for comparison.

**Architecture:**

- Input layer: 123 features
- Output layer: 1 neuron
- Activation function: Sigmoid

**Model Configuration:**

| Parameter | Value |
|---|---|
| Optimizer | Adam |
| Loss function | Binary Crossentropy |
| Evaluation metric | Accuracy |
| Epochs | 10 |
| Batch size | 64 |
| Validation split | 20% |

## Model Evaluation and Results

Both models are evaluated using the testing dataset containing 22,544 records.

### Accuracy Comparison

| Model | Test Accuracy |
|---|---:|
| Deep Neural Network | 78.75% |
| Single-Layer Perceptron | 74.88% |

The Deep Neural Network achieved 3.87 percentage points higher test accuracy than the single-layer model.

### Deep Neural Network Classification Report

| Metric | Normal | Attack |
|---|---:|---:|
| Precision | 0.69 | 0.92 |
| Recall | 0.93 | 0.68 |
| F1-score | 0.79 | 0.79 |

**Overall test accuracy: 78.75%**

### Deep Neural Network Confusion Matrix

| Actual / Predicted | Normal | Attack |
|---|---:|---:|
| Normal | 8,991 | 720 |
| Attack | 4,071 | 8,762 |

The model correctly classified 8,991 normal connections and 8,762 attack connections.

The results show that the model identifies normal connections more effectively than it detects all attack connections. Improving attack detection recall is an important area for future development.

### Single-Layer Perceptron Confusion Matrix

| Actual / Predicted | Normal | Attack |
|---|---:|---:|
| Normal | 8,981 | 730 |
| Attack | 4,933 | 7,900 |

## Flask Web Application

An interactive web application is developed using Flask to demonstrate the trained intrusion detection model.

The application is titled **Network Intrusion Detector**.

### Application Features

- Enter network connection details manually.
- Select protocol type, service, and connection flag from dropdown menus.
- Enter connection duration.
- Enter source and destination bytes.
- Enter connection count.
- Enter failed login attempts.
- Enter SYN error rate.
- Predict whether a connection is Normal or Attack.
- Display the predicted probability of an attack.
- Test a randomly selected real connection from the testing dataset.
- Compare the model prediction with the actual test label.

For manual predictions, the application uses typical values for the features that are not entered by the user.

### Prediction Output

The application displays one of two results:

- **NORMAL** – The predicted probability of an attack is 50% or lower.
- **ATTACK** – The predicted probability of an attack is greater than 50%.

## Project Structure

```text
network-intrusion-detection/
│
├── datasets/
│   ├── KDDTrain+.txt
│   ├── KDDTest+.txt
│   └── README.md
│
├── Network_intrusion-system.ipynb
│
├── README.md
│
└── requirements.txt
```

## Installation and Usage

### 1. Clone the Repository

```bash
git clone https://github.com/anushaazam/network-intrusion-detection.git
```

### 2. Open the Project

```bash
cd network-intrusion-detection
```

### 3. Install Required Libraries

```bash
pip install -r requirements.txt
```

### 4. Open the Notebook

Open `Network_intrusion-system.ipynb` using Google Colab or Jupyter Notebook.

### 5. Load the Dataset

The notebook currently uses the following Google Colab file paths:

```python
/content/KDDTrain+.txt
/content/KDDTest+.txt
```

For a fresh Colab session, download the dataset files from the repository and upload them into the Colab `/content/` directory before running the notebook.

### 6. Run the Notebook

Execute the notebook cells in their intended order to preprocess the dataset, train the models, and evaluate their performance.

### 7. Run the Flask Application

Run the Flask application code after the preprocessing, model training, and scaling steps have been executed.

The application can then be accessed through the local Flask server address displayed in the output.

## Future Improvements

- Improve attack detection recall.
- Experiment with additional deep learning architectures.
- Perform hyperparameter tuning.
- Add more network traffic features to the web application.
- Save and load trained models without retraining.
- Improve the web interface and user experience.
- Add additional evaluation visualizations.

## Conclusion

This project demonstrates how deep learning can be applied to network intrusion detection using the NSL-KDD dataset.

Two neural network models were implemented and evaluated. The Deep Neural Network achieved a test accuracy of **78.75%**, while the Single-Layer Perceptron achieved **74.88%**.

The project also includes an interactive Flask application that allows users to test network connection details and view intrusion detection predictions.

## Author

**Anusha Azam**

## License

This project is intended for educational and academic purposes.
