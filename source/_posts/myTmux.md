---
title: 我的TMUX配置
date: 2023-05-28 17:30:50
cover: https://f005.backblazeb2.com/file/img-forWeb/uPic/screenshot.webp
banner: https://f005.backblazeb2.com/file/img-forWeb/uPic/3EUBht.jpg
poster:
  headline: My TUMX Configuration
  topic: terminal multitasking powerhouse
  color: yellow
tags: TMUX
---

{% image https://f005.backblazeb2.com/file/img-forWeb/uPic/1Bt3lu.png bg:pink %}
### [tmux](https://github.com/tmux/tmux/wiki)

#### Install using [tpm](https://github.com/tmux-plugins/tpm)

If you are a tpm user, you can install the theme and keep up to date by adding the following to your .tmux.conf file:

	set -g @plugin 'dracula/tmux'

Add any configuration options below this line in your tmux config.

#### Install with [Nix](https://nixos.org)

If you're using [home-manager](https://github.com/nix-community/home-manager), an example config would look similar to this:
Then run `home-manager switch`, the `Activating theme` section doesn't apply here.

```nix
programs.tmux = {
	enable = true;
	clock24 = true;
	plugins = with pkgs.tmuxPlugins; [
		sensible
		yank
		{
			plugin = dracula;
			extraConfig = ''
				set -g @dracula-show-battery false
				set -g @dracula-show-powerline true
				set -g @dracula-refresh-rate 10
			'';
		}
	];

	extraConfig = ''
		set -g mouse on
	'';
};
```

#### Activating theme

1. Make sure  `run -b '~/.tmux/plugins/tpm/tpm'` is at the bottom of your .tmux.conf
2. Run tmux
3. Use the tpm install command: `prefix + I` (default prefix is ctrl+b)

#### Configuration

To enable plugins set up the `@dracula-plugins` option in you `.tmux.conf` file, separate plugin by space.
The order that you define the plugins will be the order on the status bar left to right.

```bash
# available plugins: battery, cpu-usage, git, gpu-usage, ram-usage, tmux-ram-usage, network, network-bandwidth, network-ping, ssh-session, attached-clients, network-vpn, weather, time, mpc, spotify-tui, kubernetes-context, synchronize-panes
set -g @dracula-plugins "cpu-usage gpu-usage ram-usage"
```

For each plugin is possible to customize background and foreground colors

```bash
# available colors: white, gray, dark_gray, light_purple, dark_purple, cyan, green, orange, red, pink, yellow
# set -g @dracula-[plugin-name]-colors "[background] [foreground]"
set -g @dracula-cpu-usage-colors "pink dark_gray"
```

#### Status bar options

Enable powerline symbols

```bash
set -g @dracula-show-powerline true
```

Switch powerline symbols

```bash
# for left
set -g @dracula-show-left-sep 

# for right symbol (can set any symbol you like as separator)
set -g @dracula-show-right-sep 
```

Enable window flags

```bash
set -g @dracula-show-flags true
```

Adjust the refresh rate for the status bar

```bash
# the default is 5, it can accept any number
set -g @dracula-refresh-rate 5
```

Switch the left smiley icon

```bash
# it can accept `hostname` (full hostname), `session`, `shortname` (short name), `smiley`, `window`, or any character. 
set -g @dracula-show-left-icon session
```

Add padding to the left smiley icon

```bash
# default is 1, it can accept any number and 0 disables padding.
set -g @dracula-left-icon-padding 1
```

Enable high contrast pane border

```bash
set -g @dracula-border-contrast true
```

Hide empty plugins

```bash
set -g @dracula-show-empty-plugins false
```

#### cpu-usage options

Customize label

```bash
set -g @dracula-cpu-usage-label "CPU"
```

Show system load average instead of CPU usage percentage (default)

```bash
set -g @dracula-cpu-display-load true
```

CPU usage percentage (default) - in percentage (output: %)
Load average – is the average system load calculated over a given period of time of 1, 5 and 15 minutes (output: x.x x.x x.x)

#### battery options

Customize label

```bash
set -g @dracula-battery-label "Battery"
```

#### gpu-usage options

Note, currently only the Linux NVIDIA Proprietary drivers are supported. Nouveau and AMD Graphics Cards support are still under development.

Customize label

```bash
set -g @dracula-gpu-usage-label "GPU"
```

#### ram-usage options

Customize label

```bash
set -g @dracula-ram-usage-label "RAM"
```

#### tmux-ram-usage options

Customize label

```bash
set -g @dracula-tmux-ram-usage-label "MEM"
```

#### network-bandwidth

You can configure which network interface you want to view the bandwidth,
Displaying of the interface name, The interval between each bandwidth update.
The most common interfaces name are `eth0` for a wired connection and `wlan0` for a wireless connection.

```bash
set -g @dracula-network-bandwidth eth0
set -g @dracula-network-bandwidth-interval 0
set -g @dracula-network-bandwidth-show-interface true
```

#### network-ping options

You can configure which server (hostname, IP) you want to ping and at which rate (in seconds). Default is google.com at every 5 seconds.

```bash
set -g @dracula-ping-server "google.com"
set -g @dracula-ping-rate 5
```
### ssh-session options

Show SSH session port

```bash
set -g @dracula-show-ssh-session-port true
```

#### time options

Disable timezone

```bash
set -g @dracula-show-timezone false
```

Swap date to day/month

```bash
set -g @dracula-day-month true
```

Enable military time

```bash
set -g @dracula-military-time true
```

Set custom time format e.g (2023-01-01 14:00)
```bash
set -g @dracula-time-format "%F %R"
```
See [[this page]](https://man7.org/linux/man-pages/man1/date.1.html) for other format symbols.

#### git options

Hide details of git changes
```bash
set -g @dracula-git-disable-status true
```

Set symbol to use for when branch is up to date with HEAD
```bash
# default is ✓. Avoid using non unicode characters that bash uses like $, * and !
set -g @dracula-git-show-current-symbol ✓
```

Set symbol to use for when branch diverges from HEAD
```bash
# default is unicode !. Avoid bash special characters
set -g @dracula-git-show-diff-symbol !
```

Set symbol or message to use when the current pane has no git repo
```bash
# default is unicode no message
set -g @dracula-git-no-repo-message ""
```

Hide untracked files from being displayed as local changes
```bash
# default is false
set -g @dracula-git-no-untracked-files true
```

Show remote tracking branch together with diverge/sync state
```bash
# default is false
set -g @dracula-git-show-remote-status true
```

#### hg options

Hide details of hg changes
```bash
set -g @dracula-hg-disable-status true
```

Set symbol to use for when branch is up to date with HEAD
```bash
#default is ✓.Avoid using non unicode characters that bash uses like $, * and !
set -g @dracula-hg-show-current-symbol ✓
```

Set symbol to use for when branch diverges from HEAD
```bash
#default is unicode !.Avoid bash special characters
set -g @dracula-hg-show-diff-symbol !
```

Set symbol or message to use when the current pane has no hg repo
```bash
#default is unicode no message
set -g @dracula-hg-no-repo-message ""
```

Hide untracked files from being displayed as local changes
```bash
#default is false
set -g @dracula-hg-no-untracked-files false
```

#### weather options

Switch from default fahrenheit to celsius

```bash
set -g @dracula-show-fahrenheit false
```

Set your location manually

```bash
set -g @dracula-fixed-location "Some City"
```

Hide your location

```bash
set -g @dracula-show-location false
```

#### synchronize-panes options

Customize label

```bash
set -g @dracula-synchronize-panes-label "Sync"
```
#### attached-clients options

Set the minimum number of clients to show (otherwise, show nothing)

```bash
set -g @dracula-clients-minimum 1
```

Set the label when there is one client, or more than one client

```bash
set -g @dracula-clients-singular client
set -g @dracula-clients-plural clients
```

#### Kubernetes options

Add prefix label before the context

```bash
set -g @dracula-kubernetes-context-label "Some Label"
```

Hide user from the context string

```
set -g @dracula-kubernetes-hide-user true
```

Hide ARN (show only cluster name) - Available for EKS only (only available for cluster names that are ARNs)

```
set -g @dracula-kubernetes-eks-hide-arn true
```

Extract the account as a prefix to the cluster name - Available for EKS only (only available for cluster names that are ARNs)

```
set -g @dracula-kubernetes-eks-extract-account true

#### continuum options

Set the output mode. Options are:
- **countdown**: Show a T- countdown to the next save (default)
- **time**: Show the time since the last save
- **alert**: Hide output if no save has been performed recently
- **interval**: Show the continuum save interval

```bash
set -g @dracula-continuum-mode countdown
```

Show if the last save was performed less than 60 seconds ago (default threshold is 15 seconds)

```bash
set -g @dracula-continuum-time-threshold 60
```

#### 我的TUMX配置文件（tmux.conf）
```bash
# -- prefix
unbind C-b
set -g prefix 'C-s'

# -- display
set -g base-index 1
setw -g pane-base-index 1

setw -g automatic-rename on
set -g renumber-windows on

set -g set-titles on

set -g display-panes-time 2000
set -g display-time 2000

set -g status-interval 1

# -- navigation

# create session
bind C-c new-session

# window management
bind -n M-o new-window -c "#{pane_current_path}"
bind -n M-O break-pane
bind -n M-Q kill-pane

# window navigation
unbind n
unbind p
unbind 1
unbind 2
unbind 3
unbind 4
unbind 5
unbind 6
unbind 7
unbind 8
unbind 9
unbind 0
bind -r C-p previous-window
bind -r C-n next-window
bind -n M-1 select-window -t 1
bind -n M-2 select-window -t 2
bind -n M-3 select-window -t 3
bind -n M-4 select-window -t 4
bind -n M-5 select-window -t 5
bind -n M-6 select-window -t 6
bind -n M-7 select-window -t 7
bind -n M-8 select-window -t 8
bind -n M-9 select-window -t 9


bind -n M-! join-pane -t :1
bind -n M-@ join-pane -t :2
bind -n 'M-#' join-pane -t :3
bind -n 'M-$' join-pane -t :4
bind -n M-% join-pane -t :5
bind -n M-^ join-pane -t :6
bind -n M-& join-pane -t :7
bind -n M-* join-pane -t :8
bind -n M-( join-pane -t :9

bind u split-window -vb -c "#{pane_current_path}"
bind e split-window -v -c "#{pane_current_path}"
bind n split-window -hb -c "#{pane_current_path}"
bind i split-window -h -c "#{pane_current_path}"
bind -n M-f resize-pane -Z

# pane navigation
bind 1 select-pane -t:.1
bind 2 select-pane -t:.2
bind 3 select-pane -t:.3
bind 4 select-pane -t:.4
bind 5 select-pane -t:.5
bind 6 select-pane -t:.6
bind 7 select-pane -t:.7
bind 8 select-pane -t:.8
bind 9 select-pane -t:.9
bind 0 select-pane -t:.10
bind -n M-n select-pane -L
bind -n M-e select-pane -D
bind -n M-u select-pane -U
bind -n M-i select-pane -R
bind > swap-pane -D
bind < swap-pane -U
bind | swap-pane
bind -n M-Space next-layout

bind W choose-tree -Z
bind S choose-tree 'move-pane -v -s "%%"'
bind V choose-tree 'move-pane -h -s "%%"'

# pane resizing
bind -n M-N resize-pane -L 3
bind -n M-E resize-pane -D 3
bind -n M-U resize-pane -U 3
bind -n M-I resize-pane -R 3

set -g status-keys emacs
set -g mode-keys vi
bind -n M-v copy-mode

bind -T copy-mode-vi v send-keys -X begin-selection
bind -T copy-mode-vi C-v send-keys -X rectangle-toggle
bind -T copy-mode-vi n send-keys -X cursor-left
bind -T copy-mode-vi i send-keys -X cursor-right
bind -T copy-mode-vi u send-keys -X cursor-up
bind -T copy-mode-vi e send-keys -X cursor-down
bind -T copy-mode-vi h send-keys -X next-word-end
bind -T copy-mode-vi U send-keys -N 5 -X cursor-up
bind -T copy-mode-vi E send-keys -N 5 -X cursor-down
bind -T copy-mode-vi N send-keys -X start-of-line
bind -T copy-mode-vi I send-keys -X end-of-line
bind -T copy-mode-vi Y send-keys -X copy-end-of-line
bind -T copy-mode-vi y send-keys -X copy-selection-and-cancel
bind -T copy-mode-vi = send-keys -X search-again
bind -T copy-mode-vi = send-keys -X search-reverse


bind b list-buffers
bind p paste-buffer

# -- toggle_syn_input
bind C-g if-shell '[[ $(tmux showw synchronize-panes | cut -d\  -f2) == "on" ]]' \
'setw synchronize-panes off; set -g pane-border-style fg=magenta' \
'setw synchronize-panes on; set -g pane-border-style fg=red'


# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'dracula/tmux'

set -g @dracula-show-powerline true
# default is 1, it can accept any number and 0 disables padding.
set -g @dracula-left-icon-padding 0
# Switch from default fahrenheit to celsius
set -g @dracula-show-fahrenheit false
set -g @dracula-fixed-location "Shenzhen"
set -g @forecast-location Shenzhen

# available plugins: battery, cpu-usage, git, gpu-usage, ram-usage, tmux-ram-usage, network, network-bandwidth, network-ping, ssh-session, attached-clients, network-vpn, weather, time, mpc, spotify-tui, kubernetes-context, synchronize-panes
set -g @dracula-plugins "weather cpu-usage ram-usage ssh-session"

# available colors: white, gray, dark_gray, light_purple, dark_purple, cyan, green, orange, red, pink, yellow
# set -g @dracula-[plugin-name]-colors "[background] [foreground]"
set -g @dracula-weather-colors "cyan dark_gray"
set -g @dracula-cpu-usage-colors "yellow dark_gray"
set -g @dracula-ram-usage-colors "pink dark_gray"
set -g @dracula-ssh-session-colors "red dark_gray"

# it can accept `hostname` (full hostname), `session`, `shortname` (short name), `smiley`, `window`, or any character. 
set -g @dracula-show-left-icon smiley

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'github_username/plugin_name#branch'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.config/.tmux/plugins/tpm/tpm'

```
