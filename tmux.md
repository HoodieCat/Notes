# TMUX
What is TMUX(Terminal Multiplexer),it unbind the session with terminal, sessions still maintain despite terminal closed.(by detach or attach)
## Four significant concepts：
- Server, that is the tmux service itself
- Session, all the maintain in the tmux server, using attach/detach to connect/disconnect. Even you leave the shell(ssh disconnect), it still maintain the tmux server. That means you can still hold tasks on background.
- Window, like tabs on vim. Each winodws of serveral panes.
- Pane, the least unit of tmux display.

## Common Tmux commands:
```
# launch session with give session name and given window name
$ tmux [new -s session <name> -n <window name>]

# resume session with certain session name 
# -t means target
$ tmux at -t <session name>

# lis all sessions 
$ tmux ls

# close certain session
$ tmux kill-session -t <session name>

# close tmux server,that is, close all the sessions completely
$ tmux kill-server
```

## Common KeyMap
Tmux using the prefix key to catch Tmux action, the default is <C-b>, in my [config](https://github.com/HoodieCat/.dotfiles/blob/main/tmux/tmux.conf),change it to <C-a> compatible with nvim config.
```
# Server tier
<C-s> list all sessions with its windows display, to select and switch from

<C-d> detach from current seesion

<C-z> hangup tmux server

# Window tier
<C-c> create window

<C-&> close windows

<C-n>/<C-p> switch to [n]ext/[p]revious window

<c-w> list all windows under current session on display

# pane tier
<C--> split window horizontally (default is<C-">")

<C-+> split window vertically (default is<C-%>")

<c-x> close pane

<C-o> select the next pane

```

