# GIT reference 
## Created from multiple sources for personal use.

1) [👨‍💻 Editer](#editer-)
2) [📡 Initialize](#initialization-)
3) [🚀 Push](#Pushing-to-remote-)
4) [📸 Stage](#Stage-)
5) [📲 Stash](#stash-)
6) [🏈 Clone-fetch-pull](#clone-fetch-pull-)
7) [🎣 Cherry-pick](#Cherry-pick-)
8) [🔎 Debug changes](#Debug-changes-)
9) [🚨 Undo changes](#Undo-changes-)
10) [🔐 Merge](#Merging-)
11) [📀 Rebase](#Rebase-)
12) [🌴 Branch](#Branch-)
13) [🚦 Public to private Fork](#Public-to-private-Fork-)


### Editer 👨‍💻

##### ➡️ Save 

Mac `CTRLX or CTRLS` to save. <br>
Windows	`CTRLX or CTRLC` to save <br>
Linux `CTRX (and Y to confirm)` to save <br>	
	
Windows GIT Bash press `i` to enter inline insert mode. Type the description at the very top, press `esc` to exit insert mode, 
then type `:x!` (now the cursor is at the bottom) and hit `enter` to save and exit. If typing `:q!` instead, will exit the editor 
without saving (and commit will be aborted)

##### ➡️ Commands 

> :qa!	(exit and abort) <br>
> :wq (save and exit) <br>
> :w Enter (save) <br>
> :q (close file) <br>
	
### Initialization 📡

> git init <br>
> git config --global user.name \<user name used on github\> <br>
> git config --global user.email \<email used on github\> <br>
> Create .gitignore (node_modules, .parcel-cache, dist, .env, .DS_store) <br>

### Pushing to remote 🚀

👉 Don't create readme.md when creating a repositary as it will cause a conflict. <br>
> git remote add origin \<repo link\> <br>
> git push origin master (or any other branch) <br>
> git push origin new-feature (if want to push all branches) <br>
> git push --force {remote} {branch} (DANGEROUS) <br>
> git push --force-with-lease {remote} {branch} (SAFE push with force) <br>
> git push --all (push all local branches) <br>
> `git push -f <remote> <local branch>:<remote branch>` <br>
> git push origin -u \<newname\> (push and set upstream) <br>
> git remote remove origin (Remove origin) <br>
> git remote remove <remote_name> <br>
> git remote set-url origin git://new.url.here (change origin) <br>
> git remote show <remote_name> (shows info about remote) <br>
> git remote -v (list all remotes) <br>
> git remote set-url <remote-name> <remote-url> (chnage remote url) <br>

👉 After renaming local branch: <br>
> git push origin new_branch_name:master (now changes will go to master branch but your local branch name is new_branch_name)

### Stage 📸

> git add [file name] (Stage) <br>
> git add {file-name-1} {file-name-2} (stage multoiple files) <br>
> git add *.{file_extension} (only certain files) <br>
> git add . (stage all new and modified files AND NOT deleted files) <br>
> git add -A (stage all anew and mofified AND deleted files) <br>
> git add -p OR git add --patch (allows you to review each change made one at a time) <br>
> git commit -m “[descriptive message]” (Commit) <br>
> git commit {file-name-1} {file-name-2} -m "Add commit message here" (commit specific file) <br>
> git commit (opens VIM; to save commit: click Esc, type :wq, click Enter) <br>
> git commit --amend -m "Add the improved message here" (ammend previous commit) <br>
> git commit -am "Add message here" (stage and commit in one line) <br>

> git show <commit_hash> (shows info)<br>
> git status (Shows modified and staged files) <br>
> git diff (Diff of what is changed but not staged) <br>
> git diff --staged (diff of what is staged but not yet committed) <br>

##### ➡️ Output of patching

👉 Before we advance, let’s break down the output quickly:<br>
`diff --git a/planets.csv b/planets.csv` - this means there are changes between two files; a) the original file, and b) the modified one <br>
`index 846b016..5739dbf 100644` - this uniquely identifies this specific change (basically an ID) <br>
`-- a/planets.csv` - this is the original file of the planets.csv file <br>
`+++ b/planets.csv` - this is the modified version of the planets.csv file <br>
`@@ -1,9 +1,9 @@` - this is the “hunk” of changes. A hunk is a portion of code that has been added or modified. So the hunk in this example would be the 9 lines in the CSV file (1 header, 8 rows). <br>
In the -1,9 section, the 1 means the hunk starts at line 1 in the original version, and the 9 means the file contains 9 lines. The same principle applies to the +1,9 for the modified version.
We can decide to advance with this patch by typing y into the terminal, or we can reject the changes by typing n. There are other options included but that will be for a future article, so stay tuned for that!
By typing y, we advance to the next change that needs reviewing:

