# asdf-vars
An asdf extension that safely sets global and per-project environment variables, based upon rbenv

This is basically a port of the [rbenv-vars plugin](https://github.com/rbenv/rbenv-vars/).

# Install

Make sure you already have [asdf](https://github.com/asdf-vm/asdf#setup) installed before following these steps.

```bash
asdf plugin add vars https://github.com/excid3/asdf-vars
```

Add the following to `~/.asdf/lib/commands/command-exec.bash` before it executes the shim.

```bash
eval "$($ASDF_DIR/bin/asdf vars)"
with_shim_executable "$shim_name" exec_shim || exit $?
```

# Usage

Define environment variables in an `.asdf-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    RUBY_GC_MALLOC_LIMIT=50000000
    RUBY_HEAP_MIN_SLOTS=15000
    RUBY_FREE_MIN=4096

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `GEM_PATH`:

    GEM_PATH=$GEM_PATH:/u/shared/gems

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.asdf/vars` file will be set
first. Then variables specified in `.asdf-vars` files in any parent
directories of the current directory will be set. Variables from the
`.asdf-vars` file in the current directory are set last.

# Author

* [Chris Oliver](https://github.com/excid3)

# License

© 2018-2020 Chris Oliver. Released under the MIT license. See LICENSE for details.
