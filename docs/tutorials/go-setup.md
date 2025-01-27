# Setting up a dev container for Go

* Primary author: [Jonathan Jacob](https://github.com/hashunc)
* Reviewer: [Jacob Gogel](https://gitgub.com/jacobala1)

### Steps 0-2 are adapted from COMP 423's [mkdocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-1-initialize-mkdocs).

## Step 0: Prerequisites
<!-- Just adding a brief explanation on what Docker will do-->
* VSCode: [install](https://code.visualstudio.com/) 
    * with the Dev Containers Extension: [install](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
* Docker Desktop: Needed to configure and run the container [install](https://www.docker.com/products/docker-desktop) 
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
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
        "vscode": {
            "settings": {},
            "extensions": ["ms-python.python","golang.go"]
        }
    },
    "postCreateCommand": "go version"
}
```
    * name: Informative name for dev container
    * image: Docker image (for this project, latest Go environment from Microsoft)
    * customizations: VSCode configuration, including marketplace extensions using their string identifiers
    * postCreateCommand: Command that runs post-container creation (for us, checking the version of Go)

5. Open Docker Desktop

6. From the VSCode window with the project open, press Control/Command + Shift + P, then select "Dev Containers: Reopen in Container." In a few minutes, the window should reopen as a dev container.

### Steps 3 and 4 are adapted from [the official Go documentation](https://go.dev/doc/tutorial/getting-started)

## Step 3: Preparing Go

1. Check the version of Go you have installed. Our dev container configuration automatically runs "go version" after creation, so it will show in our current terminal.

2. Close the terminal window by pressing any key or using the trash can icon. Open a new terminal window.

3. Make a directory to say hello in and navigate inside with the code below
```
mkdir hello
cd hello
```
4. Use "go mod" to enable dependency tracking. When writing code in Go, you will usually need to import packages. This command initializes a file to keep track of the packages your project depends on.
!!! Citation
    Taken directly from the official Go tutorial
```
go mod init example/hello
go: creating new go.mod: module example/hello
```
5. Click the "hello" folder in VSCode, then click "New File" to make a file named hello.go. Our code will go in this file.

## Step 4: Saying Hello in Go

Let's start writing code! In hello.go, insert the following code:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

This code does the following things:

1. Declare a "main" package (groups the files in this directory into one package of functions)
2. Import the fmt package, which contains the Println() function we use later and other functions for formatting text
3. Name a main() function that uses Println() to print our message to the console. The main() function runs automatically when we run the main package.

Now we are ready to go back to the console, compile, and run our code. First, we will do these steps separately. Go code is compiled using the build subcommand:

```
go build
```

This creates a binary file with the same name "hello" as the package we are building. It is comparable to the gcc command which compiles C code into an executable file. In our case, we are using a Linux system. This means we can run our file using this command in the console:
```
./hello
```
Compiling and running in separate steps is a good idea for real world use, because the executable file can be neatly exported and run. However, when we are testing and developing code, we do not need to spend storage creating an executable file. Instead, we can use this command to compile and run all at once:
!!!Note
    In this case, we are running a single known package that we pattern match using the ".", but in other situations you can also provide a file path, import path, or a list of .go source files
```
go run .
```
If everything works correctly, you should see your message in the console. Congratulations! Now you know how to use a dev container to run Go code. Commit your work to your repository by navigating to your root directory, staging your changes, and committing with an informative message.
```
git add .
git commit -m "Wrote and compiled go code to print a message"
```