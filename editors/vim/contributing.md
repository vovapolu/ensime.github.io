---
layout: section
order: 5
title: Contributing
---

## Contributing to the ENSIME-Vim Plugin

First you'll need to pull the repository, add a symlink to the plugin directory used by your respective Vim plugin manager, and add the line to `.vimrc`/`init.vim` to load the plugin if necessary.

Steps:

1. Fork the https://github.com/ensime/ensime-vim repo
1. Pull locally:

    ```
    $ git clone git@github.com:YOURUSER/ensime-vim
    $ git remote add upstream git@github.com:ensime/ensime-vim
    ```
1. Install your fork of ENSIME-Vim instead of the ensime org's master. For most plugin managers this means replacing the ensime organization's name with your own in the argument to the install function (e.g. `Plugin` for Vundle, `Plug` for vim-plug, `NeoBundle` for neobundle, etc.).
    - If you have already installed ENSIME-VIM you may need to clean your plugins to remove references to the upstream before installing your fork.

### Getting Help

The best place for help is [the ensime-vim Gitter channel][gitter channel]. If nobody there can help you, please open an issue on the repository!

### Code Organization

ENSIME-Vim is written in a combination of Python and VimL. The VimL code is really just for integrating with Vim & other plugins, while the Python code handles ENSIME functionality.

##### ENSIME integration

- The majority of the interesting code lives in the `ensime_shared` directory. Here you'll find
    - `ensime.py`, which implements all of the request and response handling logic around ENSIME. This is the heart of the plugin.
    - `launcher.py`, which is responsible for starting up ENSIME, loading the config, and generating classpath files
    - Several other helper files like `config.py`, `error.py`, etc. that each implement small functions dealing with their namesakes

- **Common Tasks**
    - Fixing a bug:
        First understand if the bug is happening in ENSIME or the Vim plugin. The best way to determine this is to issue a command and compare the input/output of the call in the `.ensime_cache/ensime-vim.log` of your project.
         - If the bug is on what we're sending to ENSIME, simply follow the path of the command through the code until you reach the send call. 
         - For bugs in response handling, you'll want to check the `handlers` dictionary and find the function mapped to the ENSIME server response type you're seeing.
    - Extending an existing Command:
         - All of the existing commands are defined in `rplugin/python/ensime.py` or `plugin/ensime.vim`, depending on Neovim or Vim:
         - Each of the `com_do_something` calls is implemented in the `Ensime` class in `ensime_shared/ensime.py`, which indicates which API handling functions are called
         - To change the behavior, you'll likely only need to make changes in the request/response handling code, as the command has already been wired up.
    - Adding a new Command:
        - New ENSIME-Vim commands are a very similar to existing ones, except you're responsible for determining whether it is a standard command or an autocommand. Standard commands are initiated by the user, while autocommands are executed by Vim whenever certain events occur. For a good overview of commands & autocommands I recomend reading Steve Losh's book [Learn VimScript the Hard way](http://learnvimscriptthehardway.stevelosh.com/chapters/12.html)
        - The new command should be added to `plugin/ensime.vim`, `rplugin/python/ensime.py`, `autoload/ensime.vim`, and of course implemented in `ensime_shared/ensime.py`, plus any helper files necessary.
        - To expose your new command Neovim users may need to run `:UpdateRemotePlugins`
    - Exposing New Vim Functionality:
        - ENSIME-Vim has a number of Vim commands we execute, all of which can be found in the `commands` dictionary in `ensime_shared/ensime.py`. Adding a new command is as simple as adding a new pair to the dictionary. 

##### Testing

The test suite consists of BDD feature specifications executed with [Lettuce][], a Python framework supporting the Gherkin language. These tests are located in `ensime_shared/spec/features` and can be run with `make test` or simply `make`.

This test suite is relatively young, after dropping old test infrastructure that had fallen into disrepair. Contributions restoring and extending coverage are most welcome. A unit testing setup may be desirable but does not yet exist, it is hoped that some higher-level Gherkin acceptance specs can eventually be shared with other editor plugins.

##### Useful Links

- [ENSIME Contributing](/contributing/)
- [ENSIME API Source](https://github.com/ensime/ensime-server)
- [VimScript The Hard Way](http://learnvimscriptthehardway.stevelosh.com/)
- Vim Documentation (`:h <your-term-here>`)
- Other Vim Plugins
    - [NerdTree](https://github.com/scrooloose/nerdtree) Lots of great insights on how to extend Vim's UI
    - [vimmode-python](https://github.com/klen/python-mode) Good for learning about autocomplete, loc vs. qf lists, preview buffers, etc...

[gitter channel]: https://gitter.im/ensime/ensime-vim
[Lettuce]: http://lettuce.it/
