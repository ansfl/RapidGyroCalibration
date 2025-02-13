# RapidGyroCalibration

Here, you can find the dataset of the paper <span style="font-family:Arial; font-size:18px;">Rapid Gyroscope Calibration: A Deep Learning Approach </span>

## Abstract

<p style="font-family:Verdana; font-size:14px;">
Low-cost gyroscope calibration is essential for ensuring the accuracy and reliability of gyroscope measurements. Stationary calibration estimates the deterministic parts of measurement errors. To this end, a common practice is to average the gyroscope readings during a predefined period and estimate the gyroscope bias. Calibration duration plays a crucial role in performance, therefore, longer periods are preferred. However, some applications require quick startup times and calibration is therefore allowed only for a short time. In this work, we focus on reducing low-cost gyroscope calibration time using deep learning methods. We propose an end-to-end convolutional neural network for the application of gyroscope calibration. We explore the possibilities of using multiple real and virtual gyroscopes to improve the calibration performance of single gyroscopes. To train and validate our approach, we recorded a dataset consisting of 186.6 hours of gyroscope readings, using 36 gyroscopes of four different brands. We also created a virtual dataset consisting of simulated gyroscope readings. The six datasets were used to evaluate our proposed approach. One of our key achievements in this work is reducing gyroscope calibration time by up to 89% using three low-cost gyroscopes. 
</p>

## Network

Recall that the basic NN approach uses single gyroscope readings as input to output its bias. Following this approach, we used a fixed number of input channels and increased the training data using real and virtual MGs. Given that an IMU consists of three orthogonal gyroscopes, we set the input channels to three. We sought to implement a basic DL principle according to which when increasing the training data the performance of NNs improves until reaching a steady state solution, that is, until additional data no longer influences performance. Therefore, increasing the training data should improve the calibration performance of the gyroscope, up to a steady-state solution (saturation). For example, when training the network with data from three gyroscopes, the minimum training set consists of $3 \cdot M$ samples.  When increasing the training set by an additional $N$ IMUs, the training set consists of $3 \cdot M \cdot N$ samples.  The input channels, however, remain three in those two examples. Figure 1 [](#training-data-expansion)  provides a graphic illustration of our approach and demonstrates how incorporating additional gyroscopes increases the volume of the training data while maintaining the size of the input channels. .

![Training Data Expansion](https://github.com/ansfl/RapidGyroCalibration/blob/main/raising_train_n_gyro.jpg)

*Figure 1: Block diagram illustrating our approach for increasing the training data. The upper diagram depicts a setup with three gyroscopes; the lower diagram shows 3N gyroscopes. The figure shows the differences in the training data size. N is the number of IMUs, M is the number of samples recorded by each gyroscope, and S is the window size.*

Our network focus on convolutional neural network architecture, as presented in Figure 2 [](#Network). 
It consists of a convolution layer followed by a LeakyReLU activation function and a max-pooling layer. Next, two fully connected layers, with a LeakyReLU activation function between them, process the output features.

![Network](https://github.com/ansfl/RapidGyroCalibration/blob/main/Network_illustraion.jpg)

*Figure 2: Our baseline network architecture. The network receives gyroscope measurements and outputs the gyroscope deterministic bias.*


## Dataset

## Citation   

If you find the paper, dataset, or code helpful in your research, please cite our paper:
```bibtex
@article{stolero2024rapid,
  title={Rapid Gyroscope Calibration: A Deep Learning Approach},
  author={Stolero, Yair and Klein, Itzik},
  journal={arXiv preprint arXiv:2409.00488},
  year={2024}
}
