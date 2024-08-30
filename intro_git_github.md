# Introduction to Git and GitHub: A Hands-on Tutorial

**Prepared by:** Leandro Ariza

----

## Overview:

In this tutorial, we will cover the basics of version control using Git and how to utilize GitHub for collaborative development. Version control is crucial for tracking changes in code, collaborating with team members, and managing project history effectively.

## Git vs GitHub

* Git: Version control system for tracking changes in code.
* GitHub: Web-based platform hosting Git repositories, facilitating collaboration.
* Key aspect: Git is the tool, GitHub is the service.

## Part 1: Getting Started with Git

### 1.1. Installing Git

If you haven't already installed Git, you can download and install it from here:

https://git-scm.com/downloads

### 1.2. Checking Git version

Open your terminal (Command Prompt on Windows, Terminal on macOS/Linux) and execute:

```bash
git version
```

### 1.3. Configuring Git

Configure our username used in the commit history:

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

Explanation:

* `git config`: This command is used to set configuration options for Git on your local machine.

* `--global`: This flag indicates that the configuration applies globally to all repositories on your system.

* `user.name` and `user.email`: These are configuration keys for setting your name and email address associated with your Git commits.

### 1.4. Initializing a local Git Repository

Navigate to your project directory in the terminal and initialize a Git repository (aka _repo_):

```bash
cd path/to/your/project
git init
```

Explanation:

* `git init`: This command initializes a new Git repository in the current directory, creating a hidden .git directory where Git stores its internal data for tracking changes.

### 1.5. Git's Key Components:

 Git operates through a structured workflow that involves three key states for files:

    Working Directory                 Staging Area                     Repository
    +----------------+             +----------------+             +-----------------+
    |      File      |   git add   |      File      |  git commit |       File      |
    |   (Modified)   |------------>|    (Staged)    |------------>|   (Committed)   |
    +----------------+             +----------------+             +-----------------+

- **Working directory:**
    - Your current work directory.
    - Holds project files you're working on.
    - Changes here are detected by Git.

- **Staging Area:**
    - A middle ground between your work and repository.
    - Allows staging (or preparing) changes before permanently save them.
    - Files in the staging area begin to be tracked by Git.
    - Staged changes are ready to be committed to the repository.

- **Repository:**
    - Stores complete project history and committed changes.
    - Created snapshots of the project are stored here when committed from staging area.
    - Contains all files and directories as they were staged.
    - Usually located in a hidden directory named .git in the project's root.
    - Holds metadata and objects necessary for managing the project's history.

### 1.6. File States in Git

- **Modified:**
Files that have been changed since the last commit but have not yet been staged for commit.

- **Staged:**
Files that have been marked for inclusion in the next commit using git add. These changes are ready to be committed.

- **Untracked:**
Files that are not currently tracked by Git. These files have not been added to the repository and will not be included in the next commit unless explicitly staged.

- **Committed:**
Files that have been successfully saved to the Git repository with a commit. They represent a snapshot of the project at a specific point in time.

### 1.7. Checking repo status

Check the current status of your repository:

```bash
git status
```
Explanation:

* `git status` provides information about:
    - Which files are modified but not staged for commit.
    - Which files are staged for commit.
    - Which files are untracked.

### 1.8. Creating a first file

Now that we know how Git’s tracking system works, we’re ready to apply our first changes to our repository:

1. Use a text editor to create a new text file.

2. Write some content in the file.

3. Save the file with a descriptive name, such as first_text.txt, in the root directory of your project.

4. Open your terminal and navigate to the project directory where you saved the text file.

5. Use the `git status` command to see the status of your repository. You'll notice that the new file is listed as "untracked".

### 1.9. Staging Changes with Git

1. Open your terminal and navigate to the project directory where you saved the text file.

2. Use the `git status` command to see the status of your repository. You'll notice that the new file is listed as "untracked".

3. Add the file to the staging area using the `git add` command:

    ```bash
    git add first_text.txt
    ```

3. Check the status again with `git status` to confirm that the file is now staged for commit.

### 1.10. Committing Changes to the Repository

A commit in Git is a snapshot of the project at a specific point in time. It records the changes you have made to the files in your repository.

To create our first commit, we will use `git commit` with a descriptive message:

```bash
git commit -m "Add first_text.txt with initial content"
```

Explanation:

- `-m`: This flag tells Git to record a message in the log for this commit.
- After committing, Git will display information about the commit, including the commit hash and the number of files changed.

### 1.11. Reverting File Changes

1. Edit and modify the first text file.

2. Check the repo status using  `git status`.

