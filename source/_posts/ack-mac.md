title: Ack on Mac OS
tag:
- ack
- mac
categories: nix
date: 2016-06-02 11:00:00
---
Install and Use Ack, a good replacement for find and grep. Here will show you how to use on Mac OS.

<!-- more -->

### Install on Mac OS

``` bash
$ brew update && brew install ack
```

More info: [Homebrew official site](http://brew.sh/)

### Config Ack

``` bash
$ echo '--pager=less -RFX' >> ~/.ackrc
```

**That is to say, your configuration file of ack is under ~/ .**

### Useful command of Ack

- search something under ./ 

``` bash
$ ack -w restrict
```

- search something under ./ with specific file type

``` bash
$ ack -w --python restrict
```

- count the occurence time of the specific item

``` bash
$ ack -c restrict
```

- match the specific item and show before and after lines.

``` bash
$ ack -w -B 5 restrict
```

``` bash
$ ack -w -A 5 restrict
```

- match the specific item and get 3 lines of context in either direction

``` bash
$ ack -w -C 3 restrict
```

- Just print the files that have matches

``` bash
$ ack -w -C 3 restrict
```

More info: [Reference](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-ack-a-grep-replacement-for-developers-on-ubuntu-14-04)
