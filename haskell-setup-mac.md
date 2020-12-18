# Haskell Setup


## 1. Install ghcup (and ghc, and cabal)

[Haskell.org](https://haskell.org/downloads) has instructions for minimal and platform installation. I recommend the platform  install, as it will make things like getting your IDE set up easier later. [The Mac platform instructions](https://www.haskell.org/platform/mac.html) recommend [installing ghcup](https://www.haskell.org/ghcup/) first.  It will include both ghc and cabal-install. After successfully installing `ghcup` via curl/sh, you are asked if you'd like to install the Haskell Language Server, or HSL--which you do, however, I recommend installing it separately afterward (instructions below), as the auto installed HSL was out of date. It will even detect your shell and ask if you'd like it to add `ghc` and `ghcup` to your path. 

**NOTE:** I had to manually edit my `.zshrc` to move the line it added to its own line. Could be a bug in their script or something with my `.zshrc`. Not sure.
`¯\_(ツ)_/¯`

Make sure it all worked:
```sh
$ which ghcup
$ which ghc
$ which cabal
```

Check your version of the GHC (Glasgow Haskell Compiler) and update if necessary:
```sh
$ ghcup list
$ ghcup install ghc 8.10.2
```

Awesome! We describe how to use `ghcup` to install the HSL below.


## 2. Install Stack

Next, it is recommended to install the [stack](https://docs.haskellstack.org/en/stable/README/) dev tool which is used for:
* Installing isolated GHC
* Installing Haskell dependencies
* Building, testing, and benchmarking your Haskell project

Check yourself:
```sh
$ which stack
```

Update Stack:
```sh
$ stack upgrade
```


## 3. Try it out!

1. Try the REPL:
```sh
$ stack ghci
```
**NOTE:** to exit the REPL, type `:quit` and press enter.

2. Create a new project:
```sh
$ stack new my-project
```

3. Manage your project's dependencies in the `project.yaml` or `*.cabal` file
   (for example, add the `text` package) and then run:
```sh
$ stack build
```

4. Run your project as an executable:
```sh
$ stack exec my-project-exe

```
5. Check out the rest of the stack commands:
```sh
$ stack --help
```

6. Read the [stack guide](https://docs.haskellstack.org/en/stable/GUIDE/).


## 4. Set up your IDE

* [Install the Haskell Language Server](https://github.com/haskell/haskell-language-server#installation) and get your favorite IDE (e.g.: [Vim](https://github.com/haskell/haskell-language-server#using-haskell-language-server-with-vim-or-neovim), [VSCode](https://github.com/haskell/haskell-language-server#using-haskell-language-server-with-vs-code)) set up to use it so you can get hints and autocompletion in your IDE. This will be different for everyone depending on your IDE, OS, etc.
* If you are using VIM, you'll need to installthe [COC plugin](https://github.com/neoclide/coc.nvim), and you'll want to check out the vimrc suggestions in the COC README file.


## Other Important Notes

* **Be wary of Haskell Wiki** (https://wiki.haskell.org) as it seems to have a lot of outdated information.
	* e.g.: the page on Vim still instructs you to install the deprecated ~haskell-ide-engine~ (which you should not do).


## TODOs

Things that confused me at some point, and I'd like to explain for other new Haskellers and future me.

* What is ghcup? It seems like it just installs everything Haskell dev related.
* How do `stack` and `cabal` differ? They both seem to be build tools? Maybe
  `stack` just uses `cabal` for builds under the hood? Who the what? Huh? Wat?
* What's the difference between editing `project.yaml`, your `*.cabal` file,
  and running `stack build` vs. `stack install <package-name>`?
* Does `stack` already come with ghcup? I seemed to already have it, but I may have previously installed it at some point.

