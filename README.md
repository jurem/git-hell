# git-hell
Git hosting on one shell account.

Similar to git-shell, but supports multiple private accounts identified via user's public key. Similar to gitosis and gitolite, but with minimum administration - public keys are installed by users themselves.

Some features:
* one shell account can host multiple git-hell accounts
* each git-hell account can host multiple repositories
* users are identified via public key
* each public key corresponds to one git-hell account
* installation of public key is done by user via classical username/password identification

Installation
------------

Installation is done on the remote machine. Superuser account is needed to create new user.

1) Create a shell account to be used for hosting git repositories and login into newly created account. As an example here account "git" and home directory "/home/git" are used. Git-hell is to be installed into "/home/git/git-hell". Change these to suit your needs. 

    sudo useradd -m -c "Git-hell hosting" -d "/home/git" -s "/home/git/git-hell/exec/shell" git
    sudo passwd git
    sudo su -s /bin/bash git
    cd

2) Download or clone source code.

    git clone git@github.com:jurem/git-hell.git

3) Edit tab-delimited accounts file "~/git-hell/conf/accounts.csv". For each account specify at least user and password. Passwords are (currently) stored as plain text.

Usage
-----

To get help

     ssh git@hostname.org help

Enable account and change password

    ssh git@hostname.org enable
    ssh git@hostname.org passwd

Generate private/public key (do this only if you do not already have done it before)

    ssh-keygen

Install public key to git-hell

    cat .ssh/id_rsa.pub
    # copy printed key (including ssh-rsa and user@hostname)
    ssh git@hostname.org addkey
    # paste key when asked

Create and clone repository

    ssh git@hostname.org init repository.git
    git clone git@hostname.org:repository.git
