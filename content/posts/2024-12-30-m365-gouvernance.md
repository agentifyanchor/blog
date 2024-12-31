---
title: M365 gouvernance
description: "A guide on how to set up Hugo and create your first project."
date: 2024-12-31T02:53:45.721Z
preview: ""
draft: false
tags: ["Hugo", "Static Site Generator", "Tutorial"]
categories: ["Web Development", "Static Sites"]
---

## Introduction

Hugo is a fast and flexible static site generator written in Go. This guide will walk you through the steps to set up Hugo and create your first project.

## Prerequisites

Before you begin, ensure you have the following installed on your system:
- [Go](https://golang.org/dl/)
- [Git](https://git-scm.com/)

## Step 1: Install Hugo

To install Hugo, run the following command:

```bash
brew install hugo
```

Alternatively, you can download the appropriate version for your operating system from the [Hugo releases page](https://github.com/gohugoio/hugo/releases).

## Step 2: Create a New Site

Once Hugo is installed, you can create a new site by running:

```bash
hugo new site my-first-site
```

This command will create a new directory called `my-first-site` with the necessary folder structure.

## Step 3: Add a Theme

Navigate to your new site directory and add a theme. For example, to add the Ananke theme, run:

```bash
cd my-first-site
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
```

## Step 4: Create Your First Post

You can now create your first post using the following command:

```bash
hugo new posts/my-first-post.md
```

This will create a new Markdown file in the `content/posts` directory.

## Step 5: Start the Hugo Server

To see your site in action, start the Hugo server:

```bash
hugo server
```

Open your browser and navigate to `http://localhost:1313` to view your new site.

## Conclusion

Congratulations! You have successfully set up Hugo and created your first project. You can now start customizing your site and adding more content.
