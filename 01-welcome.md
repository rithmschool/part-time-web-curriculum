#### [Table of Contents](./readme.md) | [Next ⇒](./02-html-part-1.md)

# Getting started with essential installations

### Objectives:

By the end of this chapter, you should be able to:

- Use oh-my-zsh to move around the terminal faster
- Install packages using homebrew and the package manager in Sublime
- Navigate in Sublime Text 3 much faster

### Important Note

The installation process assumes that you are using a Mac with OSX. If you are not running OSX, please first update so that you can follow along easier.

### Spotlight

Navigating your computer is a daily task, but sometimes it's difficult to find things. That's where Spotlight comes in. To launch Spotlight, simply type Command + spacebar and start searching. Anytime you need to open something, do it with Spotlight instead of using the mouse, you will get much faster!

Alternatively, if you'd like a tool that's a little more robust, [Alfred](https://www.alfredapp.com/) is a popular choice.

### Shiftit / Divvy

Unfortunately, Mac OSX does not have a great way to separate different windows into other locations on the screen. To solve this and improve your workflow you can either install [ShiftIt](https://github.com/fikovnik/ShiftIt) or download a free trial of [divvy](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=divvy%20free%20trial)

### Homebrew

Homebrew labels itself as "The missing package manager for OS X". Basically, homebrew is a one stop show to install things that do not come built into OSX. We will be using Homebrew quite a bit to install various packages/tools including Git.

[http://brew.sh/](http://brew.sh/)

### Xcode Command Line Tools

In the terminal type `xcode-select --install` and follow the instructions when it prompts you to install. If you already have this installed you will see a message saying `xcode-select: error: command line tools are already installed, use "Software Update" to install updates`. These tools are essential for compiling code during certain installations. 

### Git

Let's first start by installing git. You can see if you have `git` installed by typing `git --version`. If you see something like `command not found: git`, then keep going - overwise move on to the next tool. Open up the `Terminal` application and type in `brew install git` (it does not matter what directory/folder you are in)

### Oh my ZSH

To make it easier to navigate the terminal (and for use with Git) we will be installing `oh-my-zsh` which is a way to manage your `zsh` configuration. ZSH will be the shell we use in terminal. If you want to read more about those terms you can find some good info [here](http://superuser.com/questions/144666/what-is-the-difference-between-shell-console-and-terminal)

To install `oh-my-zsh` run this command anywhere in your terminal:

```bash
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
```

You may be prompted for your password. This is the same password you use when logging into your computer, but when you type characters you will not see them (this is for security). Once you have typed your entire password, press enter. If you have done this correctly, the installation should continue.

When you are done, run the following command:

```bash
chsh -s /bin/zsh
```

Now restart terminal (command + q) and then open up the terminal again. Anywhere in the terminal, type `echo $0` and if you see `-zsh` you have installed this successfully!

### Google Chrome

We will be using Chrome as our browser for this course since it has some of the most robust development tools. You can install it [here](https://support.google.com/chrome/answer/95346?hl=en).

### MacDown

MacDown is an open source Markdown editor which we will be using for writing and opening README files. You can install it [here](http://macdown.uranusjr.com/)

To learn more about markdown, head through the tutorial [here](http://www.markdowntutorial.com/). It is essential to have a basic understanding of Markdown so spend 10 minutes and walk through the tutorial and practice a bit using MacDown.

### Node

Node.js is a technology that allows us to run javascript on the server, but it is essential for testing javascript and installing other tools such as our linter. To install node, we will be using a tool called `nvm` which allows us to have different versions of node (useful for developing/debugging). To install nvm, run the following command anywhere in the terminal

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
```

Once this has finished, quit Terminal (command + q) and open it up again and type `command -v nvm` which should output `nvm`. If you are still having trouble, you can install node directly from [https://nodejs.org/en/](https://nodejs.org/en/). 

### Sublime Text 3

Sublime Text 3 is a text editor which we will be using for the program. While there is plenty of debate as to which editor to use, the truth is that it does not matter. However, we will be installing quite a few tools that are specific to Sublime that will **drastically** improve your speed and understanding, so it is **very** highly recommended that you use it. 

If you have Sublime Text 2 installed you will need to delete it, because many newer tools do not work with the older version. To check which version of Sublime you're using, open up the application. If you see Sublime Text 2 in the upper-left corner you are using 2 - if you just see Sublime Text then you are using Sublime Text 3.

You can install Sublime Text 3 [here](https://www.sublimetext.com/3 ) 

### Setting the subl alias

In order to open up Sublime Text, we either have to click on the icon or drag a file/folder to the icon, and this can be quite cumbersome. It would be quite nice if we could open up Sublime from the terminal using a command called `subl`. To do that, let's follow the instructions below: 

- **NOTE** instead of your `~/.bash_profile` you will be adding commands to `~/.zshrc` (the `.zshrc` file that lives in your home (`~`) directory)

[http://stackoverflow.com/questions/16199581/opening-sublime-text-on-command-line-as-subl-on-mac-os](http://stackoverflow.com/questions/16199581/opening-sublime-text-on-command-line-as-subl-on-mac-os)

### Package Control

The same way that Homebrew is a package manager for OSX, Sublime Text 3 has a package manager of its own which it calls package control. This is what must be installed so that we can download lots of helpful tools and add-ons to Sublime Text. Follow the instructions [here](https://packagecontrol.io/installation)

### Shortcuts

When learning how to code, one of the most valuable things you can do is learn how to move around your computer, terminal and text editor quickly. The same way that you learned many shortcuts, this just requires a bit of muscle memory and patience, but being able to move around quicker will tremendously help you as a developer. Here are some essential shortcuts - we **cannot** stress how important they are to learn and use:

#### Terminal Shortcuts

| Command | Result |
|---|---|
| Tab | Auto-complete files and folder names |
| Ctrl + A | Go to the beginning of the line you are currently typing on |
| Ctrl + E | Go to the end of the line you are currently typing on |
| Ctrl + U | Clear the line before the cursor |
| Ctrl + K | Clear the line after the cursor |
| Ctrl + W | Delete the word before the cursor |
| Ctrl + T | Swap the last two characters before the cursor |
| Esc + T | Swap the last two words before the cursor |
| Ctrl + R | Lets you search through previously used commands |
| Ctrl + L or Command + K | Clears the Screen |
| Ctrl + C | Kill whatever you are running |
| Ctrl + D | Exit the current shell | 

#### Sublime Shortcuts

|Command|Result|
|---|---| 
| *⌘T* | go to file |
| *⌃G* | go to line |
| *⌘KB* | toggle side bar |
| *⌃ `* | python console |
| *⌘⇧N* | new window (useful for new project) |

|Command|Result|
|---|---| 
| *⌘L* | select line (repeat select next lines) |
| *⌘D* | select word (repeat select others occurrences in context for multiple editing) |
| *⌃⇧M* | select content into brackets |
| *⌘⇧↩* | insert line before |
| *⌘↩* | inter line after |
| *⌃⇧K* | delete line |
| *⌘KK* | delete from cursor to end of line |
| *⌘K⌫* | delete from cursor to start of line |
| *⌘⇧D* | duplicate line(s) |
| *⌘J* | join lines |
| *⌘KU* | upper case |
| *⌘KL* | lower case |
| *⌘ /* | comment |
| *⌘⌥ /* | block comment |
| *⌘Y* | redo or repeat |
| *⌘⇧V* | past and ident |
| *⌃ space* | autocomplete (repeat to select next suggestion) |
| *⌃M* | jump to matching brackets |
| *⌘U* | soft undo (movement undo) |
| *⌘⇧U* | soft redo (movement redo) |

h2. Find/Replace

|Command|Result|
|---|---| 
| *⌘F* | find |
| *⌘⌥F* | replace |
| *⌘⌥G* | find next occurrence of current word |
| *⌘⌃G* | select all occurrences of current word for multiple editing |
| *⌘⇧F* | find in files |

|Command|Result|
|---|---| 
| *⌘⌥1* | single column |
| *⌘⌥2* | two columns |
| *⌘⌥5* | grid (4 groups) |
| *⌃[1,2,3,4]* | focus group |
| *⌃⇧[1,2,3,4]* | move file to group |
| *⌘[1,2,3...]* | select tab |

### Exercise

[https://typing.io/](https://typing.io/)

[http://play.typeracer.com/](http://play.typeracer.com/) 

### Additional Resources

[http://www.wdtutorials.com/cheat-sheets/sublime-text-keyboard-shortcuts-cheat-sheet-win-os-x-and-linux](http://www.wdtutorials.com/cheat-sheets/sublime-text-keyboard-shortcuts-cheat-sheet-win-os-x-and-linux)

[https://www.viget.com/articles/my-overused-sublime-text-keyboard-shortcuts](https://www.viget.com/articles/my-overused-sublime-text-keyboard-shortcuts)

#### [Table of Contents](./readme.md) | [Next ⇒](./02-html-part-1.md)
