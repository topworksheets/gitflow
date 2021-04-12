# git-flow (TopWorksheets Edition)

A collection of Git extensions to provide high-level repository operations
for Vincent Driessen's [branching model](http://nvie.com/git-model "original
blog post"). This fork adds functionality not added to the original branch and
customizations done by TopWorksheets.


## Installing git-flow

Use the following command to install the latest stable version:

```shell
curl -sL https://github.com/topworksheets/gitflow/raw/master/contrib/gitflow-installer.sh | sudo bash -s install stable
```


## Integration with your shell

Use this [fork of git-flow-completion](https://github.com/petervanderdoes/git-flow-completion)
which offers tab-completion for git-flow subcommands and branch names.


## Settings

These are the settings that have to be applied after installing the scripts.

```shell
git config gitflow.multi-hotfix yes
git config gitflow.showcommands yes

git config gitflow.feature.start.fetch yes
git config gitflow.feature.start.force-pull yes
git config gitflow.feature.finish.squash yes
git config gitflow.feature.finish.rebase yes
git config gitflow.feature.finish.push yes
git config gitflow.feature.finish.force-delete yes
git config gitflow.feature.finish.force-pull yes
git config gitflow.feature.rebase.fetch yes

git config gitflow.hotfix.start.fetch yes
git config gitflow.hotfix.start.force-pull yes
git config gitflow.hotfix.finish.fetch yes
git config gitflow.hotfix.finish.squash yes
git config gitflow.hotfix.finish.notag yes
git config gitflow.hotfix.finish.nobackmerge yes
git config gitflow.hotfix.finish.push yes
git config gitflow.hotfix.finish.force-delete yes
git config gitflow.hotfix.finish.force-pull yes
git config gitflow.hotfix.rebase.fetch yes
```

## License terms

git-flow is published under the FreeBSD License, see the
[LICENSE](LICENSE) file. Although the FreeBSD License does not require you to
share any modifications you make to the source code, you are very much
encouraged and invited to contribute back your modifications to the community,
preferably in a Github fork, of course.


## git flow usage

### Initialization

To initialize a new repo with the basic branch structure, use:

    git flow init [-d]

This will then interactively prompt you with some questions on which branches
you would like to use as development and production branches, and how you
would like your prefixes be named. You may simply press Return on any of
those questions to accept the (sane) default suggestions.

The ``-d`` flag will accept all defaults.

![Screencast git flow init](http://i.imgur.com/lFQbY5V.gif)

### Creating feature/release/hotfix/support branches

* To list/start/finish/delete feature branches, use:

```shell
git flow feature
git flow feature start <name> [<base>]
git flow feature finish <name>
git flow feature delete <name>
```

  For feature branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To push/pull a feature branch to the remote repository, use:

```shell
git flow feature publish <name>
git flow feature track <name>
```

* To list/start/finish/delete release branches, use:

```shell
git flow release
git flow release start <release> [<base>]
git flow release finish <release>
git flow release delete <release>
```

  For release branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To list/start/finish/delete hotfix branches, use:

```shell
git flow hotfix
git flow hotfix start <release> [<base>]
git flow hotfix finish <release>
git flow hotfix delete <release>
```

  For hotfix branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

* To list/start support branches, use:

```shell
git flow support
git flow support start <release> <base>
```

  For support branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

### Share features with others

You can easily publish a feature you are working on. The reason can be to allow other programmers to work on it or to access it from another machine. The publish/track feature of gitflow simplify the creation of a remote branch and its tracking.

When you want to publish a feature just use:
```shell
git flow feature publish <name>
```

or, if you already are into the `feature/<name>` branch, just issue:
```shell
git flow feature publish
```

Now if you execute `git branch -avv` you will see that your branch `feature/<name>` tracks `[origin/feature/<name>]`. To track the same remote branch in another clone of the same repository use:
```shell
git flow feature track <name>
```

This will create a local feature `feature/<name>` that tracks the same remote branch as the original one, that is `origin/feature/<name>`.

When one developer (depending on your work flow) finishes working on the feature he or she can issue `git flow feature finish <name>` and this will automatically delete the remote branch. All other developers shall then run:
```shell
    git flow feature delete <name>
```

to get rid of the local feature that tracks a remote branch that no more exist.

### Share hotfixes with others

You can publish an hotfix you are working on. The reason can be to allow other programmers to work on it or validate it or to access it from another machine.

When you want to publish an hotfix just use (as you did for features):
```shell
git flow hotfix publish <name>
```

or, if you already are into the `hotfix/<name>` branch, just issue:
```shell
git flow hotfix publish
```

Other developers can now update their repositories and checkout the hotfix:
```shell
git pull
git checkout hotfix/<name>
```
and eventually finish it:
```shell
git flow hotfix finish
```


### Using Hooks and Filters

For a wide variety of commands hooks or filters can be called before and after
the command.
The files should be placed in .git/hooks
In the directory hooks you can find examples of all the hooks available.