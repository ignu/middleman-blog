---
title: Manipulate History for Meaningful Commits
date: 2013-05-05
tags: git
---

<div><img src="https://dl.dropboxusercontent.com/s/557cxr504tong76/quantum-leap.jpg" alt="Quantum leap" title="quantum-leap.jpg" border="0" width="500" height="373" /></div>

One of git's most powerful features is the ability to rewrite history.

While developing, I commit after every step of the red-green-refactor cycle. I prepend them with the word 'wip' as a reminder not to share them with the world.

<pre> ~/code/paleospots/ [venues] <b>gl</b>
5bdc625 - wip - refactoring
7733fc7 - wip - passing unit test
acfd9dc - wip - failing unit test
2e14ec9 - wip - failing acceptance spec
1d65cf1 - Added Ability for Users to Create Tips [completes #14]</pre>

These commits are meaningful while developing a feature.

5 weeks from now, I am not going to care about the commit that introduced a failing unit test.

Because git is decentralized, I can make these micro-commits locally and worry about squashing them into one commit later.

For example, if I want to try a completely different implementation, I can create a new branch and revert to that failing spec in seconds:

<pre> ~/code/paleospots/ [venues] <strong> git checkout 5bdc625</strong>
You are in 'detached HEAD' state. [...]

HEAD is now at 5bdc625...  failing acceptance tests

&gt; <strong> git checkout -b different-implementation</strong></pre>

p Now, once that feature is complete, it's time to think about the future audience. Two months from now no one's going to care about a commit with just a failing spec. You might want to revert an entire feature, or look at the files involved in a feature.  That's where git rebase comes in.  Run <strong>git rebase -i SHA-BEFORE-ALL-THE-COMMITS-TO-SQUASH</strong>

<pre> ~/code/paleospots/ [venues] <strong>git rebase -i 1d65cf1</strong></pre>

Then you'll see this screen.

<img src="https://dl.dropboxusercontent.com/s/y8js0jqdrv5p64e/Screen-Shot-2012-10-17-at-8.46.49-PM.png" border="0" width="600" height="351" />

Pick the first commit, and change the word "pick" to "s" to squash all the other commits into it. 

Save and exit.

<img src="http://www.barrison.com/wp-content/uploads/2012/10/Screen-Shot-2012-10-17-at-8.50.10-PM.png" border="0" width="600" height="441" />


Now you'll be presented with a chance to edit your commit message.  You'll see a list of your previous commit messages and all the files changed, so you have no excuse to document exactly what you did, packing as many searchable keywords in that first line as possible.  (You're not going to search for "fixed the issue" a month from now, so use as precise wording as possible.)

<pre> ~/code/paleospots/ [venues] <strong>git log</strong>
498a02f - (HEAD, venues) Users create Venues, Venues update their lat/long from an address [completes #23421] (7 hours ago) Len Smith
1d65cf1 - Added Ability for Users to Create Tips [completes #14] (2 weeks ago) Len Smith</pre>

And bam. Your history is meaningful.

Before you push, take a second look at your commit.  You're not going to be able to change it once its published. Use "<a href="http://nathanhoad.net/git-amend-your-last-commit">git commit --amend</a>" if you need to reword your commit.

<strong>* </strong>Once you push to a remote branch that other people might use, you can no longer change history without mucking up the time stream.
