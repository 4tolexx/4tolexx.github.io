---
layout: post
title: 'How to setup helix editor for ruby'
date: 2024-02-19
---

I have been a longtime VScode user, and I still like it. It is very
beginner-friendly. It's pretty much a plug-and-play editor as it has many extensions
for most tasks you want to perform, requiring very little configuration on your part.
Additionally, it has a large community around it.

For a long time, I have always wanted to try out a terminal editor - something
really light and simple. In my quest to find one that I resonate with, I spent time
researching on so many lightweight terminal editors. They include:

* Vim
* Emacs
* Kakoune
* Helix
* Neovim
* Lapce
* Litexl
* Microedit

In the end, I had to settle for Helix. [Helix](https://helix-editor.com/) is a lightweight editor written in Rust.
It draws inspiration from the Kakoune editor and it's opensource too. I opted for
Helix because it's fairly easy to learn compared to Vim, Emacs or even Neovim.
It has several things set up for you upfront and, its LSP support is quite good.

I currently work professionally with Ruby and develop web applications with Ruby on Rails.
I'll share how I was able to setup a fairly simple configuration for developing in
Ruby with Helix. Most of your configurations will be in the `languages.toml` file
for language-specific configurations and `config.toml` file for editor-specific
configurations. You will need the following libraries installed on your computer:

* [Solargraph](https://solargraph.org/): This provides IntelliSense and autocomplete functionality
* [Completion Language Server](https://github.com/estin/simple-completion-language-server): This
is a Rust library and will require Cargo installed. Essentially, it's a snippets
library that provides autocompletion. You can read the README for installation guidelines.

My experience with the editor so far has been decent. It's not perfect yet, but it's 
good enough. I am still looking forward to proper integration with Git. Check [config](https://github.com/4tolexx/helix-editor-config)
for configuration ideas. It is also worth reading the official documentation of
Helix Editor for learning key bindings and other configurations.
