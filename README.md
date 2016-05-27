# Caffe Augmentation Extension
This is a recent caffe version (2016/05/25, 4bf4b18607) with additional transformation options in ImageData layer. The following transformations have been added to support:

* min_side - resize and crop preserving aspect ratio
* rotation_angle - max angle for an image rotation
* contrast_adjustment - enable/disable contrast adjustment
* min_alpha - min contrast multiplier
* max_alpha - min contrast multiplier
* smooth_filtering - enable/disable smooth filterion
* max_smooth - max blur multiplier

## How to use
You could specify your network prototxt as:

    layer {
    name: "data"
    type: "ImageData"
    top: "data"
    top: "label"
    include {
      phase: TRAIN
    }
    transform_param {
        mirror: false
        contrast_adjustment: true
        smooth_filtering: true
        rotation_angle: 10
        min_side: 256
        crop_size: 224
        mean_file: "/home/your/imagenet_mean.binaryproto"
        min_alpha: 0.8
        max_alpha: 1.2
        max_smooth: 6
    }
    image_data_param {
      source: "/home/your/image/list.txt"
      batch_size: 32
      shuffle: true
    }
    }


## Setup caffe-augmentation
Adjust Makefile.config and simply run the following commands:

    $ make all -j8
    $ make test -j8
    $ make runtest -j8

For a faster build, compile in parallel by doing `make all -j8` where 8 is the number of parallel threads for compilation (a good choice for the number of threads is the number of cores in your machine).


## Acknowledgment
This project is based upon 
[@kevinlin311tw](https://github.com/kevinlin311tw)'s [caffe-augmentation](https://github.com/kevinlin311tw/caffe-augmentation),
[@ChenlongChen](https://github.com/ChenglongChen)'s [caffe-windows](https://github.com/ChenglongChen/caffe-windows), [@ShaharKatz](https://github.com/ShaharKatz)'s [Caffe-Data-Augmentation](https://github.com/ShaharKatz/Caffe-Data-Augmentation), and [@senecaur](https://github.com/senecaur)'s [caffe-rta](https://github.com/senecaur/caffe-rta).
