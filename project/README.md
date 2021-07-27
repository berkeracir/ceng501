# Signal Detection and Classification in Shared Spectrum: A Deep Learning Approach

This readme file is an outcome of the [CENG501 (Spring 2021)](http://kovan.ceng.metu.edu.tr/~sinan/DL/) project for reproducing a paper without an implementation. See [CENG501 (Spring 2021) Project List](https://github.com/sinankalkan/CENG501-Spring2021) for a complete list of all paper reproduction projects.

# 1. Introduction

In this project, I have tried to implement signal classifier with the combination of Convolutional and Recurrent Neural Networks as described in the paper[1] which is accepted for publishing in [IEEE INFOCOM 2021 Main Conference](https://infocom2021.ieee-infocom.org/accepted-paper-list-main-conference). 

## 1.1. Paper summary

Authors of the paper develop a deep neural network for classification of coexisting signal types such as IEEE802.11 (WiFi), LTE (Long Term Evolution) and 5G-NR (5G New Radio). Also, this network works on directly received signal's I/Q (In-Phase and Quadrature) samples meaning that receiver side does not have to decode the received signal in order to detect its type. The proposed architecture combines both CNN and RNN and uses segment of I/Q samples for training. It is trained in both simulation environment and experimental environment with the trasmitter and receiver hardware. Their results show that proposed architecture can achieve accurate classification in both environments.

WiFi, LTE and 5G-NR signals can coexist in the shared spectrum (5-6 GHz) so assesment of the wireless environment is crucial in terms of better communication. In the paper, there are 7 classes for the classification task: WiFi, LTE, 5G, WiFi+LTE, WiFi+5G, LTE+5G, WiFi+LTE+5G

Authors compare their architecture with other machine and deep learning architectures such as SVM (Support Vector Machine), RF (Random Forests), CNN (Convolutional Neural Networks) and LSTM (Long Short-Term Memory) and the proposed architecture shows better performance in the classification task. The authors also try to improve the architecture's accuracy by introducing Frequency-Domain Analysis (FDA) into the input segment. They exhibit extensive analysis on the impact of FDA, RNN layer, and segment length. Also, they show their analysis on SNR (Signal-to-Noise Ratio) and receiver antenna gains.

# 2. The method and my interpretation

## 2.1. The original method

### 2.1.1 Data Generation

The wavefroms are generated with *MATLAB Communication Toolbox* and *5G Toolbox* with different set of signal features such as channel bandwidth, modulation and coding scheme, subcarrier spacing, allocated resource blocks etc. Signal features can be seen in the *Table I*. The generated waveforms are transmitted by three transmitter antennas and received by one receiver antenna. Each transmitter antenna is responsible for one signal type and the receiver system collects received signal's raw I/Q values. Then, 512 consequent I/Q pairs are saved together as a segment. There are approximately 100,000 segments are used in training and testing the classifier. The dataset is split into 80% for training and %20 for testing. Experimental setup of the authors can be seen in *Figure 10*. Also, they introduce additive white Gaussian noise (AWGN) channel model with different SNR values to the data in order to simulate the noise in the wireless environment.


<p align="center">
<table>
<tr>
    <td>
    <p align="center">
        <img src="./figures/table1.png" alt="Parameter Options for Waveform Generator" style="width: 30vw"/>
        <br>Table I from the paper: Parameter Options for Waveform Generator</br>
    </p>
    </td>
    <td>
    <p align="center">
        <img src="./figures/figure10.png" alt="Experiment setup used for performance evaluation" style="width: 70vw"/>
        <br>Figure 10 from the paper: Experiment setup used for performance evaluation</br>
    </p>
    </td>
</tr>
</table>

### 2.1.2 CNN-LSTM Architecture

Proposed architecture can be seen from the *Figure 2*. STFT (Short-Time Fourier Transform) is applied to the segmented sequence of 512 I/Q pairs with Kaisar-Bessel window function and this is fed into convolutional layer, and then pooling layer. Convoluted and pooled input is flattened and further fed into LSTM layer. Output of the LSTM layer is passed to dense layer and then softmax layer.

<p align="center">
  <img src="./figures/figure2.png" alt="Overview of the proposed FDA-CNN-LSTM classifier" style="width: 80vw"/>
  <br>Figure 2 from the paper: Overview of the proposed FDA-CNN-LSTM classifier</br>
</p>

## 2.2. My interpretation 

### 2.2.1 Data Generation

Authors are used hardware (three NI USRP-2921s and one NI USRP-2944R) for creating the dataset and I do not have any equipment for transmission and reception.

# 3. Experiments and results

## 3.1. Experimental setup

Describe the setup of the original paper and whether you changed any settings.

## 3.2. Running the code

Explain your code & directory structure and how other people can run it.

## 3.3. Results

Present your results and compare them to the original paper. Please number your figures & tables as if this is a paper.

# 4. Conclusion

Discuss the paper in relation to the results in the paper and your results.

# 5. References

[1]: [Zhang, W., Feng, M., Krunz, M., & Abyaneh, A. (2020). Signal Detection and Classification in Shared Spectrum: A Deep Learning Approach. *IEEE INFOCOM 2021*.](http://wireless.ece.arizona.edu/sites/default/files/Infocom_2021_wenhan.pdf)

# Contact

Berker Acır - berker.acir@metu.edu.tr, berkeracir159@gmail.com
