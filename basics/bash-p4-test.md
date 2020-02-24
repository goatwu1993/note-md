---
title: "Bash - test"
date: 2020-01-20T03:04:32+08:00
draft: false
diagram: false
tags: [shell, bash]
slug: bash-p4-test
toc: true
weight: 40
summary: bash test, condition and operator.
---

## What is test

```bash
$ man test
NAME
     test, [ -- condition evaluation utility

SYNOPSIS
     test expression
     [ expression ]

DESCRIPTION
     The test utility evaluates the expression and, if it evaluates to true, returns a zero (true) exit status; oth-
     erwise it returns 1 (false).  If there is no expression, test also returns 1 (false).

     All operators and flags are separate arguments to the test utility.
```

Condition 為真的話是返回 0，否則返回 1  
在 bash 可用以下方式呼叫

- test expression
- [ expression ]

bash 裡面 "[" 就是 test

## 測試給定的檔名/檔案

```bash
# 判斷檔名是否存在(Exist)
test -e REAME.md
# 判斷檔名是否存在且為檔案
test -f REAME.md
# 判斷檔名是否存在且為資料夾
test -d dir
#
```

## 測試給定的兩個檔名/檔案

```bash
# Newer than
test file1 -nt file2
# Older than
test file1 -ot file2
# True if file1 and file2 exist and refer to the same file.
test file1 -ef file2
```

還有許多其他的，但不常用到(block, Socket 等等)

## 測試給定的字串

```bash
# True if string is not the null string
test string
# True if the length of string is zero.
test -z string
# True if the length of string is nonzero.
test -n string

# True if the strings s1 and s2 are identical.
test s1 = s2
# True if the strings s1 and s2 are not identical.
test s1 != s2
# True if string s1 comes before s2 based on the binary value of their characters.
test s1 < s2
# True if string s1 comes after s2 based on the binary value of their characters.
test s1 > s2
```

## 測試給定的整數

```bash
# True if the integers n1 and n2 are algebraically equal.
test n1 -eq n2
# True if the integers n1 and n2 are not algebraically equal.
test n1 -ne n2
# True if the integer n1 is algebraically greater than the integer n2.
test n1 -gt n2
# True if the integer n1 is algebraically greater than or equal to the integer n2.
test n1 -ge n2
# True if the integer n1 is algebraically less than the integer n2.
test n1 -lt n2
# True if the integer n1 is algebraically less than or equal to the integer n2.
test n1 -le n2
```

## 算子

```bash
## not
! expression
## and
test expression1 -a expression2
## or
expression1 -o expression2
## ()
( expression )
```

and 優先於 or

## References

- <http://linux.vbird.org/linux_basic/0340bashshell-scripts.php#test>
