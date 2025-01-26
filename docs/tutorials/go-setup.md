# Setting up a dev container for Go

* Primary author: [Jonathan Jacob](https://github.com/hashunc)
* Reviewer: [Jacob Gogel](https://gitgub.com/jacobala1)

## Step 0: Prerequisites

* VSCode: [install](https://code.visualstudio.com/) 
    * with the Dev Containers Extension: [install](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
* Docker Desktop: [install](https://www.docker.com/products/docker-desktop)
* git: [install](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Step 1: Make a Repository

1. Open your terminal or command prompt

2. Navigate to the directory you wish to house your project

3. Make a new directory for your project and open it
!!! Note
    Remember: if your directory name has spaces, put the name in quotations so that your machine knows to parse it as one argument!
```
mkdir helloGo
cd helloGo
```
4. Initialize a git repository with a README file

```
git init
echo "# Hello COMP423 in a dev container for Go" > README.md
git add .
git commit -m "Initial commit adding README"
```

## Step 2: Setting up the Dev Container

A dev container standardizes the environment for development and facilitates management of software dependencies.

1. Open the helloGo directory in VSCode using File > Open Folder
2. Make a .devcontainer folder in the project folder
3. Make a new file inside of .devcontainer named devcontainer.json
4. Fill out your dev container configuration inside devcontainer.json
```json
{
    "name": "Hello COMP423 in a dev container for Go",
    "image": "mcr.microsoft.com/devcontainers/python:latest",
    "customizations": {
        "vscode": {
            "settings": {},
            "extensions": ["ms-python.python","golang.go"]
        }
    },
    "postCreateCommand": "pip install -r requirements.txt"
}
```
    * name: Informative name for dev container
    * image: Docker image (for this project, latest Python environment from Microsoft)
    * customizations: VSCode configuration, including marketplace extensions using their string identifiers
    * postCreateCommand: Command that runs post-container creation (for us, installing the requirements listed in the next step using pip)
5. Make a file named requirements.txt in your project's root directory with the Python dependencies needed for the project. In this case, we only need mkdocs-material, which we can add by inserting the text below into requirements.txt
```
mkdocs-material~=9.5
```
6. Open Docker Desktop
7. From the VSCode window with the project open, press Control/Command + Shift + P, then select "Dev Containers: Reopen in Container." In a few minutes, the window should reopen as a dev container. Close the terminal window by pressing any key or using the trash can icon.

## Step 3: Preparing Go



## Step 4: Saying Hello in Go

