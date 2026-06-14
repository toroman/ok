# ok
ok tells you whether the last command was okay.

Check the PRESS.md for the press release.

## Project Motto

Everything is going to be ok.


## Basic usage

Run something, then check whether it was ok.

```
$ sleep 10  # and CTRL+C immediately
$ ok
✗ not okay — exit code 130 (SIGINT — Ctrl-C, the universal 'nope')
```


## Install

```sh
ok install && source ~/.bashrc  # or ~/.zshrc for zsh; fish reloads automatically
```

Or specify your shell explicitly:

```sh
ok install bash|zsh|fish
```

## Usage

After installing, just call `ok` after any command — the shell function captures `$?` automatically:

```sh
cargo build
ok
# ✓ okay, nailed it

npm test
ok
# ✗ not okay — exit code 1 (general error)
```

You can also pass an exit code directly:

```sh
ok 139
# ✗ not okay — exit code 139 (SIGSEGV — segmentation fault (memory said no))
```

## Idiomatic use

Run a command and immediately check it:

```sh
make && ok
```

Check after a long-running command you may have walked away from:

```sh
sleep 60; ok
```

Use in a sequence to get feedback at each step:

```sh
./configure && make && ok
```

Chain with `||` to only report on failure:

```sh
./deploy.sh || ok
```

Use `ok &&` as a readable checkpoint between steps — no backslashes needed:

```sh
ls /some/folder
ok && cd /some/folder
ok && du .
ok && false
ok || echo "That didn't work for some reason"

```

Each step only runs if the previous one succeeded, and you get feedback at every stage.

## Output

- `✓ okay` — exit code 0, with a randomly selected encouraging message
- `✗ not okay — exit code N (reason)` — non-zero exit, with a human-readable explanation of common exit codes and signals (e.g. `SIGSEGV`, `SIGKILL`, command not found, etc.)

`ok` passes through the original exit code, so it's safe to use in scripts and pipelines.
