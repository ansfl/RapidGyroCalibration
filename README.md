# RapidGyroCalibration

Here, you can find the dataset of the paper <span style="font-family:Arial; font-size:18px;">Rapid Gyroscope Calibration: A Deep Learning Approach </span>

## Abstract

<p style="font-family:Verdana; font-size:14px;">
Low-cost gyroscope calibration is essential for ensuring the accuracy and reliability of gyroscope measurements. Stationary calibration estimates the deterministic parts of measurement errors. To this end, a common practice is to average the gyroscope readings during a predefined period and estimate the gyroscope bias. Calibration duration plays a crucial role in performance, therefore, longer periods are preferred. However, some applications require quick startup times and calibration is therefore allowed only for a short time. In this work, we focus on reducing low-cost gyroscope calibration time using deep learning methods. We propose an end-to-end convolutional neural network for the application of gyroscope calibration. We explore the possibilities of using multiple real and virtual gyroscopes to improve the calibration performance of single gyroscopes. To train and validate our approach, we recorded a dataset consisting of 186.6 hours of gyroscope readings, using 36 gyroscopes of four different brands. We also created a virtual dataset consisting of simulated gyroscope readings. The six datasets were used to evaluate our proposed approach. One of our key achievements in this work is reducing gyroscope calibration time by up to 89% using three low-cost gyroscopes. 
</p>

## Network

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
