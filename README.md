# PM-DL-Mortality-Prediction

A framework for mortality prediction in healthcare using a combination of Process Mining (PM) and Deep Learning (DL) techniques on the MIMIC-III critical care database.

## Overview

This project implements a novel approach to mortality prediction by combining process mining techniques, which capture the sequential nature of healthcare processes, with deep learning methods that can learn complex patterns from high-dimensional clinical data. The framework processes patient data from the MIMIC-III database, creates process models, enhances them with temporal information, and trains neural attention models for mortality prediction.

## Project Structure

The codebase is organized into several directories and a sequence of numbered Python scripts that form a processing pipeline:

### Core Directories:
- `mimic3/`: Code for interacting with the MIMIC-III databaseL
- `icd/`, `icd9/`: Processing of ICD (International Classification of Diseases) codes
- `pydream/`: Custom framework for process mining and enhancement
- `seq2seq/`: Sequence-to-sequence models for processing temporal healthcare data
- `baselines/`: Comparison models/methods for benchmarking
- `data/`: Data storage and management
- `config/`: Configuration files
- `converter/`: Tools for data transformation and preprocessing

### Processing Pipeline:

The numbered Python scripts represent a sequential workflow:

1. **1_CreateUtilData.py**: 
   - Extracts comorbidity information from the MIMIC database
   - Processes ICD-9 and ICD-10 codes
   - Uses the Elixhauser comorbidity index

2. **2_CreateTraceDataset.py**:
   - Creates raw patient traces and metadata from MIMIC-III
   - Splits data into training, validation, and test sets
   - Prepares data for sequence-to-sequence learning

3. **3_CreateArtificialEvents.py**:
   - Processes medical embeddings
   - Trains a sequence-to-sequence model
   - Creates embedded events and adds artificial events to patient traces

4. **4_CreateFinalXES.py**:
   - Converts the processed data into XES format (standard for event logs in process mining)

5. **5_ProcessDiscoveryEnhancement.py**:
   - Discovers process models using inductive miner
   - Enhances the process models with various configurations
   - Uses different decay functions (LinearDecay, ExpDecay, LogDecay)

6. **6_CreateTSS.py**:
   - Creates Timed State Samples (TSS) from the enhanced process models
   - Performs decay replay on the logs

7. **7_TrainNAP.py**:
   - Trains the Neural Attention Process (NAP) model

8. **8_Evaluate.py**:
   - Evaluates the model's performance on mortality prediction

## Key Technologies and Approaches

1. **Process Mining**:
   - Uses PM4Py library for process discovery and enhancement
   - Creates process models from event logs
   - Enhances models with temporal information

2. **Deep Learning**:
   - Sequence-to-sequence models for temporal data
   - Neural attention mechanisms
   - Medical concept embeddings

3. **Healthcare Data Processing**:
   - ICD code processing (diagnosis codes)
   - Discretization of clinical values (glucose, creatinine, hemoglobin)
   - Comorbidity analysis

## Requirements

The project requires several Python packages, which are listed in `requirements.txt`. Key dependencies include:

- TensorFlow 1.15.2
- Keras 2.3.1
- PM4Py 1.2.10
- pandas 1.0.0
- scikit-learn 0.22.1
- hcuppy 0.0.7 (for Elixhauser comorbidity index)

## Setup and Usage

### Prerequisites

1. Access to the MIMIC-III database (requires credentialing)
2. Python 3.6+ environment

### Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/PM-DL-Mortality-Prediction.git
   cd PM-DL-Mortality-Prediction
   ```

2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

3. Set up the MIMIC-III database according to the instructions in the `mimic3` directory.

### Running the Pipeline

Execute the scripts in numerical order:

1. Create utility data:
   ```
   python 1_CreateUtilData.py
   ```

2. Create trace dataset:
   ```
   python 2_CreateTraceDataset.py
   ```

3. Create artificial events:
   ```
   python 3_CreateArtificialEvents.py
   ```

4. Create final XES:
   ```
   python 4_CreateFinalXES.py
   ```

5. Perform process discovery and enhancement:
   ```
   python 5_ProcessDiscoveryEnhancement.py
   ```

6. Create timed state samples:
   ```
   python 6_CreateTSS.py
   ```

7. Train the Neural Attention Process model:
   ```
   python 7_TrainNAP.py
   ```

8. Evaluate the model:
   ```
   python 8_Evaluate.py
   ```

## Baselines

The `baselines` directory contains implementation of baseline methods for comparison, including traditional machine learning approaches and CNN-based models.

## License

This project is licensed under the terms included in the LICENSE file.

## Citation

If you use this code in your research, please cite:

```
@article{PM-DL-Mortality-Prediction,
  title={Mortality Prediction using Process Mining and Deep Learning},
  author={Your Name},
  journal={Your Journal},
  year={2023}
}
```

## Acknowledgments

- MIMIC-III database for providing the clinical data
- PM4Py team for the process mining framework
- Stanford for the medical embeddings