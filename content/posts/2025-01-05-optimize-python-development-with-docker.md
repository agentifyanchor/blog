---
title: Optimize Python Development with VSCode and Docker
description: ""
date: 2025-01-05T22:47:31.510Z
preview: ""
draft: false
tags: 
    - Python
    - Docker
    - VSCode
categories: []
---

In today's world, Python is used for many purposes in large projects, especially in AI, LLM, and RAG. However, maintaining a healthy environment, managing compatibility, and handling packaging can be challenging tasks.

For this reason, using containers not only for deploying Python apps but also as a development environment could be a suitable approach.

In this post, we will show how simple it is to start developing Python projects without needing to install Python, manage multiple versions, create virtual environments, set environment variables, and handle other prerequisites.

We can achieve this directly from VSCode using just one extension.

### Presenting the Extension
We’ve probably all seen the `.devcontainer` folder and the `devcontainer.json` file in other projects. But what do they do?

The `.devcontainer` folder and its JSON file are used to define a containerized development environment. This setup ensures that all developers on a project have a consistent development environment, regardless of their local machine configurations. The `.devcontainer` configuration can specify the base image, extensions, and settings needed for the project.

We’re going to make this easy by generating the configuration files automatically—no need to craft them manually from scratch! 😉

So let's get started...

### Prerequisites
Before we dive in, make sure we have [Docker](https://docs.docker.com/get-docker/) and [VSCode](https://code.visualstudio.com/download) installed.

### Step 1: Installing the Extension
First, let’s install the necessary extension in VSCode. We can do this by visiting the [Dev Container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) page or by searching for it directly in the extension manager in Visual Studio Code. Use the `Ctrl+Shift+X` shortcut to open the extension manager.

![](/images/post1/im1.png)

### Step 2: Generate the DevContainer Folder
After installing the extension, we should find an icon at the bottom left side of our IDE. Click on it and follow the wizard steps to generate the `.devcontainer` folder and configuration files.

![](/images/post1/im2.png)

Select **Add Dev Container Configuration Files**.

![](/images/post1/im3.png)

Then select **Add Configuration to Workspace**. This will add the `.devcontainer` folder and related configuration to our current project directory.

![](/images/post1/im4.png)

We can choose from a variety of preset configurations. In our case, we will select **Python 3**.

![](/images/post1/im5.png)

We’ll be prompted to choose the Python version for your container. Pick any version you’re comfortable with (we’ll go with `Python 3.12 bullseye`).

![](/images/post1/im6.png)

In the following step, we can choose additional **features**. We’ll select [`uv`](https://docs.astral.sh/uv/), a great package and project manager that we’ll use further in this post.

![](/images/post1/im7.png)

We can also select additional configurations for the features, so let’s enable the shell autocompletion option.

![](/images/post1/im8.png)
![](/images/post1/im9.png)

{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
We can skip the next step if we don't want to use the `Dependabot` functionality. Dependabot helps us keep our dependencies up to date by automatically checking for updates and creating pull requests.
{{< /alert >}}

![](/images/post1/im10.png)

After running the wizard, we’ll end up with the following root project structure.

![](/images/post1/im13.png)

🎉 Once the `.devcontainer` folder is set up, there’s no need to build an image manually—the extension will handle that for us! We’re now ready to connect to the containerized environment and start using it as our development environment. We’ll explore this process in Part 2 of this post, so stay tuned!

Happy coding, and see you in the [`next part`](/posts/2025-01-08-streamline-python-development-in-devcontainer-with-uv/)!
