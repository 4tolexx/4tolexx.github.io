---
layout: post
title: 'Why I switched from VScode to herdr'
date: 2026-10-22
description: "Why I moved my day-to-day work from VScode to herdr and TTT, now that I read more code than I write."
image: /assets/images/herdr-setup.jpg
---

A while back I wrote about [setting up Helix for Ruby]({% post_url 2024-02-19-how-to-setup-helix-editor-for-ruby %}).
In that post I said I was a longtime VScode user and still liked it. That stayed
true for a long time after. Helix was something I played with, but VScode was
where I did my actual work.

Recently I installed [herdr](https://github.com/herdrdev/herdr), and since then
VScode has not been my main setup. This post is about why I made the
switch and what I use now.

## I stopped writing most of my code by hand

The biggest change was not the tool. It was the way I work. These days AI coding
agents write most of the code, and my job is mostly to read it. I review what they
changed, follow a method to where it is defined, check where something is used,
and decide whether the change is right.

VScode is built around writing code, and for what I was doing it started to feel
heavy. It is also hungry for memory. Out of curiosity I measured it on the Rails
app I am working on right now. With one VScode window open, VScode was using about
**1.2 GB** of memory spread over 20 processes. That number includes my extensions
and the language servers they start.

My current setup on the same machine: two TTT editor instances use about **50 MB**
together, and herdr itself, the server and its clients, uses about **40 MB**. (These are
PSS numbers, which count shared memory only once. TTT's number does not include
`ruby-lsp`, which runs as its own process.)

So I wanted something lighter that is built for reading code and keeping an eye on
agents, not for typing all day.

## herdr

herdr describes itself as a "terminal workspace manager for AI coding agents". If
you have used tmux, some of it will feel familiar: you get workspaces, tabs and split
panes in your terminal. The difference is that herdr knows about the agents running
inside those panes.

These are the parts that matter to me:

* **One workspace per project.** I have a workspace for each project I am working on,
  and each one keeps its own tabs and layout.
* **Agent status.** The sidebar shows whether each agent is working, blocked, done
  or idle, across every workspace. When an agent is waiting on me, I can see it
  without hunting through tabs.
* **Things keep running.** herdr runs your panes in a background server. I can
  detach with `ctrl+b q`, and the panes and agents keep running. Running `herdr`
  again puts me back where I was. I also use named sessions, so
  `herdr session attach hobby` takes me to my side projects. Each named session
  runs as its own herdr server.
* **It is scriptable.** There is a CLI for almost everything, like `herdr pane split`,
  `herdr agent start` and `herdr tab create`. The commands return JSON, so a bit of
  shell and `jq` goes a long way.

## TTT for reading code

For the editor I use [TTT](https://github.com/eugenioenko/ttt) (Terminal Text Tool).
It describes itself as "the IDE that lives in your terminal", and it is a single Go
binary. It also comes with a herdr plugin, which is how I installed it.

What sold me is its LSP support, which is exactly what you need when you read more
code than you write. TTT ships with configurations for 25 language servers. You
install the server, and TTT picks it up. For Ruby that is `ruby-lsp`. With it I get
go to definition (`F12`), find all references (`Ctrl+L R`), hover documentation
(`Ctrl+K I`), and diagnostics shown inline.

TTT also has Git built in. The changes panel lets you stage, unstage, discard and
commit, and it opens a diff for any changed file, either side by side or unified.
That is where I review what an agent did. It is also a little funny, because at the
end of my Helix post I said I was still looking forward to proper Git integration.
I got it in the end, just in a different editor.

## My setup

Here is a short recording of my setup.

<video src="{{ '/assets/images/herdr-setup.mp4' | relative_url }}" poster="{{ '/assets/images/herdr-setup.jpg' | relative_url }}" controls muted loop playsinline style="max-width: 100%;"></video>

TTT is on the left. On the right are two Claude Code panes and an opencode pane. In
the recording I open my Helix post in TTT and ask one of the Claude panes a question
about the blog. Then I create a second workspace for another repository. Its layout
builds in the background, and you can see its Claude panes show up as blocked in
the sidebar, because they are waiting for me to trust the folder.

### A plugin for the layout

I use this same layout for almost every project, so I wrote a small local herdr
plugin for it. A plugin is a manifest plus a script. This is part of the manifest:

```toml
id = "tolexx.dev-layout"
name = "Dev Layout"
version = "0.1.0"
min_herdr_version = "0.9.0"
description = "ttt on the left; claude, claude and opencode stacked on the right"
platforms = ["linux", "macos"]

[[actions]]
id = "apply"
title = "Apply dev layout"
contexts = ["workspace"]
command = ["sh", "layout.sh", "apply"]
```

and the part I like the most:

```toml
[[events]]
on = "workspace.created"
command = ["sh", "layout.sh", "auto"]
```

When I create a new workspace inside a Git repository, the script splits the panes,
runs `ttt .` on the left, and starts the agents on the right with `herdr agent start`.
I don't have to do anything.

### Keybindings

The rest lives in `~/.config/herdr/config.toml`. These are some of my bindings:

```toml
[[keys.command]]
key = "prefix+d"
type = "plugin_action"
command = "tolexx.dev-layout.apply"
description = "dev layout: ttt + 2 claude + opencode"

[[keys.command]]
key = "prefix+a"
type = "plugin_action"
command = "tolexx.dev-layout.spawn-claude"
description = "spawn claude below focused pane"

[[keys.command]]
key = "prefix+f"
type = "popup"
command = "exec \"${SHELL:-sh}\""
description = "floating scratch shell"
width = "80%"
height = "80%"

[[keys.command]]
key = "prefix+shift+a"
type = "pane"
command = "claude"
description = "zoomed throwaway claude (closes on exit)"
```

The floating shell and the throwaway Claude pane are for quick one-off things. The
shell opens as a popup without changing my layout. The Claude pane opens zoomed and
closes by itself when I exit Claude.

## What is not perfect

herdr is young. I installed version 0.9.3, and there have been two releases since
then, one of them a hotfix. Since June there has been a new stable release about
every week or two. Nothing has broken for me so far, but expect rough edges.

There is also a learning curve. VScode is still more beginner-friendly, and I would
still recommend it to someone just starting out. With herdr you will spend time in
the docs and the `--help` output. To get the most out of it, you will write a bit
of shell.

I also have not uninstalled VScode. I still open it now and then, mostly to look at
a Markdown file. It is just not where I spend my day anymore.

## Conclusion

My experience so far has been good. My work has moved from writing code to reading
it and managing the agents that write it, and herdr with TTT fits that much better
than VScode did. It also uses a lot less memory. If your days look like mine, I
think it is worth a try.
