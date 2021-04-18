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

<img src="images/fig1.JPG" width="500">

<img src="images/fig2.JPG" width="300">

### 3.2. Data Preprocessing
putEMG data contains raw sEMG signals directly collected from the muscles therefore these signals contain noises. Due to the amplifier's direct current offsets, the signals will have low-frequency noises and due to electronic devices (computers, radio broadcasts, etc.), the signal will have high-frequency noises [16]. Typically, sEMG signals are within the 10-700 Hz frequency range and signals beyond this range are considered not useful. Furthermore, sEMG signals may contain interference noises generated by the main power line and other equipment used during the acquisition of data. Therefore, a 5th order bandpass filter of range 20 and 700 Hz was used to filter out low, high-frequency noises, and an adaptive notch filter (ANF) was used to reduce interferences. Attenuating frequencies used for ANF were 30, 50, 90, 60, and 150 Hz. These filter parameters were determined using the suggestions made by the true authors of the dataset [4].  Figure 3 shows the sEMG signals before and after using a bandpass and notch filter. Furthermore, each active gesture in the dataset is of 1 second or 3 seconds, separated by a 3-second idle gesture. Therefore, the dataset contains more ‘idle’ gestures than any other active gestures hence the dataset is unbalanced. Therefore, extra idle gestures were removed to balance the dataset.

<img src="images/fig3.JPG" width="400">

### 3.3. Feature Extraction
For the classification using classic machine learning models, ten features from time, frequency, time-frequency domains were extracted from each channel. They were integral absolute value, mean absolute value, mean frequency, median frequency, root mean square, slope sign change, variance, waveform length, Willison amplitude, zero-crossing, and Mel-frequency cepstral coefficients. In previous works, it is found that these features give higher performance, high insensitivity to window size, and low computational complexity [17].
Root mean square (RMS) which is a time-domain feature gives insights into the amplitude of the signals. The amplitude of the sEMG signal is related to the contraction level of muscles and muscle force involved during the movements. this feature was calculated as,

<img src="images/fe1.JPG" width="200">

sEMG signal frequencies vary with different muscle movements.  Therefore, frequency domain features such as mean frequency (MNF) and median frequency (MDF) of the signal are also used in the feature vector that is fed into gesture recognition classifiers. These features were calculated as,

<img src="images/fe2.JPG" width="300">

Other time domain features mean absolute value (MAV), wave-length (WL), variance (VAR), slope sign change (SSC), and Willison amplitude (WAMP) were calculated as follows,

<img src="images/fe3.JPG" width="200">
<img src="images/fe4.JPG" width="400">

To find Mel-frequency cepstral coefficients (MFCC), the mfcc function from the librosa python library is used. While calculating these features sliding windows size of 2048 and hop length size of 1024 is used. These extracted features were grouped into four separate sets and fed into classifiers separately. The first feature set consists of root mean square, mean frequency, and median frequency. The feature sets II and III were based on previous studies. The second feature set is based on the suggestion made by Hudgins et al. [18] which consists of features mean absolute value, wave-length, zero-crossing, slope sign change. The third feature set consists of integral absolute value, variance, wave-length, zero-crossing, slope sign change, and Willison amplitude was proposed by Du et al. [19]. Finally, feature set IV is made up of MFCC data. Moreover, both preprocessed data and MFCC data were used to train the neural network models.

## Experiment Setup and Implementation

## Results and Analysis
Feature Set I: root mean square, mean frequency, median frequency
Feature Set II: mean absolute value, wave-length, zero-crossing, slope sign change.
Feature Set III: integral absolute value, variance, wave-length, zero-crossing, slope sign change, and Willison amplitude
Feature Set IV: Mel-frequency cepstral coefficients
 
Classifier models: linear discriminant analysis, k-nearest neighbor, support vector machine, random forest

<img src="images/t1.JPG" width="350">

<img src="images/t2.JPG" width="350">

<img src="images/t3.JPG" width="350">

<img src="images/fig8.JPG" width="350">

<img src="images/fig9.JPG" width="350">

<img src="images/fig10.JPG" width="350">

<img src="images/t4.JPG" width="350">

<img src="images/t5.JPG" width="350">

<img src="images/t6.JPG" width="350">

<img src="images/fig11.JPG" width="350">

<img src="images/fig12.JPG" width="350">

<img src="images/fig13.JPG" width="350">



