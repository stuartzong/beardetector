# Training the Model

1.  Deep learning library
2.  Setting up GPU
3.  Getting the data
4.  Training the model 

## Deep learning library:  fastai
The [fastai](https://github.com/fastai/fastai) deep learning library, version 1.0 was utilized.  Fastai runs on top of PyTorch.   The [fastai MOOC](https://docs.fast.ai) was officially released to the public in early 2019.

## GPU: GeForce GTX TITAN
The model was trained on GeForce GTX TITAN GPU.

## Dataset:  igv screenshots from GIAB project and some inhouse genome sequencing data
The [GIAB](https://www.nist.gov/programs-projects/genome-bottle) data was used to generate 4000 positive and negative igv screenshots.  Thus, each class had about 4000 images.

## Training the data:  Resnet-34 CNN

