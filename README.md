# git-hell
Git-hell is a login shell replacement which supports hosting many repositories on one shell account. Normal shell sessions are disabled and only predefined commands are accepted. New commands can easily be added.

The main motivation for this project is to be able to support hosting of many private git repositories with minimal administration. For example, many student repositories which are shared only with a teacher.

Features:
* one shell account can host multiple git-hell accounts
* each git-hell account can host multiple repositories
* users are identified via public key
* each public key corresponds to one git-hell account (many-to-one)
* initial authentication and set up is done via classical username/password identification
* initial installation of public key is done by the users themselves
* supports several commands such as help, list, addkey, init, ...
* easy to extend

Git-hell is similar to git-shell, but supports multiple private accounts identified via user's public key. It is also similar to gitosis and gitolite, but with minimum administration necessary - public keys are installed by users themselves.

Installation
------------

Installation is done on the remote machine. Superuser account is needed to create new user.

1) Create a shell account to be used for hosting git repositories and login into newly created account. As an example here account "git" and home directory "/home/git" are used. Git-hell is to be installed into "/home/git/git-hell". Change these to suit your needs. 

    sudo useradd -m -c "Git-hell hosting" -d "/home/git" -s "/home/git/git-hell/exec/shell" git
    sudo passwd git
    sudo su -s /bin/bash git
    cd

2) Download or clone source code.

    git clone https://github.com/jurem/git-hell.git

3) Edit tab-delimited accounts file "~/git-hell/conf/accounts.csv". For each account specify at least user and password. Passwords are (currently) stored as plain text.

Usage
-----

To get help

     ssh git@hostname.org help

Enable account and change password

    ssh git@hostname.org enable
    ssh git@hostname.org passwd

Generate private/public key (only if you haven't done it before)

    ssh-keygen

Install public key to git-hell

    cat .ssh/id_rsa.pub
    # copy printed key (including ssh-rsa and user@hostname)
    ssh git@hostname.org addkey
    # paste key when asked

Create and clone repository

    ssh git@hostname.org init repository.git
    git clone git@hostname.org:repository.git
