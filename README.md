# O(1) Labs Opam Repository

This is O(1) Labs's custom [opam](https://opam.ocaml.org/) repository.
We use this repository as incubator before publishing packages to the [official opam repository](https://github.com/ocaml/opam-repository).

## Publishing to this repository

We use [dune-release](https://github.com/ocamllabs/dune-release) to publish to this repository. 

1. to do this, you will first have to install dune release:
    ```console
    $ opam install dune-release
    ```
1. then fork this repository (let's say under `your_name/opam-repository`) and clone this repository somewhere (at some point `dune-release` will ask you for that information)
1. add the new version (following [semver](https://semver.org/)) and a changelog to your `CHANGES.md` file (see [example](https://github.com/o1-labs/ppx_version/blob/master/CHANGES.md)), as well as your `<package>.opam` or `opam` file.
1. optionally make sure your opam file is in sync with your dune file
    ```console
    $ opam install opam-dune-lint
    $ opam-dune-lint
    ```
1. make sure your opam file is ready to be published
    ```console
    $ dune-release lint
    ```
1. tag your release (this should pick up the version automatically from the `CHANGES.md` file)
    ```console
    $ dune-release tag
    ```
1. produce artifacts
    ```console
    $ dune-release distrib
    $ dune-release publish
    $ dune-release opam pkg
    ```
1. create a PR to your fork of this repository, where `<USER>` is your Github username, `<REMOTE>` is your fork of this repository (most likely `<USER>/opam-repository`), and `<LOCAL>` is the local path to a clone of your fork.
    ```console
    $ dune-release opam submit --opam-repo=o1-labs/opam-repository --user <USER> --remote-repo <REMOTE> --local-repo <LOCAL>
    ```
1. once the PR has been created, merge it in your own fork, then create a PR manually between your fork and this repository.

The `dune-release` flow is summarized in their nice diagram below.

![dune release flow](https://ocaml-explore.netlify.app/images/dune-release.png)

## Known issues

* [custom opam repositories are not well-handled](https://github.com/ocamllabs/dune-release/issues/362)
