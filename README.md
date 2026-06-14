# ok
ok tells you whether the last command was okay.

## Usage

```sh
ok install bash && source ~/.bashrc # install shell function into ~/.bashrc
```

After running `ok install bash`, you can just call `ok` after any command — the shell function captures `$?` automatically.

## Output

- `✓ okay` — the command exited with code 0
- `✗ not okay — exit code N (reason)` — the command failed, with a human-readable explanation of common exit codes and signals (e.g. `SIGSEGV`, `SIGKILL`,
  command not found, etc.)
