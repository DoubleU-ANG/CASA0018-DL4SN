# CASA0018-DL4SN


# Magic Wand

Zhenkun Wang, https://github.com/DoubleU-ANG/CASA0018-DL4SN / https://studio.edgeimpulse.com/studio/384213

## Introduction
This project aims to develop a home window assistant based on gesture recognition, allowing users to interact with windows in their house using natural movements and gestures instead of  physical contact or input methods provided by traditional home assistant like keyboards or touchscreens. This project deploys deep learning model on a ‘magic wand’ to make it recognize users’ gestures, and open and close window according to those gestures.

This magic wand detects users’ gestures via inertial sensor group (Accelerometer, Gyroscope and Magnetometer) on Arduino nano, and processes and analyzes the motion pattern to turn it into command to control window to open and close.

### Inspiration:
#### 1. The weather of London
London is known for its ever-changing weather pattern which can swiftly change between rainy and sunny day. Consequently, the windows in the home need to be open and closed frequently, which is quite annoying.
#### 2. Gesture Recognition
By analyzing motion patterns captured by sensors or cameras, gesture recognition systems can recognize specific gestures and translate them into commands or actions, facilitating human-computer interaction experiences in various applications such as gaming, virtual reality, augmented reality, robotics, and smart devices.
#### 3. Harry Potter
I am a big fan of Harry Potter, and I always want to have my own magic wand. So in this project I deploy deep learning on a magic wand model to make it magical, enabling it to control the window by recognizing specific gestures.

This project is building based on a tutorial on youtube which make arduino nano to recognize two motion patterns: move left-right and up-down.

## Research Question
How can gesture recognition technology be effectively integrated into home assistant “magic wand” to enable the  control of windows based on user gestures.

## Application Overview
This project develops a gestured-based smart home assistant “magic wand” and can be mainly divided into five parts:
### 1. Data Collection
Collecting motion patterns data including clockwise rotation, counterclockwise rotation and stop along with some background random movements via inertial sensor group.
### 2. Building Deep Learning Model
Deciding which signal processing block and learning block to use in order to extract features and classify new data.
### 3. Features Extraction & Classification
Process the data by extracting features and classify them based on those features.
### 4. Deep Learning Model Training & Evaluation
Use different deep learning model by changing their training parameters including number of epochs, learning rate, neural network architecture, evaluate their performance and choose the best one to deploy on the physical device.
### 5. Deployment & Application
Deploy the best trained deep learning model on the Arduino nano 33 BLE, and test the functionality of the model: recognizing clockwise rotation and counterclockwise rotation, and control the window open or close based on the motion patterns.

<img src="DL/workflow.jpg" height="500em" />

## Data
### Data Collection
The dataset in this project contains three different types of motion samples, including clockwise rotation, counterclockwise rotation and stop, collected by Arduino. To ensure the diversity and complexity of the data, both the motion samples of clockwise and counterclockwise rotation are recorded in different speed (fast, medium and slow). Additionally, to prevent classifying other motions into clockwise rotation and counterclockwise rotation, noise was added by randomly shaking the wand when collecting the data of stop.

### Data Preprocessing
Assigning a label to each data point, indicating the content it represents. By doing so during training, the model can learn the mapping relationship between the input data features and the labels, enabling accurate prediction or classification of new data.

### Dataset
This data set contains three types of data with a total of 150 samples and a duration of 25 minutes. The entire dataset was split into two parts: training set and testing set, with 80% split for the training set and 20% to the test set, which facilitates effective model training and evaluation, ensuring the model's generalization ability and reliability.

## Model
In this project, two different methods for processing block have tried, they are: Spectral Analysis and IMU. And the model used in learning block is Classification.

### Spectral Analysis
Spectral analysis in deep learning refers to the process of analyzing the frequency domain representation of signals or data using techniques derived from spectral analysis methods, which isgreat for analyzing repetitive motion, such as data from accelerometer.

### IMU (Syntiant)
The IMU is a sensor device that measures and reports specific kinematic properties of an object, such as acceleration, angular velocity, and sometimes magnetic field strength. IMUs are commonly used in various applications, including robotics, virtual reality, motion tracking, and wearable devices. In deep learning, IMU can be utilized as input sources to train models for tasks such as gesture recognition, activity recognition, pose estimation, and navigation.

