# jjw

An interactive terminal browser for Jujutsu workspaces and Git worktrees, with reports and confirmed cleanup.

## Interactive browser

Run `jjw` in a terminal to open the browser. Use `/` to filter, `s` to cycle sort fields, `v` to reverse order, `u` to check dirty state, `z` to measure workspace size, and `Ctrl-R` to rescan. State and size checks run in the background.

## Reports

Use `jjw list` for tables, JSON, or TSV output:

```sh
jjw list
jjw list --check-state
jjw list --format json
jjw list --format tsv
jjw list --sort last-change
jjw list --sort size
jjw list --size --format json
```

Sort fields include `last-change`, `age`, `created`, `size`, `name`, `repository`, `state`, and `action`. Size is measured on request; table sizes use decimal units and structured output retains exact bytes. `--age-basis` selects last change or creation time for age calculations.

The default Jujutsu workspace is omitted unless `--with-default` is supplied. A path shared by Jujutsu and Git is reported once.

## Cleanup

Run `jjw cleanup` to filter candidates and select them with `fzf`. The command rechecks status and age after confirmation, then forgets Jujutsu workspaces or removes Git worktrees without forcing removal. Current, dirty, unknown, and repository-root paths are protected.

## Requirements and build

Requires Go 1.26 or newer, Jujutsu, and Git. Cleanup selection also uses `fzf`.

```sh
go build -o jjw .
```

The Nix package wraps the binary with its runtime tools on `PATH`; packaging and workstation integration live in [nixfiles](https://github.com/astahmer/nixfiles).

## License

MIT
