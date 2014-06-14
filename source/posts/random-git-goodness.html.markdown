---
title: Random Git Goodness
date: 2011-07-01
tags: git
---

## git add -p

Interactively stage files.

The best part about this command is that you can add, not add or split a hunk. &nbsp;I've started using this command constantly to double check the modifications I've made and it's ridiculous how often I would otherwise commit debugging code and stupid comments into repositories.

<p style="padding-left: 30px;"><strong>[format]</strong></p>
<strong>&nbsp; &nbsp; pretty=format:%C(yellow)%h%Creset -%C(red)%d%Creset %s %Cgreen(%ar) %C(bold blue)&lt;%an&gt;%Creset</strong></p>
<p><strong>%d</strong> is a format option that shows ref names</p>

I stole that line from Gary Bernhardt's <a href="https://github.com/garybernhardt/dotfiles">dotfiles</a>. &nbsp;The <strong>%d </strong>there shows which commits have pointers to them. It's a reminder to delete merged branches and a better visualisation of your divergence from master or other branches. It is beautiful.

<p style="padding-left: 30px;"><strong>git config --global rerere.enabled = 1</strong></p>

Enabling git rerere will let git remember how you resolved conflicts, if it ever encounters the same conflict again. Enable this if you don't like reresolving merge conflicts.</p>