### Model Test
After experimental comparison, the performance of spectral analysis and IMU was quite different in accuracy. The performance of spectral analysis was good, whose accuracy was nearly 90%, while the performance of IMU was poor, whose accuracy was nearly 50%. Therefore, I adopted the model combination of spectral analysis and classification for training in the following experiments.

## Experiments
In order to find the best model, Dozens of experiments were conducted. During these experiments, several parameters were modified to evaluate the performance of the model. Additionally, to evaluate the performance of the model by considering all the factor, I customized a script for calculating performance: score = training accuracy*0.6-loss*0.6+ test accuracy * 0.4

### Parameter 1: Number of training cycles (Epoch) 
This parameter refers to how many times that the model pass through the entire training dataset during the training phase of a neural network model.

According to the line graph, the increase in number of epochs cannot ensure better performance of the network, which also has the disadvantage of increasing training time. Therefore, the number of epochs was set as 20 in the rest of the training.

### Parameter 2: Learning rate
This parameter refers to the rate at which the model's parameters (weights and biases) are updated during training

According to this line graph, increasing learning rate to 0.001 can improve the performance. When its value was between 0.001 and 0.002, the model's performance declined and began to climb after 0.002 to peak at 0.003, and then continued to decline, which indicates overfit. Therefore, the value of learning rate was set as 0.001 in the rest of training.

### Parameter 3: Drop out rate
This parameter refer to the probability of dropping out each neuron in a layer during training

According to the line graph, during the increase of dropout rate from 0.1, the overall performance of the model showed a downward trend. Therefore, the value of dropout rate was set as 0.1 in the rest of training. 

### Neural network architecture
Neural network architecture refers to the structure and organization of layers and nodes within a neural network. The complexity and type of neural network architecture can vary widely, depending on the task it is designed to perform.

According to the experiments, too simple or complex network architecture is detrimental to the model performance. 

The final neural network architecture and parameter was decided after the experiment:

## Results and Observations
Finally, a well-performed deep learning model successfully deployed on Arduino, which enable Arduino to recognize three different types of gesture: clockwise rotation, counterclockwise rotation and stop. Here, I use my magic wand to control another arduino nano and turn on different color light to represent the open window , close window and stop.

### Observation 1:
During the first deployment test, the data was collected very properly and easy to identify, for example: make the arduino completely static while collecting the ‘stop’, so that when the wand detects other actions including random shaking, those actions are also classified into clockwise and counterclockwise rotation. I think the reason is that the ‘stop’ training dataset is not diverse enough. Therefore, in the next data collection process, the complexity of the ‘stop’ data is increased: noise(random movement) is added to the ‘stop’ dataset. After that the problem is greatly improved, and the random movements will no longer be classified into clockwise and counterclockwise rotation.

### Observation 2：overfit
During the second deployment test, When the rotation speed is moderate or low, the model was performed with a high accuracy rate. But when the rotation is faster, Both clockwise rotation and counterclockwise rotation were classified to clockwise rotation, I think this phenomenon is the overfit, which means that the model finds a cheat code: all the fast rotations are classified to clockwise rotation. The reason should be that the training samples of counterclockwise rotation is insufficient, which lacks the sample of counterclockwise rotation in high speed. Therefore, in the next data collection process, the samples of counterclockwise rotation in high speed were added to the training dataset. After that, the problem have been largely alleviated. The model improves the accuracy in the deployment test.

## Future Development

1. Recollect gesture data to increase the number and diversity of samples
2. Retrain the neural network model and adjust structure and parameters, trying to find better deep learning model
3. Add more gesture categories to expand functionality of the magic wand
4. Make a real model of window by 3D printing

## Reflection
By this project, I learned how to train the deep learning model, from collecting data, to how to build the model and adjust the model parameters and neural network architecture, and finally successfully deploying the model on the device. In this process, I encountered the common problem: overfit in the model training process, and the dataset was adjusted by the corresponding solution, which finally undermined the problem and improved the accuracy of the model.

## Bibliography
*If you added any references then add them in here using this format:*

1. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

2. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

*Tip: we use [https://www.citethisforme.com](https://www.citethisforme.com) to make this task even easier.* 

----

## Declaration of Authorship

I, Zhenkun Wang, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


Zhenkun Wang

2024/5/1

Word count:1569 
