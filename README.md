# Conformer-VC

Conformer-VC is inspired by [Non-autoregressive sequence-to-sequence voice conversion](https://arxiv.org/abs/2104.06793) that is parallel voice conversion methods by using conformer.

The differences between original paper are

- NOT using reduction-factor.
- Mel-spectrograms are not normalized by speaker statistics.
- Use HiFi-GAN instead of PrallelWaveGAN

# Requirements

- pytorch
- numpy
- pyworld
- accelerate
- soundfile
- librosa
- cython
- omegaconf
- tqdm
- resemblyzer
- matplotlib
- scipy

If you get an error about the package, please install it.

# Usage

1. Preprocess

Note that this project is for my dataset.  
So, if you wanna train your dataset, please rewrite configs/preprocess.yaml and preprocess.py properly.

```bash
# setup for dtw module
$ cd dtw && python setup.py build_ext --inplace && cd ..
$ python prerprocess.py
```

2. Training

single gpu training

```bash
$ ln -s ./dataaset/feats DATA
$ python train.py
```
or multi gpus

```bash
$ accelerate config

answer question of your machine.

$ accelerate launch train.py
```

3. Validation

```bash
$ python validate.py --model_dir {MODEL_DIR} --hifi_gan {HIFI_GAN_DIR} --data_dir DATA
```

if this script run correctly, outputs directory is generated and synthesized wav is in it.
