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
<img src = "https://user-images.githubusercontent.com/44993623/57560795-3d0aa400-7356-11e9-8919-6f3ac7b08913.PNG" width = "850">

### Performance
<img src = "https://user-images.githubusercontent.com/44993623/57560811-56135500-7356-11e9-9012-cbbe3af6124f.PNG" width = "850">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/44993623/57560833-76431400-7356-11e9-926b-59d2938a3432.PNG" width = "850">
<BR><BR>
  
### Setup: CIFAR 10 Data

<img src = "https://user-images.githubusercontent.com/44993623/57560846-91158880-7356-11e9-9d8f-1af664e95de4.PNG" width = "850">
  
### Performance
<img src = "https://user-images.githubusercontent.com/44993623/57560858-a8547600-7356-11e9-9bf3-07518b119916.PNG" width = "850">

### Effect of Temperature on Accuracy
<img src = "https://user-images.githubusercontent.com/44993623/57560875-c0c49080-7356-11e9-82f7-a789baa7375e.PNG" width = "850">

## Conclusion
* Knowledge Distillation increases the ability of shallow neural nets to perform better
* Reduction in size is not always guaranteed but speedup is always present
* For config1 on MNIST we observe a speedup of 6x in student model as compared to LeNet-5 and a speedup of 5.21x compared to LeNet-300-100 while for config 2 on MNIST, we observe a speedup of 7.72x in student model as compared to LeNet-5 and a speedup of 5.05x compared to LeNet-300-100
* For config1 on CIFAR10 we observe a speedup of 6.67x in student model compared to both LeNet-5 and LeNet-300-100 while for config2, we find the speedup of 6.20x compared to both LeNet-5 and LeNet-300-100 
* Accuracy takes quite a hit but maybe compensated for changing epochs, optimizer and learning rate
* Temperature is a hyperparameter whose value needs to be experimented with to determine best distilled model

# Pruning <BR>
Pruning is a method to reduce the storage and computation required by neural networks by learning only the important connections, thereby, converting a fully connected layer into a sparse one. One of the methods proposed to prune the network follows a three step process. First, training of the network to learn which connections are important. Second step is to prune away the less significant weights, which could either be done by absolute value pruning or by a hessian loss function. The third and the final step is to retrain the pruned network to maintain accuracy. Second and third steps are repeated many times to perform iterative pruning which helps further to boost compression without loss of accuracy when compared to single aggressive pruning.<BR>
  
 <img src = "https://user-images.githubusercontent.com/44993623/57560365-13e91400-7354-11e9-9def-97eb9b07035f.png" width = "850">
  
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
<img src = "https://user-images.githubusercontent.com/44993623/57560397-33803c80-7354-11e9-9a6d-d6189dbc3b4a.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560409-42ff8580-7354-11e9-842d-02f3005b4736.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560433-5ad70980-7354-11e9-94a0-de3b404a4acd.png" width = "850">

### Total Parameters
<img src = "https://user-images.githubusercontent.com/44993623/57560471-9a055a80-7354-11e9-9424-455487284f77.PNG" width = "850">

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
<img src = "https://user-images.githubusercontent.com/44993623/57560496-bef9cd80-7354-11e9-804a-396f303c567a.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560508-d933ab80-7354-11e9-880a-85e10920cee3.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560520-eb154e80-7354-11e9-8d38-c93cdfa36ddb.png" width = "850">

### Total Parameters
<img src = "https://user-images.githubusercontent.com/44993623/57560558-0da76780-7355-11e9-8ac9-cee0328ff207.PNG" width = "850">


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
<img src = "https://user-images.githubusercontent.com/44993623/57560591-2e6fbd00-7355-11e9-9cbc-b71677a9dd7c.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560609-421b2380-7355-11e9-88a2-1f182dbbadc9.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560624-53643000-7355-11e9-845e-578f9e194aa3.png" width = "850">

### Total Parameters
<img src = "https://user-images.githubusercontent.com/44993623/57560659-742c8580-7355-11e9-9d84-b8923a299753.PNG" width = "850">


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
<img src = "https://user-images.githubusercontent.com/44993623/57560680-8dcdcd00-7355-11e9-83b2-c8f1b9b46f35.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560695-a2aa6080-7355-11e9-8289-12a6b4c7dc83.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57560703-b3f36d00-7355-11e9-95a8-aafbc501c78d.png" width = "850">

### Total Parameters
<img src = "https://user-images.githubusercontent.com/44993623/57560739-d7b6b300-7355-11e9-81a1-3daf620e961a.PNG" width = "850">

## Conclusion
* Increasing the sparsity reduces the size significantly but the accuracy also take a big hit, so we need to consider a tradeoff between them
* Though the network might be pruned deeply, the inference time per image becomes constant after a certain pruning limit but we record a speedup of 2x to 4x on LeNet-300-100 and around 1.2x on LeNet-5 on MNIST and CIFAR-10 datasets. 
* We also record a size compression of 5x on LeNet-300-100 on MNIST while a compression of 18x on LeNet-5 on MNIST datasets with accuracy within + 3% of baseline models and similar compression rates on CIFAR-10 with accuracy within + 6% of baseline models.

