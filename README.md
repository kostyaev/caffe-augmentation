# Caffe Augmentation Extension
This is a recent caffe version (2016/05/25, 4bf4b18607) with additional transformation options in ImageData layer. The following transformations have been added to support:

* min_side - resize and crop preserving aspect ratio, default 0 (disabled);
* max_rotation_angle - max angle for an image rotation, default 0;
* contrast_brightness_adjustment - enable/disable contrast adjustment, default false;
* smooth_filtering - enable/disable smooth filterion, default false;
* min_contrast - min contrast multiplier (min [alpha](http://docs.opencv.org/2.4/doc/tutorials/core/basic_linear_transform/basic_linear_transform.html)), default 0.8;
* max_contrast - min contrast multiplier (max [alpha](http://docs.opencv.org/2.4/doc/tutorials/core/basic_linear_transform/basic_linear_transform.html)), default 1.2;
* max_brightness_shift - max brightness shift in positive and negative directions ([beta](http://docs.opencv.org/2.4/doc/tutorials/core/basic_linear_transform/basic_linear_transform.html)), default 5;
* max_smooth - max smooth multiplier, default 6;
* apply_probability - how often every transformation should be applied, default 0.5;
* debug_params - enable/disable printing tranformation parameters, default false;

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
        contrast_brightness_adjustment: true
        smooth_filtering: true
        max_rotation_angle: 10
        min_side: 256
        crop_size: 224
        mean_file: "/home/your/imagenet_mean.binaryproto"
        min_contrast: 0.8
        max_contrast: 1.2
        max_smooth: 6
        apply_probability: 0.5
        debug_params: false
    }
    image_data_param {
      source: "/home/your/image/list.txt"
      batch_size: 32
      shuffle: true
    }
    }


## Setup caffe-augmentation
There are two options:

1. Pull and run docker container: 
  
    ```$ docker pull kostyaev/caffe-gpu```

    ```$ nvidia-docker run -it kostyaev/caffe-gpu /bin/bash```

2. Install from source code:
Clone this repo, adjust Makefile.config and simply run the following commands:

    ```$ make all -j8```
    
    ```$ make test -j8```
    
    ```$ make runtest -j8```

For a faster build, compile in parallel by doing `make all -j8` where 8 is the number of parallel threads for compilation (a good choice for the number of threads is the number of cores in your machine).


## Acknowledgment
This project is based upon 
[@kevinlin311tw](https://github.com/kevinlin311tw)'s [caffe-augmentation](https://github.com/kevinlin311tw/caffe-augmentation),
[@ChenlongChen](https://github.com/ChenglongChen)'s [caffe-windows](https://github.com/ChenglongChen/caffe-windows), [@ShaharKatz](https://github.com/ShaharKatz)'s [Caffe-Data-Augmentation](https://github.com/ShaharKatz/Caffe-Data-Augmentation), and [@senecaur](https://github.com/senecaur)'s [caffe-rta](https://github.com/senecaur/caffe-rta).
