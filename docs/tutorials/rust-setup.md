# Setting Up a Dev Container For Rust
## Prerequisites
### Docker
<p>What makes this all possible is a software called Docker. It can emulate exact and repeatable enviroments to erradicate the popular problem "it only works on my machine". </p>
<p><a href="https://www.docker.com/">Docker and its tutorials can be found here</a></p>
---

### Git and Github

<p>Git is a powerfull yet simple Source Code Management System. By commiting and branch your able is easily debug and merge different versions and parts of your program</p>
<p><a href="https://git-scm.com/">Git can be found here</a></p>

<p>Github however is a software made to give cloud services to git. By its name, it can be seen as a "Hub" of Gits.</p>
<p><a href="https://github.com/">Github can be found here</a></p>

---
### VSCode

<p> Vscode is a light, fast, free and extremely popular IDE devloped by microsft. It has built in Git and Github features like autodetection and seamless pushing and pulling. However, what is we are really after is an offcial extension called <b>Dev Container</b>.</p>
<p><a href="https://code.visualstudio.com/">Vscode can be found here</a></p>
<p><a href="https://code.visualstudio.com/docs/devcontainers/containers">Dev Container tutorial can be found here</a></p>
---

### **Rust ?**
Since we are downlaoding the extension into VSCode and opening a container with an image, we **don't** actually need to formally install Rust! However, if you want to do some personal programming with the language thats heavily encouraged!
<p><a href="https://www.rust-lang.org/tools/install">Download Rust here!</a></p>
---

## Step 1 - Configure Git
### Create a Git Repository in desired Location
<p>Open a comman prompt or Powershell and navigate to your desired directory. Once there run the commands: </p>
```shell 
mkdir COMP423-Rust
cd COMP423-Rust
```
Then initialize a new Git Repository:
```shell
git init
```
While this program is a short tutorial, for best practice create a README file:
```shell
echo  "# COMP423 Rust Hello World" >> README.md
echo  "[Tutorial Link](https://.github.io/comp423-course-notes/tutorials/rust-setup/)" >> README.md
```
!!! note
    The ```echo``` command appends text to the ```READEME.md``` file.
Now stage and commit the README.
```shell
git add README.md
git commit -m "Initial commit with README"
```
---

## Step - 2 Connecting to GitHub

### Link the local Repo to GitHub
<p>1 - Navigate to the <b>Create a New Reposity page</b> in <a href="https://github.com/">Github</a></p>
<p>2 - Use these details:</p>
* <b>Repository Name: </b>COMP423-Rust
* <b>Description: </b>"My first Rust Hello World for Comp 423"
* <b>Visibility: </b>Public
<p>3 - Do not initialize with a README, .gitignore or license.</p>
<p>4 - Click <b>Create Repository</b></p>

### Add The GitHub Repo As a Remote:

```shell
git remote add origin https://github.com/<your-username>/COMP423-Rust.git
```

!!! warning
    Run ```git branch```. If you have an older version of git, you current working branach might be named ```master```. These day the name is ```main``` is used instead. Use ```git branch -M main``` to rename it.


### Push the Local Repo
Simply push your local repo by:
```shell
git push --set-upstream origin main
```

---

## Step 3 - Set Up Dev Environment

### Deeper Dive into Dev Containers
As said before, containers are used to create consistent environments to reduce variance across systems. Essentailly, your computer is using its resources to emulate another with preconfigured specifications. Things such Languages, libraries and tools are standardized.
<br>

With every memember of a team using a the same container, everbody can be sure that whatever works for them can be worked on and debugged by any member of the team. Furthermore, onboarding new members becomes far easy as you can skip lengthy steps to configure a new machine.

### Dev Container Configuration
1. In VS Code, open the ```COMP423-Rust``` directory.
2. Make sure the Dev Container extension is installed
3. Create a ```.devcontainer``` directory in the root of your project
<!-- -->
<!-- -->
In VS Code create a file called ```devcontainer.json``` within the ```.devcontainer``` directory.
<br>
This file configures you dev environment. We will specify:

