# TMUX Installation & Configuration

```bash
# Remap prefix to Control + a
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Be able to go to beginning of line
bind a send-prefix

# Force a reload of the config file
unbind r
bind r source-file ~/.tmux.conf \; display "Reloaded ~/.tmux.conf"

# Make a smaller delay so we can perform commands after switching windows
# for example
set -sg escape-time 0
set -sg repeat-time 600

# Enable mouse mode
set -g mouse on
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mouse-select-window on

# Less stretching to get to the first item.
set -g base-index 1
setw -g pane-base-index 1

# Quick pane cycling
unbind ^A
bind ^A select-pane -t :.+


# Use Alt-vim keys without prefix key to switch panes
bind -n M-h select-pane -L
bind -n M-j select-pane -D
bind -n M-k select-pane -U
bind -n M-l select-pane -R

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
bind -n M-Left  previous-window
bind -n M-Right next-window

# send a command to all panes
bind -n C-x setw synchronize-panes on
bind -n M-x setw synchronize-panes off

# Use Vi mode
setw -g mode-keys vi
set -g status-keys vi

# More straight forward key bindings for splitting
unbind %
bind | split-window -h
unbind '"'
bind - split-window -v
bind _ split-window -v

# Terminal emulator window title
set -g set-titles on
set -g set-titles-string '#S:#I.#P #W'
# Terminal junks!
set -g default-terminal "screen-256color"

# Bad Wolf
set -g status-fg white
set -g status-bg colour234
set -g window-status-activity-attr bold
set -g pane-border-fg colour245
set -g pane-active-border-fg colour39
set -g message-fg colour16
set -g message-bg colour221
set -g message-attr bold

# Custom status bar
# Powerline symbols: <U+2B82> <U+2B83> <U+2B80> <U+2B81> <U+2B64>
set -g status-fg colour231
set -g status-bg colour234
set -g status-left-length 20
set -g status-left '#[fg=colour16,bg=colour254,bold] #S #[fg=colour254,bg=colour234,nobold]'
set -g status-right '#[fg=colour233,bg=colour241,bold] %d %b %R #(eval tmux-airline `tmux display -p "#{client_width}"`)'
set -g status-right-length 150

set -g window-status-format "#[fg=colour244,bg=colour234]#I #[fg=colour240] #[default]#W "
set -g window-status-current-format "#[fg=colour234,bg=colour31] #[fg=colour117,bg=colour31] #I  #[fg=colour231,bold]#W #[fg=colour31,bg=colour234,nobold]"

set-window-option -g window-status-fg colour249
set-window-option -g window-status-activity-attr none
set-window-option -g window-status-bell-attr none
set-window-option -g window-status-activity-fg yellow
set-window-option -g window-status-bell-fg red


# Activity
setw -g monitor-activity on
set -g visual-activity on

# Autorename sanely.
##setw -g automatic-rename on

# Better name management
bind c new-window
bind , command-prompt "rename-window '%%'"

# Don't prompt for killing panes and windows
bind-key x kill-pane
bind-key & kill-window

# Scrollback lines
set-option -g history-limit 3000

# Don't wait so long for commands
set -s escape-time 0

# Workaround for macOS pasteboard in tmux sessions
set-option -g default-command 'command -v reattach-to-user-namespace >/dev/null && exec reattach-to-user-namespace -l "$SHELL" || exec "$SHELL"'

# Tmux Plugin Manager
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

run '~/.tmux/plugins/tpm/tpm'

# save tmux session when close window
set -g @plugin 'tmux-plugins/tmux-resurrect'


```