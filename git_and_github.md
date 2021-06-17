# Git and Github

Git has a ton of useful features, but I won't be able to build muscle-memory on most of them (because I'll be using Git to track changes in my personal repositories, not collaborative ones).
So, I've decided to document my learning in the meantime!

## Configuring Git

```shell
git config --global user.name "Maya Angelou"
git config --global user.email MayaAngelou@poets.com
```

For the most part, this is all the code you need.
This information you enter with `git config` can be found at `~/.gitconfig`.

## Setting up a repository

```shell
git init
touch .gitignore
git add .gitignore
git commit -m "Added .gitignore"
git branch -m main
```

This part is pretty self explanatory.
Don't forget to add `.gitignore` to hide sensitive information, and to rename (`-m`) the `master` branch to `main` (more on the reason [here](https://www.theserverside.com/feature/Why-GitHub-renamed-its-master-branch-to-main)).
Also, remember that changing a branch name only works after the first commit.

## Inspecting a repository

The following code is useful in inspecting the status of the "three trees": the working directory, the staged snapshot, and the commit history.

```shell
git status
git log --oneline
```

![The three trees](https://wac-cdn.atlassian.com/dam/jcr:0c5257d5-ff01-4014-af12-faf2aec53cc3/01.svg?cdnVersion=1527)

## Syncing to Github

You can link to a remote repository with the following code.

```shell
git remote add <alias> <url>
```

Entering `git remote` alone will list all the remote repositories you've entered. `add` is the sub-command that adds the `alias` of the remote repo (usually `origin`) and its `url`.

You can push to the remote repo with:

```shell
git push -u <alias> <branch>
```

`git push` is the main command, and the `-u` flag tells Git that you're entering the default upstream repo (meaning `git push` will default to what you just entered).
Typically, you enter `origin` for the alias and `main` for the branch (this is the branch name of the remote repo).
You can view all the data you entered in `.git/config`.

## Personal access token

I want to add a section here about using a personal access token (PAT).
[Github is no longer accepting passwords when authenticating operations](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/), so I'm switching over to PAT.
I'm following the guide [here](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Reviewing and undoing commits

Okay, this is where things get a bit complicated.
I've tried to break this part down into several sections.

### Reviewing an old commit

Suppose you want to look back at all your files in a previous commit.
You can get the previous commit hash with `git log --oneline` and run:

```shell
git checkout <commit hash>
```

After reviewing, you can go back to the current file state with `git checkout main`.

You can retrieve a file with `git checkout <commit hash> <file path>`; however, I do believe this will discard the current version of your file (if pre-commit) so be careful.

### Comparing changes between files

`git diff` is a flexible command that allows you to compare two files.
By default, `git diff` will show you any uncommitted changes since the last commit.
You can also specify the comparisons you want to make.
Here are some examples:

```shell
git diff origin/main main
git diff <commit hash (older)> <commit hash (newer)>
```

Just make sure that the older (or original) commit hash comes first, and the newer (or modified) commit hash comes second.

### Undoing a commit

Suppose you made a commit erroneously and want to go back.
In that case, you can use `git reset <commit hash>`, which takes you back to whatever commit you specified.
This defaults to `git reset --mixed <commit hash>`, which reverts the Staging Area and Commit History, but not the Working Directory.
There are three flags in total and I've summarized the results below.

- `--hard`: Resets Working Directory, Staging Area, and Commit History
- `--mixed`: Resets Staging Area and Commit History
- `--soft`: Resets Commit History

So, if you preform a `--soft` reset, `git commit` will bring you right back to where you just started from.

Note: all of this is easier if you haven't pushed to `origin` yet.
If you have, I recommend using `git revert` instead.
Otherwise, you will have to use `git push -f`, which forces the `push`, which is not recommended when used collaboratively (so it's likely best that you don't build the muscle-memory for this when working individually too).

More information on `git push` from this article [here](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset).

### Amending the most recent commit

Perhaps this is the best option when you've made a mistake with the commit message.

```shell
git commit --amend -m "an updated commit message"
```

The `--amend` flag can also be useful when forgetting to add a file, or if you find a typo in the file you just committed.

```shell
# the initial commit
git add <file_one>
git commit

# amending the commit after you realized the error
git add <file_one> <file_two>
git commit --amend --no-edit
```

Again, this is most effective when you haven't pushed to Github!

### Reverting a commit

Lastly, let us look at `git revert`, which allows us to go to back to a previous commit without losing history (which is important for the integrity of revision history and reliable collaboration).
This is useful if we have already pushed to Github, but want to go back to a previous commit.
To revert the current commit, we can run the following.

```shell
git revert HEAD
```

Reverting multiple commits at a time appears to be much more complicated and a case-by-case.

## Commands to look into in the future

This is all for now.
But, in the future, I would like to look into:

- `git branch`
- `git pull`
- `git rebase`
