# cDCGAN-MNIST

This Repository contain a IPython notebook of an example implementation of conditional Deep Convolutional Generative Adversarial Networks or cDCGAN or DC cGAN.
This cDCGAN model is trained using MNIST handwritten digits data, and after trained the generator can output MNIST-like handwritten digits by just specifying a label (number from 0-9) and a vector of 100 noise.

This implementation is based on DCGAN tutorial by Tensorflow.
https://www.tensorflow.org/tutorials/generative/dcgan

The difference is instead just training the GAN using image only, cGAN also uses label to train the neural network. And also i had to convert the sequential API used by CDGAN to Functional API because the cDCGAN model 

I am also personally believe that cGAN is much more useful than GAN because we can control the output of the generator just by specifying labels.

## Model

The model 




## Training 
The training algorithm is visually described by this helpful graph i found in Mathworks website
![](https://www.mathworks.com/help/examples/nnet/win64/TrainConditionalGenerativeAdversarialNetworkCGANExample_02.png)

To train the image we just feed the label and a set random noise to the generator. The generator then produces 'fake images'.

Then we fed both the image and label pair of the real image (from the dataset) and 'fake images' to the discriminator. 

We want the discriminator to produces value of 1 for real images and 0 for fake images. So we use that to calculate the loss of the discriminator. 

We want the generator to produce image that make the discriminator thinks that the generated fake images are a real image. So we also use that to calculate the loss of the generator by comparing the output value of the discriminator to value of 1 when the discriminator was fed fake image.

Then, we calculate the gradient of the discriminator and the generator using their loss respectively and apply those graident to each model accordingly.

