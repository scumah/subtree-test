# subtree-test

This repo serves as an example of using subtrees to organize shared frontend code in a rails application.

### How does it work?

We are using a [git subtree](https://www.atlassian.com/blog/git/alternatives-to-git-submodule-git-subtree) inside the `subtree` folder in `app/assets/stylesheets`. This generate local copies of the files of the [sub-project](https://github.com/scumah/subtree-test-frontend), so they work just as they do on every other rails project.

### How was the subtree added

First we need two repos, [one sub-project with the shared code](https://github.com/scumah/subtree-test-frontend), and the parent one that's using it, which is this very same repo.

Then, to add the subtree we need to:

```
git subtree add --prefix app/assets/stylesheets/subtree https://github.com/scumah/subtree-test-frontend.git master --squash
```

This creates a local copy of the sub-project repo in this parent one. We can use all the created files normally.

To update the shared code from the parent repo, we need to:

```
git subtree pull --prefix app/assets/stylesheets/subtree https://github.com/scumah/subtree-test-frontend.git master --squash
```

### Pushing code to the sub-project from the parent repo

Just work as usual with no worries. When everything is commited in the parent repo and you are ready to push, run:

```
git subtree push --prefix app/assets/stylesheets/subtree https://github.com/scumah/subtree-test-frontend.git pull-request-branch
```

Since git is smart enough to filter out files and commits and only pushes changes in the sub-project folder, this will create a new branch named `pull-request-branch` in the sub-project with the changes made from the parent repo.

### Caveats

 - There are probably ways of sharing only folders of the project, but right now we are sharing everything.
