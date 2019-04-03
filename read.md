# Abstract <BR>
Neural Networks today find their application in variety of fields, from Computer Vision to Natural Language processing, from Speech Recognition to classification. But they are computationally expensive, memory intensive and difficult to deploy on embedded systems. To attempt to solve this problem, the project will present the survey of degree of compression and the performance of various Deep Neural Network(DNN) compression techniques like Quantization, Pruning and Knowledge Distillation(KD). The motivation for the proposed project is to leverage some/all of these DNN acceleration approaches to reduce the size of DNN model with little to no loss of accuracy to make the baseline models as fast and compressed as possible to enable the use of energy-efficient and real-time processing DNNs on embedded systems. The compressed models will be benchmarked on CPU and GPU using MNIST and CIFAR-10 datasets.<BR>  
  
# Introduction <BR>
Deep Neural networks have become ubiquitous today being employed in a wide variety of applications but they are very computationally intensive and memory intensive. With modern DNN having more than a billion parameters, the amount of memory required to store them is significantly high. This makes them difficult to deploy them on embedded systems with limited hardware and processor resources. For example, Iphones do not allow installation of apps having memory requirements over 100 MBs on the cellular networks. Also, the energy consumption aspect of the DNN poses another hindrance to their use in smartphones and embedded technologies. Under 45nm CMOS technology, a 32 bit floating point add consumes 0.9pJ, a 32bit SRAM cache access takes 5pJ, while a 32bit DRAM memory access takes 640pJ (Han et al., 2016). The amount of energy that will be cosumed in computing a billion parameters will quickly drain the device and is beyond the power envelope of the of a typical device. Also, since the network won’t be able to fit on-chip storage, it would require costly DRAM access which makes real time processing a challenge on the smartphones.<BR>
Thus, there is a need to compress these neural network models by reducing the number of insignificant parameters & weights and storing them with sufficient precision to make the DNN storage and energy efficient while at the same time maintaining the accuracy of the original model. The reduced precision and parameters will make the model faster due to quick arithmetic operations between small-bits parameters and also, due to smaller number of parameters. The smaller models can be used in the mobile systems for processing rather than using clouds to process the data. The project proposes the use of the compression techniques like Quantization, Pruning and Knowledge Distillation to reduce the size of the DNN and investigating the compatibilty of these techniques in a single pipeline to attain further compression while preserving accuracy and reducing loss of energy. <BR>

# Quantization <BR>
Quantization refers to the process of reducing the number of bits that represent a number. In the context of deep learning, the predominant numerical format used for research and for deployment has so far been 32-bit floating point, or FP32. Thus, quantization is used to reduce the model precision from FP32 to n-bits integers (commonly used is INT8 or 8-bits integer). The parameters are mapped from a space of 32 bit floating point to 8 bit integers to accelerate inference on processors that support low precision math with reduced memory bandwidth. (Goncharenko et al., 2018) <BR>

## Findings <BR>
<img src = "https://user-images.githubusercontent.com/46529465/55491436-76d3e680-5603-11e9-9281-75a56fd241d2.png" width = "600">

### Setup
* Model: LeNet-300-100
* Learning Rate: 0.01
* Epochs: 4000
* Batch Size: 256
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: MNIST
* Framework: TensorFlow

* Training Accuracy: 98.078%
* Hardware Setup: Intel Core i7-8565U, NVIDIA GeForce MX150
  
<img src = "https://user-images.githubusercontent.com/46529465/55491665-e6e26c80-5603-11e9-8813-19f548cb27dd.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55491670-e944c680-5603-11e9-810d-50b41cce3f1b.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55491673-eb0e8a00-5603-11e9-9995-74e8d9691079.png" width = "600">


### Setup
* Model: LeNet-300-100
* Learning Rate: 0.001
* Epochs: 500
* Batch Size: 64
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: CIFAR-10
* Framework: TensorFlow

* Training Accuracy: 79.628 %

<img src = "https://user-images.githubusercontent.com/46529465/55492662-95d37800-5605-11e9-99db-86d16acc8cba.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55492669-979d3b80-5605-11e9-9bd2-f21caa50def4.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55492672-9966ff00-5605-11e9-8264-95837d9c4a00.png" width = "600">


