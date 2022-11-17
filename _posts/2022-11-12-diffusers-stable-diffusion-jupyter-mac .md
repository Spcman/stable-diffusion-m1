---
layout: single
title:  "Diffusers Library Example within a Jupyter Notebook using Apple Mac M1/2"
comments: true
date:   2022-11-10
---

Building on our success so far in the previous posts the next logical step, in my opinion, is to experiment with the Hugging Face diffusers library. This library let's us get text to image output with just a few lines of code.

For this example I downloaded a the latest Hugging Face Mmdel (at the time). This model is more like 8 GB! 

Start your Jupyter notebook and ensure you're logged into hugging face

```python
!huggingface-cli whoami
```
This will reveal your userid

```python
from diffusers import StableDiffusionPipeline
DEVICE='mps'
pipe = StableDiffusionPipeline.from_pretrained("stable-diffusion-v1-5", use_auth_token=True).to(DEVICE)
```

A simple text to image via a prompt


```python
image = pipe(prompt="a happy dog working on a macbook air, sythwave").images[0]
image
```


      0%|          | 0/51 [00:00<?, ?it/s]


    
![png]({{ site.url }}{{ site.baseurl }}/images/002/output_15_1.png)


