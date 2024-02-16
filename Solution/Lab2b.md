# Solution to Lab2b

## Vim

1. Use `10kd10d` or `:.-10,.d`
2. Use `:shell` command and you can use `fg` to go back to vim
3. Use `:split filename` to split the space horizonally or `:vsplit filename` to split vertically
4. First enter visual mode and select box, then using `>` or `<` for indentation. You can also add numbers at the begining, same as what `10k` does

## Tmux

1. First use `Ctrl-B` and type `:split -v / - h` to split the window. Next use `Ctrl-B` and then type `:resize-pane -D / -U / -L / -R ` + `size` to adjust the pane size. Install the `htop` package to show resource monitors
