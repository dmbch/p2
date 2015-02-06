# P2 git repo manager

P2 is a small set of bash scripts meant to be used with [git-shell][gs] and git's post-receive [hook][gh] to enable [heroku][hk]-style git push initiated builds and deployments. It's only really tested on recent versions of Ubuntu Linux. And of course, it uses [docker][dr] if available.


## Usage

Clone this repo into your home folder on a remote server:

```text
git clone https://github.com/dmbch/p2.git ~/git-shell-commands
```

Launch git-shell - you should see output similar to this:

```text
$ git-shell
 ____  ____
(  _ \(___ \
 ) __/ / __/
(__)  (____)  https://github.com/dmbch/p2

Saúde, dmbch! P2 is a git repo manager.
Available commands (type 'exit' to leave):

create
debug
deploy
destroy
help
list

git>
```


Now, you can create (list, destroy) bare git repos that you can use as remote build machines. Every repo you create will be wired to work with p2 automatically:

Whenever you `git push` to it, the p2 deploy script will be run which in turn checks if there is an executable `p2file` in your repo. If `p2file` exists, it'll be called with the current git branch, project and repo location as arguments.


## Commands

`deploy <repo> <branch>`

This is the very script that is run after pushing commits. It takes two required arguments, a repository name and a branch name. The `<repo>` and `<branch>` arguments are required.


`debug`

Enable or disable debug mode: Run grunt in verbose mode, log all output to `~/debug` and dump a worktree tarball there, too.


`list`

List all managed repositories (and respective urls) for current user.


`create <repo>`

Create a new managed repository. The `<repo>` argument is required.


`destroy <repo>`

Delete a managed repository. The `<repo>` argument is required.


[gs]: http://git-scm.com/docs/git-shell
[gh]: http://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks
[hk]: https://devcenter.heroku.com/articles/git
[dr]: https://www.docker.com