# Setting up a dev container for Rust

* Primary author: [Emily Chen](https://github.com/emsesc)
* Reviewer: [Daniel Islas](https://github.com/DanielBautista7799)

This tutorial is a quickstart on how to set up a Rust container for a development environment. By the end of this tutorial, you will have a working Rust dev container!

## 🔑 Prerequisites
Before we begin the tutorial, you'll want to have the following:
* [Docker](https://docs.docker.com/engine/install/)
* Visual Studio Code [(VS Code)](https://code.visualstudio.com/download)
* A [`git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) installation.
Click on the links to find out how to install these applications if you don't have them!

## Part 1: Creating Your Git Repository
Open your terminal and change directories to where you want to set up your dev container.

Run the following commands to create a new directory.
```
mkdir rust-dev-container
cd rust-dev-container
```

Now, let's initialize a new Git repository.
```
git init
```

Finally, we'll add a README file.
```
echo "# Rust Dev Container" > README.md
git add README.md
git commit -m "Initial commit with README"
```

## Part 2: Setting Up Your Dev Container
### Step 1: Configuring your container
In your new directory that is currently being tracked by git, add the following JSON object to a file named `devcontainer.json` in a hidden directory `.devcontainer`. The full file path should be `.devcontainer/devcontainer.json`.
```
{
    "name": "Rust Development Environment",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "rust-lang.rust-analyzer"
            ]
        }
    }
}
```
* The **name** allows you to differentiate development environments.
* The **image** specifies the prebuilt Rust container image from Microsoft that we will be using.
* The **customizations** species to also install the official `rust-analyzer` VSCode plugin by the Rust Programming Language Group that helps with Rust development.

### Step 2: Start your environment
1. Open VS Code
2. Open the directory that contains your repository
3. Install the [Dev Containers VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
4. Open the command palette from the menu bar through **View > Command Palette.**
5. Start building your dev container by entering the command `>Dev Containers: Open Dev Container`.

### Step 3: Verify your environment
Let's make sure the container is working as expected.
1. Open terminal in the running container
2. Run `rustc --version`. It should show the most recent version of Rust.

## Part 3: Dusting off the Rust
Now that the backbone is set up, we can now create our Rust project.
### Step 1: Create a binary project
Let's create a new binary project named "hello_world" using the following command. We are are adding the `--vcs none` option because we don't need to create a new `git` repository.
```
cargo new hello_world --bin --vcs none
```

In the `src/main.rs` file, `cargo` has created the following file for you:
```rust
fn main() {
    println!("Hello, world!");
}
```

Let's customize it for ourselves by making it output "Hello COMP423" instead. Modify the file to read the following:
```rust
fn main() {
    println!("Hello COMP423");
}
```

### Step 2: Building and running your project
There are two ways to build and run your project.

The first way is to use `cargo build`.
```
cargo build
./target/debug/hello_world
```

The second way is to do both commands in one step with `cargo run`.
```
cargo run
```

The difference is....

put in tooltip -> You can find more information about `cargo` in [this documentation](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html)!