### Stash 📲
Save a change in a temporary location: <br>

In Git, stashing allows you to save changes in a temporary location and then resume when you’re ready to continue from where you left off with them.
This is used mainly when you have changes that are staged, modified or even untracked that you’re not ready to commit yet even though you need to make other changes elsewhere e.g. in another branch. Stashing will make your working directory clean enough for you to work on different changes while you have others stored elsewhere.
<br>

> git stash <br>
> git stash save {custom_name_for_stash} (shash with name) <br>
> git stash list (list stashes) <br>
> git stash apply (apply most recebt stash) <br>
> git stash apply {stash-id} (apply specific stash) <br>
> git stash drop <br>
> git stash drop {stash-id} <br>
> git stash pop (apply and delete) <br>

### Clone fetch pull 🏈

➡️ `FETCH` from remote branch WITHOUT merging with local branch: <br>

`Git fetch` gathers any commits from the target branch that do not exist in the current branch and 
stores them in your local repository. However, it does not merge them with your current branch. 
This is particularly useful if you need to keep your repository up to date, but are working on something 
that might break if you update your files. To integrate the commits into your current branch, you must use 
git merge afterwards.
<br>

> git fetch <br>
> git fetch {remote} <br>
> git fetch \[alias\] (fetch down changes from all the branches from that Git remote) <br>
> git diff master origin/master <br>


➡️ `PULL` retrieves all changes AND merges them: <br>

`Git pull` tries to automatically merge after fetching commits. It is context sensitive, so all pulled commits 
will be merged into your currently active branch. git pull automatically merges the commits without letting 
you review them first. If you don’t carefully manage your branches, you may run into frequent conflicts.
<br>

> git pull (fetch and merge any commits from the tracking remote branch) <br>
> git pull {remote} {branch} <br>
> git pull --all <br>
> git pull --rebase (rebase while pulling) <br>

➡️ `CLONE`: <br>
> git clone \[url\] <br>

### Cherry-pick 🎣
For picking an individual commit from one branch and pasting it into another
As the name implies, git cherry-pick lets you select specific commits from one branch and apply them to another, without merging the changes from the source branch.
```
# Switch to the branch you want to apply the selected commits to
git checkout {target_branch}
```
```
# Apply the commit to the target/child branch
git cherry-pick {commit_hash}
```

Cherry pick multiple commits.
```
# Switch to the branch you want to apply the selected commits to
git checkout {target_branch}
```

```
# Apply the commits to the target/child branch
git cherry-pick {commit_hash_1} {commit_hash_2}
```

Cherry pick a merge commit from the source branch.
```
# Switch to the branch you want to apply the selected commits to
git checkout {target_branch}
```
```
# Apply the commits to the target/child branch
git cherry-pick -m {parent_no} {commit_hash}
```

