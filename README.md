
# MOSFET Modelling with Neural Networks

This repository contains the code, datasets, and trained models developed for a final-year project at the University of Manchester. The project investigates the use of artificial neural networks (ANNs) to model and characterise MOSFET behaviour using both synthetic SPICE data and experimentally measured datasets.

## 🧠 Project Overview

Traditional MOSFET modelling relies on SPICE simulations and physics-based equations, which can be complex, time-consuming, and hard to generalise to real-world data. This project replaces parts of this workflow with neural networks, which are trained to:

- Predict drain current (\( I_D \)) from gate-source (\( V_{GS} \)) and drain-source (\( V_{DS} \)) voltages.
- Extract key transistor parameters like threshold voltage (\( V_{TH} \)) and process transconductance parameter (\( K_P \)) directly from I–V characteristics.

## 📁 Project Structure

The project is organised into four main phases:

### Phase 1: Drain Current Prediction from Public Dataset

A feedforward neural network was trained on a publicly available NMOS dataset to predict drain current (\(I_D\)) from gate-source (\(V_{GS}\)) and drain-source (\(V_{DS}\)) voltages. The model achieved near-perfect accuracy (R² = 0.99995), demonstrating the effectiveness of deep learning for device-specific modelling.

#### Files:
- `Phase1.ipynb` – Full pipeline for data loading, preprocessing, training, and evaluation of the neural network using a public NMOS dataset.

Includes:
- StandardScaler normalisation
- Keras-based model training with MSE loss
- Prediction and evaluation (R², RMSE)
- Plots of predicted vs actual drain current


### Phase 2: Drain Current Prediction from Experimental Data

In this phase, device-specific neural networks were trained on measured I–V data from five commercial NMOS transistors. Each notebook contains the data processing, training, evaluation, and plotting pipeline for a different device.

#### Files:
- `BS170FTA_script.ipynb` – Neural network model for BS170FTA transistor.
- `BSS127S-7_script.ipynb` – Model trained on BSS127S-7 experimental data.
- `bss126ixtsa1.ipynb` – Model for BSS126IXTSA1 device.
- `LND150N8-G_script.ipynb` – Full model workflow for LND150N8-G transistor.
- `LND150K1-G_script.pdf` – PDF version of the script used for the LND150K1-G device, including preprocessing, training, and evaluation steps.

Each script includes:
- Data reshaping and preparation
- MinMax scaling
- Fully connected neural network training using TensorFlow/Keras
- Evaluation using MAE, RMSE, and R²
- Comparison plots between real and predicted characteristics

### Phase 3: Synthetic Data Generation via SPICE Simulation

This phase involves generating large-scale synthetic datasets using SPICE models and training neural networks to predict drain current from voltage inputs. Both Level 1 and Level 3 models were used to simulate thousands of MOSFET devices with randomly sampled parameters.

#### Files:
- `Level1SingleMOSFET.ipynb` – Generates synthetic I–V data for a single NMOS transistor using Level 1 SPICE model; trains a predictive model.
- `Level1MultiMOSFET_v9.ipynb` – Simulates 10,000+ devices using randomized Level 1 parameters; trains a generalised neural network across the entire parameter space.
- `Level3MultiMOSFET_v4.ipynb` – Performs the same pipeline with Level 3 model complexities to evaluate ANN performance under more realistic transistor behaviour.

Each notebook includes:
- Parameter randomisation for synthetic SPICE datasets
- PySpice simulation and data collection
- Keras-based training and evaluation
- Performance metrics and visual validation

### Phase 4: Parameter Extraction and Prediction

This phase explores the prediction of key physical parameters — threshold voltage (\(V_{TH}\)) and process transconductance parameter (\(K_P\)) — using synthetic SPICE datasets. It consists of two parts: traditional extraction through curve fitting, followed by supervised training of neural networks to predict these parameters directly from I–V data.

#### Parameter Extraction (Linear Fitting)

Ground-truth values of \(V_{TH}\) and \(K_P\) were first extracted from synthetic I–V curves using linear and quadratic extrapolation methods.

**Files:**
- `LinearExtrap_v2.ipynb`, `LinearExtrap_v4.ipynb` – Extract \(V_{TH}\) from Level 1 SPICE simulations.
- `LinearExtrap_KP_v1.ipynb`, `LinearExtrap_KP_v2.ipynb` – Extract \(K_P\) from Level 1 datasets via quadratic saturation fitting.
- `LinearExtrap_Level3_v1.ipynb`, `LinearExtrap_Level3_v2.ipynb` – Perform \(V_{TH}\) extraction from Level 3 data.
- `LinearExtrap_KP_L3_v1.ipynb`, `LinearExtrap_KP_L3_v2.ipynb` – Estimate \(K_P\) from Level 3 SPICE output.

Each notebook includes visual verification, data reshaping, and export of ground-truth values.

#### Neural Network Parameter Prediction

Neural networks were trained to regress \(V_{TH}\) and \(K_P\) from the synthetic I–V curves using the extracted values as labels.

**Files:**
- `level1_NN_v9_VTO.ipynb`, `level3_NN_v11_VTO_only.ipynb` – Predict threshold voltage from full I–V data (Level 1 and Level 3).
- `level1_NN_v2_kp.ipynb`, `level3_NN_v2_kp.ipynb` – Predict process transconductance from saturation-region data.

Each model was evaluated on R², MAE, and RMSE, showing strong performance and generalisation across parameter spaces.

#### Timing and Inference Benchmarks

**Files:**
- `Timing_Level1_VTO_NN_v2.ipynb`, `Timing_Level3_VTO_NN.ipynb` – Evaluate inference speed for \(V_{TH}\) predictors.
- `Timing_Level1_KP_NN.ipynb`, `Timing_Level3_KP_NN.ipynb` – Benchmark performance of \(K_P\) models.


#### Trained Models

Four Keras model files are included for direct inference or future reuse:

- `mosfet_VTO_model_v9.keras` – Trained on Level 1 data for \(V_{TH}\) prediction.
- `mosfet_VTO_model_Level3_v11.keras` – Trained on Level 3 data for \(V_{TH}\) prediction.
- `mosfet_kp_model_v2.keras` – Level 1 dataset model for \(K_P\) regression.
- `mosfet_level3_kp_model_v2.keras` – Level 3 dataset model for \(K_P\) regression.


## 📊 Technologies Used

- **Python 3**
- **TensorFlow / Keras** – ANN implementation
- **PySpice** – Circuit simulation and synthetic dataset generation
- **NumPy / Pandas / Matplotlib** – Data processing and visualisation
- **Scikit-learn** – Standardisation, model evaluation




## 📈 Results Summary

- ANN-based models effectively replace SPICE-based MOSFET models for current prediction.
- Trained models generalise well from simulation to real-world measurements.
- Neural networks can directly extract physical parameters, reducing reliance on manual curve fitting and commercial tools.

## 🔬 Future Work

- Incorporate BSIM-level compact models.
- Explore hybrid physics-informed neural networks.
- Improve generalisation across process corners using transfer learning or ensemble methods.
- Integrate models into circuit-level simulation flows.

## 🧾 Citation

If you use this work in academic or commercial projects, please cite:

**Mustafa Iqbal Kodvavi**, *Modelling and Characterisation of MOSFETs via Artificial Neural Networks Trained on Synthetic and Measured Data*, University of Manchester, March 2025.
