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
4. Write or paste in some Python code and using 'File' > 'Save as..' save the new Python file with `.py` extension. 
5. Highlight code, right-click and select 'Format Document' from menu that comes up. In bottom left corner you'll see 'auto-pep8' not installed  for formatting/linting and options to chooser another formatter. Choose **Use black**! It will show in the corner 'no pip installer availabe in current environment.' Dismiss this message. We'll fix this by using settings in VS Code to point things at the installation that was put there in the build of the session.
6. Click though `File` menu > `Preferences` > `Settings` to get settings window open. Start typing `python.format` in search bar at the top of this window and you should see  'Black Path' among the items listed. 
7. Change what is in the bar below 'Black Path' one to be the following path:

  ```bash
  /srv/conda/envs/notebook/bin/black
  ```
8. Now highlight your Python code, right-click and select 'Format Document' from menu that comes up, and it should format  it with black now!

You could further enable to format upon saves, see https://dev.to/adamlombard/how-to-use-the-black-python-code-formatter-in-vscode-3lo0

#### Expected result when black is integrated within VS Code and 'Format Document' works:

If you write the following code:

```python
print("test" )
dict = {"apple": "red", "grape": 'purple',
    'orange':'orange', 'watermelon': 'green',
'lemon':'yellow'   }
```
Then right-clicl and select 'Format Document':

You'll see it produce the following result:

```python
print("test")
dict = {
    "apple": "red",
    "grape": "purple",
    "orange": "orange",
    "watermelon": "green",
    "lemon": "yellow",
}
```
