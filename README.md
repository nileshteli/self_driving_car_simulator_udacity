# Self-Driving Car Simulation Project

A deep learning project that trains a Convolutional Neural Network (CNN) to autonomously drive a car in the Udacity Self-Driving Car Simulator using behavioral cloning.

## 🚗 Project Overview

This project uses a CNN model to predict steering angles based on camera images from a simulated car. The model learns to drive by mimicking human driving behavior captured in training data.

## 📋 Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Download Udacity Simulator](#download-udacity-simulator)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Training the Model](#training-the-model)
- [Running the Autonomous Mode](#running-the-autonomous-mode)
- [Troubleshooting](#troubleshooting)
- [Model Architecture](#model-architecture)
- [Results](#results)

## ✨ Features

- CNN-based behavioral cloning for autonomous driving
- Real-time steering angle prediction
- Multiple trained models with different epochs
- Data augmentation and preprocessing
- Compatible with Udacity Self-Driving Car Simulator

## 🔧 Prerequisites

- Python 3.7 or higher
- pip package manager
- Udacity Self-Driving Car Simulator
- Minimum 4GB RAM
- GPU recommended for training (optional)

## 📦 Installation

### 1. Clone or Download this Repository

```bash
git clone https://github.com/nileshteli/self_driving_car_simulator_udacity.git
cd simulator-linux
```

### 2. Install Required Python Packages

```bash
pip install -r requirements.txt
```

**Important:** If you encounter connection issues with the simulator, install these specific versions:

```bash
pip install python-engineio==3.13.2
pip install python-socketio==4.6.1
```

### 3. Required Dependencies

The `requirements.txt` includes:
- opencv-contrib-python
- numpy
- matplotlib
- tensorflow
- keras
- python-socketio
- Flask
- eventlet

## 🎮 Download Udacity Simulator

Download the Udacity Self-Driving Car Simulator for your operating system:

### Official Download Links:

**Linux:**
- [Linux Simulator](https://github.com/udacity/self-driving-car-sim/releases)

**Windows:**
- [Windows Simulator](https://github.com/udacity/self-driving-car-sim/releases)

**macOS:**
- [macOS Simulator](https://github.com/udacity/self-driving-car-sim/releases)

### Installation Steps:

1. Go to the [Udacity Self-Driving Car Simulator Releases](https://github.com/udacity/self-driving-car-sim/releases)
2. Download the appropriate version for your OS (Term 1 Simulator)
3. Extract the downloaded file
4. For Linux: Make the executable file runnable:
   ```bash
   chmod +x "Default Linux desktop Universal.x86_64"
   ```
5. Run the simulator executable

## 📁 Project Structure

```
simulator-linux/
├── Self_Driving_Car.ipynb      # Main Jupyter notebook for training
├── drive.py                     # Script to run autonomous mode
├── drive_fixed.py              # Alternative drive script
├── requirements.txt            # Python dependencies
├── issue.txt                   # Known issues and solutions
├── convert_model.py            # Model conversion utility
├── inspect_model.py            # Model inspection utility
├── data/                       # Training data directory
│   ├── driving_log.csv        # Steering angles and image paths
│   └── IMG/                   # Camera images from simulator
├── model.h5                    # Trained model (H5 format)
├── best_model.keras           # Best performing model
├── modelfifteen.keras         # Model trained for 15 epochs
├── modelhundred.keras         # Model trained for 100 epochs
└── Default Linux desktop Universal.x86_64  # Simulator executable
```

## 📊 Dataset

### Collecting Training Data

1. Launch the Udacity Simulator
2. Select **Training Mode**
3. Choose a track
4. Click **Record** and select a directory to save data
5. Drive the car manually using keyboard/mouse
6. The simulator will save:
   - `driving_log.csv`: Contains image paths and steering angles
   - `IMG/`: Folder with center, left, and right camera images

### Using Provided Data

The project includes pre-collected training data in the `data/` directory:
- **driving_log.csv**: ~11,000+ data points
- **IMG/**: Corresponding camera images

## 🎓 Training the Model

### Option 1: Using Jupyter Notebook (Recommended)

1. Open the notebook:
   ```bash
   jupyter notebook Self_Driving_Car.ipynb
   ```

2. Run all cells sequentially to:
   - Load and preprocess data
   - Build the CNN model
   - Train the model
   - Save the trained model

### Option 2: Training Parameters

The model uses:
- **Architecture**: NVIDIA CNN architecture for self-driving cars
- **Input**: 160x320x3 RGB images (preprocessed to 66x200)
- **Output**: Steering angle prediction
- **Loss Function**: Mean Squared Error (MSE)
- **Optimizer**: Adam

### Available Pre-trained Models

- `best_model.keras` - Best performing model (15 epochs)
- `modelfifteen.keras` - 15 epochs training
- `modeltenepoch.keras` - 10 epochs training
- `modelhundred.keras` - 100 epochs training
- `model.h5` - Original H5 format model

## 🚀 Running the Autonomous Mode

### Step 1: Start the Simulator

1. Launch the Udacity Simulator executable
2. Select **Autonomous Mode**
3. Choose Track 1 or Track 2

### Step 2: Run the Drive Script

```bash
python drive.py best_model.keras
```

Or use the H5 model:
```bash
python drive.py model.h5
```

### Step 3: Watch the Car Drive!

The car should now drive autonomously around the track. The script will:
- Receive images from the simulator
- Predict steering angles using the trained model
- Send steering commands back to the simulator

### Optional: Save Autonomous Driving Images

```bash
python drive.py best_model.keras run1
```

This saves images to the `run1/` directory for later analysis.

## 🔧 Troubleshooting

### Connection Issues

**Problem**: Simulator not connecting to Python script

**Solution**: Install specific package versions:
```bash
pip install python-engineio==3.13.2
pip install python-socketio==4.6.1
```

### Model Loading Errors

**Problem**: Error loading `.keras` or `.h5` files

**Solution**: 
- Ensure TensorFlow/Keras versions are compatible
- Use `convert_model.py` to convert between formats
- Try `drive_fixed.py` instead of `drive.py`

### Poor Driving Performance

**Problem**: Car drives off the track

**Solutions**:
- Try different pre-trained models
- Collect more training data with better driving
- Train for more epochs
- Add data augmentation

### Simulator Performance

**Problem**: Simulator runs slowly

**Solutions**:
- Lower graphics quality in simulator settings
- Close other applications
- Use a machine with better GPU

## 🧠 Model Architecture

The project uses a CNN architecture inspired by NVIDIA's self-driving car model:

```
- Input: 66x200x3 normalized images
- Convolutional Layer 1: 24 filters, 5x5 kernel, 2x2 stride
- Convolutional Layer 2: 36 filters, 5x5 kernel, 2x2 stride
- Convolutional Layer 3: 48 filters, 5x5 kernel, 2x2 stride
- Convolutional Layer 4: 64 filters, 3x3 kernel
- Convolutional Layer 5: 64 filters, 3x3 kernel
- Flatten
- Fully Connected Layer 1: 100 neurons
- Fully Connected Layer 2: 50 neurons
- Fully Connected Layer 3: 10 neurons
- Output: 1 neuron (steering angle)
```

**Activation**: ReLU for all layers except output

## 📈 Results

- Successfully trained models can complete Track 1 autonomously
- Best model achieves smooth steering with minimal oscillation
- Training time: ~5-30 minutes depending on epochs and hardware
- Model size: ~3MB

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements!

## 📝 License

This project is for educational purposes.

## 🙏 Acknowledgments

- Udacity Self-Driving Car Nanodegree for the simulator
- NVIDIA for the CNN architecture
- Community solutions for socketio compatibility issues

## 📧 Contact

For questions or issues, please open an issue in the repository.

---

**Happy Autonomous Driving! 🚗💨**
