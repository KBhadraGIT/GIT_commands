# **GIT Commands:**

-   **Procedure to initiate git in the folder containing source code**:

    ```
    git init
    ```
-    **Naming the git branch**:

    ```
    git branch -M main
    ```

**Check if any git repository connected or not**, the remote consists of a variable name origin that contains the github repo link:

    ```
    git remote -v
    ```

-  To add the github repo link in origin if the origin is empty:

    ```
    git remote add origin github_Repo_Link
    ```

    -  To update/replace the github repo link, first we need to remove the old link then add the new link:

    1. This will remove the old link
    ```
    git remote remove origin
    ```

    2. This will add the new link
    ```
    git remote add origin github_Repo_Link
    ```

    NOTE: You can add .gitignore, LICENSE and many more pre built files offered by github from the repository after that you need to update your source code in youre system:

    *NOTE: Here, I am using the branch name as 'main'*
    ```
    git pull origin main
    ```

-  To update any changes in your github repo first you need to select the file by its directory andn then push the code to your repo:

    1. Select the file or its relative path
    ```
    git add relative_path_of_file
    ```

    If you need to update all the changed file at once then use '.'
    ```
    git add .
    ```
    2. You need to add the comment with the file you are updating

    *NOTE: Thecomments should be inside either single quote or double quote*
    ```
    git commit -m "comment"
    ```
    -  Suppose while building your source code you don't want to upload some of your file or folders to the github because it may contain all your private keys, logs of production and many more. So, to deal with this case you need to add the relative path of those files and folders in `.gitignore` file.

    - If you want to creat your own global ignore file using the following commands:

    ```
    git config --global core.excludesfile [filename]
    ```

    -  After working on a long project, due to pulling and pushing of the code there is a chance of accumulation of cache file in the repo due to which the git commands might get slow. Thus, for this you can remove the cache by

    ```
    git rm -r --cached .
    ```

## **Deleteing and renaming file**

-  **You can simply delete the file you want to and then update it by add**
    ```
    git add . && git commit -m "Deleted this file."
    git push origin main
    ```

-  **To restore the deleted files**
    ```
    git restore .
    ```

-  **To remove any file using git command**
    ```
    git rm relative_file_path
    ```
    *Note: After doing the above step it will be going to stagging area*
    To undo the above stage
    ```
    git restore --staged .
    ```
    OR
    ```
    git restore --staged file_name
    ```
    Instead of using --staged you can use -s i.e.
    ```
    git restore -s .
    ```
-  **Proper way to rename a file in git**:

    If we rename a file in the source code and try to add it to stagging area then two process will take place:
    
    1. The deletion od file with oold name.
    2. Addition of file with new name.

    So, the best practice to follow is using the git command to rename the file:
    ```
    git mv file_name new_file_name
    ```
## **Difference between your last version of git push source code and current version of code**

-  **To check any differences you can do the following**
    ```
    git diff
    ```
## **git logs**
    ```
    git log
    ```

-  **For better view of git logs, use the following command:**
    ```
    git log --oneline
    ```
## **Editing git history**

-  **Ammending**:

    ```
    git commit --ammend
    ```
    It does two things:
    1. Modifying the commit message: When you run "git commit --amend", it opens the default text editor with the commit message of the most recent commit. You can edit the message to provide more descriptive or accurate information about the commit.

    2. Adding changes to the commit: If you have forgotten to include some files or make certain changes in the previous commit, you can stage those changes and run "git commit --amend". It adds the staged changes to the previous commit, effectively modifying it to include the additional changes.

-  **To roll back to speccific log**:

    ```
    git reset first_5_log_id
    ```
    This code won't affect the code is src but it will just unstage them from the logs and the files will be in modified stage.

-  **Hard reset**:

    ``` 
    git reset --hard first_5_log_id
    ```
    This code will affect the coode in src. This will get rid off all the changes you made until now, and it will roll back to previous version of the code at of that specific log.

-  **Rebasing**:

    The ```git rebase``` command is used in Git to apply changes from one branch or commit onto another branch. It is primarily used for integrating changes from one branch into another, typically to incorporate the latest changes from a parent branch into a feature branch.

    ```
    git rebase <branch>/<commit>
    ```
    This command performs a rebase operation, where the changes from the specified ```<branch>``` or ```<commit>``` are applied onto the current branch. It effectively moves the entire branch to a new base point, replaying the commits from the specified branch or commit onto the current branch. This can be useful when you want to update your branch with the latest changes from another branch.

    ```
    git rebase -i HEAD~#
    ```
    This command performs an interactive rebase operation. The ```-i``` option stands for "interactive" allowing you to interactively choose which commits to modify, reorder, edit, squash, or drop during the rebase. ```HEAD~#``` refers to the number of commits you want to include in the interactive rebase. 

    For example, ```HEAD~3``` would include the last three commits. It opens an editor where you can specify the actions to be performed on each commit.

    ```
    git rebase -i --root
    ```
    This command performs an interactive rebase starting from the root commit of the branch, going through all the commits in the branch history. The ```--root``` option indicates that the rebase should start from the initial commit of the branch rather than a specific commit. It allows you to modify the entire history of the branch interactively, reordering, editing, or dropping commits as needed.

    **NOTE**: *Interactive rebasing (```git rebase -i```) is a powerful tool that provides flexibility in manipulating commit history, such as squashing multiple commits into one, reordering commits, editing commit messages, or even dropping commits altogether. It gives you fine-grained control over the branch's commit history to create a more organized and coherent series of commits before merging or pushing the changes.*

