# Example: How to depend on [GE211] in a subdirectory

This repo contains a minimal, complete example of how a project can depend
on [GE211] in a subdirectory, rather than by installing it on your system.
The [`CMakeLists.txt`] expects `3rdparty/ge211/` to be (linked to)
a subdirectory containing the [GE211] library. For the purposes of
testing, we assume that we check out this repo as a submoduls of the
GE211 repository at `examples/vendored/`, and `ge211` is a [symbolic link
to `../../../`][the symlink].

There are two strategies to replace the symlink with a copy of GE211 that
doesn’t depend on the context of this repository: You can add a submodule
reference or copy GE211’s code directly into your repository.

## Including [GE211] by reference

To include a reference to [GE211], you should remove the
symlink and add it as a Git submodule instead:

```ShellSession
$ cd 3rdparty
$ git rm ge211
$ git submodule add https://github.com/tov/ge211.git
$ git commit -m 'Added GE211 as submodule'
```

## Including [GE211] by copy

To include a copy of [GE211], you should remove the symlink, clone the
repository, remove its `.git/` directory, and then add it to your own
repository:

```ShellSession
$ cd 3rdparty
$ git rm ge211
$ git clone https://github.com/tov/ge211.git 
$ rm -Rf ge211/.git
$ git add ge211
$ git commit -m 'Vendored GE211'
```

[GE211]:
    https://github.com/tov/ge211.git 
    
[`CMakeLists.txt`]:
    https://github.com/tov/ge211-vendored-example/blob/master/CMakeLists.txt
    
[the symlink]:
    https://github.com/tov/ge211-vendored-example/blob/master/3rdparty/ge211
    
