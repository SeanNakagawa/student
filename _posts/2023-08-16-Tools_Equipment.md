---
toc: true
comments: true
layout: post
title: VSCode, Python, Jupyter, ...
description: Homebrew
courses: { csse: {week: 0}, csp: {week: 0}, csa: {week: 0} }
type: hacks
---

## How to Install Homebrew
> Homebrew install
- Copy and Paste to Install from Terminal
    - Copy ```bash ... curl ...```  command using copy box on website
    - Launch ```terminal``` from search bar
    - Paste ```bash ... curl ...``` command into Terminal ... 
    - Make sure command starts, this should provide feedback/output in terminal and could take a long time, like 10-min, there could be a  prompt in the middle, at about 5-minutes.  Follow any on screen instructions provided in terminal output to finish.

- It should look like this:
```bash
(base) iMac:~ jmort1021$
```

> Key Packages needed on MacOS
- <mark>Close and Start a new terminal</mark>, run each command in Terminal
```bash
$ brew list   
$ brew update   
$ brew upgrade   
$ brew install git   
$ brew install python   
$ python --version   
```

> Install Jupyter and check python kernel 
```bash
(base) id:~$ conda --version 
(base) id:~$ conda install jupyter # install jupyter
(base) id:~$ jupyter kernelspec list # list installed kernels
Available kernels:
  python3    /home/shay/.local/share/jupyter/kernels/python3
```
