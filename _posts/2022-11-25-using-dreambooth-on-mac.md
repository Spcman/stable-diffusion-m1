---
layout: single
title:  "Using DreamBooth on a Mac"
comments: true
date:   2022-11-25
---
With DreamBooth you can fine-tune and add your own images into the AI art’s learning model.  Unoriginally I thought I would experiment by feeding it images of me! Feeding it only 15 pictures I was still blown away.

Note, I tried to get this running locally on my Mac but ended up using Google’s CoLab for this experiment.  I saved the newly fine-tuned model to my Google Drive.  I might use the model I generated again one day for more local experiments on the Mac.

Google’s free Collaboratory (colab) is sufficiently powerful enough for this task.  Having Google Drive (gdrive) setup is also handy so you can permanently save the new check-point model generated. The only other prerequisite is having a HuggingFace access token but this is free also https://huggingface.co/

The [DreamBooth colab notebook I used is here](https://colab.research.google.com/github/ShivamShrirao/diffusers/blob/main/examples/dreambooth/DreamBooth_Stable_Diffusion.ipynb)

I’m not going to do a full tutorial as you’ll find good ones quite easily by searching for DreamBooth on Google or YouTube.  You don’t need programming skills as such and can use the checkpoint model you create in [DiffusionBee](https://diffusionbee.com/) for fast results without any programming skills.  

Here are the code blocks I updated (as per the instructions on the notebook).


## Login to HuggingFace

`HUGGINGFACE_TOKEN: xxxxx` (paste your own token from hugging face after generating)

## Settings and Run

`save_to_gdrive = True (checked)`

`OUTPUT_DIR stable_diffusion_weights/nigeladams`

This is the output directory on gdrive where the check-point model will be saved.  Once you have the model you can download it and use in other experiments or programs like DiffusionBee to generate the AI art.

## Start Training

concepts_list = [
    {
        "instance_prompt":      "photo of nigel adams spcman",
        "class_prompt":         "photo of a man",
        "instance_data_dir":    "/content/data/nigeladams",
        "class_data_dir":       "/content/data/man"
    },

Obviously remember the instance prompt as that will trigger your image in the AI art generator.

When you get to the Upload your images cell, refresh the files list and drag and drop your training images as per below.

![gif]({{ site.url }}{{ site.baseurl }}/images/005/ezgif.com-gif-maker.gif)

## Run for Generating images.

`--save_sample_prompt="photo of nigel adams spcman" \`

Run the rest the without changing the code/defaults.

## After running the cells

At the end of the process navigate to the OUTPUT_DIR in your gdrive and find your checkpoint model.  This will be approximately 2 GB or more.

Pictures Generated in DiffusionBee (with custom model) with the prompt: picture of nigel adams spcman as neo from the movie matrix, green digital background, badass

![png]({{ site.url }}{{ site.baseurl }}/images/005/nigel_adams_brisbane.png)

