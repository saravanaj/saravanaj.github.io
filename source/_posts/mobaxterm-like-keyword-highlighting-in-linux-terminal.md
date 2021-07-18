title: MobaXterm-like Keyword Highlighting in Linux Terminal
date: 2021-07-15 22:23:27
tags:
- ssh
- linux
---

One of the features that almost all terminal emulators on Linux lack is regex-based keyword highlighting. 
For example MobaXterm on Windows highlights SSH session outputs automatically. It highlights IP addresses, common keywords like 'error', 'success', 'failed', etc. [iTerm2](https://stackoverflow.com/a/41468739/2419531) on macOS has had it for years.

#### Keyword highlighting in MobaXterm:

![MobaXterm keyword highlighting](/images/moba-feature-syntax-highlighting.png)

Gnome terminal has a [feature request open](https://gitlab.gnome.org/GNOME/gnome-terminal/-/issues/7771) for a long time, but no progress so far. There are many great colorizers like [grc](https://github.com/garabik/grc) or [ccat](https://github.com/owenthereal/ccat), but none of them work with interactive programs like SSH.

What worked for me is [ChromaTerm](https://github.com/hSaria/ChromaTerm). You can wrap `ssh` with ChromaTerm and it will automatically colorize your SSH session:

```bash
ssh() { /usr/bin/ssh "$@" | ct; }
```

#### Here's `ifconfig` from an SSH session colorized with ChromaTerm:

![SSH session with keyword highlighting](/images/terminal-chroma-term.png)

Out of the box ChromaTerm highlights IP addresses and common words. You can use your own keywords and regex to highlight. 
Just create a configuration file at `~/.chromaterm.yml` with your [own highlight rules](https://github.com/hSaria/ChromaTerm#highlight-rules):

```yaml
rules:
- description: My first rule colors the foreground
  regex: hello.+world
  color: f#ff0000
```

If you are a network engineer and work with a lot of devices, the [netcli-highlight](https://github.com/danielmacuare/netcli-highlight) repo has a lot of custom ChromaTerm rules for Cisco/Arista/Juniper devices!