### Setup
* Model: LeNet-5
* Learning Rate: 0.001
* Epochs: 10
* Batch Size: 128
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: MNIST
* Framework: TensorFlow

* Training Accuracy: 99.02725%

<img src = "https://user-images.githubusercontent.com/46529465/55492822-e054f480-5605-11e9-947e-7dd216c59735.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55492826-e21eb800-5605-11e9-8361-9b3dd4dccd2e.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55492851-e9de5c80-5605-11e9-8d7c-e45a384c85c0.png" width = "600">

### Setup
* Model: LeNet-5
* Learning Rate: 0.00009
* Epochs: 250
* Batch Size: 32
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: CIFAR-10
* Framework: TensorFlow

* Training Accuracy: 79.51%

<img src = "https://user-images.githubusercontent.com/46529465/55493020-3a55ba00-5606-11e9-9ef2-53915c9b5fa5.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55493027-3de94100-5606-11e9-9043-d5fcc287d1f9.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55493034-3fb30480-5606-11e9-87d9-944f692715a1.png" width = "600">

## Conclusion
* Quantization to 8 bits leads to a 4x reduction in compression
* The test accuracy is within +- 0.05 % of the actual accuracy with float32
* Quantization leads to 1.5x to 2x speedup in inference time 


# Knowledge Distillation <BR>
Knowledge Distillation is a model compression method in which a small model is trained to mimic a pre-trained, larger model (or ensemble of models). This training setting is sometimes referred to as “teacher-student”, where the large model is the teacher and the small model is the student. The teacher model transfer generalizations to the student model rather than weights. In Knowledge Distillation the teacher models passed the “Dark Knowledge” to the student model i.e. which classes the teacher found to be more similar to the predicted class. Thus, Dark knowledge is the information, that, given the input, which classes are more likely to be the output besides the predicted class and is therefore, information about the relation of the input to the each class.(ner, 2017) <BR>
The formula described by Hinton et al. is as follows:
<img src = "https://user-images.githubusercontent.com/46529465/55493546-2494c480-5607-11e9-908c-d3767e593052.png" width = "300">

<BR>Knowledge Distillation architectures: <BR>
<img src = "https://user-images.githubusercontent.com/46529465/55493551-25c5f180-5607-11e9-8144-194886a148fb.png" width = "450">
<img src = "https://user-images.githubusercontent.com/46529465/55493553-26f71e80-5607-11e9-82a7-a8c082356d14.png" width = "500">

## Findings
### Setup: MNIST Data
<img src = "https://user-images.githubusercontent.com/46529465/55494038-0a0f1b00-5608-11e9-9ef3-a785bb8374d0.png" width = "700">

### Performance
<img src = "https://user-images.githubusercontent.com/46529465/55494044-0bd8de80-5608-11e9-8159-8d463e35dfc3.png" width = "800">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/46529465/55494048-0da2a200-5608-11e9-88ed-72522ab2545b.png" width = "700">
<BR><BR>
### Setup: CIFAR 10 Data
<img src = "https://user-images.githubusercontent.com/46529465/55494056-109d9280-5608-11e9-96bc-b6da7039d1e6.png" width = "700">
  
### Performance
<img src = "https://user-images.githubusercontent.com/46529465/55494069-14c9b000-5608-11e9-9140-5c6d3a6964af.png" width = "800">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/46529465/55494072-16937380-5608-11e9-815a-a89fc1468b95.png" width = "700">

## Conclusion
* Knowledge Distillation increases the ability of shallow neural nets to perform better
* Reduction in size is not always guaranteed but speedup is always present
* Accuracy takes quite a hit but maybe compensated for changing epochs, optimizer and learning rate
* Temperature is a hyperparameter whose value needs to be experimented with to determine best distilled model

# Pruning <BR>
Pruning is a method to reduce the storage and computation required by neural networks by learning only the important connections, thereby, converting a fully connected layer into a sparse one. One of the methods proposed to prune the network follows a three step process. First, training of the network to learn which connections are important. Second step is to prune away the less significant weights, which could either be done by absolute value pruning or by a hessian loss function. The third and the final step is to retrain the pruned network to maintain accuracy. Second and third steps are repeated many times to perform iterative pruning which helps further to boost compression without loss of accuracy when compared to single aggressive pruning.<BR>
  
