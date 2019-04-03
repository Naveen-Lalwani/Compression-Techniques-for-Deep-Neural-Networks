## <B>ABSTRACT</B> <BR>
Neural Networks today find their application in variety of fields, from Computer Vision to Natural Language processing, from Speech Recognition to classification. But they are computationally expensive, memory intensive and difficult to deploy on embedded systems. To attempt to solve this problem, the project will present the survey of degree of compression and the performance of various Deep Neural Network(DNN) compression techniques like Quantization, Pruning and Knowledge Distillation(KD). The motivation for the proposed project is to leverage some/all of these DNN acceleration approaches to reduce the size of DNN model with little to no loss of accuracy to make the baseline models as fast and compressed as possible to enable the use of energy-efficient and real-time processing DNNs on embedded systems. The compressed models will be benchmarked on CPU and GPU using MNIST and CIFAR-10 datasets.<BR>  
  
## <B>INTRODUCTION</B> <BR>
Deep Neural networks have become ubiquitous today being employed in a wide variety of applications but they are very computationally intensive and memory intensive. With modern DNN having more than a billion parameters, the amount of memory required to store them is significantly high. This makes them difficult to deploy them on embedded systems with limited hardware and processor resources. For example, Iphones do not allow installation of apps having memory requirements over 100 MBs on the cellular networks. Also, the energy consumption aspect of the DNN poses another hindrance to their use in smartphones and embedded technologies. Under 45nm CMOS technology, a 32 bit floating point add consumes 0.9pJ, a 32bit SRAM cache access takes 5pJ, while a 32bit DRAM memory access takes 640pJ (Han et al., 2016). The amount of energy that will be cosumed in computing a billion parameters will quickly drain the device and is beyond the power envelope of the of a typical device. Also, since the network won’t be able to fit on-chip storage, it would require costly DRAM access which makes real time processing a challenge on the smartphones.<BR>
Thus, there is a need to compress these neural network models by reducing the number of insignificant parameters & weights and storing them with sufficient precision to make the DNN storage and energy efficient while at the same time maintaining the accuracy of the original model. The reduced precision and parameters will make the model faster due to quick arithmetic operations between small-bits parameters and also, due to smaller number of parameters. The smaller models can be used in the mobile systems for processing rather than using clouds to process the data. The project proposes the use of the compression techniques like Quantization, Pruning and Knowledge Distillation to reduce the size of the DNN and investigating the compatibilty of these techniques in a single pipeline to attain further compression while preserving accuracy and reducing loss of energy. <BR>

## Quantization <BR>
Quantization refers to the process of reducing the number of bits that represent a number. In the context of deep learning, the predominant numerical format used for research and for deployment has so far been 32-bit floating point, or FP32. Thus, quantization is used to reduce the model precision from FP32 to n-bits integers (commonly used is INT8 or 8-bits integer). The parameters are mapped from a space of 32 bit floating point to 8 bit integers to accelerate inference on processors that support low precision math with reduced memory bandwidth. (Goncharenko et al., 2018) <BR>

### Findings <BR>
<img src = "https://user-images.githubusercontent.com/46529465/55491436-76d3e680-5603-11e9-9281-75a56fd241d2.png" width = "600">

#### Setup
* Model: LeNet-300-100
* Learning Rate: 0.01
* Epochs: 4000
* Batch Size: 256
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: MNIST
* Framework: TensorFlow
<BR>
* Training Accuracy: 98.078%
* Hardware Setup: Intel Core i7-8565U, NVIDIA GeForce MX150
  
<img src = "https://user-images.githubusercontent.com/46529465/55491665-e6e26c80-5603-11e9-8813-19f548cb27dd.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55491670-e944c680-5603-11e9-810d-50b41cce3f1b.png" width = "600">
<img src = "https://user-images.githubusercontent.com/46529465/55491673-eb0e8a00-5603-11e9-9995-74e8d9691079.png" width = "600">



## Knowledge Distillation <BR>
Knowledge Distillation is a model compression method in which a small model is trained to mimic a pre-trained, larger model (or ensemble of models). This training setting is sometimes referred to as “teacher-student”, where the large model is the teacher and the small model is the student. The teacher model transfer generalizations to the student model rather than weights. In Knowledge Distillation the
teacher models passed the “Dark Knowledge” to the student model i.e. which classes the teacher found to be more similar to the predicted class. Thus, Dark knowledge is the information, that, given the input, which classes are more likely to be the output besides the predicted class and is therefore, information about the relation of the input to the each class.(ner, 2017) <BR>

## Pruning <BR>
Pruning is a method to reduce the storage and computation required by neural networks by learning only the important connections, thereby, converting a fully connected layer into a sparse one. One of the methods proposed to prune the network follows a three step process. First, training of the network to learn which connections are important. Second step is to prune away the less significant weights, which could either be done by absolute value pruning or by a hessian loss function. The third and the final step is to retrain the pruned network to maintain accuracy. Second and third steps are repeated many times to perform iterative pruning which helps further to boost compression without loss of accuracy when compared to single aggressive pruning.<BR>
  
