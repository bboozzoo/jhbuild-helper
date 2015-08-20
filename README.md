# jhbuild-helper

A tiny `jhbuild` helper for building mutli package projects.

The helper script `jh` will pass your configuration when calling
`jhbuild` along with any command line parameters. By default
`jhbuildrc` from this repo will be used as the configuration file.
This behavior can be changed by setting `JHRC` environment variable to
point to your preferred configuration file.

A limited integration with Emacs, vim and tmux is provided. The
wrapper script tries to find out if it's running under Emacs or vim
and disables `jhbuild`'s interactive mode. An additional command `ss`
(usable under tmux only) pops up a shell (as in `jhbuild shell`) in a
new window.

## Example:

Assuming the following structure:
```
.
├── build
│   ├── jh
│   ├── jhbuildrc
│   ├── my-moduleset.modules
├── buildroot (only if out of source builds are enabled)
│   ├── ...
│   └── my-sample-module
├── my-sample-module (described in moduleset)
│   ├── ...
│   ├── configure
│   ├── configure.ac
│   ├── depcomp
│   ├── Makefile
│   ├── Makefile.am
│   ├── Makefile.in
│   ├── src
│   └── ...
├── install-root (stuff gets installed here)
│   ├── bin
│   ├── etc
│   ├── include
│   ├── _jhbuild
│   ├── lib
│   ├── lib64
│   ├── libexec
│   ├── share
│   └── var
...
```

Add `build` to your `PATH`:

`export PATH=$PWD/build`

Then to build everything:

`jh build`

To build `my-sample-module`:

`jh build my-sample-module`

## eproject-compile helper

An example `.eproject` will setup some predefined compile commands for
`eproject-compile` that invoke the `jh` helper. Typically accessed via
`C-c C-k`.
