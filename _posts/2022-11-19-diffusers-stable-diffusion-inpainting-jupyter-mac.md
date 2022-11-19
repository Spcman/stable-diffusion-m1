---
layout: single
title:  "Text-Guided Image Inpainting In Jupyter Notebook on Apple Silicon (MPS)"
comments: true
date:   2022-11-19
---

For this one we need to download the Hugging Face [Stable-Diffusion-Inpainting Model](https://huggingface.co/runwayml/stable-diffusion-inpainting). You need to read/accept the licence, download it and place in your models folder. I suggest you get this this using `git lfs install` then 
`git clone https://huggingface.co/runwayml/stable-diffusion-inpainting` . This will download the model checkpoint and associated files needed to make the following code block to work.

```python
from diffusers import StableDiffusionInpaintPipeline
DEVICE='mps'
pipe = StableDiffusionInpaintPipeline.from_pretrained("models/stable-diffusion-inpainting").to(DEVICE)
```


```python
import PIL
import requests
import torch
from io import BytesIO
```

The following code downloads our initial image and mask image examples.


```python
def download_image(url):
    response = requests.get(url)
    return PIL.Image.open(BytesIO(response.content)).convert("RGB")

img_url = "https://raw.githubusercontent.com/CompVis/latent-diffusion/main/data/inpainting_examples/overture-creations-5sI6fQgYIuo.png"
mask_url = "https://raw.githubusercontent.com/CompVis/latent-diffusion/main/data/inpainting_examples/overture-creations-5sI6fQgYIuo_mask.png"

init_image = download_image(img_url).resize((512, 512))
mask_image = download_image(mask_url).resize((512, 512))
```


```python
init_image
```




![png]({{ site.url }}{{ site.baseurl }}/images/003/output_6_0.png)
    




```python
mask_image
```




![png]({{ site.url }}{{ site.baseurl }}/images/003/output_7_0.png
    




```python
prompt = "Face of a yellow cat, high resolution, sitting on a park bench"
image = pipe(prompt=prompt, image=init_image, mask_image=mask_image).images[0]
```


      0%|          | 0/50 [00:00<?, ?it/s]



```python
image
```


![png]({{ site.url }}{{ site.baseurl }}/images/003/output_9_0.png)










    


    



