# Image-to-Image

A Python notebook for transforming one style of image into another using a cycle generative adversarial network (CycleGAN). This project transforms between two types of airport security x-ray images: isosurface and transparency.

## Cycle Generative Adversarial Network (CycleGAN)

A CycleGAN is a machine learning framework that allows us to transform between image styles without the need for paired images in the training data. The entire framework consists of four competing machine learning models: two generators and two discriminators. Each generator transforms images from one domain into another, trying to make the transformed images look as realistic as possible. Each discriminator attempts to discern which images are real and which are fake (created by a generator).

### Details

For example, generator G: X->Y transforms images from the X domain (isosurface) into the Y domain (transparency). Discriminator D: Y->[0, 1] attempts to predict whether or not an image in the Y domain is real (output close to 1) or fake (output close to 0). Similarly, there is a generator that transforms from the Y domain to the X domain and a corresponding discriminator for the X domain.

Each generator competes with a discriminator. The goal of a generator is to trick its corresponding discriminator into thinking the generated image is real. The goal of a discriminator is to correctly determine which images are fake and which are real.

As the weights of a generator are adjusted to decrease its loss, the loss of the corresponding discriminator inherently increases. Similarly, as the weights of a discriminator are adjusted to decrease its loss, the loss of the corresponding generator inherently increases. This race condition incentivises each model to be the best it can be.

Furthermore, each generator's loss function takes into account a cycle loss. Images are cycled between the domains and then compared to the original to see how close to the original they are. In other words, an image will be transformed from the isosurface domain to the transparency domain, and then back to the isosurface domain. The cycled isosurface image (the "fake" image) will be compared to the original isosurface image (the "real" image) to see how closely they match. A good generator will make them nearly indistinguishable.
