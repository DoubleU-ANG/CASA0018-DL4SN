# CASA0018-DL4SN


# Magic Wand

Zhenkun Wang, https://github.com/DoubleU-ANG/CASA0018-DL4SN / https://studio.edgeimpulse.com/studio/384213

## Introduction
This project aims to develop a home window assistant based on gesture recognition, allowing users to interact with windows in their house using natural movements and gestures instead of  physical contact or input methods provided by traditional home assistant like keyboards or touchscreens. This project deploys deep learning model on a ‘magic wand’ to make it recognize users’ gestures, and open and close window according to those gestures.

This magic wand detects users’ gestures via fusion sensor group (Accelerometer, Gyroscope and Magnetometer) on Arduino nano, and processes and analyzes the motion pattern to turn it into command to control window to open and close.

### Inspiration
#### The weather of London
London is known for its ever-changing weather pattern which can swiftly change between rainy and sunny day. Consequently, the windows in the home need to be open and closed frequently, which is quite annoying.
#### Gesture Recognition
By analyzing motion patterns captured by sensors or cameras, gesture recognition systems can recognize specific gestures and translate them into commands or actions, facilitating human-computer interaction experiences in various applications such as gaming, virtual reality, augmented reality, robotics, and smart devices.
#### Harry Potter
I am a big fan of Harry Potter, and I always want to have my own magic wand. So in this project I deploy deep learning on a magic wand model to make it magical, enabling it to control the window by recognizing specific gestures.

This project is building based on a tutorial on youtube which make arduino nano to recognize two motion patterns: move left-right and up-down.

## Research Question
How can gesture recognition technology be effectively integrated into home assistant “magic wand” to enable the  control of windows based on user gestures.

## Application Overview
This project develops a gestured-based smart home assistant “magic wand” and can be mainly divided into five parts.

### Data Collection
Collecting motion patterns data including clockwise rotation, counterclockwise rotation and stop along with some background random movements via fusion sensor group.
### Building Deep Learning Model
Deciding which signal processing block and learning block to use in order to extract features and classify new data.
### Features Extraction & Classification
Process the data by extracting features and classify them based on those features.
### Deep Learning Model Training & Evaluation
Use different deep learning model by changing their training parameters including number of epochs, learning rate, neural network architecture, evaluate their performance and choose the best one to deploy on the physical device.
### Deployment & Application
Deploy the best trained deep learning model on the Arduino nano 33 BLE, and test the functionality of the model: recognizing clockwise rotation and counterclockwise rotation, and control the window open or close based on the motion patterns.


## Data
### Data Collection
The dataset in this project contains three different types of motion samples, including clockwise rotation, counterclockwise rotation and stop, collected by Arduino. To ensure the diversity and complexity of the data, both the motion samples of clockwise and counterclockwise rotation are recorded in different speed (fast, medium and slow). Additionally, to prevent classifying other motions into clockwise rotation and counterclockwise rotation, noise was added by randomly shaking the wand when collecting the data of stop.

### Data Preprocessing
Assigning a label to each data point, indicating the content it represents. By doing so during training, the model can learn the mapping relationship between the input data features and the labels, enabling accurate prediction or classification of new data.

### Dataset
This data set contains three types of data with a total of 150 samples and a duration of 25 minutes. The entire dataset was split into two parts: training set and testing set, with 80% split for the training set and 20% to the test set, which facilitates effective model training and evaluation, ensuring the model's generalization ability and reliability.

## Model
In this project, two different methods for processing block have tried, they are: Spectral Analysis and IMU. And the model used in learning block is Classification.

### Spectral Analysis: Spectral analysis in deep learning refers to the process of analyzing the frequency domain representation of signals or data using techniques derived from spectral analysis methods, which isgreat for analyzing repetitive motion, such as data from accelerometer.

### IMU (Syntiant): The IMU is a sensor device that measures and reports specific kinematic properties of an object, such as acceleration, angular velocity, and sometimes magnetic field strength. IMUs are commonly used in various applications, including robotics, virtual reality, motion tracking, and wearable devices. In deep learning, IMU can be utilized as input sources to train models for tasks such as gesture recognition, activity recognition, pose estimation, and navigation.

### Model Test
After experimental comparison, the performance of spectral analysis and IMU was quite different in accuracy. The performance of spectral analysis was good, whose accuracy was nearly 90%, while the performance of IMU was poor, whose accuracy was nearly 50%. Therefore, I adopted the model combination of spectral analysis and classification for training in the following experiments.

## Experiments
What experiments did you run to test your project? What parameters did you change? How did you measure performance? Did you write any scripts to evaluate performance? Did you use any tools to evaluate performance? Do you have graphs of results? 

*Tip: probably ~300 words and graphs and tables are usually good to convey your results!*

## Results and Observations
Synthesis the main results and observations you made from building the project. Did it work perfectly? Why not? What worked and what didn't? Why? What would you do next if you had more time?  

*Tip: probably ~300 words and remember images and diagrams bring results to life!*

## Bibliography
*If you added any references then add them in here using this format:*

1. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

2. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

*Tip: we use [https://www.citethisforme.com](https://www.citethisforme.com) to make this task even easier.* 

----

## Declaration of Authorship

I, AUTHORS NAME HERE, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


*Digitally Sign by typing your name here*

ASSESSMENT DATE

Word count: 
