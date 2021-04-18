---
layout: home
permalink: index.html

# Please update this with your repository name and title
repository-name: e15-4yp-Hand-Gesture-Recognition-using-sEMG
title:
---

[comment]: # "This is the standard layout for the project, but you can clean this and use your own template"

# Hand Gesture Recognition using sEMG

#### Team

- E/15/043, Yasiru Bhagya T.P., [yasirubhagya@eng.pdn.ac.lk](mailto:yasirubhagya@eng.pdn.ac.lk)
- E/15/131, Hisni Mohammed M.H., [hisnimohammed@eng.pdn.ac.lk](mailto:hisnimohammed@eng.pdn.ac.lk)
- E/15/348, Suhail S., [suhailsajahan@eng.pdn.ac.lk](mailto:suhailsajahan@eng.pdn.ac.lk)

#### Supervisors

- Dr. Isuru Nawinne, [isurunawinne@eng.pdn.ac.lk](mailto:isurunawinne@eng.pdn.ac.lk)
- Prof. Roshan Ragel, [roshanr@eng.pdn.ac.lk](mailto:roshanr@eng.pdn.ac.lk)
- Mr. Theekshana Dissanayake, [theekshanadis@eng.pdn.ac.lk](mailto:theekshanadis@eng.pdn.ac.lk)

#### Table of content

1. [Abstract](#abstract)
2. [Related works](#related-works)
3. [Methodology](#methodology)
4. [Experiment Setup and Implementation](#experiment-setup-and-implementation)
5. [Results and Analysis](#results-and-analysis)
6. [Conclusion](#conclusion)
7. [Links](#links)

---

## 1. Abstract
Identifying hand gestures using surface electromyography (sEMG) signals is vital in the development of next-generation human-machine interfaces (HMI). sEMG based HMIs provide users with a more natural and convenient way to communicate with computing systems. sEMG signals recorded from muscle tissues give information about the intended muscle movements triggered by the brain waves. Identifying these movements allows developing interfaces that can control computing devices. In this research, an attempt was made to improve a hand gesture recognition model that could be used as a human-machine interface using an online open dataset of sEMG signals. First sEMG signals were preprocessed using a bandpass filter and notch filter to remove noises in the signal. Then various time, frequency, and time-frequency domain features extracted and they were fed into machine learning algorithms such as random forest, support vector machines (SVM), K-nearest neighbors (K-NN), and recurrent neural networks. All the results were validated using 10-fold cross-validation. Maximum testing accuracy of 90.03% was obtained using an SVM classifier with root mean square, mean frequency, and median frequency of the signal as features for 24 channel data. Later an attempt was also made to use this result to control a simple game developed in Unity using sEMG signals collected from an 8-channel signal acquisition device.

## 2. Related works
Various approaches have been proposed in the area of EMG-based applications. As sEMG signals from different muscle groups exhibit different characteristics, different techniques have been employed to characterize muscle movement. But in general, it is all down to feature extraction to represent the signal as a vector of features, followed by feature selection to reduce the vector’s dimensionality, and finally, classification to determine each vector as belong to one of a fixed set of classes [5].
Paleari et al. [6] have used the root mean square (RMS) feature with a neural network model to classify hand movements using 192 channel high-density sEMG (HD-sEMG) signals from the forearm. Stango et al. [7] have used the SVM classifier with variogram, which is a measure of the degree of spatial correlation to build a model to control upper limb prostheses using HD-sEMG signals. Liu et al. [8] proposed an invariant feature extraction (IFE) framework based on kernel fisher discriminant analysis to enhance the robustness of myoelectric pattern recognition. Tsai et al. [9] proposed multi-channel EMG-based motion pattern recognition. They have used the SVM classifier with STFT-ranking features based on short-time Fourier transform and principal component analysis to feature selection. Amma et al. [10] used HD-sEMG signals recorded by 192 electrodes to classify finger gestures using the RMS feature and a naive Bayes classifier. Most of these researches based on HD-sEMG signals and complex feature extraction with complex deep learning models that give higher accuracy are not suitable to implement in a real-time environment as they have higher latencies, expensive in terms of electrode configuration, and inconvenient for the user. 

## 3. Methodology
### 3.1. Data Set
An online open dataset “putEMG” [4] published by Kaczmarek et al. was used for our research. This dataset is a database of sEMG signals collected through an experiment conducted on a group of 45 subjects. This group consisted of 37 males and 8 females aged between 19 and 37 years old. To record sEMG signals, a signal acquisition device with 24 electrodes placed in 3 elastic bands such that 8 electrodes per elastic band was used. Signals were recorded from right forearm muscles. The signals were sampled at the rate of 5120 Hz, with a 12-bit analog to digital converter.
The sEMG signals were recorded when subjects were not moving the hand-keeping the muscles relaxed (idle gesture), when hand fist, while flexion of the hand, while the extension of the hand, and while pinching the fingers (pinching with thumb and index finger, pinching with thumb and middle finger, pinching with thumb and ring finger, and pinching with thumb and small finger). Therefore, this dataset includes the idle gesture and 7 active gestures. Figure 1 shows all the gestures that are included in the dataset and Figure 2 shows the electrode placement configurations used to acquire signals.
It is very important to record sEMG signals when subjects perform gestures repetitively as when doing the same gesture again and again subjects tend to perform gestures in a similar pattern [4]. putEMG dataset was created using an experiment that was conducted such that each data instance consists of 20 repetitions of each gesture. Therefore, this dataset allows us to develop and evaluate more robust algorithms for gesture recognition systems.

<img src="images/fig1.JPG" width="700">

<img src="images/fig2.JPG" width="700">

### 3.2. Data Preprocessing
putEMG data contains raw sEMG signals directly collected from the muscles therefore these signals contain noises. Due to the amplifier's direct current offsets, the signals will have low-frequency noises and due to electronic devices (computers, radio broadcasts, etc.), the signal will have high-frequency noises [16]. Typically, sEMG signals are within the 10-700 Hz frequency range and signals beyond this range are considered not useful. Furthermore, sEMG signals may contain interference noises generated by the main power line and other equipment used during the acquisition of data. Therefore, a 5th order bandpass filter of range 20 and 700 Hz was used to filter out low, high-frequency noises, and an adaptive notch filter (ANF) was used to reduce interferences. Attenuating frequencies used for ANF were 30, 50, 90, 60, and 150 Hz. These filter parameters were determined using the suggestions made by the true authors of the dataset [4].  Figure 3 shows the sEMG signals before and after using a bandpass and notch filter. Furthermore, each active gesture in the dataset is of 1 second or 3 seconds, separated by a 3-second idle gesture. Therefore, the dataset contains more ‘idle’ gestures than any other active gestures hence the dataset is unbalanced. Therefore, extra idle gestures were removed to balance the dataset.

### 3.3. Feature Extraction


## Experiment Setup and Implementation

## Results and Analysis

## Conclusion

## Links

- [Project Repository](https://github.com/cepdnaclk/{{ page.repository-name }}){:target="_blank"}
- [Project Page](https://cepdnaclk.github.io/{{ page.repository-name}}){:target="_blank"}
- [Department of Computer Engineering](http://www.ce.pdn.ac.lk/){:target="_blank"}
- [University of Peradeniya](https://eng.pdn.ac.lk/){:target="_blank"}

[//]: # "Please refer this to learn more about Markdown syntax"
[//]: # "https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet"