### Debug changes 🔎
> git log --oneline (see commits) <br>
> git log --since="time period" (filter by time period) <br>
> git log --since="earlier date" --until="later date" (filter by date range) <br>
> git log --author={name_of_user} (filter by author) <br>
> git log --author="{name_of_user_1}|{name_of_user_2}" (filter by author) <br>
> git log -p OR git log --patch (Filter the log commits by multiple authors) <br>
> git log branchB..branchA (show the commits on branchA that are not on branchB) <br>
> git log --follow \[file\] (show the commits that changed file, even across renames) <br>
> git log --stat -M (show all commit logs with indication of any paths that moved) <br>
> git status <br>
> git ls-tree --full-tree --name-only -r HEAD (see all tracked files) <br>
> git worktree list (list working tree) <br>
> git show <commit_hash> (shows info) <br>
> git diff --staged (diff of what is staged but not yet committed) <br>
> git diff --color-words (to make it easier to see) <br>
> git diff --name-only (show names of modified files) <br>
> git diff --name-status (show names & status of modified files) <br>
> git diff --stat (stats of modified files) <br>
> git diff -p {commit_hash_1} {commit_hash_2} (compare) <br>
> git diff -patch {commit_hash_1} {commit_hash_2} (compare) <br>
> git diff branchB...branchA (show the diff of what is in branchA that is not in branchB) <br>
> git blame <file_name> (Shows who last modified each line)
> git grep "{string_of_text}" (search for a key word in repo) <br>
> git grep "{string_of_text}" {sub_directory_path}/ (search for a key word in sub dir) <br>
> git grep "{string_of_text}" {branch_name} (search for a key word in branch) <br>
> git grep --cached "{string_of_text}" (search for a key word in staging area) <br>
> git grep --untracked "{string_of_text}" (search for a key word in untracked file) <br>
> git grep -c "{string_of_text}" (Search for the number of matches for a term) <br>


👉 `REFLOG` <br>
Lists the changes made in Git <br>
The git reflog command shows the list of changes made in the Git repository. This command is useful for recovering lost commits caused by merges, rebases and resets, among other actions.
The main difference between the git reflog and git log command is that git reflog shows all the commits and changes of any branch within your repository, including the ones created, modified and deleted. git log only shows the complete commit history of the current (or specified) branch, and therefore doesn’t include commits from other branches or deleted ones.

> git reflog <br>
> git reflog {branch_name} <br>
> git reflog -n {number_of_entries} <br>
> git reflog show --all (log for all references) <br>
> git reflog --pretty=oneline <br>
> git reflog --pretty=short <br>
> git reflog --pretty=medium <br>
> git reflog --pretty=full <br>

### Undo changes 🚨
#### CREATE COPY OF BRANCH FOR SAFETY, AND TEST STRATEGY! <br>
##### REMOVE commit from remote -> reset local and force push.

#### ➡️ Delete file or directory
> git rm {file-name} (permanently delete file from git) <br>
> git rm -f {file_name} <br>
> git clean -n (Dry run for removing untracked files) <br>
> git clean --dry-run (Dry run for removing untracked files) <br>
> git clean -f (remove untracked files) <br>
> git rm -r --cached . (removes files from staging area/index and undoes ADD)<br>
> git rm -r {directory-path}/ (remove directory) <br>
> git rm --cached *.log (remove staged files with .log format from the index) <br>

#### ➡️ Unstage
> git ls-tree --full-tree --name-only -r HEAD (Show tracked files) <br>
> git rm --cached {file_name} (Remove from staging, and undo ADD. Removes the copy of the file from the index / staging-area/ index, without touching the working tree copy. ) <br>
> git rm -r --cached <folder> (removes from index, Undo ADD) <br>
> $ git rm --cached` and `$ git update-index (temporary untrack file) <br>
> $ git update-index --assume-unchanged (temporary untrack file) <br>
> git restore --staged index.html (Undo ADD. Git copies the file from the HEAD commit into the index, without touching the working tree copy. The index copy and the HEAD copy now match, whether or not they matched before. A new commit made now will have the same copy of the file as the current commit.) <br>

#### ➡️ Uncommit
> git reset \[file\] (Not commited file, unstage, but retain changes) <br>
> git reset --soft HEAD^ (Uncommit but keep changes) <br>
> git restore --staged <br>

