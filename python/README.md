### Python

This project comes with both Python `2.7` and `3.4`, which correspond to the
`python` and `python3` commands respectively.

Virtualenv is already installed, and is the recommended way of creating
isolated Python environments.

To start a new `Python 2.7` project:

```shell
cd ~/code
virtualenv myproject
cd ~/code/myproject
source bin/activate
```

For a `Python 3` project, the process is almost exactly the same, only with the python version explicitly specified with `--python`:

```shell
cd ~/code
virtualenv --python=python3 myproject
cd ~/code/myproject
source bin/activate
```
