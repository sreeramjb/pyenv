# Command Reference

Like `git`, the `pyenv` command delegates to subcommands based on its
first argument.

The most common subcommands are:

* [`pyenv commands`](#pyenv-commands)
* [`pyenv local`](#pyenv-local)
* [`pyenv global`](#pyenv-global)
* [`pyenv shell`](#pyenv-shell)
* [`pyenv install`](#pyenv-install)
* [`pyenv uninstall`](#pyenv-uninstall)
* [`pyenv rehash`](#pyenv-rehash)
* [`pyenv version`](#pyenv-version)
* [`pyenv versions`](#pyenv-versions)
* [`pyenv which`](#pyenv-which)
* [`pyenv whence`](#pyenv-whence)


## `pyenv commands`

Lists all available pyenv commands.


## `pyenv local`

Sets a local application-specific Python version by writing the version
name to a `.python-version` file in the current directory. This version
overrides the global version, and can be overridden itself by setting
the `PYENV_VERSION` environment variable or with the `pyenv shell`
command.

    $ pyenv local 2.7.6

When run without a version number, `pyenv local` reports the currently
configured local version. You can also unset the local version:

    $ pyenv local --unset

Previous versions of pyenv stored local version specifications in a
file named `.pyenv-version`. For backwards compatibility, pyenv will
read a local version specified in an `.pyenv-version` file, but a
`.python-version` file in the same directory will take precedence.


### `pyenv local` (advanced)

You can specify multiple versions as local Python at once.

Let's say if you have two versions of 2.7.6 and 3.3.3. If you prefer 2.7.6 over 3.3.3,

    $ pyenv local 2.7.6 3.3.3
    $ pyenv versions
      system
    * 2.7.6 (set by /Users/yyuu/path/to/project/.python-version)
    * 3.3.3 (set by /Users/yyuu/path/to/project/.python-version)
    $ python --version
    Python 2.7.6
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3

or, if you prefer 3.3.3 over 2.7.6,

    $ pyenv local 3.3.3 2.7.6
    $ pyenv versions
      system
    * 2.7.6 (set by /Users/yyuu/path/to/project/.python-version)
    * 3.3.3 (set by /Users/yyuu/path/to/project/.python-version)
      venv27
    $ python --version
    Python 3.3.3
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3


## `pyenv global`

Sets the global version of Python to be used in all shells by writing
the version name to the `~/.pyenv/version` file. This version can be
overridden by an application-specific `.python-version` file, or by
setting the `PYENV_VERSION` environment variable.

    $ pyenv global 2.7.6

The special version name `system` tells pyenv to use the system Python
(detected by searching your `$PATH`).

When run without a version number, `pyenv global` reports the
currently configured global version.


### `pyenv global` (advanced)

You can specify multiple versions as global Python at once.

Let's say if you have two versions of 2.7.6 and 3.3.3. If you prefer 2.7.6 over 3.3.3,

    $ pyenv global 2.7.6 3.3.3
    $ pyenv versions
      system
    * 2.7.6 (set by /Users/yyuu/.pyenv/version)
    * 3.3.3 (set by /Users/yyuu/.pyenv/version)
    $ python --version
    Python 2.7.6
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3

or, if you prefer 3.3.3 over 2.7.6,

    $ pyenv global 3.3.3 2.7.6
    $ pyenv versions
      system
    * 2.7.6 (set by /Users/yyuu/.pyenv/version)
    * 3.3.3 (set by /Users/yyuu/.pyenv/version)
      venv27
    $ python --version
    Python 3.3.3
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3


## `pyenv shell`

Sets a shell-specific Python version by setting the `PYENV_VERSION`
environment variable in your shell. This version overrides
application-specific versions and the global version.

    $ pyenv shell pypy-2.2.1

When run without a version number, `pyenv shell` reports the current
value of `PYENV_VERSION`. You can also unset the shell version:

    $ pyenv shell --unset

Note that you'll need pyenv's shell integration enabled (step 3 of
the installation instructions) in order to use this command. If you
prefer not to use shell integration, you may simply set the
`PYENV_VERSION` variable yourself:

    $ export PYENV_VERSION=pypy-2.2.1


### `pyenv shell` (advanced)

You can specify multiple versions via `PYENV_VERSION` at once.

Let's say if you have two versions of 2.7.6 and 3.3.3. If you prefer 2.7.6 over 3.3.3,

    $ pyenv shell 2.7.6 3.3.3
    $ pyenv versions
      system
    * 2.7.6 (set by PYENV_VERSION environment variable)
    * 3.3.3 (set by PYENV_VERSION environment variable)
    $ python --version
    Python 2.7.6
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3

or, if you prefer 3.3.3 over 2.7.6,

    $ pyenv shell 3.3.3 2.7.6
    $ pyenv versions
      system
    * 2.7.6 (set by PYENV_VERSION environment variable)
    * 3.3.3 (set by PYENV_VERSION environment variable)
      venv27
    $ python --version
    Python 3.3.3
    $ python2.7 --version
    Python 2.7.6
    $ python3.3 --version
    Python 3.3.3


## `pyenv install`

Install a Python version (using [`python-build`](https://github.com/pyenv/pyenv/tree/master/plugins/python-build)).

    Usage: pyenv install [-f] [-kvp] <version>
           pyenv install [-f] [-kvp] <definition-file>
           pyenv install -l|--list

      -l/--list             List all available versions
      -f/--force            Install even if the version appears to be installed already
      -s/--skip-existing    Skip the installation if the version appears to be installed already

      python-build options:

      -k/--keep        Keep source tree in $PYENV_BUILD_ROOT after installation
                       (defaults to $PYENV_ROOT/sources)
      -v/--verbose     Verbose mode: print compilation status to stdout
      -p/--patch       Apply a patch from stdin before building
      -g/--debug       Build a debug version

To list the all available versions of Python, including Anaconda, Jython, pypy, and stackless, use:

    $ pyenv install --list

Then install the desired versions:

    $ pyenv install 2.7.6
    $ pyenv install 2.6.8
    $ pyenv versions
      system
      2.6.8
    * 2.7.6 (set by /home/yyuu/.pyenv/version)

## `pyenv uninstall`

Uninstall a specific Python version.

    Usage: pyenv uninstall [-f|--force] <version>

       -f  Attempt to remove the specified version without prompting
           for confirmation. If the version does not exist, do not
           display an error message.


## `pyenv rehash`

Installs shims for all Python binaries known to pyenv (i.e.,
`~/.pyenv/versions/*/bin/*`). Run this command after you install a new
version of Python, or install a package that provides binaries.

    $ pyenv rehash


## `pyenv version`

Displays the currently active Python version, along with information on
how it was set.

    $ pyenv version
    2.7.6 (set by /home/yyuu/.pyenv/version)


## `pyenv versions`

Lists all Python versions known to pyenv, and shows an asterisk next to
the currently active version.

    $ pyenv versions
      2.5.6
      2.6.8
    * 2.7.6 (set by /home/yyuu/.pyenv/version)
      3.3.3
      jython-2.5.3
      pypy-2.2.1


## `pyenv which`

Displays the full path to the executable that pyenv will invoke when
you run the given command.

    $ pyenv which python3.3
    /home/yyuu/.pyenv/versions/3.3.3/bin/python3.3

Use --nosystem argument in case when you don't need to search command in the 
system environment.

## `pyenv whence`

Lists all Python versions with the given command installed.

    $ pyenv whence 2to3
    2.6.8
    2.7.6
    3.3.3
    
    
    
    
    
    ########### Virtual Environment ################
    # Ben's VirtualEnv Cheatsheet #

This cheat sheet describes my usage/implementation of virtualenv with virtualenv wrapper and the bash foo that I added with the help of many blogs to make it all tick together in fun land. 

**Quick Reference**

    $ echo $WORKON_HOME
    /Users/benjamin/.virtualenvs

    $ echo $PROJECT_HOME
    /Users/benjamin/Repos/git/

## Commands ##

All of the commands below are to be used on the Terminal Command line.

#### venv ####
List or change working virutal environments (alias `workon`)

    venv [environment_name]

#### venv.exit ####
Switch from the virtual environment back to system Python (alias `deactivate`)
    
    venv.exit
    
#### venv.ls ####
List all of the environments (alias `lsvirtualenv`)

    venv.ls [-b] [-l] [-h]

`-b` Brief mode, disables verbose output
`-l` Long mode, verbose output, default
`-h` Print help

#### venv.show ####
Show the details for a single virtualenv
    
    venv.show [env]

#### venv.init ####
Create a new environment in the `WORKON_HOME` (alias `mkvirtualenv`)

    venv.init ENVNAME
    venv.init [-a project_path] [-i package] [-r requirements.txt] [virtualenv opts] ENVNAME

#### venv.rm ####
Remove an environment in the `WORKON_HOME` (alias `rmvirtualenv`). Note that you must be deactivated before you can remove the current environment.
    
    venv.rm ENVNAME

#### venv.switch ####
A semantic alias for `venv` (e.g. `workon`) to faciliate switching to other virtual environments.
    
    venv.switch ENVNAME

#### venv.add ####
Adds the specified directories to the Python path for the currently active virutal environment (alias `add2virtualenv`). Useful for providing non-pip packages or local development packages into the enivronment without messing with .pth files.
    
    venv.add dirpath dirpath ..

#### venv.cd ####
Changes the current working directory to the one specified as the project directory for the active virtual env (alias `cdproject`). Note that you must have the project specified.
    
    venv.cd

#### venv.cdsp ####
Changes the current working directory to the `site-packages` directory of the current virtual environment (alias `cdsitepackages`).
    
    venv.cdsp [subpackage]

#### venv.cdenv ####
Changes the current working directory to the directory of the current virtual environmment (alias `cdvirtualenv`).
    
    venv.cdenv [subdir]

#### venv.lssp ####
Lists the contents of the site-packages directory in the current active virtual environment (alias `lssitepackages`).

    venv.lssp

#### venv.proj ####
Create a new virtualenv and a new project directory in associated HOME directories (alias `mkproject`).
    
    venv.proj [-f|--force] [-t template] [virtualenv opts] ENVNAME

#### venv.setproj ####
Bind an existing virtualenv to an existing project (alias `setvirtualenvproject`)

    venv.setproj [virtualenv_path project_path]

An association is made so thtat when venv activtes the virtualenv the project is also activated. 

Note that if no arguments are provided, the current virtualenv and the current working directory are assumed.

#### venv.wipe ####
Remove all of the installed third-party packages in the current virtualenv (alias `wipeenv`).
    
    venv.wipe

### Dependencies ###

In order to make this happen you need to install the following:
    
* pip
* virtualenv
* virtualenvwrapper

## Appendix: .bash_profile ##
 
    # virtualenv
    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/Repos/git/
    source /usr/local/bin/virtualenvwrapper.sh
    
    alias venv="workon"
    alias venv.exit="deactivate"
    alias venv.ls="lsvirtualenv"
    alias venv.show="showvirtualenv"
    alias venv.init="mkvirtualenv"
    alias venv.rm="rmvirtualenv"
    alias venv.switch="workon"
    alias venv.add="add2virtualenv"
    alias venv.cd="cdproject"
    alias venv.cdsp="cdsitepackages"
    alias venv.cdenv="cdvirtualenv"
    alias venv.lssp="lssitepackages"
    alias venv.proj="mkproject"
    alias venv.setproj="setvirtualenvproject"
    alias venv.wipe="wipeenv"
