# Lecture 02: Setting up GitHub and creating first repositories

## GitHub

GitHub is a web-based platform that allows you to store and manage your code. It is widely used by developers and data scientists to collaborate on projects and share their work with others. In this course, we will be using GitHub to store and share our code, both for the exercises as well as the final assignment. Below, you can see how a local environment (laptop) interacts with the remote environment (GitHub browser) by first downloading (`clone`) a code-based project (`repository`) and then updating the remote version with changes done locally on your computer (arrows going up) or updating the local version with changes being done by colleagues (arrows going down).

![Git Workflow](../assets/git_workflow.jpeg)
*Scheme explaining the Git Workflow taken from [this blogpost](https://medium.com/@itsmepankaj/git-workflow-add-commit-push-pull-69adf44cf812), which has more detailed information on it.*

This Git workflow ensures that changes are tracked, saved, and shared in a structured way, preventing data loss and enabling collaboration. Staging (`add`) selects changes, committing (`commit`) saves them with a message, and pushing (`push`) syncs them with a remote repository for others to access.

Now, you will create your first repository, a profile README that will appear on your user page. 


### 1. Create a Profile README
A profile README is a special repository that is automatically displayed on your GitHub profile. It is a great way to introduce yourself and showcase your work. Take your time to create such a README on the GitHub website.

<details>
<summary>Detailed steps</summary>

1. On GitHub, in the upper-right corner of any page, click on the `+` and then click `New repository`.
2. Name the repository with your GitHub username (must match exactly!).
3. Select the `Public` option.
4. Check the box to `Initialize this repository with a README`.
5. Click `Create repository`.
6. Above the right sidebar, click on `Edit README` and start editing the file.
7. You can use the [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/) to format your README.
8. Once you are done, click on `Commit changes`.

</details>


### 2. GitHub Basics: Create a new repository
Finally, we will create our first repository and update it via the command line. Please make sure to create a public repository (so the TAs can see it) and to add a README file.

#### Creating a new repository

1. Go to the GitHub website and click on the `+` in the top right corner and then `New repository`.
2. Name the repository `ppchem` and select the `Public` option. Also check the box to `Initialize this repository with a README`.

#### Create a `Personal Access Token` (PAT)

Git will ask for your password when you clone a repository (next step). In order ot increase security, GitHub requires one to add a password that is different from your login password. For that, we can create a PAT like so:

⚠️ This is crucial for connecting to GitHub from your computer!

1. Go to the GitHub website and click on your profile in the upper right corner and then `⚙️ Settings`
2. Scroll to the end of the option bar on the left and click on `<> Developer settings` > `🔑 Personal access tokens` > `Tokens (classic)`
3. Next, in the upper right, click on `Generate new token` and choose the classic version.
4. Set token name (e.g., "Python-Course-Access").
5. Select scopes:
   - `repo`
   - `workflow`
   - `write:packages`
   - `delete:packages`
     
   ![PAT](../assets/PAT.png)
6. Generate token
7. ⚠️ **IMPORTANT**: Copy and save your token somewhere safe! You'll need it when Git asks for your password. It will start with `ghp_` followed by a bunch of numbers and letters.

#### Cloning the repository

8. Open your terminal and **navigate (`cd`) to the directory where you want to store the repository** (replace `~/git` with that folder). This is often a folder called `git` in your home directory (`~`). You have to create the folder with e.g. `mkdir git` if it does not exist yet.
   ```bash
   cd ~/git
   ```
9. Type the following command to clone (download) the repository to your local machine (don't forget to replace `username` with your username):
   ```bash
   git clone https://github.com/username/ppchem.git
   ```
10. When prompted type in your GitHub username and PAT for the password.
    - :bulb: *Note*: You will not see any characters appearing in the password prompt when typing/copying your PAT. This is for security reasons. You can just `enter` when you are done typing.
11. Navigate into the repository by typing `cd ppchem`.

In order to clone any repository, you need to have the URL of the repository. You can find the URL by clicking on the green `Code` button on the repository's page.

#### Making changes and committing them

Whenever you make changes to your repository, you need to commit them to save the changes to the repository's history.

11. Add an image from the internet of your favorite molecule to the repository directory on your computer. Your TAs recommend `Caffeine` :coffee:. You can do this by drag and drop on your file system or by using the `mv` command shown in the [command table](#summary-of-important-general-commands) after downloading an image.
12. Type one of the following commands to stage the changes:
```bash
git add caffeine.png # stages only the added file - replace with the actual file name
git add . # stages all changes if you adapted more files
```
13. Type the following command to commit the changes:
```bash
git commit -m "Some message" # Replace with a meaningful message
```

#### Pushing the changes to GitHub

For now, we only made changes to the local repository and committed them (prepared them for upload). We need to push the changes to GitHub to make them available to others.

14. Type the following command to push the changes to GitHub:
```bash
git push origin main # Replace with the branch name if you are not on the main branch
```

You can check the status of your repository at any time by typing `git status` in your terminal in the folder of the repository. This will also show you the changes you made and the files you staged as well as the branch you are currently on.


#### Working with branches

15. Type the following command to create a new branch and switch to it:
```bash
git checkout -b new-branch-name
```
16. Publish the branch to GitHub by typing:
```bash
git push -u origin new-branch-name
```

Changing branches locally will change the version that you have access to locally. So if you have a specific file only in the new branch you cannot find it in `main` and therefore also not push changes from there. If you simply want to switch branch, type:
```bash
git checkout <branch-name>
```

#### Pulling changes from GitHub

If you are working on a repository with others, you might want to pull the changes they made to your local repository. You can do this by typing `git pull` in your terminal in the folder of the repository.


#### Summary of important commands

| Command | Description |
|---------|-------------|
| `git config --global user.name "name"` | Set your name in git configuration (only once)|
| `git config --global user.email "email"` | Set your email in git configuration (only once)|
| `git clone https://github.com/username/repository.git` | Clone a GitHub repository to your local machine |
| `git branch branch-name` | Create a new branch |
| `git checkout branch-name` | Switch to another branch |
| `git add .` | Track all changes in directory |
| `git commit -m "commit message"` | Commit your tracked changes |
| `git push origin branch-name` | Push your local commits to the GitHub |
| `git pull origin branch-name` | Fetch the newest updates from the remote branch |
| `git status` | Check the status of your local repository |
| `git diff` | Show changes between your working directory and the last commit |
| `git diff --staged` | Show changes between your staging area and the last commit |

Above are the basic Git commands you'll frequently use which cover most of the general use cases from cloning repositories to making changes and updating your remote branches. Each command is a powerful tool in Git, and they are designed to work together to create a seamless workflow.

Remember, the best way to become comfortable with Git is practice. Try using these commands to manage a test project and experiment until you're confident with the functionality of each one.

