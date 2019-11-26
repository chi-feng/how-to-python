# How to python

## Key concepts
1. **Use a separate virtual environment for each project.** This promotes reproducibility since your projects will be using consistent versions of packages. 
1. **Keep virtual environments in a single location in your home directory** (e.g. `~/venvs/`). This makes it easy to find them later on, and doesn't encumber your project directory with thousands of files and large python packages which will be annoying when you want to move/copy your project. 
1. **Don't put virtual environments in shared/sync folders** (e.g. Dropbox) that will be used by multiple computers with different operating systems. This is because many packages install platform-specific binaries that won't run on other operating systems.

## Creating a virtual environment
1. Navigate to the directory where you store your virtual environments
    ```
    [user@local ~]$ cd ~/venvs
    ```
1. Create a virtual environment called `project-name`
    ```
    [user@local venvs]$ python3 -m venv project-name
    ```
    This creates a python virtual environment in `~/venvs/project-name`

## Activating a virtual environment
1. Before you can run code or install packages, you will need to activate the virtual environment
    ```
    [user@local ~]$ source ~/venvs/project-name/bin/activate
    ```
    You should now see a prefix in front of your prompt
    ```
    (project-name) [user@local ~]$ 
    ```
    
## Deactivating a virtual environment
If you want to switch between environments, you must first deactivate your current active environment
```
(project-name) [user@local ~]$ deactivate
[user@local ~]$
```

## Installing and updating packages
1. Upgrading `pip` and `wheel`. Sometimes your system python installs outdated versions of package management tools. Run the following command to update these tools
    ```
    (project-name) [user@local ~]$ pip install --upgrade pip wheel
    ```
1. Install packages manually
    ```
    (project-name) [user@local ~]$ pip install package1 package2
    ```
1. OR install packages from a `requirements.txt` file
    ```
    (project-name) [user@local project]$ pip install -r requirements.txt
    ```

## Useful python packages
Data science
1. numpy
1. pandas
1. sklearn
1. scipy
1. statsmodels

Visualization
1. matplotlib
1. seaborn

## Running python scripts
1. Navigate to the directory containing the script you want to run. 
1. Run a standalone python script `script.py`
    ```
    (project-name) [user@local project]$ python script.py
    ```
1. If you want to run the script *interactively* so that you have access to a python shell after the script finishes
    ```
    (project-name) [user@local project]$ python -i script.py
    ```

## Jupyter
1. Install the `jupyter` package if it is not already installed
    ```
    (project-name) [user@local ~]$ pip install jupyter
    ```
1. Start the jupyter notebook server
    ```
    (project-name) [user@local project]$ jupyter notebook
    [I 23:00:50.504 NotebookApp] Serving notebooks from local directory: /home/user/project
    [I 23:00:50.504 NotebookApp] The Jupyter Notebook is running at:
    [I 23:00:50.504 NotebookApp] http://localhost:8888/?token=da365240ef9e8c5b5b72c75097e823dcf256c137fa18f31e
    [I 23:00:50.504 NotebookApp]  or http://127.0.0.1:8888/?token=da365240ef9e8c5b5b72c75097e823dcf256c137fa18f31e
    [I 23:00:50.504 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
    [C 23:00:50.517 NotebookApp] 

        To access the notebook, open this file in a browser:
            file:///home/user/.local/share/jupyter/runtime/nbserver-30400-open.html
        Or copy and paste one of these URLs:
            http://localhost:8888/?token=da365240ef9e8c5b5b72c75097e823dcf256c137fa18f31e
         or http://127.0.0.1:8888/?token=da365240ef9e8c5b5b72c75097e823dcf256c137fa18f31e
    ```
  This will automatically open your web browser and navigate to the correct URL

### Install jupyter notebook extensions. 
```
(project-name) [user@local ~]$ pip install jupyter_contrib_nbextensions
```
This only installs the extensions but does not let you enable them. Copy the extensions to the jupyter server's search directory
```
(project-name) [user@local ~]$ jupyter contrib nbextension install --user
```

### Running jupyter notebooks on a remote server using SSH tunnel
Start a SSH tunnel as a background process
```
ssh -NfL localhost:8888:localhost:8888 user@remote
```
SSH into the remote host and start the jupyter notebook server
```
[user@local ~] ssh user@remote
[user@remote ~] source ~/venvs/project-name/bin/activate
(project-name) [user@remote ~] jupyter notebook --no-browser
```
Open the displayed URL in a browser on your local machine
