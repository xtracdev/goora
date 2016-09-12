## GoOra - Go Oracle

This project has a couple Docker files useful when working with Oracle 
in golang.

Dockerfile.golang is an image for compiling golang applications
that need to use cgo to integrate with Oracle (indirectly through
go sql drivers). To use it for working with the github.com/mattn/go-oci8
driver:

<pre>
docker build -f Dockerfile.goracle . -t dasmith/goora
cd $GOPATH
docker run --rm -it -v "$PWD":/go -w /go/src/github.com/xtraclabs dasmith/goora bash

# In the shell
cd appreg
go get github.com/rjeczalik/pkgconfig/cmd/pkg-config
go get -v github.com/mattn/go-oci8
go build -o appreg
</pre>

Dockerfile creates a base image that is configured with the Oracle instant
client software. It can be used to containerize go applications that require
the Oracle instant client software.
