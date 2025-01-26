# Setting up a dev container for Rust

* Primary author: [Emily Chen](https://github.com/emsesc)
* Reviewer: [Daniel Islas](https://github.com/DanielBautista7799)

This tutorial is a quickstart on how to set up a Rust container for a development environment. By the end of this tutorial, you will have a working Rust dev container!

## 🔑 Prerequisites
Before we begin the tutorial, you'll want to have the following:

* [Docker](https://docs.docker.com/engine/install/)
* Visual Studio Code [(VS Code)](https://code.visualstudio.com/download)
* A [`git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) installation.

!!! Note
    If you're missing any of these tools, click the links above for installation instructions before proceeding.

## Part 1: Creating Your Git Repository
Open your terminal and change directories to where you want to set up your dev container.

Run the following commands to create a new directory.
```
mkdir rust-dev-container
cd rust-dev-container
```

!!! info
     This ensures you start with a clean working directory for your Rust project.

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
1. Open VS Code
2. Open the directory that contains your repository
3. Install the [Dev Containers VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

In this new directory that is currently being tracked by git, add the following JSON object to a file named `devcontainer.json` in a hidden directory `.devcontainer`. The full file path should be `.devcontainer/devcontainer.json`.
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

### Step 3: Start your environment
1. Open the command palette from the menu bar through **View > Command Palette.**
2. Start building your dev container by entering the command `>Dev Containers: Open Dev Container`.

!!! tip 
    Use the shortcut Ctrl+Shift+P (or Cmd+Shift+P on Mac) to quickly open the command palette.

### Step 4: Verify your environment
Let's make sure the container is working as expected.

1. Open terminal in the running container
2. Run `rustc --version`.

You should see an output like this:
```
rustc 1.83.0 (90b35a623 2024-11-26)
```
Success! You are now running Rust in a development container.

## Part 3: Dusting off the Rust
Now that the backbone is set up, we can now create our Rust project.
### Step 1: Create a binary project
Let's create a new binary project named "hello_world" using the following command. We are are adding the `--vcs none` option because we don't need to create a new `git` repository.
```
cargo new hello_world --bin --vcs none
```

In the `hello-world/src/main.rs` file, `cargo` has created the following file for you:
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

Before we begin, change directory into your new binary project.
```
cd hello_world
```

**(1) The first way is to use `cargo build`.**
```
cargo build
./target/debug/hello_world
```
Running both of these commands will yield:
```
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.01s
Hello COMP423
```
`cargo build` compiles the code in your Rust file into machine code, similar to that of how `gcc` does so for C code. The compiled binary is then stored in the `target` directory.

!!! info
     If you run into an error with `cargo build` when you are running the development container on MacOS, make sure you have experimental features turned off in Docker.

**(2) The second way is to do both commands in one step with `cargo run`.**
```
cargo run
```
You'll receive an output like so:
```
   Compiling hello_world v0.1.0 (/workspaces/rust-dev-container/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.54s
     Running `target/debug/hello_world`
Hello COMP423
```

The difference between `cargo run` and `cargo build` is that `run` will compile and run the program in one command, whereas `cargo build` only compiles your code.

!!! note 
    For more information about cargo, refer to [this documentation.](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html)


