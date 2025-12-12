# `~/.claude`

This folder contains configurations to be put in your home directory (`~/` or `$HOME`).

> [!TIP]
> Remember to back up your home directory before making changes.
>
> ```sh
> cp -r ~/.claude ~/claude_backup
> ```

You can either copy the files directly to your home directory or use symbolic links to point to them:

```sh
# copy the files
cp -r HOME/.claude/* ~/.claude/
```

OR

```sh
# create symbolic links
ln -s $(pwd)/HOME/.claude ~/.claude
```

> [!WARNING]
> Symbolic links **must be absolute paths**. That's why we are using `$(pwd)` to get the current directory.
> This also assume the command is run from the root of the repository.

> [!DANGER]
> If you commit your `~/.claude` in your dotfiles, make sure to **exclude RuleKit files**, they can only be shared with people who have a license for Vue RuleKit.
