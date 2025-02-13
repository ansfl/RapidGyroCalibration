# RapidGyroCalibration

Here, you can find the dataset, contains only the real recordings, of the paper <span style="font-family:Arial; font-size:18px;">Rapid Gyroscope Calibration: A Deep Learning Approach </span>

## Abstract

<p style="font-family:Verdana; font-size:14px;">
Low-cost gyroscope calibration is essential for ensuring the accuracy and reliability of gyroscope measurements. Stationary calibration estimates the deterministic parts of measurement errors. To this end, a common practice is to average the gyroscope readings during a predefined period and estimate the gyroscope bias. Calibration duration plays a crucial role in performance, therefore, longer periods are preferred. However, some applications require quick startup times and calibration is therefore allowed only for a short time. In this work, we focus on reducing low-cost gyroscope calibration time using deep learning methods. We propose an end-to-end convolutional neural network for the application of gyroscope calibration. We explore the possibilities of using multiple real and virtual gyroscopes to improve the calibration performance of single gyroscopes. To train and validate our approach, we recorded a dataset consisting of 186.6 hours of gyroscope readings, using 36 gyroscopes of four different brands. We also created a virtual dataset consisting of simulated gyroscope readings. The six datasets were used to evaluate our proposed approach. One of our key achievements in this work is reducing gyroscope calibration time by up to 89% using three low-cost gyroscopes. 
</p>

## Network

