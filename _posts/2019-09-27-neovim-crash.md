---
title: "neovim crashes terminal when using netrw"
date: 2019-09-27
---
Due to a problem with neovim when combined with netrw crashing the terminal that was used to launch the  neovim session, I was forced into the situation where I had to revert back to using vim only.

I had set up my init.vim file to automatically launch netrw upon opening neovim. After doing this, I noticed that it would work as expected. However, when I closed the terminal and opened another terminal or neovim session, the entire terminal would freeze and there would be no characters on the terminal screen. Instead, I just saw a black screen that I was unable to interact with.
The only way to close the terminal screen was to kill the terminal session.

Since switching over to vim with a similarly modified version of init.vim (.vimrc for vim), I have found no problems at all with netrw working together with vim, which is great.

However it was a big pain to make vim work my neovim was working and I am still in the process of getting it to work as it used to. For example, getting commands like gg=G to work required some modification to the filetype plugin indent settings and I am happy now but still have some work to do, specifically realting to gettin the plugin that makes my JSX code format correctly. This a work in progress and I hope to remember why I had that plugin in the first place and restore it to the way that it was by the end of the weekend.
