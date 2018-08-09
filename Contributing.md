# Contribution Workflow

## Getting changes into master
1. Clone repository.
1. Update `master` with `git pull`.
1. Create and checkout feature branch using `git checkout -b <name>` or `git branch <name> && git checkout <name>`.
1. Make, test and commit changes.
1. Checkout and update local master branch, e.g. `git checkout master && git pull`.
1. Checkout feature branch and rebase master `git checkout <name> && git rebase master`. 
    As there may be multiple commits with conflicts, the following process may need to be repeated:
    - `git` will prompt you to resolve conflicts
    - First resolve the conflicts in a text editor
    - Then `git add` the edited file(s)
    - Then `git rebase --continue`
1. Push to remote using `git push -u origin <name>`.
1. Create pull request on Github and (optionally) assign and notify reviewers.

## Checking out other branches
To review changes made by others:
1. Use `git fetch` to update the local repository. 
1. Use `git checkout <their-branch-name>` to checkout their branch.

## Frequent issues

### Push and rebase and push
If you have pushed to your feature branch before rebase (e.g. in the scenario where you want to save your work and/or maybe have others look at it), it's possible that you may need to do a force push using `git push --force` after rebasing (as history may be rewritten). 

### Forgot to create a feature branch before making changes?
If you have used `git branch <name>` and forgot to checkout the feature branch before making changes (perhaps whilst being on master),
you can checkout the newly branch without losing changes (provided that you haven't committed), and make the commit. 

Alternatively, use `git stash` to stash current changes and use `git stash pop` to unstash the changes on the new branch. 

If have already make a commit, here are 2 methods that you could employ to resolve the problem. 
1. Branch and reset
    1. Delete new branch, `git branch -d <name>`
    1. Branch off from current branch (at the current commit), `git branch <name>`
    1. Reset current branch to previous commit, `git reset HEAD~1 --hard`

2. Reset and cherry-pick
    1. Note hash of current commit
    1. Reset current branch to previous commit, `git reset HEAD~1 --hard`
    1. Checkout new branch
    1. Cherry-pick the (now orphaned) commit, `git cherry-pick <commit-hash>`, to apply it to the new branch

Now, you should have the new branch with the commit that you accidently made on the other branch. 

### Useful commands
- To discard the changes to a file, use `git checkout -- <file-path>`
- To unstage a file, use `git reset <file-path>`

### References
- [Git Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
- [Resolving merge conflicts](https://help.github.com/articles/resolving-merge-conflicts-after-a-git-rebase/)

