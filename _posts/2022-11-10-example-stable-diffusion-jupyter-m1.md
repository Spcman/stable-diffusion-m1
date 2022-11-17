---
layout: single
title:  "Stable Diffusion Example within a Jupyter Notebook using Mac A1 Chip"
comments: true
date:   2022-11-10
---

Review the [Setup post here]({{ site.url }}{{ site.baseurl }}/setup-stable-diffusion-jupyter-m1/)

In Jupyter, navigate to the stable-diffusion folder and create a new notebook.  Let's check our Python Version.

{% highlight python %}
import sys
sys.path.append(".")
sys.version
{% endhighlight %}

The output from this cell should be something like this.
{% highlight plaintext %}
3.10.6 (main, Oct 24 2022, 11:04:07) [Clang 12.0.0 ]
{% endhighlight %}

Now let's check our OS.

```python
import platform
platform.platform()
```
The output from this cell should be something like this 
{% highlight plaintext %}
macOS-13.0-arm64-arm-64bit
{% endhighlight %}


Now let's just call the txt2img.py file with a prompt as a test.

```python
%run scripts/txt2img.py --prompt "a red juicy apple floating in outer space, like a planet" --n_samples 1 --n_iter 1 --plms

```
Here is the output.  See bottom of the page for troubleshooting.

