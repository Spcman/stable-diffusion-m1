---
layout: single
title:  "Stable Diffusion Diffusers Toolbox 01 (NSFW, Image Size and Generating Mutiple Images)"
comments: true
date:   2022-11-20
---

Let's look at a few esential tools that will come in handy later.

```python
from diffusers import StableDiffusionPipeline
DEVICE='mps'
pipe = StableDiffusionPipeline.from_pretrained("stable-diffusion-v1-5", use_auth_token=True).to(DEVICE)
```

# Not Safe for Work Flag (NSFW)

At your own discression you can turn off the NSFW checker.  This will prevent any NSFW messages but may introduce images that possibly have mature content. 

```python
pipe.safety_checker = lambda images, clip_input: (images, False)
```

# Output Image Size (Resolution)

As the plan to eventually produce AI generated TikTok videos, let's experiment with getting a quality portrait image up to 1080 x 1920 resolution. If we use an 3x upscaler (discussed later) the output from stable diffusion should be ...


```python
1080/3, 1920/3
```

    (360.0, 640.0)

Note `height` and `width` have to be divisible by 8.  We're good with the values above.

Let's set a height and width image dimensions and try out an example.

```python
image = pipe("realistic photo of woman vampire, wide mouth showing fangs, moody, foggy, gloomy", height=640, width=360).images[0]
image
```

      0%|          | 0/51 [00:00<?, ?it/s]

![png]({{ site.url }}{{ site.baseurl }}/images/004/output_9_1.png)


# Upscaling Images

I will come back to this problem. I tried to install a potential library called `super-image` but had package version conflicting dependencies.  For now I have a good Mac App that let's me upscale images in batch and why re-invent the wheel?  The App I use FYI is called [Super Photo Upscaler](https://apps.apple.com/au/app/super-photo-upscaler-waifu2x/id450451849?mt=12).


# Generating and Saving Multiple Images in loop.

As you're probably aware already, sometimes you have to generate mutliple images to get a few really good ones.

Working on the same prompt as above, let's get our Apple Silicon working and generating mutiple images in our 'outputs' folder.

Note: I'm aware you can also do this by passing in multiple prompts to the pipeline, but let's play with that later.


```python
num_images=50
prefix='img_'
out_path='outputs/'
for i in range(num_images):
    image = pipe("realistic photo of woman vampire, wide mouth showing fangs, moody, foggy, gloomy", height=640, width=360).images[0]
    filename=prefix+str(i).zfill(5)+'.png'
    image.save(out_path+filename)
```


      0%|          | 0/51 [00:00<?, ?it/s]



      0%|          | 0/51 [00:00<?, ?it/s]



      0%|          | 0/51 [00:00<?, ?it/s]



   [Snipped]


      0%|          | 0/51 [00:00<?, ?it/s]



      0%|          | 0/51 [00:00<?, ?it/s]



      0%|          | 0/51 [00:00<?, ?it/s]


This will generate 50 images in out ouputs folder. [Let's use these to create a video]({{ site.url }}{{ site.baseurl }}/stable-diffusion-m1/stable-diffusion-local-jupyter-ffmpeg/).