#### ➡️ Restore a file(s) to original/previous state
Restores an existing file in the working directory to its previous state.
It reverts all unstaged and uncommitted files in the working directory to the version they had in the last commit. This is useful for reversing accidental modifications made to files, similar to how Ctrl + Z is used.
It’s also important to note that this does not affect the staging area or the commit history, so it is generally recommended to discard staged changes using git reset HEAD if you need to record the changes made in the commit history too.

> git restore {file_name} (restore a single file) <br>
> git restore {file_name_1} {file_name_2} <br>
> git restore . (all files) <br>

#### ➡️ RESET takes commit you want to keep (deletes commit and will put this branch behind, will have to use push --force).
In Git, the git reset command is used to undo changes made in the working directory and/or staging area. This is achieved by the HEAD pointer moving to a previous commit, which means any changes since that commit will be permanently deleted.

> git reset --soft {commit_hash} (Reset the commit history only (soft reset)🟢) <br>
This reverts to the commit specified by the user while leaving the changes untouched in the working directory and staging area. In other words, this approach only changes the commit history and not the staging area or working directory.

> git reset {commit_hash} OR git reset --mixed {commit_hash} (Reset the commit history and staging area only (mixed reset)🟡)

This undoes any changes to the commit history and the staging area by resetting the HEAD pointer to the previous (or specified) commit, and therefore will permanently wipe out all staged changes that have not been committed.

> git reset --hard {commit_hash} (Reset the commit history, working tree and staging area (hard reset)🔴) <br>

This approach resets any changes made to the commit history, staging areas and the working directory. This is done by resetting the HEAD pointer to the specified commit.
⚠️Warning: This could impact the work of other colleagues if you’re working on the same repository, so only use this if you know exactly what you’re doing, otherwise consider safer alternatives. <br>

[Article by Stephen David-Williams on medium](https://medium.com/gitconnected/git-commands-i-wish-i-knew-earlier-as-a-developer-a5f9f47d5644)
<br>
 
> git reset HEAD^ (Uncommit and unstaged but keep my file tree) <br>
> git reset --hard HEAD^ (Reset changes to previous commit) <br>
> git push -f

#### ➡️ REVERT takes commit you want to undo, creates an opposit commit and you can push. 

> git revert HEAD <br>
> git revert {commit_hash} <br>
> git revert -m {parent_number} {commit_hash} (Revert a merged commit) <br>
> git revert -i HEAD~n (Revert last commit. Change n to the number of your choice) <br>


##### Strategy 1️⃣
`Reset and use --force to push. `<br>

##### Strategy 2️⃣ 
`Create a branch, use reset, then merge and push.` <br>

##### Strategy 3️⃣
`Use revert and push.` <br>


##### EXAMPLE 1️⃣<br>
👉 If not commited the change:
1) cmd: git reset --hard HEAD (reverts changes to most recent commit)
2) cmd: git checkout HEAD^ -- working_file (restore the file with the previous version)

👉 If committed:
1) cmd: git log (shows all commits, choose desired commit an d type :q to exit log)
2) cmd: git reset --hard \<id of commit\>
3) cmd: git checkout -- filename.txt (undo single file)
4) cmd: git restore filename.txt (undo single file)
5) cmd: git checkout COMMIT_HASH FILE (undi sibgle file to previous commit)
   
##### EXAMPLE 2️⃣<br>
> git revert HEAD (creates new commit which is opposite of an existing commit) <br>
> git revert \< commit number\> <br>
> git revert first-bad-commit^..last-bad-commit <br>

##### EXAMPLE 3️⃣: undelete file <br>
> git checkout deleted_file

##### EXAMPLE 4️⃣: Discard newly added files <br>
> git status <br>
> git clean -n (dry run to see files) <br>
> git clean -f (Removes untracked files) <br>
> git clean -fd (Removes untracked directory) <br>

