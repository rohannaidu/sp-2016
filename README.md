### Description

Seizure Prediction

- [Competition page at Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction)
- This is a proof-of-concept for applying deep learning techniques to EEG data converted into spectrograms.
- This code builds a separate model for each subject (there are three subjects).

### Usage

These steps take about 30 minutes on a system with 4 processors, a single GPU and a spinning hard-disk. **Tested only on Ubuntu**.

1. Download and install [neon](https://github.com/NervanaSystems/neon) **1.5.4**

    ```
    git clone https://github.com/NervanaSystems/neon.git
    cd neon
    git checkout v1.5.4
    make
    source .venv/bin/activate
    ```
2. Verify neon installation

    Make sure that this command does not result in any errors:
    ```
    ./examples/cifar10_msra.py -e1
    ```

3. Install prerequisites

    ```
    pip install scipy sklearn scikits.audiolab
    ```
4. Download the data files from [Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction/data):

    Save all files to a directory (referred to as /path/to/data below) and unzip the .zip files.

5. Clone this repository

    ```
    git clone https://github.com/anlthms/sp-2016.git
    cd sp-2016
    ```
6. Train models and generate predictions

    ```
    ./run.sh /path/to/data
    ```
7. Evaluate predictions

    Submit subm.csv to [Kaggle](https://www.kaggle.com/c/melbourne-university-seizure-prediction/submissions/attach)

### Notes
- The model requires 3GB of device memory.
- If using AWS, see slide 10 on [this deck] (https://github.com/anlthms/meetup2/blob/master/audio-pattern-recognition.pdf) for instructions on how to configure an EC2 instance.
- The first run takes longer due to conversion of .mat files into .wav files.
- Conversion of data to spectrograms is performed on the fly by neon.
- As provided, the run.sh script uses data from the first electrode. This means that only 1/16th of the data is used.
- If using a different electrode, use clear.sh to delete cached data files.
- A leaderboard AUC score of 0.5864 may be obtained by using this code as is.
