title: Using Visual Studio 2015 as Diff and Merge Tool with Git
date: 2015-11-09 20:51:49
tags:
- git
- visual studio
- mergetool
---

Fixing merge conflicts in git without a good merge tool is a pain. If you are like me and are used to using Visual Studio for everything, you can setup Visual Studio to be your default diff and merge tool.

Add the following to your `.gitconfig` file in your home folder.

```
[diff]
    tool = vsdiffmerge
[difftool]
    prompt = false
[difftool "vsdiffmerge"]
    cmd = \"C:\\Program Files (x86)\\Microsoft Visual Studio 14.0\\Common7\\IDE\\vsdiffmerge.exe\" \"$LOCAL\" \"$REMOTE\" //t
    keepBackup = false
    trustExitCode = true
[merge]
    tool = vsdiffmerge
[mergetool]
    prompt = false
    keepBackup = false
[mergetool "vsdiffmerge"]
    cmd = \"C:\\Program Files (x86)\\Microsoft Visual Studio 14.0\\Common7\\IDE\\vsdiffmerge.exe\" \"$REMOTE\" \"$LOCAL\" \"$BASE\" \"$MERGED\" //m
    keepBackup = false
    trustExitCode = true
```

Once it is setup you can run `git difftool` for diffs and `git mergetool` when a conflict appears.