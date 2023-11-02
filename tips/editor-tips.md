# Configuring VI

The exam environment will not come with an IDE, so it is crucial to become confortable
using a terminal-based editor such as 'vim' or 'nano' for editing.

I recommend to become confortable with 'vim' since the labs already come with this editor pre-configured
and aliased to 'vi'.

There are a few resources out there for this, but I would recommend the following for differente learning approaches:

- https://github.com/kodekloudhub/community-faq/blob/main/docs/vi-101.md  as a cheatsheet 
- https://vim-adventures.com/ as an interactive game to learn vim motions

Now, what is important is to set some basic configurations to allow for speed.
Enter 'vi ~/.vimrc' in the console and type the following:

```
set nu    # Sets line numbers
set rnu   # Sets relative line numbers
set sw=2  # Set shift width to 2 characters
set et    # Set expand tabs to spaces
set ts=2  # Set tabstop to 2 characters
set ai    # Set auto indent
```

Try to remember a acronym to ease the input of this configuration from memory like using the first
words of the config:

- SET-A-NR (set a number) which would translate to:

```
set sw=2
set et
set ts=2
set ai
set nu
set rnu
```

Get creative here and type these configurations for some days until you memorize them.
After the configuration file has been edited, save it using `ZZ` and then source it to apply 
the configurations using `source ~/.vimrc`.

# Configuring aliases 

