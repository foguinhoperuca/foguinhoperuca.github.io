---
layout: post
title: # My Personal Repository.
---

Dropbox act as file storage in the cloud. Here is all my files that I need share between multiple devices and it isn't private (if it is private then it shouldn't be in a third-party cloud server). The Dropbox account is the main one between others cloud vendor.
The files can be grouped as:

# Folder Structure.

TODO

# Kind of Files.

There is some special kind of file. For any different kind, I have a different policy.

## Static Files.

This kind of file is not editable. Of course, it is writable but, in a normal situation, there is no need to update the file. A exemple is the pdf files. Other good exemple is media file, like mp3, ogg, etc. In general, binary files can't be update easily.
So, this kind of file will live straight in a folder (under static).

## Working Space (Non Static Files).

This kind of file will be edited with a various frequency. A high frequency means that file is important. Sometime, this file must have a version control. For that, I will use git to do this.

### Git Repository.

In Dropbox, all git repository will be stored as a remote repository (create it with option --bare and, by convention, the folder has .git in the end of name of file). The editable repository will live under ~/universal using the same layout of Dropbox. Exemple:

Dropbox folder:

~/Dropbox/documents/financial/money/gnucash.git

universal folder:

~/universal/documents/financial/money/gnucash

### Source Code.

TODO
