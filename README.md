git-pushed
==========

**git-pushed** is a command line tool to get last modified heads from remote git
repository.

## Usage

```
$ git-pushed https://github.com/PauloASilva/node-http-mitm-proxy.git
```
### Remarks

**git-pushed** keeps track of remote repository heads in `$HOME/.cache/git-pushed`.<br />
On first run, because there's no cache, all heads will be reported as they had been changed.

## Motivation

Gitlab fires a jenkins job on push events. jenkins job runs commands over SSH on a remote machine which should checkout the repository, in which the push event occured, if and only if push was done on a specific head.

### Example

```shell
ssh user@remote-machine<<<EOF
    status=$(git-pushed git@gitlab.somehost.com/project.git | grep "ref/heads/development")
    if [ "$status" -ne 0 ]; then
        echo "Nothing to do!"
        exit 0
    fi

    git checkout git@gitlab.somehost.com/project.git -b development

    # some other remote commands
    # ...
EOF
```

## Instalation

* Git checkout
```
$ cd /tmp
$ git checkout https://github.com/PauloASilva/git-pushed.git git-pushed
```
* make `git-pushed` executable
```
$ cd git-pushed
$ chmod a+x git-pushed
```
* copy `git-pushed` to a system location (requires `sudo`)
```
$ sudo cp git-pushed /usr/local/bin
```