Recall that the basic NN approach uses single gyroscope readings as input to output its bias. Following this approach, we used a fixed number of input channels and increased the training data using real and virtual MGs. Given that an IMU consists of three orthogonal gyroscopes, we set the input channels to three. We sought to implement a basic DL principle according to which when increasing the training data the performance of NNs improves until reaching a steady state solution, that is, until additional data no longer influences performance. Therefore, increasing the training data should improve the calibration performance of the gyroscope, up to a steady-state solution (saturation). For example, when training the network with data from three gyroscopes, the minimum training set consists of $3 \cdot M$ samples.  When increasing the training set by an additional $N$ IMUs, the training set consists of $3 \cdot M \cdot N$ samples.  The input channels, however, remain three in those two examples. Figure 1 [](#training-data-expansion)  provides a graphic illustration of our approach and demonstrates how incorporating additional gyroscopes increases the volume of the training data while maintaining the size of the input channels. .

![Training Data Expansion](https://github.com/ansfl/RapidGyroCalibration/blob/main/Figures/raising_train_n_gyro.jpg)

*Figure 1: Block diagram illustrating our approach for increasing the training data. The upper diagram depicts a setup with three gyroscopes; the lower diagram shows 3N gyroscopes. The figure shows the differences in the training data size. N is the number of IMUs, M is the number of samples recorded by each gyroscope, and S is the window size.*

Our network focus on convolutional neural network architecture, as presented in Figure 2 [](#Network). 
It consists of a convolution layer followed by a LeakyReLU activation function and a max-pooling layer. Next, two fully connected layers, with a LeakyReLU activation function between them, process the output features.

![Network](https://github.com/ansfl/RapidGyroCalibration/blob/main/Figures/Network_illustraion.jpg)

*Figure 2: Our baseline network architecture. The network receives gyroscope measurements and outputs the gyroscope deterministic bias.*

## Dataset

We employed four types of gyroscopes for our experiments: (a) Movella Dot , (b) SparkFun , (c) NG-IMU  and (d) Memsense MS-IMU3025. The specifications for these gyroscopes, as provided by the manufacturers, are shown  in Table 1.

### Specifications of the Gyroscopes

| **Sensor Name**  | **Sample Rate [Hz]** | **Noise Density [mdps/√Hz]** | **Bias Stability [°/h]** |
|-----------------|---------------------|----------------------------|-------------------------|
| Movella DOT    | 120                 | 7                          | 10                      |
| SparkFun       | 130-145             | 3.8                        | N/A                     |
| NG             | 200                 | N/A                        | N/A                     |
| Memsense       | 250                 | 14.8                        | 2.6                     |

*Table 1: Specifications of the gyroscopes, as provided by the manufacturers.*

We used four Movella DOTs and four SparkFun IMUs in our experiments. After evaluating our approach on those devices, we further tested our approach on the NG and Memsense IMUs to evaluate its generalization. During data acquisition, all 12 IMUs from each brand were placed on a stable table to minimize external disturbances.
For synchronization, different methods were applied based on sensor type. Movella DOT sensors were synchronized using built-in Bluetooth functionality, allowing simultaneous activation and recording via a mobile application. For SparkFun, NG, and Memsense IMUs, which do not have built-in synchronization, we designed and 3D-printed custom placeholders to keep the sensors in a fixed position and connected them to a single power hub. A centralized data acquisition script, controlled by Arduino, was implemented to trigger data logging simultaneously across all connected sensors, ensuring time alignment of the recorded gyroscope readings.
To account for potential variations in gyroscope performance due to manufacturing inconsistencies, we conducted experiments using multiple units of each IMU type. Despite being from the same manufacturer, individual sensors exhibited slight differences in bias and noise characteristics. By including multiple sensors in our dataset and evaluating performance across different models, we ensured that our approach remains robust to these variations.

To achieve an accurate bias estimate from a single recording, a substantial number of samples is necessary to average out the Gaussian mean-zero noise. Consequently, 13,000 samples were recorded for each of the gyroscopes. The bias distribution was estimated by repeating the experiment 100 times. The training dataset should include a variety of bias values to allow generalization. Consequently, we turned off the device and waited 10 seconds before turning it back on. By doing so, we obtained different bias values in each experiment, which contributed to the training process and allowed for generalization.

![Network](https://github.com/ansfl/RapidGyroCalibration/blob/main/experimental_setup.jpg)

*Figure 3: Experimental setup: (right) Movella DOTS IMUs configuration, (left) SparkFun IMUs configuration.*

For the evaluation process, we divided the real data into four datasets:
- **Dataset-1**:  
  Contains recorded data from all 12 SparkFun gyroscopes across 100 recordings, each with 13,000 measurements corresponding to 87 seconds of recording time per session.  
  - **Training set**: 23.2 hours of recording  
  - **Testing set**: 1.45 hours of recording (not present in training)  

- **Dataset-2**:  
  Includes data from all 12 DOT gyroscopes across 400 recordings, each with 13,000 measurements corresponding to 120 seconds of recording time per session.  
  - **Training set**: 32 hours of recording  
  - **Testing set**: 2 hours of recording (not present in training)  

- **Dataset-3**:  
  The dataset contains 100 recordings of each of the 6 NG gyroscopes. Each recording consists of 13,000 measurements lasting 65 seconds.  
  - **Training set**: 8.67 hours  
  - **Testing set**: 1.08 hours (not included in training)  

- **Dataset-4**:  
  The dataset contains 100 recordings of each of the 6 Memsense gyroscopes. Each recording consists of 13,000 measurements lasting 52 seconds.  
  - **Training set**: 6.83 hours  
  - **Testing set**: 0.87 hours (not included in training)  
Table 2 shows the duration of all \hlc{six} datasets. Overall, the {six} datasets contain \hlc{186.6} hours of gyroscope measurements from \hlc{36} real gyroscopes and 48 virtual ones. \\

The table below provides a detailed breakdown of the total training and testing time across selected datasets.

| Dataset | Train [hours] | Test [hours] | Total [hours] |
|---------|-------------|------------|--------------|
| 1       | 23.2       | 1.45       | 24.65        |
| 2       | 32         | 2          | 34           |
| 3       | 8.67       | 1.08       | 9.75         |
| 4       | 6.93       | 0.87       | 7.8          |

*Table 2: Detailed description of the total training and testing time across all datasets.*





## Citation   

If you find the paper, dataset, or code helpful in your research, please cite our paper:
```bibtex
@article{stolero2024rapid,
  title={Rapid Gyroscope Calibration: A Deep Learning Approach},
  author={Stolero, Yair and Klein, Itzik},
  journal={arXiv preprint arXiv:2409.00488},
  year={2024}
}