3. Run the following command to discard changes made to the file in the working directory and restoring it to the state it was in at the last commit:

    ```bash
    git restore first_text.txt
    ```

4. Check the file using a text editor to confirm that the file changed to its original state.

5. Chack again the repo status using  `git status`.

### 1.12. Removing file from Stagging Area

1. Use a text editor to create another text file, such as second_text.txt, in the project directory, similar to the previous step.

2. Add the file to the staging area:
    ```bash
    git add second_text.txt
    ```
3. Suppose that you mistakenly added the file. To remove it from the staging area, run the following command:

    ```bash
    git restore --staged second_text.txt
    ```

    Explanation:

    - `--staged`: This flag tells Git to remove the file from the staging area while keeping the modifications in the working directory.

### 1.13. Adding and Committing Changes Simultaneously

1. Edit and modify the first text file.

2. Check the repo status using  `git status`.

3. Run the following command to stage any modified files (tracked by Git) and commit them in one go:

    ```bash
    git commit -am "Modifying first file"
    ```

4. The above command won't add untracked file to the commit (you can use `git status` to verify this). If you have new files that need to be committed, like the second text file, you'll still need to add them separately using `git add`:

    ```bash
    git add second_text.txt
    ```
    And, then, you will commit the files as usual:

    ```bash
    git commit -m "Add a second text file"
    ```

### 1.14. Modifying a commit message

If you need to modify your last commit message, you can do the following:

```bash
git commit --amend -m "Add second_text.txt"
```

### 1.14. Inspecting commits

1. You can use he `git log` command displays a chronological list of commits in the repository. Each commit is listed with information including the commit hash, author, date, and commit message.
2. Use the arrow keys or scroll wheel to navigate through the commit history.
3. Press q to exit the `git log` display and return to the command prompt.

## Part 2: Branching in Git

### 2.1. Managing branches

1. List all the current branches in your repo as follows:

    ```bash
    git branch
    ```

    An asterisk (*) will appear next to your currently active branch.
    In this case, `main`, Git's initial branch.

2. Run the following command to create a new branch for feature development:

    ```bash
    git branch feature/readme
    ```

3. To rename a existing branch, run the following command:

    ```bash
    git branch -m feature/readme feature-readme
    ```

4. Use `git branch` again to see the current state of the branches.


### 2.2. Switching branches

Switch to the `feature-readme` branch as follows:

```bash
git checkout feature-readme
```
**Note:** You can consolidate the creation and checkout of a new branch by using the `-b` flag:

```bash
git checkout -b feature-readme
```

### 2.3. Working in the development branch

1. Use a text editor to create a new text file.

2. Write some content in the file.

3. Save the file as `README.md` in the root directory of your project.

4. Use the `git status` command to see the status of your repository. You'll notice that the new file is listed as "untracked".

5. Add the file to the staging area.

6. Commit the file to the local repo with a descriptive message.

### 2.4. Merging Branches

1. To merge changes from one branch into another, you must first switch to the branch that will receive the merge. This branch is typically the main branch:

    ```bash
    git checkout main
    ```

2. Merge the `feature-readme` branch into the `main` branch as follows:

    ```bash
    git merge feature-readme
    ```

3. If necessary, a Git merge operation can be canceled as follows:

    ```bash
    git merge --abort
    ```

### 2.5. Deleting branches

1. Before deleting a local branch, ensure that you are not currently on the branch you want to delete. For example, you can switch to the `main` branch as usual:

    ```bash
    git checkout main
    ```

2.  You can delete the `feature-readme` branch since you no longer need it by running the following command:

    ```bash
    git branch -d feature-readme
    ```

3. Verify that the branch has been deleted using the `git branch` command.

## Part 2: Connecting with GitHub

### 2.1. Setting up remote repository on GitHub

1. Log in to your GitHub account and navigate to the repository creation page.

2. Click on the "New" button to create a new repository.

3. Provide a name for your repository, optionally add a description, choose visibility settings, and click on the "Create repository" button.

### 2.2. Connecting local repository to GitHub

1. In your terminal, navigate to your local project directory.

2. Use the following command to add a remote repository named "origin" (you can replace <repository-url> with the URL of your GitHub repository):

    ```bash
    git remote add origin <repository-url>
    ```

### 2.3. Pushing changes to remote repository

1. After making changes and committing them locally, you can push those changes to your GitHub repository using the following command:

    ```bash
    git push -u origin main
    ```
    **Note:** Replace `main` with the name of your main branch if it's different (e.g., `master`).

2. If prompted, enter your GitHub credentials (username and password) to authenticate and push changes to the remote repository.