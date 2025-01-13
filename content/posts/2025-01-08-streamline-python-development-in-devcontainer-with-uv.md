---
title: Streamline Python Development in DevContainer with UV
description: ""
date: 2025-01-08T01:28:12.670Z
preview: ""
draft: false
tags:
  - Python
  - DevContainer
  - VSCode
  - Docker
  - WSL
  - Podman
  - DevOps
categories: []
types: ""
---

In our series exploring how to set up a streamlined and organized way to start your Python development journey using the **DevContainer VSCode extension** and **Docker** (or WSL/Podman), we've already seen how simple it is to define our development environment using just the DevContainer extension. Now, we're ready to move on to the next part of the series: [Optimize Python Development with VSCode and Docker](/blog/posts/2025-01-05-optimize-python-development-with-docker/).

### Running Our Environment for the First Time

In this post, we will run our development environment for the first time and start working with Python using an amazing package and project manager, **`uv`**.

After generating the definition for our environment, we now have a **devcontainer.json** file structure. Let’s dig in to explore what we have in this setup:

![DevContainer Structure](/images/post2/im12.png)

### Breaking Down the devcontainer.json Structure

1. **Image Section**:  
   This section specifies the **container image** reference, which is hosted on the **Microsoft Container Registry**.  
   **Note**: You can also use a **local image** if you prefer. use DockerFile or Docker compose file.

2. **Features Section**:  
   Think of this section as a way to **enhance the environment** with additional tools and packages. In our case, we’re using `uv` (with shellautocompletion option enbaled).

2. **customization Section**: 
   The **`customization`** section is used to fine-tune the container development environment. It allows us to install additional extensions that will only be loaded inside the container, apply specific settings related to VSCode preferences, and execute additional commands.

{{< alert "circle-info" >}}
For more information on available features, visit the [Dev Containers Features Documentation](https://containers.dev/features).
{{< /alert >}}

### 
> If you're working with a rootless container, you can find relevant information.
> [here](https://aka.ms/dev-containers-non-root).



### Launching Our Environment for the First Time 🚀

Now it's time to launch our environment for the first time! To do this, simply click on the **Dev Container** icon and choose **Reopen in Container**.

![Reopen in Container](/images/post2/im14.png)

In the background:
- An image will be added to your Docker images list.
![](/images/post2/im29.png)
- A container should be running.
![](/images/post2/im24.png)
- A volume will be created.
![](/images/post2/im25.png)
- VSCode will reload, but this time, it will run **under the container**.
![Container Information](/images/post2/im32.png)


### Time to Verify

The **Remote Indicator** in the status bar will display additional information, such as the name of the container we're currently in and the distribution of the image being used.


![Container Information](/images/post2/im16.png)

### Verifying Python Version and Testing `uv`

Let’s perform a couple more checks by verifying the Python version being used and testing if `uv` is running correctly.

![Python Version Check](/images/post2/im31.png)  
![Testing `uv`](/images/post2/im30.png)

Everything seems good so far! The next step is to create our first project and run it. That’s exactly what we’ll cover in the [**next post**](https://agentifyanchor.github.io/blog/posts/2025-01-12-getting-started-with-uv-in-docker-step-3-explained/). 

**Stay tuned!** 





  