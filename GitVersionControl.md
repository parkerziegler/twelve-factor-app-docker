## Use Git Flow as a Reliable Version Control Model
**Git flow** as a technique for version control that is particularly suited to scaling teams. By default `git` repositories are created on the `master` branch.

```bash
git init
git add README.md
git commit -m "Initial commit."
git remote add origin git@github.com:parkerziegler/example.git
git push -u origin master
```

The `develop` branch of a twelve-factor app always contains completed features and fixes – it is the working tree of the source repository.

```bash
git checkout -b develop
git push -u origin develop
```

All new development is done on a `feature` branch off of `develop`, prefixed as `feature/`. This keeps all development related to individual features isolated.

```bash
git checkout -b feature/chart develop
git add chart.js
git commit -m "Add chart to feature/chart branch."
git push -u origin feature/chart
```

When you finish your feature, it is merged back into the `develop` branch usually through a pull request. This allows it to pass a full code review by another developer.

When you're worried that updates from a `remote origin` may cause conflicts with your local changes, `rebase` your branch. This will `pull` from the `remote origin` and replay your local commits on top of it.

```bash
git rebase develop
```

When you are ready to release, create a `release` branch off of `develop`, prefixed with `release/<version-number>`. 

```bash
git checkout -b release/1.0
```

After a release, we merge `release` back into `develop` to ensure that all changes get applied to the working tree. We also want to merge `release` back into `master` once it has been deployed. This is done via pull requests. When we are ready to push it to up to be published, we `tag` it with the version number.

```bash
git tag v1.0.0
git push -u v1.0.0
```

**Hotfixes** can be used to make emergency changes to released code or the `master` branch when an issue arises. Hotfix branches are prefixed `hotfix/`. Make sure that hotfixes get merged into both `master` and `develop` so changes aren't lost.

Finally, when releases are complete it is generally a good idea to delete all development branches (`feature`, `hotfix`, `release`) that contributed to that deployment, and start the next set of branching of a fresh copy of `develop`.