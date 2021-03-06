Deep CNN for Image Denoising- Tensorflow implementation

This model is trained for blind denoising at multiple noise levels (\[0, 55\]).

[DnCNN paper (TIP 2017)](http://www4.comp.polyu.edu.hk/~cslzhang/paper/DnCNN.pdf)

## Results on CBSD68 dataset
![CBSD68](./imgs/denoised.png)


| Noise Level | CBM3D | CDnCNN-B |
|:-----------:|:-------:|:----------------:|
| 25          | 30.70   | **31.23**        |
| 50          | 27.38   | **27.97**        |

## Getting Started


### Prerequisites
```
natsort==5.4.1
numpy==1.16.0
tensorflow==1.13.1
Pillow==5.4.1
```

## Training the network

First, 128x3000 patches are extracted from the CBSD432 images as follows:

```
python generate_patches_rgb_blind.py
```
Then train the network:
```
python main_blind.py --phase train
```
You can also control other paramaters such as batch size, number of epochs. More info inside main.py.

The checkpoints are saved in ./checkpoint folder. Denoised validation images are saved after each epoch in ./sample folder.

### Tensorboard summaries
```
tensorboard --logdir=./logs
```

## Testing using the trained network

To test the network for sigma=50:
```
python main_blind.py --phase test --sigma 50.0
```
Denoised images are saved in ./test folder.


## Reference
* Code structure follows the repository [DnCNN-Tensorflow](https://github.com/crisb-DUT/DnCNN-tensorflow) of @crisb-DUT (dataset import and feeding, loading checkpoints etc.).


