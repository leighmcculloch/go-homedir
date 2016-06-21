# homedir
[![Linux/OSX Build Status](https://img.shields.io/travis/leighmcculloch/homedir.svg?label=linux%20%26%20osx)](https://travis-ci.org/leighmcculloch/homedir)
[![Windows Build Status](https://img.shields.io/appveyor/ci/leighmcculloch/homedir.svg?label=windows)](https://ci.appveyor.com/project/leighmcculloch/homedir)
[![Codecov](https://img.shields.io/codecov/c/github/leighmcculloch/homedir.svg)](https://codecov.io/gh/leighmcculloch/homedir)
[![Go Report Card](https://goreportcard.com/badge/github.com/leighmcculloch/homedir)](https://goreportcard.com/report/github.com/leighmcculloch/homedir)
[![Go docs](https://img.shields.io/badge/godoc-reference-blue.svg)](https://godoc.org/github.com/leighmcculloch/homedir)

A Go library for getting the user's home directory without cgo allowing for cross compilation.

This is a tracking fork of [mitchellh/go-homedir](https://github.com/mitchellh/go-homedir) that is kept up-to-date with changes upstream. The original uses runtime checks to select the logic used. This fork uses go build tags rather than runtime checks. This was suggested in a two PRs ([#13](https://github.com/mitchellh/go-homedir/issues/13), [#10](https://github.com/mitchellh/go-homedir/issues/10)) but wasn't a fit for the specific purpose that the original had been developed for, leading to this fork.

## Usage

```go
import "github.com/leighmcculloch/homedir"

// Call `homedir.Dir()` to get the home directory of the current user.
homePath := homedir.Dir()

// Call `homedir.Expand()` to expand the `~` in a path to the home directory of the current user.
absPath := homedir.Expand("~/a/path/in/the/home")
```

## Why not use the built in `os/user`?

The built-in `os/user` package requires cgo on Darwin (Mac) systems. This means that any Go code that uses that package cannot cross compile. Much of the time the use for `os/user` is only to retrieve the home directory, which we can do for the current user without cgo. This library does that, enabling cross-compilation.