Table 1 and Figure 8 illustrate the validation results obtained for different classifier models with different feature sets using 24 channel data. According to the results feature set I which consists of root mean square (RMS), mean frequency, and median frequency, gives the best result for all classifier models. Furthermore, the support vector machine (SVM) classifier gives the highest accuracy of 90.3% for 24 channel data. The linear discriminant analysis (LDA) model has the second-best accuracy of 89.92%. Feature set IV has the lowest accuracy for all the classifier models.
Table 2 and Figure 9 illustrate the precision score for each gesture when different classifiers are used with feature set I and 24 channel data. Similarly, Table 3 and Figure 10 illustrate the recall value for each gesture when different classifiers are used with feature set I and 24 channel data. Results from Table 2 and Table 3 for we can see that idle, fist, flexion, and extension gestures have higher precision and recall scores, that is all the classifier models tend to predict more accurately these sets of gestures than pinching gestures. Idle gestures are correctly classified by the random forest classifier model with the highest recall score of 0.96 and fist gestures are correctly identified by the SVM classifier with the highest recall of 0.89. LDA has the highest recall for flexion and extension of hand with scores of 0.91 and 0.94 respectively. Pinching thumb with index finger have the lowest recall value for all the classifiers with the best recall score being 0.64 with the LDA classifiers. Other pinching gestures are also correctly identified by the LDA model with the highest recall values of 0.85, 0.86, and 0.88 for pinch thumb-middle, pinch thumb-ring, and pinch thumb-small gestures.
Table 4 and Figure 11 illustrate the classifier results for 8 channel data. For classifying 8 gestures, the highest accuracy of 86.02% was achieved using the SVM classifier with feature set I. LDA model performed better with the feature set III achieving an accuracy of 85.47% and the random forest model also performed better with the feature set III with an accuracy of 85.17%.
Table 5 and Table 6 illustrate the precision score and recall value respectively for each gesture when different classifiers are used with feature set I and 8 channel data. The same result is graphically illustrated in Figures 12 and 13. Similar to 24 channel data results pinching finger gestures had low precision and recall values compared to the other 4 gestures. Predicting idle, fist, and flexion of hand have the highest recall value when SVM classifier is used while k-nearest neighbor classifier predicts extension of hand more accurately with the recall value of 0.94. For pinching fingers, SVM predicted more accurately with the highest recall values of 0.52, 0.65, and 0.72 for pinch thumb-index, pinch thumb-middle, and pinch thumb-small gestures. 

<img src="images/t7.JPG" width="350">

Few researchers have worked on the putEMG dataset for different sEMG applications, and Table 6 illustrates the results obtained. Tsinganos et al. [21] have worked on data augmentation methods and with the use of these techniques, they have achieved a maximum testing accuracy of 96.97%. Our results do not match with their results but their research was mainly based on data augmentation techniques that are to create new data from existing data. The performance of machine learning models improves with the amount of data available. This could be the reason that they have achieved higher accuracy. Nacpil et al. [22] have worked on creating a model to control steering wheel for drivers with disabilities and they have achieved a precision score of 96% and 94% for extension and flexion of the hand. We have achieved a precision of 95% for both of these gestures using the SVM classifier with feature set I and also we are classifying eight gestures.




## Conclusion
The objective of this research was to find a hand gestures recognition model that could be useful to interact with machine interfaces using sEMG signals. If we consider results obtained for 24 channel data, the difference in classification accuracies achieved by LDA and SVM are insignificant for feature set I. From precision and recall results also suggest that both LDA and SVM classifiers have similar results. If we consider results obtained for 8 channel data, the SVM classifier with the feature set I performed better. Precision and recall results also suggest that the SVM classifier gives a better result. In both cases, pinching gestures were not accurately classified compared to other gestures: idle, fist, flexion, and extension gestures. Therefore, a system that utilizes a support vector machine classifier with root mean square, mean frequency, and median frequency as features could be adopted to implement an end-user human-machine interface that utilizes limited gestures. This system might not be very useful for classifying pinching gestures as they have lower precision and recall values, and on average they are below 70%.
sEMG signals characteristic from different muscle groups and characteristics of a single muscle group of different locations have variations. These results obtained depend on the muscle location where signals are acquired and the signal acquisition device used in the experiment. Therefore, when implementing a real-world end-user system these factors also need to be considered.


## Links

- [Project Repository](https://github.com/cepdnaclk/{{ page.repository-name }}){:target="_blank"}
- [Project Page](https://cepdnaclk.github.io/{{ page.repository-name}}){:target="_blank"}
- [Department of Computer Engineering](http://www.ce.pdn.ac.lk/){:target="_blank"}
- [University of Peradeniya](https://eng.pdn.ac.lk/){:target="_blank"}

[//]: # "Please refer this to learn more about Markdown syntax"
[//]: # "https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet"