* <b>Name: </b>Just the name of the dev container
* <b>Image: </b> The docker image you would want to use. In this case, Microsofts latest version of Rust.
* <b>Customizations: </b>This adds configurations to VSCode such as the Rust extension. This preconfigues the dev environment for easy repeatability.
<!-- -->
<!-- -->
```json
{
    "name": "COMP423 Rust Hello World",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations" : {
        "vscode" : {
            "settings" : {},
            "extensions" : ["rust-lang.rust-analyzer"]
        }
    }   
}
```
### Reopen the Project in the VSCode Devcontainer
Do ```Crtl+Shift+P``` or if you use Mac use ```Cmd+Shift+P```. In the search bar that appears, type "Dev Containers: Reopen in Container and select the option. Let the image take its time to download.
<br>
After the container opens, run:
```shell
rustc --version
```
You should see the latest version of Rust and you're ready to get started with Hello World!

---

## Step 4 - Hello, New Rustation!

### Doing Hello World!
* Now, in your root directory run:
```shell
cargo new Hello-COMP423 --vcs none
cd Hello-COMP423
```


!!! abstract "In Fact"
    ```cargo new Hello-COMP423 --vcs none``` Creates a **project folder**. In the next steps, we will be doing commands in this directory. Make sure to be in it!

* Now in VSCord, go through ```Hello-COMP423/src/main.rs``` and modify the pre made print statement to be the desired ```Hello COMP423```

<!-- -->
<!-- -->
In total it should look like this:
```Rust
fn main() {
    println("Hello COMP423");
}
```
**This should be it!**
<br>
Make sure to save the file using ```Ctrl+S``` or ```Cmd+S```. 

### Running The File
**There are 2 main ways to run this Rust file**
<br>

1. using ```cargo build```
2. using ```cargo run```

The difference between both methods is that ```cargo build``` first compiles the program and then outputs an **executable** that can be ran when needed. ```cargo run``` on the other hand, much like what the run button in VSCode does, simply directly compiles (if necessary) and runs the code.

!!! note
    this can be done by using ```cd <directory-name>``` and ```cd ..```. ```ls``` is used to list the contents of each directory.


#### Method 1
navigate to and enter the project directory ```Hello-COMP423```


Now, run:
```shell
cargo build
```
this command will create an executable in ```./COMP423-Rust/Hello-COMP423/target/debug/COMP423-Rust``` along with creating ```Cargo.toml``` and ```Cargo.lock```

#### Method 2
navigate to and enter the project directory ```Hello-COMP423```

Now, run:

```shell
cargo run
```
The program should compile and then run directly.<br>
---
**You should see something along the lines of**
```shell
vscode ➜ /workspaces/COMP423-Rust (master) $ cd Hello-COMP423
vscode ➜ /workspaces/COMP423-Rust/Hello-COMP423 (master) $ cargo run
   Compiling Hello-COMP423 v0.1.0 (/workspaces/COMP423-Rust/Hello-COMP423)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 2.61s
     Running `target/debug/Hello-COMP423`
Hello COMP423
```
!!! Note
    This was done with ```cargo run``` as you can see

### Pushing to GitHub

now to push to GithHub, you first to need to stage all files using ```git add .```, then commit with a message of your choice using ```git commit -m "Completed Hello COMP423 in Rust"``` and lastly push to GitHub using ```git push --set-upstream origin main```.

In total it should look like:
```shell
git add .
git commit -m "Completed Hello COMP423 in Rust"
git push --set-upstream origin main
```
>**I'VE TYPED THESE COMMANDS BEFORE!**<br>
you can actually use ```-u``` in place of ```--set-upstream```. The full short hand world be 
```shell
git push -u origin main
```
---

<br>

* Primary author: [Ian Forlemu](https://github.com/Meepyster)
* Dev Container tutorial primarily made by Kris Jordan and the CSXL Team [here](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-3-link-your-local-repository-to-github)
---