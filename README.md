# VS Code on Binder

[![PyPI](https://img.shields.io/pypi/v/jupyter-vscode-proxy)](https://pypi.org/project/jupyter-vscode-proxy/)
[![Install with conda](https://anaconda.org/conda-forge/jupyter-vscode-proxy/badges/installer/conda.svg)](https://github.com/conda-forge/jupyter-vscode-proxy-feedstock)

VS Code on Binder, because sometimes you need a real editor.

Try it: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/vscode-binder/master?urlpath=lab)


# Final few steps to get Black intgrated with VS Code running in Binder sessions launched from here

I was finding what had worked in the past with sessions launched from the source of this fork, namely just installing [Black](https://black.readthedocs.io/en/stable/) via pip and setting `python.formatting.provider`, wasn't allowing black to format the documents. (Maybe this will work again eventually?)    
My fork gets closer to restoring this by actually installing black with pip as the image is built, but you still need to a few things to make it work when you launch your session and launch VS Code. Here are the steps I worked out for activating black to work inside VS Code in those sessions:

1. Launch a session using the `Launch binder` badgse above.
2. Click the 'VS Code' button from the launcher. 
3. Selecte Dark theme, if you prefer.
4. Write ('Application Menu' (<img src="documentation/bars-solid.svg" width="10" height="10">) > 'File' > 'New File') or paste in some Python code and using 'Application Menu' (<img src="documentation/bars-solid.svg" width="10" height="10"> in upper left) >  'File' > 'Save as..' save the new Python file with `.py` extension. 
5. Highlight code, right-click and select 'Format Document' from menu that comes up. In bottom left corner you'll see 'Formatter autopep8 is not installed' in response to trying to trigger formatting/linting and an option to chooser another formatter. Choose **Use black**! Another messgae will then show in the corner 'no pip installer availabe in current environment.' Dismiss this message. We'll fix this by using settings in VS Code to point things at the installation that was put there in the build of the session.
6. Click though 'Application Menu' >  `File` > `Preferences` > `Settings` to get settings window open. Start typing `python.format` in search bar at the top of this window and you should see  'Black Path' among the items listed. 
7. Change what is in the bar below 'Black Path' one to be the following path:

  ```bash
  /srv/conda/envs/notebook/bin/black
  ```
8. Now highlight your Python code, right-click and select 'Format Document' from menu that comes up (`Shift-option-F` is shortcut on Mac), and it should format the code with black now!

You could further enable to format upon saves, see Adam Lombard's post [VSCode: Using Black to automatically format Python](https://dev.to/adamlombard/how-to-use-the-black-python-code-formatter-in-vscode-3lo0).

---------

---------

#### Expected result when black is integrated within VS Code and 'Format Document' works:

If you write the following code (adpated from example shown [here](https://dev.to/adamlombard/how-to-use-the-black-python-code-formatter-in-vscode-3lo0)):

```python
print("test" )
my_dict = {   "apple": "red", "grape": 'purple',
    'orange':'orange', 'watermelon': 'green',
'lemon':'yellow'   }
```
Then right-click and select 'Format Document' (`Shift-option-F` is shortcut on Mac):

You'll see it produce the following result:

```python
print("test")
my_dict = {
    "apple": "red",
    "grape": "purple",
    "orange": "orange",
    "watermelon": "green",
    "lemon": "yellow",
}
```
