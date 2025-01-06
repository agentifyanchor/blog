---
title: Optimize Python Development with VSCode and Docker
description: "Streamline your Python development with VSCode, Docker, and DevContainers."
date: 2025-01-05T22:47:31.510Z
preview: ""
draft: false
tags: []
categories: []
---

# Optimize Python Development with VSCode and Docker

In today’s world, Python is the go-to language for a variety of projects, from Artificial Intelligence (AI) to Large Language Models (LLM) and Retrieval-Augmented Generation (RAG). But let’s face it—managing Python environments, dealing with compatibility issues, and juggling virtual environments can be a real headache.

That’s where containers come in handy. They’re not just for deploying Python apps; they’re a fantastic solution for creating a smooth, consistent development environment. No more installing Python versions, setting up virtual environments, or dealing with environment variables manually. 

With Docker and VSCode, you can do all this effortlessly. And the best part? We’ll use **just one extension** to get everything set up.

### Presenting the VSCode Extension

You’ve probably encountered the `.devcontainer` folder and the `devcontainer.json` file in other projects. But what do they do?

The `.devcontainer` folder and its configuration file define a containerized development environment. This ensures that every developer on the project has the same environment, regardless of their local setup. Inside the `.devcontainer` configuration, you can specify the base image, extensions, and other settings your project needs. 

We’re going to make this easy by generating the configuration files automatically—no need to craft them manually from scratch!

### Prerequisites

Before we dive in, make sure you have [Docker](https://docs.docker.com/get-docker/) and [VSCode](https://code.visualstudio.com/download) installed. These are the tools we’ll be using for this tutorial.

### Step 1: Installing the Extension

First, let’s get the necessary VSCode extension: the **Dev Containers extension**.

- Install it from the [VSCode marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

Once installed, you should see an icon in the bottom left corner of your VSCode window. Click on it and let the wizard guide you through the process of setting up the `.devcontainer` folder and all the required configuration files.

![](/images/post1/im1.png)

### Step 2: Generating the DevContainer Folder

After installing the extension, you’ll find an icon in the bottom left corner of VSCode. Click on it and follow the wizard to generate the `.devcontainer` folder and configuration files.

![](/images/post1/im2.png)

Choose the option **Add Dev Container Configuration Files**.

![](/images/post1/im3.png)

Next, choose **Add Configuration to Workspace**. This will add the `.devcontainer` folder with the related configuration files directly to your current project directory.

![](/images/post1/im4.png)

Now, you’ll have the option to choose from a list of preset configurations. Since we’re focusing on Python, select **Python 3**.

![](/images/post1/im5.png)

You’ll be prompted to choose the Python version for your container. Pick any version you’re comfortable with (we’ll go with Python 3.x).

![](/images/post1/im6.png)

In the next step, you can add extra features. For this post, let’s add **[uv](https://docs.astral.sh/uv/)**, a project manager and package manager that we’ll use in our development setup.

![](/images/post1/im7.png)

We can also enable additional features like **shell autocompletion** for even better usability.

![](/images/post1/im8.png)

Skip the **Dependabot** step unless you want to keep your dependencies automatically up to date. It's a handy feature but not strictly necessary for now.

{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
**Dependabot** helps you automatically update your project dependencies by checking for updates and creating pull requests.
{{< /alert >}}

![](/images/post1/im9.png)

![](/images/post1/im10.png)

![](/images/post1/im11.png)

![](/images/post1/im12.png)

![](/images/post1/im13.png)

### Step 3: Running the DevContainer

Once the `.devcontainer` folder is set up, there's no need to build an image manually—the extension will handle that for you! Now, you’re ready to connect to the containerized environment and start using it as your development environment.

---

### Let's Create Some Projects

Now that we have our DevContainer set up, let’s dive into creating a couple of simple projects. For simplicity, we’ll create two basic apps—`Project1` and `Project2`—that just display a simple message.

In VSCode, you can create these projects within your containerized environment:

![](/images/post1/Pasted%20image%2020250103125030.png)

Here’s how the code for `Project1` and `Project2` might look:

1. **Project1**
   - Display: "Welcome to Project 1"

![](/images/post1/Pasted%20image%2020250103130214.png)

2. **Project2**
   - Display: "Welcome to Project 2"

![](/images/post1/Pasted%20image%2020250103130346.png)

It’s that easy! You can now work on multiple projects, all within the same containerized environment.

### Final Thoughts

Congratulations! You’ve just set up a fully containerized Python development environment using VSCode and Docker. The `.devcontainer` folder and its configuration files make it easy to replicate this environment on other machines or share it with teammates. Now, you can focus on building Python applications without worrying about managing dependencies or configurations. 

Ready to take your development to the next level? Stay tuned for future posts where we’ll dive deeper into containerized Python development!
