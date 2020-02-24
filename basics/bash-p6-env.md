---
title: "Bash - basic commands"
date: 2018-06-10T17:20:14+08:00
draft: false
diagram: false
tags: [shell, bash]
slug: bash-p1-basics
toc: true
weight: 40
summary: basic bash commands
---

## Frequently used environment variable

```bash
echo $PATH
echo $SHELL
```

## Commands

```bash
# Environment variable
env
# Set env variable
env hello="world"
export hello="world"
# Append to $PATH
export $PATH = $PATH:"/somedir"
# Unset env
env -u hello
```

## References

- <https://unix.stackexchange.com/questions/368944/what-is-the-difference-between-env-setenv-export-and-when-to-use>
