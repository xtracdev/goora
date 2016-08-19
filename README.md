## El Caro

This project has a couple Docker files - one is for building a applications
that need to use cgo to integrate with Oracle (indirectly through
go sql drivers), and one to contain the runtime libraries.

Creating an image using the Dockerfile.goracle produces a golang
compile environment set up for OCI work with packages like 
github.com/mattn/go-oci8.

Example usage:

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
