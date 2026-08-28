# Assignment: Python Project Initialization

## Objective

Your task is to initialize a Python project using modern tooling. You will create a virtual environment, add a specific dependency, write and format a simple script, and use Git to submit your work. An automatic check will assess whether you completed this assignment properly.

> [!IMPORTANT]
> **This assignment does not count towards your grade.**
> It is only for you to become familiar with the workflow and tools we will use throughout the course.
> Your submission will be checked automatically for correct formatting and the exact NumPy version.

## Instructions

### Part 1: Install the required tools

You will use both Git (`git`) and the GitHub CLI (`gh`). Git manages the files and commits on your computer, while the GitHub CLI connects your terminal to GitHub.

If you do not already have a GitHub account, create one at [https://github.com/signup](https://github.com/signup) before continuing.

Feel free to skip anything you have already set up. For example, if Git is already installed, you do not need to install it again. If you are unsure, run the verification commands below and carefully read the messages printed in your terminal.


> [!IMPORTANT]
> Use this ungraded assignment as an opportunity to become comfortable troubleshooting your own setup.
> If you encounter a problem, read the error message, consult the linked documentation, and try to resolve it yourself.
> Basic Git setup is expected knowledge for the rest of the course (and in many other courses!), so only limited support for Git installation and configuration will be available at later points.


#### macOS

Install [Homebrew](https://brew.sh/) if you do not already have it, then run:

```bash
brew install git gh
```

#### Ubuntu or Debian Linux

```bash
sudo apt update
sudo apt install git gh
```

If your distribution does not provide `gh`, follow the [official GitHub CLI installation instructions](https://github.com/cli/cli/blob/trunk/docs/install_linux.md).

#### Windows

Open PowerShell and install both tools with WinGet:

```powershell
winget install --id Git.Git -e
winget install --id GitHub.cli -e
```

Open a new terminal after installation so that the commands are available. You can find other options on the [Git website](https://git-scm.com/downloads/win) and in the [GitHub CLI Windows instructions](https://github.com/cli/cli/blob/trunk/docs/install_windows.md).

> [!NOTE]
> We recommend using Linux for this course. The assignment can also be completed on Windows, but some commands (especially those related to Python and virtual environments) may differ depending on how Python is installed and which terminal you use.

#### Verify Git and GitHub CLI

```bash
git --version
gh --version
gh auth login
```

Follow the prompts from `gh auth login` to log in to GitHub.

#### Install uv

Use the [official uv standalone installer](https://docs.astral.sh/uv/getting-started/installation/).

On macOS or Linux, run:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

On Windows, open PowerShell and run:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Open a new terminal if the installer asks you to, then verify the installation:

```bash
uv --version
```

### Part 2: Git and GitHub setup

1. **Create your own empty repository:** Create a new repository named `assignment_0` in your own GitHub account. The following command creates a private repository without cloning it:

   ```bash
   gh repo create assignment_0 --private
   ```

   You may replace `--private` with `--public` if you want the repository to be public.

   Alternatively, create an empty repository at [https://github.com/new](https://github.com/new). Make sure the **Owner** field is your personal account. Select **No template** and leave **Add README**, **Add .gitignore**, and **Choose a license** off. Copy the URL of your new repository, but do not clone it yet.

2. **Clone the assignment repository:** Clone this repository and enter its directory:

   ```bash
   git clone https://github.com/atodorov284/assignment_0
   cd assignment_0
   ```

3. **Change the remote origin:** The clone initially points to the course repository. Change `origin` so that commits are pushed to the empty repository in your own account. Replace `YOUR_GITHUB_USERNAME` with your GitHub username:

   ```bash
   git remote set-url origin https://github.com/YOUR_GITHUB_USERNAME/assignment_0.git
   ```

4. **Verify the remote:** Confirm that both URLs shown for `origin` point to the repository in your own account, not the course repository:

   ```bash
   git remote -v
   ```

### Part 3: Project initialization

1. **Initialize the project:** Use `uv` to create the project files and configure the project for Python 3.12:

   ```bash
   uv init --python 3.12
   ```

2. **Add the NumPy dependency:** Add NumPy version `1.26.0`. This updates `pyproject.toml`, creates the `.venv` virtual environment, and installs the package:

   ```bash
   uv add numpy==1.26.0
   ```

3. **Activate the virtual environment:**

   On macOS or Linux:

   ```bash
   source .venv/bin/activate
   ```

   On Windows PowerShell (this might differ depending on your setup):

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

### Part 4: Code and submission

1. **Write the script:** Open `main.py`, remove the code that is there, and add the following unformatted code:

   ```python
   import numpy as np
   def add_two_integer_lists(a: list[int], b: list[int]) -> None:
       arr=np.array(a)+np.array(b)
       print(f"My added array: {arr}")
   if __name__ == "__main__":
       add_two_integer_lists([1,2,3],[4,5,6])
   ```

2. **Format the code:** The code has inconsistent spacing and missing blank lines. Automatically format it with Ruff:

   ```bash
   uvx ruff format
   ```

   Inspect `main.py` again and notice what changed.

3. **Verify your work:** Run the following commands:

   ```bash
   uvx ruff format --check
   uv run python -c "import numpy; print(numpy.__version__)"
   ```

   The formatting command must finish successfully, and the second command must print `1.26.0`. Resolve any failures before continuing.

4. **Commit and push:** Stage your changes, commit them, and push them to your repository.

   ```bash
   git add .
   git commit -m "Complete project setup and add numpy script"
   git push origin main
   ```

5. **Inspect the automated checks on GitHub:** Open your repository on GitHub and go to the **Actions** tab. The formatting and NumPy-version workflows will start after you push. Wait for both workflows to finish and make sure they have green checkmarks.

   If a workflow fails, open it and read its logs to determine what went wrong. Fix the problem locally, commit and push the correction, and inspect the new workflow run. Repeat this process until both automated checks pass.