# Pruning follwed by Quantization
* We pruned the base model and then in the same pipeline we quantized the pruned model and recorded the accuracy, inference time and size of various quantized models of different sparsity along with the non quantized counter parts. 
* This has been done for both the models LeNet-300-100 and LeNet-5 on MNIST and CIFAR-10 datasets. 

## Results
### LeNet300-100 on MNIST
<img src = "https://user-images.githubusercontent.com/44993623/57560987-53652f80-7357-11e9-961c-a6cf0be63902.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561001-6aa41d00-7357-11e9-9c05-b3977c28e10e.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561022-7d1e5680-7357-11e9-8b77-bb09dde03849.png" width = "850">

### LeNet5 on MNIST
<img src = "https://user-images.githubusercontent.com/44993623/57561043-9de6ac00-7357-11e9-88c0-e6bf6979f5e1.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561052-ac34c800-7357-11e9-9520-05f81607dc88.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561058-bc4ca780-7357-11e9-9ab0-a98c46289550.png" width = "850">

### LeNet300-100 on CIFAR10
<img src = "https://user-images.githubusercontent.com/44993623/57561272-bdca9f80-7358-11e9-8bf2-24308a1f6a19.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561277-ccb15200-7358-11e9-9a34-ae76b1367dc5.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561288-dcc93180-7358-11e9-91e4-3bd8c8fc5262.png" width = "850">

### LeNet5 on CIFAR10
<img src = "https://user-images.githubusercontent.com/44993623/57561314-f9656980-7358-11e9-8607-d70f64f65859.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561322-0a15df80-7359-11e9-85c0-0d9239d5cd5e.png" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561334-1ef27300-7359-11e9-8b21-1ea52669dcb8.png" width = "850">

## Conclusion
* Pruning and Quantization are orthogonal and don’t affect each other and can be used in a pipeline for deep compression of the neural networks. 
* With such a pipeline we could achieve about 2x to 8x speedup on LeNet-300-100 on MNIST and about 2x to 7x speed up on CIFAR-10. For LeNet-5 on MNIST we observe a speed up of 1.2x to 1.4x and similar speedups in CIFAR-10. 
* We observe very significant gain in the size compression of about 40x on LeNet300-100 on MNIST and 35x on LeNet-5 on MNIST and for LeNet-300-100 on CIFAR-10 we could expect a compression of 20x and on LeNet-5 a size compression of about 13x could be observed with minimal loss in accuracy.


# Knowledge Distillation followed by Quantization
* Distilled the knowledge of the teacher model in the student model and then in the same pipeline we have quantized the student model to int8 precision for both the datasets MNIST and CIFAR-10 for both LeNet-300-100 and LeNet-5 models.
* We have recorded the size, accuracy and the inference time per image on both the hardware configurations and have plotted the results for original distilled student model and quantized student model.

## Results
<img src = "https://user-images.githubusercontent.com/44993623/57561434-a213c900-7359-11e9-92ea-c93b37604209.PNG" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561452-c374b500-7359-11e9-9f85-45d2d9aa48c8.PNG" width = "850">
<img src = "https://user-images.githubusercontent.com/44993623/57561467-d7b8b200-7359-11e9-8e54-a039ef74b4e3.PNG" width = "850">
 
 ## Conclusion
* We see a reduction of 4x size in the quantized student model which is 25x smaller than the original LeNet-300-100 model for MNIST and CIFAR-10 datasets and 6x smaller than LeNet-5 model on MNIST and 1.7x reduction on CIFAR-10.
* There is almost no accuracy loss on quantization of student model and the accuracy is almost the same as before quantization thus, preserving accuracy.
* There is almost a 11x – 13x speedup in the quantized student model as compared to original teacher models for both the datasets.


# Final Conclusion
* Deep Neural Network Compression and acceleration techniques like Quantization, Pruning and Knowledge Distillation result always in reduction of latency and size with almost minimal loss of accuracy. 
* There are tradeoffs when applying these techniques individually but a balance between the tradeoffs can help achieve smaller and faster inference models with almost no accuracy loss.
* These techniques can be combined together in the pipelines knowledge distillation followed by quantization of student model and pruned model followed by quantization. 
* We have achieved a speedup of 2x to 12x and a size reduction 4x to 40x by applying these techniques individually and together while maintaining accuracy within + 5% levels of the baseline models and have been successful as well.

# Future Work
* We would like to do power analysis on GPUs for this we are planning to run these models on GPUs which support nvidia-smi.
* Further exploration of combinations are planned including distilling the knowledge of the original model (teacher) to a pruned model of the original model (student) and then quantizing this student model. 
* Another combination to explore is prunning a distilled model and then quantizing the pruned distilled model.


