# Setting up a dev container for Rust

* Primary author: [Emily Chen](https://github.com/emsesc)
* Reviewer: [Daniel Islas](https://github.com/DanielBautista7799)

This tutorial is a quickstart on how to set up a Rust container for a development environment.

## Prerequisites
* [Docker](https://docs.docker.com/engine/install/)
* [VS Code](https://code.visualstudio.com/download)
* [`git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Part 1: Creating Your Git Repository

## Part 2: Setting Up Your Dev Container
### Step 1: Configuring your container
In your new directory that is currently being tracked by git, add the following to a file named `devcontainer.json` in a hidden directory `.devcontainer`. The full file path should be `.devcontainer/devcontainer.json`.
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
This also installs the official `rust-analyzer` VSCode plugin by the Rust Programming Language Group that helps with Rust development.

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

You can find more information about `cargo` in [this documentation](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html)!

