# Installing Git and Using GitHub

## Table of contents

- [1. Install and configure Git](#1-install-and-configure-git)
  - [Check whether Git is already installed](#check-whether-git-is-already-installed)
  - [Install Git](#install-git)
    - [Windows](#windows)
    - [macOS](#macos)
    - [Linux](#linux)
  - [Verify the installation](#verify-the-installation)
  - [Set your name and email](#set-your-name-and-email)
- [2. Turn your CEGE0096 folder into a Git repository](#2-turn-your-cege0096-folder-into-a-git-repository)
  - [Open your course folder](#open-your-course-folder)
  - [Initialise the repository](#initialise-the-repository)
  - [Add your files to the staging area](#add-your-files-to-the-staging-area)
  - [Make your first commit](#make-your-first-commit)
- [3. Use GitHub with your CEGE0096 repository](#3-use-github-with-your-cege0096-repository)
  - [Create a GitHub account](#create-a-github-account)
  - [Create an empty repository on GitHub](#create-an-empty-repository-on-github)
  - [Connect your local repository to GitHub](#connect-your-local-repository-to-github)
  - [Set up GitHub authentication](#set-up-github-authentication)
  - [Push your local commits](#push-your-local-commits)
  - [Continue working with Git and GitHub](#continue-working-with-git-and-github)
  - [If connecting or pushing fails](#if-connecting-or-pushing-fails)
- [Troubleshooting](#troubleshooting)
- [Further resources (A YouTube video series)](#further-resources)

This tutorial sets up Git and GitHub for CEGE0096 on Windows, macOS or Linux. Follow the installation instructions for your operating system, then complete the shared Git and GitHub exercises. Installation time varies; allow extra time if macOS needs to download developer tools. You will need an internet connection and permission to install software on your computer.

**Git** records changes to files so you can review previous versions and work with others. **GitHub** hosts Git repositories online. You do not need a GitHub account to install Git or use it locally.

## 1. Install and configure Git

### Check whether Git is already installed

Open **PowerShell** on Windows or **Terminal** on macOS or Linux, then run:

```sh
git --version
```

If a Git version appears, Git is already available; continue to [Verify the installation](#verify-the-installation). If the command is not recognised or reports `command not found`, follow the installation steps below. On macOS, running it may prompt you to install Apple’s Command Line Tools; complete that installation as described under [macOS](#macos). Copy only the commands from code blocks, without any terminal prompt.

### Install Git

Follow the instructions for your operating system, then continue to [Verify the installation](#verify-the-installation).

#### Windows

1. Open the [official Git for Windows download page](https://git-scm.com/install/windows).
2. Under **Standalone Installer**, choose **Git for Windows/x64 Setup** for most Intel or AMD computers. Choose **ARM64 Setup** for a Windows computer with an ARM processor. To check your system, open **Settings → System → About** and read **System type**.
3. Save the `.exe` installer to your Downloads folder. Choose the setup installer rather than the portable edition for this tutorial.

Use the current installer offered on the official page; its version number will change over time.

Open the downloaded `.exe` file. If Windows asks for permission, check that the prompt refers to the Git installer you downloaded, then allow it to continue.

Installer screens can vary between releases. Use these choices when the corresponding screen appears, and keep the defaults for other settings:

| Setting | Choice |
| --- | --- |
| Installation location | Use a writable location such as `C:\tools\Git`, consistent with the course guidance on paths without spaces. |
| Components | Keep the defaults, including Git Bash. |
| Default editor | Choose **Visual Studio Code** if you installed it in Week 1. Otherwise, choose an installed editor you know how to use. |
| Initial branch name | Choose **Override the default branch name** and enter `main`. |
| PATH environment | Select **Git from the command line and also from 3rd-party software** so PowerShell and VS Code can find Git. |
| HTTPS, SSH, line endings, terminal and other options | Keep the defaults. |

Click **Install**, wait for setup to complete, then click **Finish**. Close any open terminal windows and restart VS Code so they pick up the new PATH setting.

#### macOS

Open **Terminal**. If Git is not already available, install Apple’s Command Line Tools:

```sh
xcode-select --install
```

Follow the installation dialog and wait for it to finish. These tools include Git; you do not need the full Xcode application for this tutorial. If macOS reports that the tools are already installed, check `git --version` again. See [Apple’s installation instructions](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools/).

Alternatively, if you already use [Homebrew](https://brew.sh/), install Git with:

```sh
brew install git
```

Choose one method; there is no need to install Git twice. These options are listed on the [official Git macOS installation page](https://git-scm.com/install/mac).

#### Linux

Open **Terminal** and use the commands for your distribution. Run only the matching set.

**Ubuntu or Debian:**

```sh
sudo apt update
sudo apt install git
```

**Fedora:**

```sh
sudo dnf install git
```

**Arch Linux:**

```sh
sudo pacman -Syu git
```

**openSUSE:**

```sh
sudo zypper install git
```

`sudo` requests administrator privileges and may ask for your login password; password characters are not displayed as you type. Review the proposed package changes before confirming. If you do not have installation privileges on a managed computer, ask IT for help. See the [official Git Linux installation page](https://git-scm.com/install/linux) for other distributions.

### Verify the installation

After installation, restart VS Code and open a **new terminal**: PowerShell on Windows, or Terminal on macOS or Linux. Run:

```sh
git --version
```

You should see output beginning with `git version`, followed by a version number. On Windows, you can also open **Git Bash** from the Start menu and run the same command. Git Bash provides a terminal with Unix-style commands; PowerShell remains suitable for the commands in this tutorial.

If you use VS Code, open **Terminal → New Terminal** and check `git --version` there too.

### Set your name and email

Git attaches an author name and email address to each commit. Replace the example values in the commands below with your own.

Set your name and email now so you can continue with the exercises. For `user.name`, use your GitHub username or any other preferred name; it does not need to match your GitHub username. If you do not have a GitHub account yet, use your preferred name and current email address. After signing up in [section 3](#create-a-github-account), return here if you need to update either setting by running the commands below again with the new values.

To associate your commits with your GitHub profile, use a verified email address on your GitHub account. Updating these settings affects future commits; it does not change the author details in existing commits.

```sh
git config --global user.name "Your Name"
git config --global user.email "your.name@example.com"
```

`--global` applies these settings to your user account on this computer. You normally set them once per computer. These values identify your commits; they do not sign you in to GitHub. Use an email you are comfortable including in shared commit history.

Check the saved values:

```sh
git config --global --get user.name
git config --global --get user.email
```

See Git's [first-time setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) for more about these settings.

## 2. Turn your CEGE0096 folder into a Git repository

The [Week 1 Python development setup guide](../01%20-%20Week/Week1_Python_Development_Setup.md#6-create-and-open-a-local-project-folder) asked you to create a **CEGE0096 folder** on your computer. Use that folder for this exercise. If you have not created it yet, create it now; refer to the linked guide for instructions. You will record a first snapshot of your code and notebooks. If you have not completed the Week 1 coding exercises, follow the guide to create `week_1/hello.py` before continuing.

### Open your course folder

In VS Code, choose **File → Open Folder** and select your `CEGE0096` folder. Open **Terminal → New Terminal**, using PowerShell on Windows or the default shell on macOS or Linux. The new terminal opens in your project folder. For example, on Windows you might see:

```text
PS E:\code\cege0096>
```

`PS` indicates PowerShell, and the path before `>` shows the terminal's current folder. On macOS or Linux, the prompt will look different, often ending in `%` or `$`. Your path will depend on where you saved `CEGE0096`; do not type the prompt itself. The `pwd`, `ls` and Git commands below work in all three systems.

Check the current location with `pwd` and list the files and subfolders with `ls`:

```sh
pwd
ls
```

Confirm that you can see your Week 1 files before continuing.

### Initialise the repository

```sh
git init -b main
git status
```

`git init` creates a new repository with `main` as its initial branch and a hidden `.git` folder that stores the repository's history; your existing files stay in place. For a new repository, `git status` should report branch `main`, no commits yet, and **untracked files**. Untracked means Git can see a file but has not started recording it. If you already initialised this folder, skip `git init` and continue with the existing repository. Check its branch with `git branch --show-current`; use that name in the later push command if it differs from `main`.

### Add your files to the staging area

The **staging area** holds the changes you want to include in the next commit. Start with the Python script you created in Week 1:

```sh
git add week_1/hello.py
git status
```

The script should now appear under **Changes to be committed**. Add your other scripts and notebooks by their paths, using quotation marks around any path containing spaces. Substitute your actual filenames in this example:

```sh
git add "path/to/your_notebook.ipynb"
```

Review `git status` before staging files. Keep generated files, Python environments, large downloaded datasets and files containing passwords or tokens out of your commits. To exclude files, create a `.gitignore` file in the `CEGE0096` folder and list their paths or patterns. For example, these patterns exclude Python caches and Jupyter checkpoint folders:

```gitignore
__pycache__/
*.pyc
.ipynb_checkpoints/
```

If you create this file, stage it too with `git add .gitignore`. To remove a mistakenly staged file from a first commit while keeping it on disk, use `git rm --cached -- "path/to/file"`.

### Make your first commit

Review the staged changes, then record them:

```sh
git diff --cached
git commit -m "Add Week 1 scripts and notebooks"
git status
git log
```

If the diff opens in a scrolling view, press `q` to return to the terminal. A **commit** is a saved snapshot of the staged changes, with your message explaining what you recorded. `git log` should show your commit history and the identifiers of your commits.

`git status` will say **nothing to commit, working tree clean** if all your changes have been committed and no untracked files remain. Otherwise, review the remaining files and decide whether to add or ignore them. Future edits need another `git add` and `git commit` to record a new snapshot. Your commits are stored locally; uploading them to GitHub is a separate step.

## 3. Use GitHub with your CEGE0096 repository

**GitHub** is an online service for hosting Git repositories. It gives your project a remote home where you can view files and commit history in a browser, access your work from another computer, and collaborate with others. For this module, pushing your commits to GitHub keeps an online copy of the work you have recorded.

Git manages the repository on your computer. GitHub hosts a **remote repository** online. The workflow is: **edit files → add changes → commit locally → push to GitHub**. Saving a file or making a commit does not automatically upload it.

### Create a GitHub account

1. Visit [GitHub sign-up](https://github.com/signup). If you already have an account, sign in and continue to the next step of this tutorial.
2. Follow the prompts to create a free personal account, choose a username, and complete any verification steps.
3. Verify your email address when prompted. Keep access to this email account so you can recover your GitHub account.

Check that the email you configured in [Set your name and email](#set-your-name-and-email) is verified on your GitHub account. If you want to use a different author name or email for future commits, return to that subsection and run the configuration commands again, then continue below.

See the official [account creation guide](https://docs.github.com/en/account-and-profile/how-tos/account-management/creating-an-account-on-github) if you need help.

### Create an empty repository on GitHub

1. While signed in, click **+ → New repository**, or open [Create a new repository](https://github.com/new).
2. Select your personal account as the **Owner** and enter `CEGE0096` as the **Repository name**. You can add a short description such as “My CEGE0096 practical work”.
3. You can specify whether your repo is a **private** one or a **public** one. A public repository can be viewed by anyone; a private repository is accessible to you and people you grant access to.
4. Leave the repository empty: **do not add a README, .gitignore or licence**, and do not choose a template. You already have a local repository and will upload its commits.
5. Click **Create repository**. On the resulting setup page, select **HTTPS** and copy the repository URL. It should look like `https://github.com/YOUR_USERNAME/CEGE0096.git`.

These steps follow GitHub's [repository creation guide](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository).

### Connect your local repository to GitHub

Return to the VS Code terminal in your local `CEGE0096` folder. Check your branch and commit history:

```sh
git status
git branch --show-current
git log --oneline
```

You should have at least one commit from section 2. The commands below assume your branch is called `main`. If it has another name, use that name in the push command.

Replace the example URL below with the HTTPS URL you copied:

```sh
git remote add origin https://github.com/YOUR_USERNAME/CEGE0096.git
git remote -v
```

**origin** is a conventional nickname for the remote repository. `git remote -v` should show your GitHub URL for both fetching and pushing. Adding the remote only records its address; it does not upload anything yet. See GitHub's [remote repository guide](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories) for details.

### Set up GitHub authentication

**Windows:** Git for Windows includes Git Credential Manager. On your first push, it may open a sign-in dialog or browser. Choose browser sign-in if offered, use the account that owns the repository, and complete any authorisation or two-factor authentication prompts.

**macOS and Linux:** For this tutorial, use **GitHub CLI** (`gh`) to authenticate Git over HTTPS. This is an additional tool, separate from Git. Install it using the [official instructions for your operating system](https://github.com/cli/cli#installation). If you already use Homebrew on macOS, run `brew install gh`; on Linux, follow the linked instructions for your distribution. Then run:

```sh
gh --version
gh auth login
```

Choose **GitHub.com**, **HTTPS**, and **Yes** when asked whether to authenticate Git with your GitHub credentials. Choose browser login and follow the prompts. Check the result with:

```sh
gh auth status
```

See GitHub’s [credential guidance](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git) and the [GitHub CLI login reference](https://cli.github.com/manual/gh_auth_login). If you already have working HTTPS authentication, reuse it. GitHub does not accept your normal account password for Git operations over HTTPS.

### Push your local commits

```sh
git push -u origin main
```

This uploads your local `main` branch and its commits to GitHub. `-u` links it to `origin/main`, allowing you to use just `git push` for future uploads from this branch. GitHub also documents this process in its [guide to uploading an existing local repository](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github).

Refresh your repository page on GitHub. You should now see the files you committed and your latest commit message. Open the commit history to check that your local commits are there. Untracked files and uncommitted edits are not uploaded.

### Continue working with Git and GitHub

After editing and saving a file, review and record the change, then upload the new commit. For example:

```sh
git status
git diff
git add hello.py
git commit -m "Update greeting script"
git push
```

Substitute the file you actually changed and write a message describing your change. If you work on another computer or edit files on GitHub, use `git pull` to bring those remote commits into your local branch before starting new edits. Start with a clean working tree; Git will ask you to resolve any conflicting changes.

### If connecting or pushing fails

| Problem | What to try |
| --- | --- |
| `remote origin already exists` | Run `git remote -v`. If the URL is correct, continue to the push. If it is wrong, use `git remote set-url origin https://github.com/YOUR_USERNAME/CEGE0096.git` with your actual URL. |
| `src refspec main does not match any` | Check `git log --oneline` and `git branch --show-current`. Create your first commit if needed, and push the branch name that actually exists. |
| `Repository not found` or permission denied | Check the remote URL and confirm that you signed in to the account with access to the repository. |
| Push rejected because the remote has commits you do not have | This can happen if you added a README on GitHub. For this exercise, create a new **empty** GitHub repository and update `origin` to its URL. |

You have completed this section when your GitHub repository shows the files and commits from your local `CEGE0096` repository.

## Troubleshooting

| Problem | What to try |
| --- | --- |
| `git` is not recognised or `command not found` | Restart your terminal and VS Code. On Windows, check the installer’s PATH option. On macOS or Linux, confirm that the installation in section 1 completed; if using Homebrew, follow its PATH setup instructions. |
| On Windows, Git works in Git Bash but not PowerShell | Check the installer's PATH option, then open a new PowerShell window. |
| `gh` is not recognised or `command not found` | Complete the GitHub CLI installation for your platform, restart your terminal, and check `gh --version`. |
| GitHub authentication fails | On Windows, check Git Credential Manager. With GitHub CLI, run `gh auth status` and, if needed, `gh auth login` again; choose HTTPS and enable authentication for Git. |
| VS Code cannot find Git | Restart VS Code after installation, then check `git --version` in its terminal. |
| Installation is blocked or requires unavailable administrator privileges | Ask your university or workplace IT team to install Git. |
| On Windows, the editor you want is missing from the installer | Install that editor first, or select another installed editor. |

**Check your progress:** You have completed this tutorial if `git --version` works, your name and email are configured, and `git log` shows your first commit in your local `CEGE0096` repository. You should also have a GitHub account and a remote repository containing the commits you pushed from your local repository.

## Further resources

This [Git and GitHub YouTube playlist](https://www.youtube.com/playlist?list=PLUaB-1hjhk8GkHlfKaCJZsF-JFOqkpS29) takes you through installing Git, working with Git in VS Code, branching and merging, and finally working with GitHub. It provides a clear, step-by-step introduction and is highly recommended as a video companion to this guide. Follow along to practise the workflow, revisit topics from the practical, and explore branching and merging in more detail.
