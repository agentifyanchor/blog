---
title: "Getting Started with UV in Docker"
description: ""
date: 2025-01-12T17:48:01.084Z
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

To conclude this series on using UV for developing Python projects within a portable environment using containers, we will create a sample project and experiment with UV.

In our scenario, we will keep it simple. Our requirement is as follows:
A store needs an API to return a list of products and filter these products by availability.

To get started, we need to set up our project and install the necessary dependencies. We will use FastAPI to create our API and Ruff as a linter to ensure code quality. Follow the steps below to initialize the project, install dependencies, and run the application.

### Steps to Follow:
1. Create the project.
2. Install dependencies (FastAPI & uvicorn ).
3. Install the linter (Ruff).
4. Run the application.
5. Explore the project structure and files.

### Create the Project

Run the command to initialize the project:

```sh
uv init Store_api
```

![Project Initialization](/images/post3/image.png)

### Explore the Project Structure
UV will create a project folder for us. It will generate the `.gitignore` file to manage which files or folders will be included or excluded from being pushed to our repository, `.Python-version` which mentions the global version of Python used, a hello world Python script, but the most important file here is `pyproject.toml`, which defines the project's behavior and definition.
![Project Structure](/images/post3/image-1.png)
### `pyproject.toml`

```toml
[project]
name = "store-api"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []
```

The `pyproject.toml` file specifies the required Python version for the project and lists the dependencies. Currently, the dependencies list is empty.

### Add Dependencies (FastAPI & uvicorn)

As mentioned, we need FastAPI to create our API. To install the packages, navigate to the root project folder and run the following command:

```sh
uv add fastapi uvicorn
```
![Installing FastAPI](/images/post3/image-2.png)
![Installing FastAPI](/images/post3/image-3.png)
As you can see, it was so fast.

To quickly test the application, simply replace the content of hello.py with the following:

```Python
from fastapi import FastAPI
from typing import List, Optional
from pydantic import BaseModel
import uvicorn

# Pydantic model for product response
class ProductResponse(BaseModel):
    id: int
    name: str
    available: bool

# Product class for internal data representation
class Product:
    def __init__(self, id: int, name: str, available: bool):
        self.id = id
        self.name = name
        self.available = available

# Sample products
products = [
    Product(1, "Jolly Jester Clown Wig", True),
    Product(2, "Bozo the Clown Nose", False),
    Product(3, "Circus Performer Clown Shoes", True),
    Product(4, "Red Balloon Animal Kit", True),
    Product(5, "Funny Clown Face Paint Set", True),
    Product(6, "Mini Clown Horn", False),
    Product(7, "Rainbow Clown Costume", True),
    Product(8, "Clown Magician Hat", True),
    Product(9, "Giggles the Clown Plush Doll", True),
    Product(10, "Clown Comedy Seltzer Bottle", False)
]

# FastAPI app initialization
app = FastAPI()

@app.get("/products", response_model=List[ProductResponse])
def get_products(available: Optional[bool] = None):
    # If 'available' query param is provided, filter products by availability
    filtered_products = products if available is None else [product for product in products if product.available == available]
    
    # Return products as list of Pydantic model instances
    return [ProductResponse(**product.__dict__) for product in filtered_products]

@app.get("/")
def main():
    return {"message": "Hello from store-api!"}

if __name__ == "__main__":
   uvicorn.run(app, host="0.0.0.0", port=8000)
   #main() # to run using command line `uv run uvicorn hello:app --port 8000`

```
### Installing and Using Tool (Ruff)
Every project needs some tooling like Ruff for linting. We can manage that by adding the tool as a dev dependency using `uv add --dev ruff` or just use `uvx`.
![Installing Ruff](/images/post3/image-4.png)

### Run the Application
To run the application, just use:
```sh
uv run hello.py
```
Click on the "Open in Browser" button from the popup. We don't need to make any additional configuration for port forwarding.
![Running Application](/images/post3/image-5.png)
![Running Application](/images/post3/image-6.png)

![Running Application](/images/post3/image-7.png)

UV also creates and manages the `.venv` folder for us.
![Running Application](/images/post3/image-8.png)

### upgrade / downgrade Python in a project
To upgrade or downgrade the Python version, simply update the version in the `pyproject.toml` file and run 
```sh
uv sync
```
If you remember, we configured our initial environment to use Python 3.12, but we can use any version in our project. We don't need to manage installation or set up multiple Python versions — UV does the job for us.

![alt text](/images/post3/image15.png)



In this post, we have successfully set up a Python project using UV, ensuring that we can go live with our container and start our productive approach with Dev Containers.

You can find the complete source code for this demo on [GitHub](https://github.com/agentifyanchor/uv_docker_lab01). If you’re a fan of Dockerfiles and prefer to manage your development environment manually, refer to this [project](https://github.com/agentifyanchor/uv_docker_lab02), which uses the official UV Dockerfile definition. 

Cheers! 🍻
