# subtree-test

This repo serves as an example of using subtrees to organize shared frontend code in a rails application.

### How does it work?

We are using a [git subtree](https://www.atlassian.com/blog/git/alternatives-to-git-submodule-git-subtree) inside the `subtree` folder in `app/assets/stylesheets`. This generate local copies of the files of the [other project](https://github.com/scumah/subtree-test-frontend), so they work just as they do on every other rails project.

### How was the subtree added

First we need two repos, [one with the shared code](https://github.com/scumah/subtree-test-frontend), and the one that's using it, which is this very same repo.

Then, to add the subtree we need to:

```bash
git subtree add --prefix app/assets/stylesheets/subtree https://github.com/scumah/subtree-test-frontend.git master --squash
```

This creates a local copy of the shared repo in this one. We can use all the created files normally.

To update the shared code from this repo, we need to:

```bash
git subtree pull --prefix app/assets/stylesheets/subtree https://github.com/scumah/subtree-test-frontend.git master --squash
```

### Caveats

 - **All changes in the shared code should be done in the shared repo**, not in this one.
 - There are probably ways of sharing only folders of the project, but right now we are sharing everything.
