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
- The [GIAB](https://www.nist.gov/programs-projects/genome-bottle) data was used to generate 4000 positive and negative igv screenshots.  Thus, each class had about 4000 images.

- it is tricky to get the right igv screen shot. You can run igv -b command to generate snapshots for many variants of interest. On my computer, the width of the snapshot is about 1720 pixels and the height of the snapshot can not be controlled. It is automatically decided by the coverage of the position. While taking the snapshots, the height will reset to the previous maximum height. So it does not matter. it depends on the coverage. It seems I need to have a option to downsample. otherwise, it only shows the first 200x or so reads.
- it is not a viable option to attempt to keep the position of interest in the middle. It is hard to preprocessing. Also CNN has the ability to detect the image at any position. we use the centre line as a cue. this way i can do data augmentation as well. presumably, the model will generalize better.
- I need to be consistent when generate those screenshots, remember to use collapse mode, zoom to the last 5th level.igv.
many parameter/options in igv batch file does not really work. for example: maxtrackheight, sort tec.
the height pixels for the screen shot changes depending on the read coverage,
- I need to be very careful when cropping the images. cropping need to start from left and top. i may need to preprocess the images before feed to fastai imagelist.
- remember some of those randomly generated negative images may be empty due to zero coverage, remove these before feeding to model.
- bedtools can generate random intervals for genome. -n number of intervals, -l length of interval, -g genome -seed random seeds
- including positions that are 2-50 base pair away from the known variant position.
- including positions that looks like a real variant, but the supporting reads also have multiple mis-matches at other places. These are the most useful training images.
- including some random positions absent from variant.

## Training the data:  Resnet-34 CNN
|  epoch 	|  train_loss	|  valid_loss	|  accuracy 	|  time  |

|  0	    |  0.020749	  |  0.023093	  |  0.994072	  |  1:34  |

|  1    	|  0.015178	  |  0.021274	  |  0.994072	  |  1:34  |
