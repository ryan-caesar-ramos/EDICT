# Note

This is an unofficial implementation of EDICT at half precision following the [comments of the original author](https://github.com/salesforce/EDICT/issues/1#issuecomment-1375994018).

This implementation was tested on Colab where condacolab was creating issues. Hence the original installation instructions were forwent and the following lines reflect the installation used instead:

```
pip install diffusers==0.6.0 scipy==1.9.3 omegaconf==2.1.1 pillow==9.2.0
pip install -U transformers
```

The first line installs packages using the versions specified by the original `environment.yaml`; an upgraded version of `transformers` was used because the version specified by the original yaml was causing issues that others reported as solved after upgrading.

The repository previously only involved minimal changes required to add half precision functionality, but as of 01/31/23 now contains undocumented QoL features for personal use. Please let me know if you need me to document these, though an official implementation for half precision [should be underway by the original authors](https://github.com/salesforce/EDICT/issues/1#issuecomment-1396216563).

The rest of the original README.md is left untouched below:

# Official Implementation of EDICT: Exact Diffusion Inversion via Coupled Transformations

[Arxiv](https://arxiv.org/abs/2211.12446)

The original framework for this code is based off of Github user bloc97's [implementation of Prompt-to-Prompt](https://github.com/bloc97/CrossAttentionControl). 

# What is EDICT?

EDICT (Exact Diffusion Inversion via Coupled Transformations) is an algorithm that closely mirrors a typical generative diffusion process but in an invertible fashion. We achieve this by tracking a *pair* of intermediate representations instead of just one. This exact invertibility enables edits that remain extremely faithful to the original image. Check out our [paper](https://arxiv.org/abs/2211.12446) for more details and don't hesitate to reach out with questions!


# Setup

## HF Auth token

Paste a copy of a suitable [HF Auth Token](https://huggingface.co/docs/hub/security-tokens) into [hf_auth](hf_auth) with no new line (to be read by the following code in `edict_functions.py`)
```
with open('hf_auth', 'r') as f:
    auth_token = f.readlines()[0].strip()
    
```

Example file at `./hf_auth`
```
abc123abc123
```

## Environment

Run  `conda env create -f environment.yaml`, activate that conda env (`conda activate edict`). Run jupyter with that conda env active

# Experimentation

Check out [this notebook](EDICT.ipynb) for examples of how to use EDICT; including edits on randomly selected in-the-wild imagery ([alternative to render in browser](EDICT_no_images.ipynb)).

# Example Results

## Changing Dog Breeds

![Dogs](figs/edits_dogs.png)

## Miscellaneous


![Some edits](figs/edits_1.png)

![Some more edits](figs/edits_2.png)

# Other Files

[edict_functions.py](edict_functions.py) has the core functionality of EDICT. [my_diffusers](my_diffusers) is a very slightly changed version of the [HF Diffusers repo](https://github.com/huggingface/diffusers) to work in double precision and avoid floating-point errors in our inversion/reconstruction experiments. EDICT editing also works at lower precisions, but to allow all experiments in a unified setting we present the double-precision floating point version of the code.

# Citation

If you find our work useful in your research, please cite:

```
@article{wallace2022edict,
  title={EDICT: Exact Diffusion Inversion via Coupled Transformations},
  author={Wallace, Bram and Gokul, Akash and Naik, Nikhil},
  journal={arXiv preprint arXiv:2211.12446},
  year={2022}
}
```

# License

Our code is BSD-3 licensed. See LICENSE.txt for details.

