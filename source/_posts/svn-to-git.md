---
title: SVN to Git - Migrating just some branches
date: 2017-05-29 22:51:36
tags:
- svn
- git
---

I recently had to migrate a very old repository (about 15 years of history) from Subversion to Git. There are already
enough guides for this, but I had one extra requirement: **clone just some branches**.

I had to search in several places for all the information I needed to successfully migrate to Git (take a look at the
references at the end of this post), so I decided to share it all in one place.

The trick is to just `init` the repo and then manually select the branches.
I tried this on Windows (using CMDER as the terminal for UNIX commands). Let's get started:


1. Generate list of users from the SVN repo
```bash
svn log --xml | grep author | sort -u | perl -pe 's/.*>(.*?)<.*/$1 = /' | tee users.txt
```

2. Clone svn repo from to git in the 'tmp' directory. Options:
`<repo_url>`: the url of the svn repository
`-T trunk`: specify your trunk path inside the svn repository
`--no-metadata`: removes the SVN commit id from the commit's history. Use this option only when you don't need to update from SVN again.
`--no-minimize-url`: allow the cloning of just subfolders
```bash

git svn init -T trunk <repo_url> --no-metadata --no-minimize-url tmp 
# Go into created directory
cd tmp
```

3. Set the list of users for the commit authors
```bash
git config svn.authorsfile ../users.txt
```

4. Update the '.git/config' file to clone only specific branches.
In this case, we're going to clone only branches that match the pattern 'feature*'
```bash
[svn-remote "svn"]
  noMetadata = 1
  url = <repo_url>
  fetch = trunk:refs/remotes/origin/trunk
  branches = branches/feature*:refs/remotes/origin/*  ## New line
```

5. Get files from the SVN repository. Use an elevated command prompt (administrator rights)
```bash
# Be patient this could take several hours...
git svn fetch
```

6. Checkout the remote branches to keep them in the local repository. Below is an example of checking out the remote
    branches `feature/foo` and `feature/bar` 
```bash
# Make sure the remote branches you want are listed
git branch -r

# Checkout remote branches to keep them in the local repo
# git checkout -b <local_branch> <remote_branch>
git checkout -b feature/foo origin/feature/foo
git checkout -b feature/bar origin/feature/bar
```

7. Clone your git-svn repository into a clean Git repository:
```bash
cd ..
git clone tmp dest_dir
cd dest_dir
```

8. Re-establish branches in the new Git repository
```bash
# git checkout -b <local_branch> <remote_branch>
git checkout -b feature/foo origin/feature/foo
git checkout -b feature/bar origin/feature/bar
```

9. If you want to commit your local repository to an existing Git repository just set the `new-repo-url`
```bash
# Set new repo url
git remote set-url origin <new-repo-url>
```

10. Finally, push all branches to the new remote repository
```bash
git push --all    
```

Another useful thing that I found is that if you don't want to import all the history you could select the revisions to import
in step 5:
```bash
git svn fetch -r $NUMBER:HEAD
```

## References
### Migrating SVN to Git
https://stackoverflow.com/a/3972103/2313246

http://blokspeed.net/blog/2010/09/converting-from-subversion-to-git/

### Cloning a subfolder from the SVN repo
http://stackoverflow.com/questions/1453416/git-svn-clone-checkouts-wrong-repo

### Selecting specific branches
http://stackoverflow.com/a/10173516/2313246

https://gist.github.com/trodrigues/1023167

### Selecting revision range
https://git-scm.com/docs/git-svn#git-svn---revisionltarggt

