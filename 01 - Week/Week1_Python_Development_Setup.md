# Setting Up Python, Conda and VS Code

## Table of contents

- [Naming files, folders and installation paths](#naming-files-folders-and-installation-paths)
- [1. Understand the tools](#1-understand-the-tools)
- [2. Python scripts and Jupyter notebooks](#2-python-scripts-and-jupyter-notebooks)
- [3. Install Miniconda](#3-install-miniconda)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux](#linux)
  - [Check the installation](#check-the-installation)
- [4. Create the course environment](#4-create-the-course-environment)
  - [Step 1: create and activate the environment](#step-1-create-and-activate-the-environment)
  - [Step 2: configure the package channel](#step-2-configure-the-package-channel)
  - [Step 3: install the course packages](#step-3-install-the-course-packages)
  - [Step 4: check Python](#step-4-check-python)
  - [If the environment already exists](#if-the-environment-already-exists)
  - [Remove an environment you no longer need](#remove-an-environment-you-no-longer-need)
- [5. Install VS Code](#5-install-vs-code)
  - [Code suggestions and GenAI-assisted coding](#code-suggestions-and-genai-assisted-coding)
- [6. Create and open a local project folder](#6-create-and-open-a-local-project-folder)
- [7. Try running a Python script](#7-try-running-a-python-script)
- [8. Work with a Jupyter notebook](#8-work-with-a-jupyter-notebook)
  - [Turn on Auto Save](#turn-on-auto-save)
  - [Open practical materials from Moodle](#open-practical-materials-from-moodle)
  - [Files and working directories](#files-and-working-directories)
  - [Optional: use Jupyter in a browser](#optional-use-jupyter-in-a-browser)
- [9. Troubleshooting and everyday use](#9-troubleshooting-and-everyday-use)

This guide sets up your own computer for the Python practicals in CEGE0096. We will install **Miniconda**, create a course environment, and use **Visual Studio Code (VS Code)** to write scripts and work with Jupyter notebooks locally. Everything needed for the setup is explained here. Download practical notebooks and any accompanying data from Moodle when instructed.

Follow the sections in order. Commands in code blocks are typed in a terminal, unless labelled as Python code. Copy only the command, without any terminal prompt such as `$` or `(base)`.

### Naming files, folders and installation paths

**Do not use spaces in filenames or folder names you create for this module**, including Python scripts (`.py`), notebooks (`.ipynb`) and folders containing your work. Use underscores instead: for example, `week_1.ipynb`, `my_script.py` and `course_data`.

When an installer lets you choose a location, choose an installation path with no spaces, including its parent folders. For example, use `C:\tools\miniconda3` rather than `C:\my tools\miniconda3`. This reduces problems with command-line tools and package installations. If your user folder contains spaces, choose another writable location; do not rename your existing user or system folders.

## 1. Understand the tools

**Python** is the programming language we will use. A Python **interpreter** executes our code. A **package** is a collection of reusable code: for example, NumPy provides numerical tools and Matplotlib draws plots.

**Conda** manages packages and environments. An **environment** is a separate installation of Python and a set of packages. Different projects can use different Python or package versions without interfering with each other. Conda finds compatible dependencies and installs them together.

**Anaconda Distribution** bundles Conda, Python and a large collection of scientific packages. **Miniconda** provides Conda, Python and a small set of supporting packages; you then install what your project needs. We recommend Miniconda because it provides a small starting point and lets the course specify its dependencies. See [Anaconda Distribution versus Miniconda](https://www.anaconda.com/docs/getting-started/concepts/anaconda-or-miniconda).

You can develop Python programs without either distribution. We use Conda to keep the course setup consistent and simplify installing geospatial packages that depend on compiled libraries such as GEOS, GDAL and PROJ. [GeoPandas recommends Conda for installing this stack](https://geopandas.org/en/stable/getting_started/install.html).

**VS Code** is our local editor and integrated development environment (IDE). It brings together project files, code editing, a terminal, notebooks and a debugger. It uses Python from your selected environment; installing VS Code alone does not install the course's Python packages.

Proper setup of the Python environment and IDE tools will make our day-to-day work smoother. After completing the setup, our daily workflow will be: **open a project folder in VS Code → select its Conda environment → write and run Python code**.

## 2. Python scripts and Jupyter notebooks

Both formats contain Python code, but organise it differently:

| File | What it contains | Typical use |
| --- | --- | --- |
| `.py` | A plain-text Python script. Running the script normally executes it from top to bottom. | Reusable functions, modules, automation and larger applications. |
| `.ipynb` | A Jupyter notebook containing code cells, Markdown text, equations and saved outputs such as tables and plots. | Learning, exploring data and explaining an analysis alongside its results. |

**We will mainly use `.ipynb` notebooks because they offer a more intuitive and flexible way to learn and experiment.** You can run one cell at a time, inspect its output immediately, and combine geospatial maps and plots with explanations. We will also introduce `.py` files for reusable code and projects.

A notebook's **kernel** is the running Python process that executes its cells. Cells share variables: a later cell can use a value created earlier. Editing a cell does not automatically rerun it or update other cells. Running cells out of order can therefore produce misleading results. Sometimes you need to restart the kernel and run all cells from top to bottom to check that your notebook works from a clean start.

## 3. Install Miniconda

If you already have working Anaconda, Miniconda or Miniforge, open its terminal and run `conda --version`. If this works, continue to section 4; you do not need a second installation.

Download **Miniconda**, choosing the installer for your operating system and processor, from the [official download page](https://www.anaconda.com/download). The Python bundled with the installer can differ from the course version: the environment creation command below selects Python 3.12 separately.

### Windows

1. Download the Windows 64-bit Miniconda graphical installer for a compatible PC.
2. Run the installer, review the licence and choose **Just Me**. Use a writable installation location with no spaces or special characters in its path, as explained above.
3. Leave **Add Miniconda to PATH** unchecked. You do not need to make it the system's default Python.
4. Finish installation. Open **Anaconda Prompt** from the Start menu as your normal user. Miniconda installs this prompt despite its name; do not run it as administrator.

For platform requirements and installer details, see the [official Windows instructions](https://www.anaconda.com/docs/getting-started/miniconda/install/windows-gui-install).

### macOS

Check **Apple menu → About This Mac**. An Apple M-series chip uses **Apple silicon / arm64**; an Intel processor uses **x86_64**. Use a native installer matching your processor.

For Apple silicon, download the Miniconda macOS arm64 graphical installer and follow its prompts. Alternatively, download the arm64 `.sh` installer to Downloads, open Terminal and run:

```bash
bash ~/Downloads/Miniconda3-latest-MacOSX-arm64.sh
```

For the terminal installer, review the licence, accept the default location in your home folder and answer **yes** when asked to initialise Conda. Close and reopen Terminal afterwards. See the official [graphical](https://www.anaconda.com/docs/getting-started/miniconda/install/mac-gui-install) and [terminal](https://www.anaconda.com/docs/getting-started/miniconda/install/mac-cli-install) instructions.

**Intel Macs:** Anaconda stopped producing new Intel Mac packages in August 2025. For a new installation, use the native macOS x86_64 installer from [Miniforge](https://github.com/conda-forge/miniforge), which also provides Conda and uses conda-forge. Follow its installation and shell-initialisation instructions, then continue below. Existing working Intel Conda installations can also use the course's conda-forge environment. [Anaconda's Intel Mac notice](https://www.anaconda.com/docs/getting-started/miniconda/install/mac-cli-install)

### Linux

Download the Miniconda shell installer matching your processor. In Terminal, run the downloaded file. For an x86_64 computer with the file in Downloads:

```bash
bash ~/Downloads/Miniconda3-latest-Linux-x86_64.sh
```

For ARM64 Linux, choose the `Linux-aarch64` installer instead and use its actual filename. Review the licence, install in your home directory, answer **yes** to initialising Conda and reopen Terminal. See the [official Linux instructions](https://www.anaconda.com/docs/getting-started/miniconda/install/linux-install).

### Check the installation

In Anaconda Prompt (Windows) or Terminal (macOS/Linux), run:

```text
conda --version
conda info
```

The first command should print a Conda version; the second shows installation details. A prompt containing `(base)` means the base environment is active. Keep `base` for managing Conda and create a separate environment for course work.

## 4. Create the course environment

### Step 1: create and activate the environment

In Anaconda Prompt (Windows) or Terminal (macOS/Linux), create an environment named `geospatial` with Python 3.12:

```text
conda create --name geospatial python=3.12 --override-channels --channel conda-forge
```

Type `y` to proceed if prompted, then activate it:

```text
conda activate geospatial
```

The prompt should now contain `(geospatial)`. Python is installed; we will add the course packages below. The channel options ensure Python and its dependencies come from conda-forge from the start.

### Step 2: configure the package channel

A **channel** is a source of Conda packages. Add conda-forge and give it strict priority:

```text
conda config --env --add channels conda-forge
conda config --env --set channel_priority strict
```

`--env` applies these settings to the active `geospatial` environment. Strict priority favours packages from conda-forge over lower-priority channels. Keeping geospatial dependencies on the same channel helps avoid incompatibilities. See [conda-forge's channel guidance](https://conda-forge.org/docs/user/introduction/).

### Step 3: install the course packages

With `geospatial` still active, you can install packages in either of the following ways. Use **Option A** for the initial setup; Option B explains how to control versions when needed.

#### Option A: let Conda choose compatible versions

Run the following command as one line:

```text
conda install numpy pandas matplotlib ipykernel notebook jupyterlab
```

Review the proposed installation and type `y` when prompted. Allow time for the packages to download and install. Conda uses the channel settings configured in Step 2, giving conda-forge priority.

This installs NumPy, pandas, Matplotlib and Jupyter tools. `ipykernel` lets VS Code run notebook cells using this environment. Conda selects versions that satisfy the packages' declared dependencies and work with the environment's Python version.

#### Option B: specify versions or version ranges

Sometimes a project requires a particular version, or two packages require incompatible versions of a shared dependency. Choosing compatible versions can help resolve these conflicts. For example, to request NumPy 1.26.4 and pandas 2.2.3:

```text
conda install numpy=1.26.4 pandas=2.2.3 matplotlib ipykernel notebook jupyterlab
```

You can also specify ranges instead of exact versions:

```text
conda install "numpy>=1.26,<3" "pandas>=2.2,<3" "matplotlib>=3.8,<4" "ipykernel>=6,<8" "notebook>=7,<8" "jupyterlab>=4,<5"
```

Here, `numpy=1.26.4` requests that specific version, while `"numpy>=1.26,<3"` allows versions from 1.26 up to, but not including, 3. Copy the quotation marks around ranges so your terminal passes them to Conda correctly.

These are alternatives, so you do not need to run all three commands. Specifying versions helps when the chosen versions are compatible; overly restrictive requirements can also cause conflicts. If Conda cannot find a solution, read its dependency message and follow the lecturer's guidance on which versions to use. Review any proposed upgrades or downgrades before proceeding.

### Step 4: check Python

```text
python --version
```

Python should report version `3.12.x`. Section 8 includes a notebook check for the installed packages.

This is a starting environment for Python coding and notebooks. The lecturer will provide instructions when a practical needs additional packages or service accounts.

### If the environment already exists

Run `conda env list` to see your environments and `conda list -n geospatial` to inspect the existing packages. If your existing environment works, keep using it; there is no need to recreate it.

If it has problems, starting with a fresh environment can sometimes (or even oftentimes!) be easier than repairing it. Package dependency issues can be difficult to diagnose, especially after several installations or upgrades. Create another environment with a different name so that you can try a clean setup while keeping the old one:

```text
conda create --name geoenv python=3.12 --override-channels --channel conda-forge
conda activate geoenv
```

Follow Steps 2–4 in the new environment, then select `geoenv` as both the Python interpreter and notebook kernel in VS Code. Use this name wherever the guide says `geospatial`. You can choose another name if `geoenv` already exists.

### Remove an environment you no longer need

Once the new environment works, you can remove an old one to free disk space. Close any terminals or notebook kernels using the old environment. If it is active in your current terminal, deactivate it first:

```text
conda deactivate
```

Check the names with `conda env list`, then remove the old environment. For example, to remove the original `geospatial` environment:

```text
conda env remove --name geospatial
```

Replace `geospatial` with the name of the environment you want to remove. This deletes that environment's Python installation and packages; your notebooks, scripts and data saved in your project folder will remain untouched. Keep the environment you are currently using and do not remove `base`.

## 5. Install VS Code

Download the desktop application from [Visual Studio Code](https://code.visualstudio.com/download), choosing your operating system and processor.

- **Windows:** Run the User Installer and follow its prompts.
- **macOS:** Move the downloaded application into Applications and open it. If it arrives in an archive or disk image, extract or open that first.
- **Linux:** Install the `.deb` or `.rpm` package appropriate to your distribution using its package manager. See the [Linux setup instructions](https://code.visualstudio.com/docs/setup/linux).

Open VS Code. In the **Extensions** view on the left, search for and install these extensions published by **Microsoft**:

| Extension | Identifier | Purpose |
| --- | --- | --- |
| Python | `ms-python.python` | Python editing, interpreter selection and integration with debugging tools. |
| Jupyter | `ms-toolsai.jupyter` | Opening and running `.ipynb` notebooks. |

Accept installation of supporting extensions such as Python Debugger when prompted. You do not need a GitHub account or an AI subscription for this workflow. See [VS Code's Python documentation](https://code.visualstudio.com/docs/languages/python).

### Code suggestions and GenAI-assisted coding

VS Code may suggest code while you type. Some suggestions are ordinary autocomplete, such as variable names and function parameters. Others, often shown as faint text completing a line or a whole block, come from generative AI tools such as GitHub Copilot. **GenAI-assisted coding is part of modern coding practice.**

For beginners, we recommend turning off AI suggestions initially so you practise writing code, recalling syntax and understanding errors yourself. To turn off VS Code's built-in AI features:

1. Open **Settings** with `Ctrl+,` on Windows/Linux or `Cmd+,` on macOS.
2. Select the **User** settings tab and search for `chat.disableAIFeatures`.
3. Enable **Chat: Disable AI Features**. This disables built-in AI features, including Copilot suggestions. Ordinary autocomplete remains available. See [VS Code's documentation](https://code.visualstudio.com/docs/setup/copilot).

If another AI extension still provides suggestions, disable it in the **Extensions** view using its gear menu.

You can also choose to embrace AI assistance and re-enable it. This is your learning, and you are responsible for it: understand the code you use, test its behaviour and make sure you can explain it.

## 6. Create and open a local project folder

Create a folder called `CEGE0096` in your Documents folder. This is where you will keep your own code, notebooks and practical data. You can create subfolders for individual practicals as you need them.

1. Choose **File → Open Folder** and select `CEGE0096`. Its files will appear in the **Explorer** view. Opening a folder keeps related scripts, notebooks and data together as a workspace.
2. Open the **Command Palette** with `Ctrl+Shift+P` on Windows/Linux or `Cmd+Shift+P` on macOS.
3. Run **Python: Select Interpreter** and select the Python installation labelled `geospatial`.
4. Choose **Terminal → New Terminal**. VS Code normally activates the selected environment in a new terminal. Check it with:

```text
python -c "import sys; print(sys.executable)"
```

The path should contain your `geospatial` environment. If Conda is available but the wrong environment is active, run `conda activate geospatial` and check again. Existing terminals may retain their previous environment, so open a new one after changing interpreters.

The **interpreter** selection controls Python scripts and debugging. Each notebook also has its own **kernel** selection. Check both when switching projects. See [VS Code's environment guide](https://code.visualstudio.com/docs/python/environments).

## 7. Try running a Python script

In Explorer, create a folder named `practice` and a file inside it named `hello.py`. Enter and save:

```python
name = "CEGE0096"
message = f"Hello, {name}!"
print(message)
```

Check that the terminal is in your `CEGE0096` folder. If needed, change directory using your actual path. In Windows Anaconda Prompt:

```text
cd /d "C:\Users\your-name\Documents\CEGE0096"
```

In Windows PowerShell, use `cd` without `/d`. On macOS/Linux:

```bash
cd ~/Documents/CEGE0096
```

With that folder as the terminal's current directory, run:

```text
python practice/hello.py
```

You should see `Hello, CEGE0096!`. You can also open the file and choose **Run Python File in Terminal** from the editor's run menu.

For another project, create its own folder, open it in VS Code and select the appropriate environment. Projects with different dependencies should have separate environments.

## 8. Work with a Jupyter notebook

1. Open the **Explorer** view in VS Code. Select the folder where you want to save your notebook, click the **New File** button, type `week_1.ipynb` and press **Enter**. **Make sure the file extension is `.ipynb`!** VS Code creates the file and opens it in the notebook editor.
2. Click **Select Kernel** at the top right. Choose **Select Another Kernel → Python Environments** if needed, then choose `geospatial`. Labels can vary slightly between extension versions.
3. Add a code cell using **+ Code**. Run it using its play button or `Shift+Enter`. Outputs appear below the cell. Markdown cells contain formatted explanations rather than executable Python.

Add a code cell with this setup check:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

print("Python:", sys.version.split()[0])
print("Interpreter:", sys.executable)
print("NumPy:", np.__version__)
print("pandas:", pd.__version__)

x = np.arange(5)
plt.plot(x, x**2, marker="o")
plt.xlabel("x")
plt.ylabel("x squared")
plt.show()
```

The output should show Python 3.12, an interpreter path containing `geospatial`, package versions and a plot. Add a Markdown cell explaining what the plot shows, then save the notebook. This combination of explanation, code and immediate output is why we mainly use notebooks in this module.

Before submitting or sharing work, use the notebook toolbar to **Restart** the kernel and **Run All**, checking that cells succeed in order. Save afterwards so the outputs match the code. Restarting clears variables from memory; it does not delete your cells or saved files. See [Jupyter notebooks in VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks).

### Turn on Auto Save

To save your work automatically, choose **File → Auto Save** in VS Code. A tick next to **Auto Save** means it is enabled. VS Code will save changes after a short delay, so you do not have to save manually after every edit.

To change the delay, open **Settings** using `Ctrl+,` on Windows/Linux or `Cmd+,` on macOS. Search for **Auto Save**, set **Files: Auto Save** to **afterDelay**, and adjust **Files: Auto Save Delay**. The delay is measured in milliseconds: `1000` means one second.

Auto Save applies to your scripts and notebooks once they have a filename and save location. It saves edits; it does not run notebook cells. After running cells, you can also press `Ctrl+S` on Windows/Linux or `Cmd+S` on macOS to save the current notebook and its outputs before closing it.

### Open practical materials from Moodle

When instructed, download the practical notebook (`.ipynb`) and its accompanying data from Moodle. Save them together in a subfolder of `CEGE0096`, preserving any folder structure specified in the practical. Keep the `.ipynb` extension when saving a notebook.

Open the notebook from VS Code's Explorer and select the `geospatial` kernel. You can use the same environment for different practical folders.

### Files and working directories

A relative path such as `data/input.csv` is resolved from the Python process's **current working directory**, which may differ between a script, terminal and notebook. Check it with:

```python
from pathlib import Path
print(Path.cwd())
```

For the script command above, the working directory is your `CEGE0096` folder. A notebook usually starts in its own containing folder. A practical may expect data in a particular subfolder, such as `Material`. Check the practical's instructions and working directory before loading data. Use relative paths where possible and avoid paths tied to one person's computer.

### Optional: use Jupyter in a browser

VS Code runs notebooks directly, so a browser server is optional. To use JupyterLab instead, activate `geospatial`, change to your working folder and run:

```text
jupyter lab
```

Open the displayed local address if a browser does not open automatically. Keep the terminal running while you work. Save your notebooks, then press `Ctrl+C` in that terminal and confirm shutdown if prompted. `jupyter notebook` is another browser interface included in the environment.

## 9. Troubleshooting and everyday use

Below are some commonly encountered issues and ways to resolve them. If you do not encounter these issues, you can skip the table.

| Problem | What to check |
| --- | --- |
| `conda` is not recognised | On Windows, use Anaconda Prompt. On macOS/Linux, reopen Terminal after installation; if initialisation was skipped, run `~/miniconda3/bin/conda init zsh` for zsh or `~/miniconda3/bin/conda init bash` for bash, then reopen it. Adjust the installation path for Miniforge or a custom location. |
| Conda works in Anaconda Prompt but not VS Code's Windows terminal | The integrated terminal may use PowerShell. In Anaconda Prompt run `conda init powershell`, then restart VS Code and create a new terminal. If local shell policy prevents activation, run commands in Anaconda Prompt; use VS Code's selected interpreter and notebook kernel for editing and execution. |
| `geospatial` is missing in VS Code | Run `conda env list` in the working Conda terminal, then reload VS Code. For scripts, use **Python: Select Interpreter → Enter interpreter path** and choose the environment's `python.exe` (Windows) or `bin/python` (macOS/Linux). Recheck the notebook's kernel separately. |
| `ModuleNotFoundError` | Print `sys.executable` in the failing script or notebook. Confirm it uses the intended environment before installing anything. Check `conda list -n geospatial` in the terminal. |
| An environment with this name already exists | Keep using it if it works. If it has issues, follow section 4 to create a fresh environment under another name and select it in VS Code. |
| Notebook results seem inconsistent | Restart the kernel and run all cells in order. Fix the first error before continuing. |
| A dataset cannot be found | Check `Path.cwd()`, the relative path and that you downloaded the accompanying data from Moodle. Preserve the folder structure specified in the practical. |
| A package has no compatible build | Check `conda info` for the platform and ensure the installer matches your processor. Use native arm64 on Apple silicon; ask for help with older or unsupported machines. |

Each time you return to the course, open the project folder, confirm the interpreter and notebook kernel, and activate `geospatial` in any terminal where you run Python commands. Use `conda deactivate` to leave the environment; this does not uninstall anything.

If instructed to add a package, activate the environment first and use `conda install package-name`, replacing `package-name` with the actual name. Conda uses the environment's configured channels. Avoid independently upgrading every package or mixing Conda and pip installations of the same library during a practical.

On a managed UCL computer, check the module's current lab instructions for available software and environment locations. The personal-computer installation steps here do not assume what is installed on a university desktop.
