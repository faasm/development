# Faasm Development Repo

This repo is used for developing the [Faasm](https://github.com/faasm) project.

*Note* submodules in this folder should be up-to-date with the latest `master`.
Don't push your local branch checkouts to them.

Having everything related to both the client and server side of Faasm in a
single repo would be prohibitively large and cause _very_ long builds.
Additionally, the system should really be treated in layers, independent of
those above them. 

However, it's still convenient to have everything in one place, especially when
you _do_ need to touch all parts. Hence the existence of this repo. 

## Layers

The Faasm project has a top layer which creates WebAssembly files, which are
executed by the Faasm runtime below, which depends on Faabric for messaging and 
state. 

- [faasm/cpp](https://github.com/faasm/cpp) - tools for building C/C++ for use
  in Faasm.
- [faasm/python](https://github.com/faasm/python) - tools for building CPython
  and Python functions for use in Faasm.
- [faasm/faasm](https://github.com/faasm/faasm) - the Faasm runtime (independent
  of specific languages used to compile the WebAssembly)
- [faasm/faabric](https://github.com/faasm/faabric) - serverless scheduling,
  messaging and state (independent of WebAssembly).

## Initial Set-up

First you need to update all the submodules:

```
git submodule update --init --recursive
```

The repos are tied together using the `/usr/local/faasm` directory, which you
can initialise with:

```
./bin/refresh_local.sh
```

If you want to run Python scripts outside the containerised environments, you 
can set up a suitable Python virtual envrionment with:

```
./bin/create_venv.sh
```

## Use

Once you've set up the repo, you can start the CLI for whichever project you 
want to work on:

```
# C++ applications
./bin/cli.sh cpp

# Python applications
./bin/cli.sh python

# Faasm 
./bin/cli.sh faasm

# Faabric
./bin/cli.sh faabric
```
