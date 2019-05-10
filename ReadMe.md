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
  
<img src = "https://user-images.githubusercontent.com/44993623/57559959-38dc8780-7352-11e9-9b8f-da15d75be224.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57559998-6295ae80-7352-11e9-8bc6-9029a9a272c5.png" width = "600">

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

<img src = "https://user-images.githubusercontent.com/44993623/57560182-24e55580-7353-11e9-947b-ae17d9bb57f5.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560193-375f8f00-7353-11e9-9a23-5f12ea39c932.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560203-45adab00-7353-11e9-86d2-5a13aaa147c3.png" width = "600">

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

<img src = "https://user-images.githubusercontent.com/44993623/57560225-60801f80-7353-11e9-8602-b6da4e55e4d4.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560240-768de000-7353-11e9-927e-83992d9525ba.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560246-83aacf00-7353-11e9-8e6f-9d3efaad9ea7.png" width = "600">


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

<img src = "https://user-images.githubusercontent.com/44993623/57560267-9e7d4380-7353-11e9-8ca3-f85573e58979.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560291-b94fb800-7353-11e9-874b-5c2025737699.png" width = "600">
<img src = "https://user-images.githubusercontent.com/44993623/57560302-c9679780-7353-11e9-9765-722c010664a7.png" width = "600">

## Conclusion
* Quantization to 8 bits leads to a 4x reduction in compression
* The test accuracy is within +- 0.3 % of the actual accuracy with float32
* Quantization leads to 1.5x to 2x speedup in inference time 


# Knowledge Distillation <BR>
Knowledge Distillation is a model compression method in which a small model is trained to mimic a pre-trained, larger model (or ensemble of models). This training setting is sometimes referred to as “teacher-student”, where the large model is the teacher and the small model is the student. The teacher model transfer generalizations to the student model rather than weights. In Knowledge Distillation the teacher models passed the “Dark Knowledge” to the student model i.e. which classes the teacher found to be more similar to the predicted class. Thus, Dark knowledge is the information, that, given the input, which classes are more likely to be the output besides the predicted class and is therefore, information about the relation of the input to the each class.(ner, 2017) <BR>
The formula described by Hinton et al. is as follows: <BR><BR>
<img src = "https://user-images.githubusercontent.com/46529465/55493546-2494c480-5607-11e9-908c-d3767e593052.png" width = "300">

<BR>Knowledge Distillation architectures: <BR>
<img src = "https://user-images.githubusercontent.com/46529465/55493551-25c5f180-5607-11e9-8144-194886a148fb.png" width = "450">
<BR><BR><BR>
<img src = "https://user-images.githubusercontent.com/46529465/55493553-26f71e80-5607-11e9-82a7-a8c082356d14.png" width = "500">

## Findings
### Setup: MNIST Data
<img src = "https://user-images.githubusercontent.com/46529465/55494038-0a0f1b00-5608-11e9-9ef3-a785bb8374d0.png" width = "850">

### Performance
<img src = "https://user-images.githubusercontent.com/46529465/55494044-0bd8de80-5608-11e9-8159-8d463e35dfc3.png" width = "850">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/46529465/55494048-0da2a200-5608-11e9-88ed-72522ab2545b.png" width = "850">
<BR><BR>
  
### Setup: CIFAR 10 Data

<img src = "https://user-images.githubusercontent.com/46529465/55494056-109d9280-5608-11e9-96bc-b6da7039d1e6.png" width = "850">
  
### Performance
<img src = "https://user-images.githubusercontent.com/46529465/55494069-14c9b000-5608-11e9-9140-5c6d3a6964af.png" width = "850">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/46529465/55494072-16937380-5608-11e9-815a-a89fc1468b95.png" width = "850">

## Conclusion
* Knowledge Distillation increases the ability of shallow neural nets to perform better
* Reduction in size is not always guaranteed but speedup is always present
* Accuracy takes quite a hit but maybe compensated for changing epochs, optimizer and learning rate
* Temperature is a hyperparameter whose value needs to be experimented with to determine best distilled model

# Pruning <BR>
Pruning is a method to reduce the storage and computation required by neural networks by learning only the important connections, thereby, converting a fully connected layer into a sparse one. One of the methods proposed to prune the network follows a three step process. First, training of the network to learn which connections are important. Second step is to prune away the less significant weights, which could either be done by absolute value pruning or by a hessian loss function. The third and the final step is to retrain the pruned network to maintain accuracy. Second and third steps are repeated many times to perform iterative pruning which helps further to boost compression without loss of accuracy when compared to single aggressive pruning.<BR>
  
## Findings
### Setup: LeNet300-100 MNIST Data
* Model: LeNet-300-100
* Learning Rate: 0.01
* Epochs: 10
* Retrain Epochs: 10
* Batch Size: 64
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: MNIST

* Training Accuracy: 99.6%
* Test Accuracy: 97.35%
* Hardware setup: Intel Core i7-8750H, NVIDIA GeForce GTX 1050Ti Max-Q

### Results
<img src = "https://user-images.githubusercontent.com/44993623/55851154-8a141400-5b25-11e9-8e2b-7ae5fa814a5b.PNG" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/55851265-ee36d800-5b25-11e9-84fa-70ba3dc31e57.PNG" width = "850">

### Setup: LeNet300-100 CIFAR10
* Model: LeNet-300-100
* Learning Rate: 0.01
* Epochs: 200
* Retrain Epochs: 200
* Batch Size: 256
* Optimization: Adam Optimization
* Activation Function: RELU
* Dataset: CIFAR-10

* Training Accuracy: 64.77%
* Test Accuracy: 48.55%

### Results
<img src = "https://user-images.githubusercontent.com/44993623/55851809-47077000-5b28-11e9-9bdd-325cb5ebaf96.PNG" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/55851464-aebcbb80-5b26-11e9-9862-389e4fff57fb.PNG" width = "850">

### Setup: LeNet5 MNIST
* Model: LeNet-5
* Learning Rate: 0.001 (Variable Learning Rate)
* Epochs: 10 (Early Stopping)
* Retrain Epochs 5
* Batch Size: 128
* Optimization: Adam Optimization
* Activation Function: RELU6
* Dataset: MNIST

* Training Accuracy: 99.79%
* Test Accuracy: 98.88%

### Results
<img src = "https://user-images.githubusercontent.com/44993623/55851521-f7747480-5b26-11e9-96b9-d6eecb5424bd.PNG" width = "850">

### Setup: LeNet5 CIFAR10
* Model: LeNet-5
* Learning Rate: 0.001(Variable Learning Rate)
* Epochs: 200 (Early Stopping)
* Retrain Epochs: 100(Early Stopping)
* Batch Size: 256
* Optimization: Adam Optimization
* Activation Function: RELU6
* Dataset: CIFAR-10

* Training Accuracy: 73.80%
* Test Accuracy: 55.37%

### Results
<img src = "https://user-images.githubusercontent.com/44993623/55851602-52a66700-5b27-11e9-8938-7592382697fb.PNG" width = "850">

## Conclusion
* Compression of upto 5x without loss in accuracy (after retraining).
* Marginal speedup of upto 1.3x when compared to baseline models.
* Cannot prune beyond a certain limit without loosing accuracy even after retraining because there is not much weight information left so that the model can fit the training data.



