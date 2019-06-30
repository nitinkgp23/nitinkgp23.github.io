---
title: Getting started with Go
excerpt: Go is a modern programming language developed at Google. It is increasingly popular for many applications and at many companies, and offers a robust set of libraries.
date: 2017-10-29
categories:
 - tutorial
tags:
 - go
comments: true
---

This tutorial walks through how I installed Go, and how I got started with it. I will keep on updating it, through my journey of learning Go.

# Installation

1. Retrieve the tarball using `curl` by the following command:
    ```
    curl -O https://storage.googleapis.com/golang/go1.6.linux-amd64.tar.gz
    ```

2. Next, use `tar` to extract the tarball :
    (Here `x` tells it to extract, `v` denotes verbose output and `f` denotes that we are mentioning a file name.)
    ```
    tar xvf go1.6.linux-amd64.tar.gz
    ```

3. This creates a directory go in the home directory. We recursively change Go's owner and group to root and move it to `usr/local` :
    ```
    sudo chown -R root:root ./go
    sudo mv go /usr/local
    ```
    (`usr/local/go` is the offical recommended location.)
    
4. Setting up paths :

    At the end of the file `~/.profile`, add the following lines:
    ```
    export GOPATH=$HOME/work/go
    export PATH=$PATH:/usr/local/bin:$GOPATH/bin
    ```
    GOPATH contains the path of the folder where you will write all your Go programs. After saving the file, refresh it by doing:
    ```
    source ~/.profile
    ```

This completes our installation process.

# Writing "Hello World" program

1. Create a working directory (which you added in the .profile as GOPATH) :
    ```
    mkdir -p work/go/src/hello
    ```

2. Create a simple Hello world file inside the above dir:
    ```
    nano ~/work/go/src/hello/hello.go
    ```

    Inside the editor, paste the code below:

    ```go
    package main

    import "fmt"

    func main() {
        fmt.Printf("hello, world\n")
    }
    ```

3. Compile the above code using `install` command:
    ```
    go install work/go/src/hello
    ```
    This will create a binary in the dir `work/go/bin`

4. Execute this by just typing
    ```
    hello
    ```
    since it is already added in the path.
