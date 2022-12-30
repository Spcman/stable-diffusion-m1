---
layout: single
title:  "Stable Diffusion Automatic 1111 and Deforum with Mac A1 Apple Silicon"
comments: true
date:   2022-12-23
---

Automatic 1111 is a game changer for me.   It’s a web interface is run locally (without Colab) that let’s you interact with Stable diffusion with no programming knowledge.  As a user you have a myriad of controls and there is a Deforum extension that you can add in really easily.
 
As a side note, I was hoping my own efforts with Python and Jupyter would lead me to start producing my own animations like those possible with [Deforums’s amazing Colab notebook](https://colab.research.google.com/github/deforum/stable-diffusion/blob/main/Deforum_Stable_Diffusion.ipynb).  I tried once or twice to convert the Deforum notebook to work on the Mac but kept getting errors relating to cuda and the general lack of support for Apple Silicon. The deeper I got also made me realize how clever Deforum’s notebook actually is.

When I stumbled on Automatic 1111 I didn’t expect there to be a Apple Mac version but [here it is](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Installation-on-Apple-Silicon).  To install it follow the instructions contained in the link. I found it quite easy to install.  The only issue I had came when I copied my checkpoint models to the models folder.  At the time of writing Automatic 1111 did not support the new stable diffusion 2 models.  After deleting the Stable Diffusion 2 models my problems went away.

Adding the [Deforum extension](https://github.com/deforum-art/deforum-for-automatic1111-webui) was also really easy.  This [excellent deforum documentation](https://dreamingcomputers.com/deforum-stable-diffusion/deforum-stable-diffusion-settings/) will help you get started with the controls and levers within the Deforum add-in.


Now I’m up and running I’m going to spend a while playing with this.  Here are my first projects.

<iframe width="604" height="1074" src="https://www.youtube.com/embed/Lln2AhtvbjQ" title="Taylor Swift Anti-hero AI Animation" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<iframe width="604" height="1074" src="https://www.youtube.com/embed/swRHw_WOn3I" title="Blace Lace Bat AI Animation" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>









