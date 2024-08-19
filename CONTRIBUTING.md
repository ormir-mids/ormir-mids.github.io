# Contributing to the ORMIR-MIDS documentation website
https://ormir-mids.github.io/

---
The website is composed of 3 pages: 
1. Home
2. Specs
3. Package

Each page corresponds to a Jupyter notebook, where the text is written in markdown, following these syntax rules: https://jupyterbook.org/en/stable/content/#. 
The Jupyter notebooks are then converted into HMTL files using Jupyter Book, version 1.

In the future, once Jupyter Book version 2 is available, we will write the documentation in [MyST](https://mystmd.org/guide/typography), an enhanced version of markdown. The changes will *not* concern plain text (i.e., the majority of this documentation), but admonitions and other graphical content. We will also have to merge the files `_config.yml` and `_toc.yml` into one single file called `myst.yml`. If you want to know more about all this, check here: https://github.com/orgs/executablebooks/discussions/1199



---
## First time set up

### 1. Clone from GitHub
1. Clone the GitHub repository https://github.com/ormir-mids/ormir-mids.github.io in your preferred way
2. Create your branch

### 2. Create a virtual environment
In terminal:  
- Create a virtual environment called, for example, `ormir-mids-doc-env`:  
  `python3 -m venv ormir-mids-doc-venv` (command for MacOS)
- Activate the virtual environment:  
  `source ormir-mids-docs-venv/bin/activate`  (command for MacOS)  

### 3. Install the packages
- Install JupyterLab:  
  `pip3 install JupyterLab`
- Install MyST for JupyterLab (if you don't use JupyterLab, find installation info here: https://mystmd.org/guide/quickstart):  
  `pip3 install jupyterlab_myst`
- Install jupyter book:
  `pip3 install jupyter-book`

### 4. Work on the documentation
- In the terminal, Open JupyterLab (from the virtual environment):
  `jupyter lab`
- In JupyterLab, navigate to the `.ipynb` files and modify whatever is needed
- If you are not familiar with MyST, find a quick guide here: https://mystmd.org/guide under `Authoring`

### 5. Create the book
- If it's the first time you create a Jupyter Book, you can learn more here: https://jupyterbook.org/en/stable/start/create.html#anatomy-of-a-book
- In the terminal, build the book with the command:
  `jupyter-book build ormir-mids-docs`
- The HTML version of the book will be in `_built/html/`

### 6. Closing the session
- In terminal, deactivate the virtual environment
  `deactivate` (command for MacOS)  
- Send a pull request

---
## Following sessions
- After the first time setup, you can work on the documentation by:
  - `cd` to the root folder (e.g. `ormir-mids-docs`)
  - Activate the virtual environment (second point in Step 2) and then follow the steps above from 4 to 6 

---
## GitHub Actions
The following is just an explanation on how GitHub Actions is implemented and used to create the website. It does not require any action from the contributors
Learning material:
- How GitHub CI/CD works: [this video](https://www.youtube.com/watch?v=mFFXuXjVgkU)
- How to deploy a Jupyter Book using GitHub Actions: [this webpage](https://jupyterbook.org/en/stable/publish/gh-pages.html)
Practically
1. In the GitHub repository, go to `Settings` tab -> `Pages` on the left panel -> Under `Build and deployment`, `Source` -> Select `GitHub Action`
2. In the GitHub repository, go to the `Code` file -> Press the button `Add file` and then `Create new file` -> In the file name prompt, if your filename is called `ci.yml`, write `.github/workflows/ci.yml`. In the file copy/paste the content from [this page](https://jupyterbook.org/en/stable/publish/gh-pages.html)
3. Make sure that in the repo, there are the following files `.nojekyll`, `requirements.txt`, `_config.yml`, `_toc.yml`, the notebooks, and the figures (in a folder)
4. Every time you push, the book will be automatically created. You can follow under the `Actions` tab
