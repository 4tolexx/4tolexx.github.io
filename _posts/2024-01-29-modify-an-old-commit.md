---
layout: post
title:  "How to modify an old commit"
date:   2024-01-29
---
There are times when you may have an existing commit, but you have just made changes to a file or a couple of files. Perhaps you don't want to create a new commit, but you would rather modify the old commit and add your changes to it. Below are the Git commands I use in such cases.

```bash
git add < changed files >
git commit --fixup=<OLDCOMMIT sha-value>
git rebase --interactive --autosquash OLDCOMMIT^
```

**explanation**

* `git commit --fixup=<OLDCOMMIT sha-value>`: This command takes the message of the OLDCOMMIT and automatically apply `fixup!` to it which is similar to when you run an interactive rebase and you apply the `fixup` option.

* `git rebase --interactive --autosquash OLDCOMMIT^`: The caret(^) symbol here refers to the parent commit of OLDCOMMIT. `--autosquash OLDCOMMIT` automatically puts any `--fixup=OLDCOMMIT` in the correct order. Note that --autosquash is only valid when the --interactive option is used.
