---
layout: single
title:  "Creating a video from multiple png files using ffmpeg"
comments: true
date:   2022-11-20
---

To make videos we're going to use the `ffmpeg` command line tool.  This is installed as an OS executable and isn't part of Python as such.

We'll need ffmpeg installed correctly. If not installed already you can use `brew install ffmpeg` to get it.  You can also use `brew update && brew upgrade` to update it. This does take a little while to download and install.

For our test I'm going to use the images created in the last post.

```python
!ls outputs/vampire01
```

    img_00000.png img_00009.png img_00018.png img_00027.png img_00036.png
    img_00001.png img_00010.png img_00019.png img_00028.png img_00037.png
    img_00002.png img_00011.png img_00020.png img_00029.png img_00038.png
    img_00003.png img_00012.png img_00021.png img_00030.png img_00039.png
    img_00004.png img_00013.png img_00022.png img_00031.png img_00040.png
    img_00005.png img_00014.png img_00023.png img_00032.png img_00041.png
    img_00006.png img_00015.png img_00024.png img_00033.png img_00042.png
    img_00007.png img_00016.png img_00025.png img_00034.png img_00043.png
    img_00008.png img_00017.png img_00026.png img_00035.png img_00044.png



```python
abs_path='/opt/homebrew/bin/'
max_frames=1000
fps = 12
image_path = "outputs/vampire01/img_%05d.png"   #note: this includes a regular expression to define the sequencing as xxx (3 digits).
mp4_path = "video/vampire.mp4"
```


```python
cmd = [
    abs_path+'ffmpeg',
    '-y',
    '-vcodec', 'png',
    '-r', str(fps),
    '-start_number', str(0),
    '-i', image_path,
    '-frames:v', str(max_frames),
    '-c:v', 'libx264',
    '-vf',
    f'fps={fps}',
    '-pix_fmt', 'yuv420p',
    '-crf', '17',
    '-preset', 'veryfast',
    '-pattern_type', 'sequence',
    mp4_path
    ]

print(' '.join(cmd))
```

    /opt/homebrew/bin/ffmpeg -y -vcodec png -r 12 -start_number 0 -i outputs/vampire01/img_%05d.png -frames:v 1000 -c:v libx264 -vf fps=12 -pix_fmt yuv420p -crf 17 -preset veryfast -pattern_type sequence video/vampire.mp4


We could run the command above in our OS shell.

**Note:** we have used the absolute path to run the ffmpeg executable to avoid ffmpeg not found errors.  This isn't required if running the ffmpeg from a shell.

## ffmpeg parameters explained

Let's check the ffmpeg command line we're about to run on the OS. `ffmpeg` parameters used


- -y **Overwrite output files without asking**

- -vcodec 'png'

- -r str(fps) **Frame rate**

- -start_number 0 **Start at sequence number 0**

- -i image_path **input which will include a squencer with a regular expression**

- -frames:v **Stops writing frames after set value**

- -c:v, libx264' **encodes all video streams with libx264**

- -vf **Create the filtergraph specified by filtergraph and use it to filter the stream.**

- fps **Not sure ... as we have -r will come back to this**

- -pix_fmt, yuv420p **pixel format**

- -crf 17 **Not sure ??? will come back to this**

- -preset veryfast

- -pattern_type sequence

- mp4_path  **The name of the output movie file to create** 

[Click here for more documentation on ffmpeg](https://ffmpeg.org/ffmpeg.html)


```python
import subprocess
```


```python
process = subprocess.Popen(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
stdout, stderr = process.communicate()
if process.returncode != 0:
    print(stderr)
    raise RuntimeError(stderr)
else:
    print('Video '+mp4_path+' rendered')
```

    Video video/vampire.mp4 rendered

{% include video id="-xtmSAvpopek" provider="youtube" %}

{% include video id="xtmSAvpopek" provider="youtube" %}


