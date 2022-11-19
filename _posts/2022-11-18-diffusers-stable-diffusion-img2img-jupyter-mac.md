---
layout: single
title:  "Text Guided Image2Image Pipeline Jupyter Notebook using Apple Silicon"
comments: true
date:   2022-11-18
---

Building on our success with Text to Image using our M1, let's check we can also run the Image to Image diffuser pipeline (guided by a text prompt).  

This example is based on the [Hugging Face img2img example here](https://huggingface.co/docs/diffusers/using-diffusers/img2img)

```python
from diffusers import StableDiffusionImg2ImgPipeline
DEVICE='mps'
pipe = StableDiffusionImg2ImgPipeline.from_pretrained("stable-diffusion-v1-5").to(DEVICE)
```


```python
import inspect
import warnings
from typing import List, Optional, Union

import torch
from tqdm.auto import tqdm
```
Load the initial input image as the base for the image2image. 

```python
import requests
from io import BytesIO
from PIL import Image

url = "https://raw.githubusercontent.com/CompVis/stable-diffusion/main/assets/stable-samples/img2img/sketch-mountains-input.jpg"

response = requests.get(url)
init_img = Image.open(BytesIO(response.content)).convert("RGB")
init_img = init_img.resize((768, 512))
init_img
```
![png]({{ site.url }}{{ site.baseurl }}/images/003/output_5_0.png)
    
```python
prompt = "A fantasy landscape, trending on artstation"
```

Here, strength is a value between 0.0 and 1.0, that controls the amount of noise that is added to the input image. Values that approach 1.0 allow for lots of variations but will also produce images that are not semantically consistent with the input.

```python
generator = torch.Generator().manual_seed(1024)
image = pipe(prompt=prompt, init_image=init_img, strength=0.7, guidance_scale=7.5, generator=generator).images[0]
image
```

    /Users/nigeemmaadams/opt/anaconda3/envs/diffusion/lib/python3.10/site-packages/diffusers/pipelines/stable_diffusion/pipeline_stable_diffusion_img2img.py:288: UserWarning: The operator 'aten::repeat_interleave.self_int' is not currently supported on the MPS backend and will fall back to run on the CPU. This may have performance implications. (Triggered internally at /Users/runner/work/pytorch/pytorch/pytorch/aten/src/ATen/mps/MPSFallback.mm:11.)
      text_embeddings = text_embeddings.repeat_interleave(num_images_per_prompt, dim=0)

      0%|          | 0/36 [00:00<?, ?it/s]

![png]({{ site.url }}{{ site.baseurl }}/images/003/output_8_2.png)
    
```python
generator = torch.Generator().manual_seed(1024)
image = pipe(prompt=prompt, init_image=init_img, strength=0.5, guidance_scale=7.5, generator=generator).images[0]
image
```
      0%|          | 0/26 [00:00<?, ?it/s]

![png]({{ site.url }}{{ site.baseurl }}/images/003/output_9_1.png)
    


    



