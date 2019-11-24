# Lightricks Neural Style workshop

## Examples: Style Transfer
### Catriona Gray and Woman I by Willem de Kooning
![Catriona](https://i.imgur.com/Cx7WEZo.jpg)

### Janelle Monae and Starry Night by Vincent van Gogh
![Janelle Monae](https://i.imgur.com/WWq6I1U.jpg)

### Andrew Y. Ng and Oil Painting of a Girl in Rain
![AndrewYNg](https://i.imgur.com/cO9YdZI.jpg)

### Style Transfers of Golden Bridge
![dubnation](https://i.imgur.com/K2eCqjA.jpg)

### Rodrigo Duterte + Increasing Style Weights of Starry Night
![Rodrigo Duterte](https://i.imgur.com/bK8bnCN.jpg)

## Examples: Style Transfer while Preserving the original color
### Janelle Monae and Starry Night by Vincent van Gogh + Preserve Original Color
![Janelle Monae Preserve](https://i.imgur.com/asrUS0A.jpg) 

## Requirements
`IMPORTANT NOTE`: On `Google-Colab` All data files and dependencies can be installed by running the uppermost cell of the notebook! See `Usage`!

### Data Files
* [Pre-trained VGG19 network weights](https://s3-us-west-2.amazonaws.com/jcjohns-models/vgg16-00b39a1b.pth) - put it in `models/` directory
* [torchvision](https://pytorch.org/) - `torchvision.models` contains the VGG19 model skeleton

### Dependecies
* [PyTorch](https://pytorch.org/)
* [NumPy](https://www.scipy.org/install.html)
* [Jupyter](http://jupyter.org/install)
* [opencv2](https://matplotlib.org/users/installing.html)
* [Copy](https://docs.python.org/3/library/copy.html)

## Usage
You will be running  the notebook in [Google Colab](https://colab.research.google.com/github/ofirbb/spectrum-workshop/blob/master/neural_style.ipynb)! Colab is a cloud service with an interface similar to Jupyter notebook. It allows you to get an accelerator, such as a GPU, for Free!

Uncomment and run the first cell to download the demo pictures, and VGG19 weights. It will also install the dependencies (i.e. PyTorch and torchvision).
```
# Download VGG19 Model
!wget -c https://s3-us-west-2.amazonaws.com/jcjohns-models/vgg19-d01eb7cb.pth
!mkdir models
!cp vgg19-d01eb7cb.pth models/

# Download Images
!wget -c https://github.com/ofirbb/spectrum-workshop/archive/master.zip
!unzip -q master.zip
!mkdir images
!cp neural-style-pytorch-master/images/1-content.png images
!cp neural-style-pytorch-master/images/1-style.jpg images
```

## Options
### Image
* `MAX_IMAGE_SIZE`: sets the max dimension of height or weight. Bigger GPU memory is needed to run larger images. Default is `512`px.
* `INIT_IMAGE`: sets the initial image file to either `'random'` or `'content'`. Default is `random` which initializes a noise image. Content copies a resized content image, giving free optimization of content loss!
* `CONTENT_PATH`: path of the content image
* `STYLE_PATH`: path of the style image
* `PRESERVE_COLOR`: determines whether to preserve the color of the content image. `True` preserves the color of the content image. Default value is `False` 
* `PIXEL_CLIP`: determines whether to clip the resulting image. `True` clips the pixel values to [0, 255]. Default value is `True` 

### Optimizer
* `OPTIMIZER`: sets the optimizer to either 'adam' or 'lbfgs'. Default optimizer is `Adam` with learning rate of 10. L-BFGS was used in the original (matlab) implementation of the reference paper.
* `ADAM_LR`: learning rate of the adam optimizer. Default is `1e1`
* `CONTENT_WEIGHT`: Multiplier weight of the loss between content representations and the generated image. Default is `5e0`
* `STYLE_WEIGHT`: Multiplier weight of the loss between style representations and the generated image. Default is `1e2`
* `TV_WEIGHT`: Multiplier weight of the [Total Variation Denoising](https://github.com/jcjohnson/neural-style/issues/302). Default is `1e-3`
* `NUM_ITER`: Iterations of the style transfer. Default is `500`
* `SHOW_ITER`: Number of iterations before showing and saving the generated image. Default is `100`

### Model
* `VGG19_PATH` = path of VGG19 Pretrained weights. Default is `'models/vgg19-d01eb7cb.pth'`
* `POOL`: Defines which pooling layer to use. The reference paper suggests using average pooling! Default is `'max'`

## Credits!!!

An implementation of the neural style in PyTorch! This notebook implements [Image Style Transfer Using Convolutional Neural Networks](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) by Leon Gatys, Alexander Ecker, and Matthias Bethge. Color preservation/Color transfer is based on the 2nd approach of discussed in [Preserving Color in Neural Artistic Style Transfer](https://arxiv.org/pdf/1606.05897.pdf) by Leon Gatys, Matthias Betge, Aaron Hertzmann, and Eli Schetman.

This implementation is a slight adaptation of the [code by Rusty](https://github.com/rrmina/neural-style-pytorch).

The [original caffe pretrained weights of VGG19](https://github.com/jcjohnson/pytorch-vgg) were used for this implementation, instead of the pretrained VGG19's in PyTorch's model zoo.
