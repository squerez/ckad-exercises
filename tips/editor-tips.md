# Configuring VI

The exam environment will not come with an IDE, so it is crucial to become confortable
using a terminal-based editor such as 'vim' or 'nano' for editing.

I recommend to become confortable with 'vim' since the labs already come with this editor pre-configured
and aliased to 'vi'.

There are a few resources out there for this, but I would recommend the following for different learning approaches:

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

Create the following file at `$HOME/.krc`:
```
#
# Kubectl Alias and Environment Variables file.
# Run 'source $HOME/.krc' if file is modified to take effect in the current shell
#
#
# Enable Kubectl autocomplete as recommended by Kubernetes cheatsheet
# Ref: https://kubernetes.io/docs/reference/kubectl/cheatsheet/
source <(kubectl completion bash) 

#
# Aliases
#
# Tip: Get used to use the shorthand versions of the commands
# If you don't know it, run `khelp` to get all shorthands
#
alias k=kubectl
alias khelp=kubectl api-resources

#
# Global helpers
#
# To use them you just need to use the command normally like so:
# `k run pod1 --image=nginx $do`
# or `k delete pod1 $now`
# or `ke pod1 -- command`
# or `kl`
#
export do='--dry-run=client -o yaml'
export dos='--dry-run=server -o yaml'
export now='--force --grace-period 0'
alias ke='kubectl exec -it'
alias kl='kubectl logs'

#
# Describe helpers
#
# To use one of this do it like so:
# `k dd`
#
export da='describe all'
export dn='describe node'
export dd='describe deploy'
export dp='describe pod'
export ds='describe service'

#
# Get helpers
#
# To use one of this do it like so:
# `k gn`
#
export gn='get ns -A'
export gno='get nodes -w'
export gd='get deploy -w'
export gp='get po -o wide -w'
export gs='get svc -w'
export ge="get events --sort-by='.lastTimestamp'"

#
# Functions
#
# Runs a command in a temporary pod
# to run use: `tmp "some command"`
#
tmp () {
    kubectl run tmp -i --rm --restart=Never --image=nginx:alpine -- /bin/sh -c "$1"
}

#
# Changes namespace
# to run use: `sns namespace`
#
sns () {
    kubectl config set-context --current --namespace $1
}

# End of $HOME/.krc
```

Now, you just need to run the following command in order for these aliases to take effect automatically: 

```echo "source ~/.krc" >> ~/.bashrc && source ~/.bashrc```

--------------------
Additional read material
--------------------

- https://freedium.cfd/https://medium.com/the-aws-way/kubernetes-certifications-cka-ckad-prep-tip-3-fast-and-furious-with-kubectl-aliases-a56a3095435a#4ae0
- https://medium.com/@jenksgibbons/cka-ckad-cks-exam-taking-tips-and-tricks-0c7d749f4021
- https://kubernetes.io/docs/reference/kubectl/quick-reference/
- https://github.com/moabukar/CKA-Exercises/blob/main/Useful-Commands%20%26%20Aliases.md
