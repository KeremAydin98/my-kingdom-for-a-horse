# MY KINGDOM FOR A HORSE

This repository is the implementation of vanilla DCGAN image geneneration on Mnist and Cifar10 datasets. Firstly, I designed a vanilla GAN and DCGAN algorithm for mnist dataset to understand the core of a vanilla GAN algorithm. Then I tried to design a DCGAN algorithm with CIFAR dataset which was the real challenge. I named this repository "my kingdom for a horse" because I only used horse images from Cifar dataset. I wanted to share some of my observations while trying to optimize the GAN algorithm by changing hyperparameters. 

## My Observations

### Design simple discriminator and generator neural networks

* While designing a discriminator and a generator neural network, general advice is to design simple networks. My observations were also fitted with this advice. Creating deeper and wider networks did not improve the performance in contrast it decreased the performance of the GAN algorithm.

### Train discriminator more than the generator

* At first I updated the discriminator and generator network at every step, however the GAN was not converging to a believable image. The general advice on this topic is to train discriminator more than the generator. Therefore I created two algorithms, first algorithm updated discriminator three times and generator one time at every epoch; second algorithm updated discriminator five times for generator's one time at every epoch. The performance of five time update was much superior to the three time update of the discriminator.

### Implement a small learning rate

* Since the convergence of the GAN algorithm is very slow at default, I tried to train the algorithm with high learning rate such as 0.008 for discriminator and 0.004 for the generator. The convergence was faster and images got closer to a horse in 3000 steps. But after a few hundred steps the network completely forgot the features of a horse and started drawing random noise images. Lower learning rate such as 0.0002 for the discriminator and 0.0001 for the generator converged much slower, but the image got better with more iterations, did not update drastically and lead to a divergent behavior.

###  Set the pixel values between [-1,1] and use tanh activation for generator output

* I am sure everyone who has read about tips for training a GAN, have seen the advice to normalize the inputs between -1,1 and use tanh activation for generator output. I tried both leaky relu and tanh activation function and observed the difference. The tanh function created more believable images, since there is no general loss to calculate the performance of a GAN algorithm I can only tell my observations on the created images by the generator.

### Use batch normalization on discriminator network

* Batch normalization is the normalization of the input values of a layer by using input values' mean and variance. The batch normalization improves the performance of the discriminator and decreases the performance of the generator. Some papers suggest using batch normalization on generators too but my observations proved otherwise. Also it should not be forgotten that batch normalization must not be put after the input layer of the discriminator.

### Use dropout layer on discriminator network

* Overfitting is another issue for training of the GAN algorithm. If the algorithm is overfitted, the discriminator loss decreases to low negative numbers and the generator loss increases exponentially to high values. To avoid this issue, dropout layer must be used on the discriminator network. Dropout layer ignores the percentage, that has been given by the user, of the neurons of that particular layer. The percentage must be given by iterations.

### Add noise to the labels

* Adding noise to the labels increases the performance of the discriminator. However, I did not understand the reason behind the improvement. It is more of an empirical discovery rather than theoretical like many of the improvements in machine learning :) 
