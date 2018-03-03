---
layout: post
title: "Installing Standard ML on OS X"
categories: "SML"
author: "ke_an"
meta: "Standard ML"
description: "Installing Standard ML on OS X. Standard ML is one of the most popular languages to start learning functional programming in academic institutions. It’s design influenced Haskell, Scala, Rust, OCaml (of course..) and other less known languages. Standard ML comes in several flavours/compilers, but most popular are Standard ML of New Jersey, Moscow ML, Poly/ML, MLton. Let’s start with SML/NJ, the most widely used one."
---
Standard ML is one of the most popular languages to start
learning functional programming in academic institutions. 
It's design influenced Haskell, Scala, Rust, OCaml (of course..)
and other less known languages. Standard ML comes in several flavours/compilers, but
most popular are Standard ML of New Jersey, Moscow ML, Poly/ML, MLton.   
Let's start with SML/NJ, the most widely used one.

First install [Homebrew package manager](https://brew.sh/){:target="_blank"} in case you don't have it yet:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next step is for SML/NJ:
```
$ brew install smlnj
```

Update your environment variables in default editor:
```
$ open -t ~/.bash_profile
```

Insert path to your SML/NJ /bin directory:
```
export PATH=/usr/local/Cellar/smlnj/110.82/bin:$PATH
```

_Cellar_ is a folder created by Homebrew for it's packages. 
Save and close the editor.   
Reload your user profile:
```
$ source ~/.bash_profile
```
Now you can run SML/NJ compiler from command line with simple:
```
$ sml
```
It should output the name of the compiler and the version, e.g.:
```
Standard ML of New Jersey v110.82 [built: Tue Jan  9 20:54:24 2018]
-
```
Close the compiler with Ctrl+Z

### - - SML Editor - -

SML files can be edited in any editor of your choice.
But classic editing tool for SML is GNU Emacs, hereinafter referred to as
Emacs - so we'll setup SML editing environment in this universal kitchen sink.

![emacs-kitchen-sink](http://ergoemacs.org/emacs/i/emacs_kitchen_sink_icon_1987.png
){:class="img-center"}

Let's get it:
```
$ brew install emacs --with-cocoa
```

After Emacs is installed, we need to be sure sml-mode is working.
Open Emacs and then package manager with:

``` 
M-x list-packages <RET>
```
which means:
```
press ALT+x then type list-packages then press ENTER
```

> Emacs shortcuts being written as **C(ontrol)-c** [Used:Ctrl-c] or **M(eta)-x** [Used:Alt-x]   
due to historic reasons - Emacs was developed on Lisp machine, using
[space-cadet keyboard](https://en.wikipedia.org/wiki/Space-cadet_keyboard){:target="_blank"} with
Meta and Control keys.   
More about Emacs shortcut history you can find in the article 
[Why Emacs's Keyboard Shortcuts are Painful](http://ergoemacs.org/emacs/emacs_kb_shortcuts_pain.html
){:target="_blank"} 

By pressing _f_, we will get into search mode, enter _sml-mode_ as a search word and 
press _Enter_.

If sml-mode package status is other than installed - place the cursor on the
line with sml-mode package and press _i_, followed by _x_. 
The package should be installed now.

### - - Running SML/NJ compiler from Emacs - -

In order to be sure SML/NJ compiler will be called within Emacs, we need to add
some configurations to user settings:
```
$ touch ~/.emacs 
```

add these lines to your _.emacs_ file:
``` lisp
(autoload 'sml-mode  "sml-mode" "Mode for editing SML." t)
(setenv "PATH" (concat "/usr/local/Cellar/smlnj/110.82/bin:" (getenv "PATH")))
(setq exec-path (cons "/usr/local/Cellar/smlnj/110.82/bin"  exec-path))
(setq sml-program-name "sml")
```

Restart Emacs. Time to test.

### - - Testing - - 

Firstly we will test sml-mode:
```
M-x sml-mode <RET>
```
after that your mode from _(Fundamental)_ should change to _(SML)_
in your 
[mode line](https://www.gnu.org/software/emacs/manual/html_node/emacs/Mode-Line.html){:target="_blank"} 

Secondly, we will test invoking compiler within Emacs:
```
M-x run-sml <RET>
```

Emacs will start SML in a new buffer. 
It should have _(Inferior-SML: run Compilation)_ in it's mode line.

Now test it with the code. Open empty buffer:
```
C+x b 
```

Type your new buffer name e.g.: _sml-mode-test_. Change to sml-mode:
```
M-x sml-mode <RET> 
```

Type: 
```
1+1;
```

in your buffer and press:
```
C-c C-b
```

this command will send the code from your buffer to the compiler.
The result should look like this:

![emacs-sml-mode](/assets/img/2018-03-03_emacs_sml.png){:class="img-center"}

You can close the buffer with:
```
C-x k bufname <RET>
```

List/switch between buffers
```
C-x b <TAB>
```

More about sml_mode commands in
[SML mode - The Emacs SML editing mode](https://www.smlnj.org/doc/Emacs/sml-mode.html){:target="_blank"}.   
You are ready to go.

