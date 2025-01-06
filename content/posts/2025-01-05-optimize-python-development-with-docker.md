---
title: Optimize Python Development with VsCode and Docker
description: ""
date: 2025-01-05T22:47:31.510Z
preview: ""
draft: false
tags: []
categories: []
---

In today's world, Python is used for many purposes in large projects, especially in AI, LLM, and RAG. However, maintaining a healthy environment, managing compatibility, and handling packaging can be challenging tasks.

For this reason, using containers not only for deploying Python apps but also as a development environment could be a suitable approach.

In this post, I will show you how simple it is to start developing Python projects without needing to install Python and manage multiple versions, create virtual environments, set environment variables, and handle other prerequisites.

We can achieve this directly from VSCode using just one extension.

### Presenting the Extension
You’ve probably encountered the `.devcontainer` folder and the `devcontainer.json` file in other projects. But what do they do?

The `.devcontainer` folder and its JSON file are used to define a containerized development environment. This setup ensures that all developers on a project have a consistent development environment, regardless of their local machine configurations. The .devcontainer configuration can specify the base image, extensions, and settings needed for the project.

We’re going to make this easy by generating the configuration files automatically—no need to craft them manually from scratch!😉

So let's start...

### Prerequisites
Before we dive in, make sure you have [Docker](https://docs.docker.com/get-docker/) and [VSCode](https://code.visualstudio.com/download) installed.

### Step 1: Installing the Extension
First, install the necessary extension in VSCode. You can do this by visiting the [Dev Container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) page or by searching for it directly in the extension manager in Visual Studio Code. You can use the `Ctrl+Shift+X` Shortcut.

![](/images/post1/im1.png)


### Step 2: Generate the Devcontainer Folder
After installing the extension, you should find an icon at the bottom left side of your IDE. Click on it and follow the wizard steps to generate the `.devcontainer` folder and configuration files.

![](/images/post1/im2.png)

Select `Add Dev Container Configuration Files`.

![](/images/post1/im3.png)

Select `Add Configuration to Workspace`. This will add the `.devcontainer` folder and the related configuration under your current work directory.

![](/images/post1/im4.png)

You can choose from a variety of preset configurations. In our case, we will choose `Python 3`.

![](/images/post1/im5.png)

In the next step, we can choose a desired version of `Python`. You can choose any version you are comfortable with.

![](/images/post1/im6.png)

In the next step, we can choose some `features`. We will select [`uv`](https://docs.astral.sh/uv/), a great package and project manager, which we will use further in this post.

![](/images/post1/im7.png)

We can select additional configuration for the features, so we will select the shell autocompletion option.

![](/images/post1/im8.png)
![](/images/post1/im9.png)

{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
You can skip the next step if you don't want to use the `Dependabot` functionality. Dependabot helps you keep your dependencies up to date by automatically checking for updates and creating pull requests.
{{< /alert >}} 

![](/images/post1/im10.png)

After running the wizard, you’ll end up with the following root project structure.

![](/images/post1/im13.png)


Once the `.devcontainer` folder is set up, there’s no need to build an image manually—the extension will handle that for you! You’re now ready to connect to the containerized environment and start using it as your development environment. We’ll explore this process in Part 2 of this post, so stay tuned!

### Final Thoughts

Congratulations on setting up your containerized Python development environment with VSCode and Docker! By using Deb Container extension, you've made your development setup consistent and portable. Now you can focus on your projects without worrying about managing environments and dependencies. Happy coding, and see you in the next part!