## **Force push**:

This allow us to push the code from source to the repo even if there is no match in the code history/log history between the source code and git repository.

```
git push origin +branch_name    
```

## **Branches**

-   **To check the all the branches related to repository**:

    ```
    git branch
    ```

-   **Making a copy of existing branch**:
    
    ```
    git switch -c branch_name
    ```

    This is used to create a new branch and switch to it in a single step. It combines two Git commands, ```git switch``` and ```git branch```, into one convenient command.

    Here's the role of this code:

    1. **Creating a new branch:**
    
        The ```-c``` option stands for "create" and is used to indicate that a new branch should be created. When you run ```git switch -c <branch-name>```, Git creates a new branch with the specified name.

    2. **Switching to the new branch:** 

        After creating the new branch, Git automatically switches to it. It means that you will be working on the newly created branch, and any subsequent commits will be made on this branch.

-   **Merging branches**

    ```
    git merge <branch_name>
    ```
    This is used to integrate changes from one branch into another branch. Two things happen:

    1. Merging branch changes: The command initiates the process of merging changes from the specified branch into the current branch. Git analyzes the commit history of both branches and applies the necessary changes to bring them together.

    2. Incorporating changes into the current branch: After the merge is successful, Git applies the changes from the specified branch to the current branch. This includes any file modifications, additions, or deletions made in the specified branch.

-   **Deleting branches**

    ```
    git branch --delete <branch_name>
    ```

    OR

    ```
    git branch -d <branch_name>
    ```

    OR

    ```
    git branch -D <branch_name>
    ```

## **STASH & CLEAN**

###  1. STASH 

-   **Stashing code**:

    Stashing code in Git is a way to temporarily save changes that you have made to your working directory without committing them. This can be useful when you want to switch to a different branch or work on a different task without committing incomplete changes. 

    1. Command to stash your changes:

    ```
    git stash save "Your stash message"
    ```

    Git will save your changes and revert your working directory to the state of the last commit. You can switch branches, work on other tasks, or perform any other operations you need. Your stashed changes are saved and can be reapplied later.

    2. To check multiple stashes use the following command:

    ```
    git stach list
    ```

    3. To apply your stashed changes back to your working directory, use the following command:

    ```
    git stash apply
    ```

    This command will apply the most recent stash. If you have multiple stashes, you can apply a specific stash by referring to it using its index, like ```git stash apply stash@{1}```.

    **Note**: The ```git stash apply``` command doesn't remove the stash. If you want to remove the stash after applying it, use ```git stash drop``` followed by the stash's index or ```git stash clear``` to remove all stashes.

    4. Apply and remove that stash

    ```
    git stash pop
    ```

    The ```git stash pop``` command is similar to ```git stash apply```, but it not only applies the most recent stash but also removes it from the stash list. This command will apply the changes from the most recent stash and revert your working directory to the state of that stash. Additionally, it removes the stash from the stash list.

###  2. Clean

The ```git clean``` command is used to remove untracked files from your working directory. Here's what each option of git clean does:

-   ```
    git clean -n
    ```
    OR 
    ```
    git clean --dry-run
    ```

    This option is used to perform a dry run of the ```git clean``` command. 
    
    It shows you a list of untracked files and directories that would be removed without actually deleting them. It helps you preview what would be cleaned up before executing the command.

-   ```
    git clean -d
    ```
    OR
    ```
    git clean --directories
    ```

    The ```-d``` option tells ```git clean``` to include untracked directories as well when cleaning. 
    
    It removes not only untracked files but also untracked directories that are not being tracked by Git. By default, ```git clean``` only removes untracked files, so using the -d option allows you to delete untracked directories too.

-   ```
    git clean -f
    ```
    OR
    ```
    git clean --force
    ```

    The ```-f``` option forces the removal of untracked files and directories. 
    
    When used with ```git clean```, it performs the actual cleanup and deletes the untracked files and directories permanently. Be cautious when using this option, as it permanently removes the files and directories without any possibility of recovery.

##  REMOTES

The ```git remote``` command is used to manage remote repositories in Git. It allows you to view, add, rename, and remove remote repositories associated with your local repository.

Here are some commonly used subcommands of ```git remote```:

-   ```
    git remote -v
    ```

    This command lists the remote repositories configured for your local repository, along with their URLs. It provides both the fetch and push URLs for each remote.

-   ```
    git remote add <name> <url>
    ```

    This command adds a new remote repository to your local repository. ```name``` is a short name or alias that you give to the remote, and ```url``` is the URL of the remote repository.

-   ```
    git remote rename <old-name> <new-name>
    ```
    This command renames an existing remote repository. You provide the current name of the remote (```old-name```) and the new name you want to assign (```new-name```).

-   ```
    git remote remove <name>
    ```
    OR
    ```
    git remote rm <name>
    ```

    This command removes a remote repository from your local repository. You specify the name of the remote repository you want to remove.

-   ```
    git remote show <name>
    ```

    This command provides detailed information about a specific remote repository, such as the fetch and push URLs, the branches that are tracked, and other configuration details.