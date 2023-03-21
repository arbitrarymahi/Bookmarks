### Table of Content
* <a href="basics">Basics<a/>
* <a href="git-submodules">Git Submodules<a/>
 
`git <command> --help` : opens mannual for that command in browser. ex: `git add --help`  
### Basics
 <details>
  
 * `git status`
    * provides a summary of the current branch. files that are staged, committed, untracked etc.
 * `git add <files>`
    * stage files for commit
 * `git commit -m "msg"`
    * commit files with a message
 * `git commit --amend`
    * to modify the most recent commit and push again, saves creating another commit id. usually for patches after review.
 * `git commit --amend -m "new msg"`
     * change commit message of the last commit
 * `git commit --amend --no-edit`
    * to modify the most recent commit without changing the commit message.
 * `git restore`
    * Used to revert modified file content to last commited contents.(Discard changes)
    * `git restore filename`
    * Used to unstage files added for staging.
    * `git restore --staged filename`
 * `git log`
    * generates a log of most recent commits in current branch. Each branch has its own series of logs.
  * `git branch <branch_name>`
     * create a new branch
 * `git checkout <branch/commit-id>`
    * This can be used to change branch(head points to another branch) or go to a certain commit(detach head and point it to some commit)
    * A head points to some branch. When head is detached, it doesn't point to a branch but some independent commit point in history. From there we can create new branch if need be.
 * `git checkout -b <branch_name>`
     * creates a new branch and checks it out also.     
 * `git rm [-f] <filename>`
     * remove a file. {-f = forcefully}
 * `git merge <other_branch>`
     * merge/bring the contents of other branch with/into current branch
 </details>
     
### working with remote repository (GitHub/GitLab)
<details>
    
* `git clone <url>`
    * clone a repo from remote location like GH.
* `git remote [other options]`
    * The git remote command lets you manage(create, view, and delete) connections to other(remote) repositories.
    * origin is the repo from which we clone.(usually it is called origin) we can name it something else also.
    * We can use the remote command with other subcommands, to do various options. like add origin(or some other repo), show url of remote repo etc.
    * https://www.git-tower.com/learn/git/commands/git-remote
    * https://www.atlassian.com/git/tutorials/syncing
    * `git remote show` 
        * shows all remote repos connection. They are used as names instead of URLs for convenience.
    * `git remote add <origin> <url>`
        * only needed if we create repo locally first then want to put on GH. or we want to add another remote repo. <origin> can be anything. it's just a convention to call it origin.
        * connects local git repo with a remote repo and add an alias(origin) for the remote repo url. (we call the remote repo by the name origin)
* `git push [-u] <remote(origin)> <branch>`
    * Ex: `git push -u origin main`
    * `-u` means upstream, therefore we are downstream.
    * <branch> name of origin for connecting with(tracking) our current branch. if our branch name is diff then remote it'll still work, but we should keep them same for simplicity.
* `git pull <repo_url> <branch>`
    * pull changes from remote repo into the current branch. 
    * Pull is used to update our current repo with new changes from remote.Ex: new commits
 
</details>

### Rebase
 
    * Usually, when we do some development, we split our own branch(say sidebranch), make some changes and then merge it to main. The point of split is the base for the new branch. 
    * Now, Before merging, if the main branch also gets some more commits, then it has moved ahead from the base of our(sidebranch) branch. If we want to merge here, we'll need to resolve conflicts, which is normal.
    * Otherwise, we can rebase to current commit of main, which deletes the branch(sidebranch) from history and log thinks that it was always on main and not merged. so basically the base of that sidebranch was changed and placed on top of current commit of node. Now if main and sidebranch fork(split) again then base of sidebranch is newer commit. Without rebasing it would've been older one.
    * We still need to resolve conflicts in case of merging.
    
### Git Submodules:
 <details>
  
* https://www.youtube.com/watch?v=8Z4Cmhji_FQ&ab_channel=GitKraken
* https://www.atlassian.com/git/tutorials/git-submodule
* https://www.vogella.com/tutorials/GitSubmodules/article.html
* https://git-scm.com/book/en/v2/Git-Tools-Submodules
 </details>
