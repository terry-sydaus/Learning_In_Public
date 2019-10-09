---
title: "vim-plug plugin manager for vim installed and plugins working again"
date: 2019-10-09
---

Just a follow up from my previous post regarding getting the JSX plugins working as they used to in Neovim.

I am happy to report that this was quite simple in the end and required me to install the vim "vim-plug" plugin manager using the followig command:

````bash
curl -flo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
````

Note, the web site that I used as the source of this command had a back slash character inserted between the "--create-dirs" and the "https..." elements of the command. When I first used that command including the "\\\", I received an error on saying that http is not supported by libcurl or a message to that effect. This is because the command as you type it at your command line is not supposed to include the "\\\". It was included by the author of the web page that I was referring to as an escape character to signify that the command was to be issued on one line and was not meant to traverse two lines, which is how the command appeared on the page. Refer to [https://github.com/junegunn/vim-plug] and you will see the command under the [Vim / Unix](https://github.com/junegunn/vim-plug) section of the web page, inclusive of the backslash, which you must **not** type when issiuing the command from the command line.

And since doing this, and reloading my .vimrc file, which will be the subject of another blog post - in terms of how I achieve this elegantly and effortlessly, I no longer receive errors related to the plugin commands that are called by my .vimrc file. Furthermore, when I issue the following command from within a vim session:

````bash
:PlugInstall
````

I can see that the two plugins (pangloss/vim-javascript & mxw/vim-jsx) that I require for the correct formatting of my javascript files and any jsx that they may contain are indeed loaded and ready to provide the functions that I require them to perform as I go about my business.

````vim
call plug#begin('~/.vim/plugged')
Plug 'pangloss/vim-javascript'
Plug 'mxw/vim-jsx'
call plug#end()
````
Hope this is useful for anyone else experiencing any issues with installing the vim-plug plugin manager and installing & activating plugins using a plugin manager.

[https://github.com/junegunn/vim-plug]: https://github.com/junegunn/vim-plug