```

    NOTE: Redirects are currently not supported in Windows or MacOs.
    Global seed set to 42


    Loading model from models/ldm/stable-diffusion-v1/model.ckpt
    Global Step: 470000
    LatentDiffusion: Running in eps-prediction mode
    DiffusionWrapper has 859.52 M params.
    making attention of type 'vanilla' with 512 in_channels
    Working with z of shape (1, 4, 32, 32) = 4096 dimensions.
    making attention of type 'vanilla' with 512 in_channels


    Some weights of the model checkpoint at openai/clip-vit-large-patch14 were not used when initializing CLIPTextModel: ['vision_model.encoder.layers.8.mlp.fc1.weight', 'vision_model.encoder.layers.23.mlp.fc1.weight', 'vision_model.encoder.layers.5.self_attn.q_proj.weight', 
    
    ---snipped----
    
     'vision_model.encoder.layers.23.self_attn.out_proj.bias', 'vision_model.encoder.layers.14.layer_norm1.bias', 'vision_model.encoder.layers.15.mlp.fc2.weight', 'vision_model.encoder.layers.3.layer_norm2.weight', 'vision_model.encoder.layers.21.layer_norm2.bias']
    - This IS expected if you are initializing CLIPTextModel from the checkpoint of a model trained on another task or with another architecture (e.g. initializing a BertForSequenceClassification model from a BertForPreTraining model).
    - This IS NOT expected if you are initializing CLIPTextModel from the checkpoint of a model that you expect to be exactly identical (initializing a BertForSequenceClassification model from a BertForSequenceClassification model).
    Sampling:   0%|          | 0/1 [00:00<?, ?it/s]
    data:   0%|          | 0/1 [00:00<?, ?it/s][A

    Data shape for PLMS sampling is (1, 4, 64, 64)
    Running PLMS Sampling with 50 timesteps


    
    
    PLMS Sampler:   0%|          | 0/50 [00:00<?, ?it/s][A[A
    
    PLMS Sampler:   2%|▏         | 1/50 [00:08<06:36,  8.10s/it][A[A
    
    PLMS Sampler:   4%|▍         | 2/50 [00:08<03:03,  3.83s/it][A[A
    
    PLMS Sampler:   6%|▌         | 3/50 [00:09<01:53,  2.41s/it][A[A
    
    PLMS Sampler:   8%|▊         | 4/50 [00:10<01:20,  1.75s/it][A[A
    
    PLMS Sampler:  10%|█         | 5/50 [00:11<01:02,  1.39s/it][A[A
    
    PLMS Sampler:  12%|█▏        | 6/50 [00:11<00:51,  1.16s/it][A[A
    
    PLMS Sampler:  14%|█▍        | 7/50 [00:12<00:44,  1.03s/it][A[A
    
    PLMS Sampler:  16%|█▌        | 8/50 [00:13<00:39,  1.06it/s][A[A
    
    PLMS Sampler:  18%|█▊        | 9/50 [00:14<00:36,  1.13it/s][A[A
    
    PLMS Sampler:  20%|██        | 10/50 [00:14<00:33,  1.20it/s][A[A
    
    PLMS Sampler:  22%|██▏       | 11/50 [00:15<00:31,  1.24it/s][A[A
    
    PLMS Sampler:  24%|██▍       | 12/50 [00:16<00:30,  1.26it/s][A[A
    
    PLMS Sampler:  26%|██▌       | 13/50 [00:17<00:28,  1.30it/s][A[A
    
    PLMS Sampler:  28%|██▊       | 14/50 [00:17<00:27,  1.30it/s][A[A
    
    PLMS Sampler:  30%|███       | 15/50 [00:18<00:26,  1.31it/s][A[A
    
    PLMS Sampler:  32%|███▏      | 16/50 [00:19<00:26,  1.31it/s][A[A
    
    PLMS Sampler:  34%|███▍      | 17/50 [00:20<00:25,  1.31it/s][A[A
    
    PLMS Sampler:  36%|███▌      | 18/50 [00:20<00:24,  1.31it/s][A[A
    
    PLMS Sampler:  38%|███▊      | 19/50 [00:21<00:23,  1.31it/s][A[A
    
    PLMS Sampler:  40%|████      | 20/50 [00:22<00:22,  1.34it/s][A[A
    
    PLMS Sampler:  42%|████▏     | 21/50 [00:23<00:21,  1.33it/s][A[A
    
    PLMS Sampler:  44%|████▍     | 22/50 [00:23<00:21,  1.33it/s][A[A
    
    PLMS Sampler:  46%|████▌     | 23/50 [00:24<00:20,  1.33it/s][A[A
    
    PLMS Sampler:  48%|████▊     | 24/50 [00:25<00:19,  1.35it/s][A[A
    
    PLMS Sampler:  50%|█████     | 25/50 [00:26<00:18,  1.34it/s][A[A
    
    PLMS Sampler:  52%|█████▏    | 26/50 [00:26<00:17,  1.34it/s][A[A
    
    PLMS Sampler:  54%|█████▍    | 27/50 [00:27<00:17,  1.33it/s][A[A
    
    PLMS Sampler:  56%|█████▌    | 28/50 [00:28<00:16,  1.35it/s][A[A
    
    PLMS Sampler:  58%|█████▊    | 29/50 [00:29<00:15,  1.37it/s][A[A
    
    PLMS Sampler:  60%|██████    | 30/50 [00:29<00:14,  1.35it/s][A[A
    
    PLMS Sampler:  62%|██████▏   | 31/50 [00:30<00:14,  1.34it/s][A[A
    
    PLMS Sampler:  64%|██████▍   | 32/50 [00:31<00:13,  1.34it/s][A[A
    
    PLMS Sampler:  66%|██████▌   | 33/50 [00:32<00:12,  1.33it/s][A[A
    
    PLMS Sampler:  68%|██████▊   | 34/50 [00:32<00:12,  1.33it/s][A[A
    
    PLMS Sampler:  70%|███████   | 35/50 [00:33<00:11,  1.33it/s][A[A
    
    PLMS Sampler:  72%|███████▏  | 36/50 [00:34<00:10,  1.34it/s][A[A
    
    PLMS Sampler:  74%|███████▍  | 37/50 [00:35<00:09,  1.33it/s][A[A
    
    PLMS Sampler:  76%|███████▌  | 38/50 [00:35<00:09,  1.32it/s][A[A
    
    PLMS Sampler:  78%|███████▊  | 39/50 [00:36<00:08,  1.32it/s][A[A
    
    PLMS Sampler:  80%|████████  | 40/50 [00:37<00:07,  1.32it/s][A[A
    
    PLMS Sampler:  82%|████████▏ | 41/50 [00:38<00:06,  1.32it/s][A[A
    
    PLMS Sampler:  84%|████████▍ | 42/50 [00:38<00:05,  1.34it/s][A[A
    
    PLMS Sampler:  86%|████████▌ | 43/50 [00:39<00:05,  1.34it/s][A[A
    
    PLMS Sampler:  88%|████████▊ | 44/50 [00:40<00:04,  1.33it/s][A[A
    
    PLMS Sampler:  90%|█████████ | 45/50 [00:41<00:03,  1.36it/s][A[A
    
    PLMS Sampler:  92%|█████████▏| 46/50 [00:41<00:02,  1.35it/s][A[A
    
    PLMS Sampler:  94%|█████████▍| 47/50 [00:42<00:02,  1.36it/s][A[A
    
    PLMS Sampler:  96%|█████████▌| 48/50 [00:43<00:01,  1.37it/s][A[A
    
    PLMS Sampler:  98%|█████████▊| 49/50 [00:43<00:00,  1.36it/s][A[A
    
    PLMS Sampler: 100%|██████████| 50/50 [00:44<00:00,  1.12it/s][A[A
    
    data: 100%|██████████| 1/1 [00:49<00:00, 49.09s/it][A
    Sampling: 100%|██████████| 1/1 [00:49<00:00, 49.09s/it]

    Your samples are ready and waiting for you here: 
    outputs/txt2img-samples 
     
    Enjoy.

```
    
Navigate to the outputs folder above and there should be an image file starting grid-000x.png

![Stable Diffusion Test]({{ site.url }}{{ site.baseurl }}/images/002/grid-0008.png)

## Troubleshooting


<ul>
  <li>Read the errors provided and install/update missing librabries</li>
  <li>Google or the error</li>
  <li>Compare output from the first two cells above, how does your Python and OS compare? You may need to update your OS or Python?</li>
</ul>