##### EXAMPLE 5️⃣: Rever changes made to working copy, not staged and not commited <br>
> git checkout . (or: git restore .) <br>

Remote is behind (push desired commit) <br>
git push --force origin 606fdfaa33af1844c86f4267a136d4666e576cdc:master
	

### Merging 🔐
> git checkout master <br>
> git merge new-feature (merges specified branch into your current branch) <br>
> it merge \[alias\]\/\[branch\] (fetch down all the branches from that Git remote) <br>
> git reset --hard {merge_commit_hash} (reverse merging) <br>
> git revert -m {parent_number} {merge_commit_hash} (reverse by creating a new commit) <br>

```
Using the git revert command by typing git revert -m 1 HEAD@{0} into the terminal opens up an interactive session via Vim like so:
The custom message provided by the system should suffice so we can advance by typing Esc + :wq and then hit Enter, which creates the new commit that reverses these changes.
```

### Rebase 📀
Moves or combines a sequence of commits to a new base commit. <br>
In Git, rebasing means integrating the changes made on one branch into another, similar to merging. But instead of maintaining the commit history of the two branches, rebasing rewrites the commit history to produce a cleaner, linear progression of changes.
So rebasing is appending all the commits of one branch to the commits of another one. This makes the commit history of the principal branch a single, clean line of commits but may be difficult to debug if conflicts occur.
⚠️Warning: Use with caution as other developers may be working on the branches you’re rebasing with. Resolving conflicts caused by rebasing can be a painful experience (trust me…I know what I’m talking about)😖

> git rebase {branch_name} <br>
> git rebase --continue (continue after resolving conflicts) <br>


### Branch 🌴
To create a branch locally and remote:<br>
Create locally ➡ checkout to new branch ➡ push to remote.
	
> git branch (shows all branches) <br>
> git branch new-feature (cerating new brtanch named new-feature) <br>
> git checkout -b <branch-name> (create new branch and switch) <br>
> git checkout new-feature (switching to a new branch) <br>
> git branch -r (show remote) <br>
> git branch -a (show all) <br>
> git branch --show-current <br>
> git switch other-branch <br>
> git switch -  # Switch back to previous branch, similar to "cd -" <br>
> git switch remote-branch  # Directly switch to remote branch and start tracking it <br>


#### ➡️ Rename local branch 
> git branch -m \<newname\> <br>
> git branch -m \<oldname\> \<newname\> <br>
> git branch -M \<newname\> (force rename) <br>
> git branch -m old_branch_name new_branch_name <br>

After renaming local branch push like this: <br>
`cmd: git push origin new_branch_name:master` (now changes will go to master branch but your local branch name is new_branch_name)

#### ➡️ Rename remote branch
> git push origin :old-name new-name (Delete the old-name remote branch and push the new-name local branch) <br>
> git push origin -u new-name (reset upstream) <br>
> push --set-upstream origin new_name (another way to set upstream) <br>

#### ➡️ Delete local branch
1) cmd: git branch -d \<branchname> 
2) cmd: git branch -D \<branchname> 

#### ➡️ Delete remote branch
1) git push \<remote_name\> --delete \<branch_name\>
2) git push \<remote_name\> :\<branch_name\> (short command)

### Public to private Fork 🚦	
1) Create empty private repo
2) Bare clone a public repo, and mirror push it to the private repo.
```
$ git clone --bare https://github.com/exampleuser/public_repo.git
$ cd public_repo.git
$ git push --mirror https://github.com/yourname/private_repo.git
$ cd ..
$ rm -rf public-repo.git
```

3) Register remote repository with public repositoryPermalink
```
$ git clone https://github.com/yourname/private_repo.git
$ cd private_repo
$ git remote add public https://github.com/exampleuser/public_repo.git
Fetching from public repoPermalink
$ git pull public master 
$ git push origin master
```

### [Git Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)
### [Git useful commands](https://medium.com/gitconnected/git-commands-i-wish-i-knew-earlier-as-a-developer-a5f9f47d5644)
