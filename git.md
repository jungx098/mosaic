# Git Cheat Sheet

-------------------------------------------------------------------------------

# Github fork sync

- Repository sync between upstream and fork

## Config upstream

```sh
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
$ git remote add upstream git@bitbucket.org:ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

## Sync

### Option 1. Creates a merge commit

```sh
$ git fetch upstream
$ git merge upstream/master
```

### Option 2. Fork rebase; local change replay on top of upstream/master

```sh
$ git fetch upstream
$ git rebase upstream/master
```

## Related docs

- [https://help.github.com/articles/configuring-a-remote-for-a-fork/](https://help.github.com/articles/configuring-a-remote-for-a-fork/)
- [https://help.github.com/articles/syncing-a-fork/](https://help.github.com/articles/syncing-a-fork/)

-------------------------------------------------------------------------------

# Github origin update

## Remote URL change

```sh
$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

## Related docs

- [https://help.github.com/articles/changing-a-remote-s-url/](https://help.github.com/articles/changing-a-remote-s-url/)

-------------------------------------------------------------------------------

# Git branch delete

## Local branch normal delete

```sh
$ git branch -d BRANCH_NAME
```

## Local branch force delete

```sh
$ git branch -D BRANCH_NAME
```

## Remote branch delete

```sh
$ git push origin -d BRANCH_NAME
```

-------------------------------------------------------------------------------

# Git patch from commit and apply

## Patch format

Prepare `n` patches from `<commit>` to `<commit> - n + 1` for e-mail submission

```sh
$ git format-patch -n <commit>
```

## Patch apply

Apply a series of patches from a mailbox and create commits

```sh
$ git am < file.patch
```

## Related docs

- [https://stackoverflow.com/questions/6658313/how-can-i-generate-a-git-patch-for-a-specific-commit](https://stackoverflow.com/questions/6658313/how-can-i-generate-a-git-patch-for-a-specific-commit)

-------------------------------------------------------------------------------

# Git push specific commit

Push `<commit SHA>` to `<remotebranchname>` at `<remotename>`

```sh
$ git push <remotename> <commit SHA>:<remotebranchname>
```

Gerrit push master; push `<a_local_branch_name or specific_commit or HEAD>` to the remote branch of `refs/for/master` at `origin`

```sh
$ git push origin <a_local_branch_name or specific_commit or HEAD>:refs/for/master
```

Gerrit push draft;  push `<a_local_branch_name or specific_commit or HEAD>` to the remote branch of `refs/draft/master` at `origin`

```sh
$ git push origin <a_local_branch_name or specific_commit or HEAD>:refs/drafts/master
```

Push specific commit to a new remote branch

```sh
git push -u origin REF_ID:refs/heads/BRANCH_NAME
```

## Related docs

- [https://git-scm.com/docs/git-push](https://git-scm.com/docs/git-push)
- [https://stackoverflow.com/a/3230241](https://stackoverflow.com/a/3230241)
- [https://stackoverflow.com/a/19158747](https://stackoverflow.com/a/19158747)

-------------------------------------------------------------------------------

# Multibyte Character Display

Disable `quotepath` for appropriate display of multibyte characters; `git` quotes and escape unusual characters with backslashes.

```sh
$  git config --local core.quotepath false
```

-------------------------------------------------------------------------------

# Git branch name change

## Change the current branch name

```sh
$ git branch -m new-branch-name
```

## Change a specific branch name
```sh
$ git branch -m old-branch-name new-branch-name
```

-------------------------------------------------------------------------------

# Git File Mode Change when Filemode Disabled

```sh
$ git update-index --chmod=+x filename
$ git update-index --chmod=-x filename
```

Run `git update-index --help` for the details.

-------------------------------------------------------------------------------

# Bare Repository

## Setup Bare Repository

In repo folder,

```sh
$ git init --bare foo.git
```

## Push Initial Commit

In project folder,

Change remote origin url, or
```sh
$ git remote set-url origin /Repos/foo.git
```

Add remote origin url,
```sh
$ git remote add origin /Repos/foo.git
```

Push origin master.
```sh
$ git push origin master
```
