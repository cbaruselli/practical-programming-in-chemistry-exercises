# Lecture 10 - Copier project templates

This lecture we will look at using a project template, Copier, to turn the CDK-Depict code you wrote last week into a simple Python package.

**What is Copier?**
   - Copier is a utility tool created to facilitate the duplication and customization of project templates. It is written in Python and enables you to efficiently generate projects by copying a template and making specified alterations defined in an easy configuration file (often YAML).
   - This tool is designed to help reduce redundant setup tasks and ensures consistency across multiple projects by allowing users to create a single project template that can be reused and customized without starting from scratch each time.

Lets go through the steps required to make this package.

#### Step 1: Set Up Your Environment

```bash
conda activate ppchem
```

#### Step 2: Organise the code

Go through the Jupyter notebook from yesterday and ensure that your code is neatly organised into functions. Once this is done move the code into a new notebook which should contain only the code required to query the CDK-Depict website. 
Place this notebook in a new folder called 'CDK-Package'.

Remember you can use the following commands to create folders and move files between directories. For the *mv* command to work you must navigate your terminal to the directory in which the file you want to move is located. In your case it should be something like '/path/to/your/practical-programming-in-chemistry-exercises/week_08/your_new_notebook.ipynb'

```bash
mkdir CDK-Package
cd CDK-Package
mv /path/to/your/practical-programming-in-chemistry-exercises/week_08/your_new_notebook.ipynb .
```

#### Step 3: Convert Your Notebook

While Jupyter notebooks are excellent tools for quickly developing small snippets of code, they are not suited for use in a Python package. To make your code compatible with a Python package we need to copy the functions into a Python module, as you did in exercise 8. Create a module called `cdktest.py`.

#### Step 4: Using Copier to Create the Package Structure**

Instead of manually creating directories and files as outlined previously, you can use the Copier template designed for consistent and quick setup of scientific projects/folders. Here’s how you can do it:

1. **Install Copier**:
   First, ensure Copier is installed in your environment:

   ```bash
   pip install copier
   ```

2. **Generate Project Structure**:
   Utilize Copier with the schwallergroup template to create your project structure. Make sure you're still within your `ppchem` environment:

   ```bash
   copier copy gh:schwallergroup/copier-liac-minimal /path/to/your/CDK-package
   ```

   Enter the directory path where you want your new project to be initiated. Follow the on-screen prompts provided by Copier to customize the project (such as naming modules or defining author details).
   Enforce the code style as : strict (precommit, ruff, mypy)

3. **Place Your Converted Module**:
   Move or copy the Python scripts (converted from your Jupyter notebooks in Step 3) into the appropriate directories within this newly created package structure. Typically you should place this in `src/package_name`.

4. **Setup ths Code**
   Open the `__init__.py` file. Add a line of the following format to import the functions from the code we generated from your notebook

   ```python
   from .cdktest import smiles_depict_url, display_svg
   ```

   Remember to use the names you gave to your functions


#### Step 6: Initialize Git Repository
1. **Create a Local Repository**
Initialize a git repository to start version control within the newly created directory structure:

```bash
cd /path/to/you/CDK-Package
git init
git add .
git commit -m "Initial package setup with Copier"
```

Next, you need to create a remote repository where your code will be stored online.

2. **Create a New Upstream Repository**
   - Navigate to the Repositories tab on Github.com and click on the "New" button.
   - Name your repository (e.g., `CDK-Package`).
   - Choose if you want your repository to be public (anyone can see this repository) or private (you choose who can see and commit to this repository).
   - **Important**: Do not initialize the repository with a README, .gitignore, or License. Your local repository already contains these files if necessary.
   - Click the "Create repository" button.

3. **Link Your Local Repository to the Remote Repository**
   - Once your repository is created, GitHub will display a page with a URL and some setup instructions. Copy the URL for the repository.
   - Go back to your terminal and link your local repository with the remote repository using the following command:
     ```bash
     git remote add origin YOUR_REMOTE_URL
     ```
     Replace `YOUR_REMOTE_URL` with the copied URL.

4. **Push Your Local Repository to GitHub**
   - Now, push the changes from your local repository to GitHub with:
     ```bash
     git push -u origin main  # or git push -u origin master
     ```
   - The `-u` flag is used to set the upstream (tracking reference) for your local branch.

5. **Verify Everything is Online**
- Go back to your repository on GitHub and refresh the page. You should now see all the files you've added locally.

#### Step 7: Install Your Local Package
Now we have the code in our package prepared, we must set it up as installable so yourself and others could access it through:
```bash
pip install -e .
```
This uses the `pyproject.toml` file created by copier.

This installs the package in editable mode (symlink) so changes are reflected immediately.


#### Step 8: Test Your Package

Ensure everything works by importing your package in Python. Try out your functions, do you get the same result as in the notebook?

#### Step 9: Create formal tests using pytest

1. **Install pytest**:
   If not already installed, you can install pytest using pip:
   ```bash
   pip install pytest
   ```

2. **Create a Test File**:
   Inside your project structure, usually under a `tests` folder, create a test file named `test_depict_url.py` or similar.

3. **Write Test Cases**:
   In the `test_depict_url.py` file, add the following Python code to create test cases for the `smiles_depict_url` function.

   ```python
   import pytest
   from cdkpackage import smiles_depict_url

   def test_smiles_depict_url():
       # test your code here
   ```

4. **Run the Tests**:
   Navigate to your project's root directory in the terminal, and run:
   ```bash
   pytest
   ```
   This command will discover and run all the tests in the `tests` directory.
