# cDCGAN-MNIST

This Repository contain an IPython notebook of an example implementation of conditional Deep Convolutional Generative Adversarial Networks or cDCGAN or DC cGAN.
This cDCGAN model is trained using MNIST handwritten digits data, and after trained the generator can output MNIST-like handwritten digits by just specifying a label (number from 0-9) and a vector of 100 noise.

This implementation is based on DCGAN tutorial by Tensorflow.
https://www.tensorflow.org/tutorials/generative/dcgan

The difference is instead just training the GAN using image only, cGAN also uses label to train the neural network. And also i had to convert the sequential API used by CDGAN to Functional API because the cDCGAN model have to take two inputs (image and label) and the sequential API are not suitable for that proupose.

I also personally believe that cGAN is much more useful than GAN because we can control the output of the generator just by specifying labels.

## Model

Below are the model of the Discriminator and the Generator 

Discriminator         |  Generator
:-------------------------:|:-------------------------:
![Discriminator](https://raw.githubusercontent.com/zokovi/cDCGAN-MNIST/master/discriminator.jpg) | ![Generator](https://raw.githubusercontent.com/zokovi/cDCGAN-MNIST/master/Generator.png) 

The discriminator output 1x1 shape of value between 0 and 1. Value of 0 for fake images and 1 for real images.
The generator take input of label (in this case 0-9) and a set of noise, then generates 28x28 pixel of image.

## Training 
The training algorithm is visually described by this helpful graph i found in Mathworks website:

![](https://www.mathworks.com/help/examples/nnet/win64/TrainConditionalGenerativeAdversarialNetworkCGANExample_02.png)

1. To train the image we just feed the label and a set random noise to the generator. The generator then produces 'fake images'.

2. Then we fed both the image and label pair of the real image (from the dataset) and 'fake images' to the discriminator. 

3. We want the discriminator to produces value of 1 for real images and 0 for fake images. So we use that to calculate the loss of the discriminator. 

4. We want the generator to produce image that make the discriminator thinks that the generated fake images are a real image. So we also use that to calculate the loss of the generator by comparing the output value of the discriminator to value of 1 when the discriminator was fed fake image.

5. Then, we calculate the gradient of the discriminator and the generator using their loss respectively and apply those graident to each model accordingly.

## Results.

This is the gif of the training process for 200 epoch. For every epoch, I make the generator produces each number from 0 to 9 by specifying label 0 to 9 with a fixed noise. 

![](https://raw.githubusercontent.com/zokovi/cDCGAN-MNIST/master/cdcgan.gif)

## Closing Statement

This repository is my attempt at learning conditional GAN because i have been blown by the capabilites that the results of generator of GANs model can produce and then the control aspect of the cGAN generator.

Feel free to use, modify, or do something else to the content provieded in this repository to study conditional GAN or any other stuff, Thanks for coming to this repository.

Thanks to kaggle I was able to Train the model in significanly faster for free by utilizing the free GPU compute that they provided.
