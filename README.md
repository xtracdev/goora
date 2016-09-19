## GoOra - Go Oracle

This project has a couple Docker files useful when working with Oracle 
in golang.

### Set Up

If you are building this behind an HTTP proxy, you'll need to copy 
apt.conf.template to apt.conf and edit it to reflect your proxy configuration.

If you are not building this behind an HTTP proxy, you need to remove the 
COPY apt.conf line from the Docker files.

Note that you will need to download the Oracle instant client files for
Linux from [Oracle](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html)
and place them locally under `oracle/linux` - refer to the Dockerfile 
for the specifics and the relative file path.

### Use

Dockerfile.golang is an image for compiling golang applications
that need to use cgo to integrate with Oracle (indirectly through
go sql drivers). To use it for working with the github.com/mattn/go-oci8
driver:

<pre>
docker build -f Dockerfile.goracle . -t xtracdev/goora
cd $GOPATH
docker run --rm -it -v "$PWD":/go -w /go/src/github.com/xtraclabs xtracdev/goora bash

# In the shell
cd appreg
go get github.com/rjeczalik/pkgconfig/cmd/pkg-config
go get -v github.com/mattn/go-oci8
go build -o appreg
</pre>

Dockerfile creates a base image that is configured with the Oracle instant
client software. It can be used to containerize go applications that require
the Oracle instant client software.

This creates a base image named elcaro.

### Contributing

To contribute, you must certify you agree with the [Developer Certificate of Origin](http://developercertificate.org/)
by signing your commits via `git -s`. To create a signature, configure your user name and email address in git.
Sign with your real name, do not use pseudonyms or submit anonymous commits.


In terms of workflow:

0. For significant changes or improvement, create an issue before commencing work.
1. Fork the respository, and create a branch for your edits.
2. Add tests that cover your changes, unit tests for smaller changes, acceptance test
for more significant functionality.
3. Run gofmt on each file you change before committing your changes.
4. Run golint on each file you change before committing your changes.
5. Make sure all the tests pass before committing your changes.
6. Commit your changes and issue a pull request.

### License

(c) 2016 Fidelity Investments
Licensed under the Apache License, Version 2.0
