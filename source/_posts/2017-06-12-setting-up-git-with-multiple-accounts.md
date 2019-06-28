---
title: Setting up git with multiple accounts
categories:
    - system
    - linux
    - git
tags:
    - debian

---
##git install

    sudo apt-get install git
    
###git config

	git config --global user.email benoit.works@gmail.com
	git config --global user.name ben
	cat .gitconfig 
	[user]
		email = benoit.works@gmail.com
		name = ben

###ssh keys

####github key
	ben@debian:~$ ssh-keygen -t rsa -C "benoit.works@gmail.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/home/ben/.ssh/id_rsa): /home/ben/.ssh/id_rsa_github
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /home/ben/.ssh/id_rsa_github.
	Your public key has been saved in /home/ben/.ssh/id_rsa_github.pub.
	The key fingerprint is:
	e0:ff:69:e3:fd:67:9b:97:7e:3b:d7:0c:5e:c8:98:94 benoit.works@gmail.com
	The key's randomart image is:
	+---[RSA 2048]----+
	|                 |
	|                 |
	|      .      .   |
	|     . .    E    |
	|      . S  . + . |
	|       .    o + .|
	|        .    . +o|
	|         .oo  .oX|
	|         o+...oBB|
	+-----------------+
	ben@debian:~$ ls -al .ssh/
	total 16
	drwx------  2 ben ben 4096 juin   7 10:01 .
	drwxr-xr-x 21 ben ben 4096 juin   7 10:00 ..
	-rw-------  1 ben ben 1675 juin   7 10:01 id_rsa_github
	-rw-r--r--  1 ben ben  404 juin   7 10:01 id_rsa_github.pub


	ben@debian:~$ ssh-add ~/.ssh/id_rsa_github
	Identity added: /home/ben/.ssh/id_rsa_github (rsa w/o comment)


Add the public key to your github account.

####bitbucket key

	ben@debian ~ $ ssh-keygen -t rsa -C "benoit.works@gmail.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/home/ben/.ssh/id_rsa): /home/ben/.ssh/id_rsa_bitbucket
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /home/ben/.ssh/id_rsa_bitbucket.
	Your public key has been saved in /home/ben/.ssh/id_rsa_bitbucket.pub.
	The key fingerprint is:
	04:75:ba:a3:71:a4:1e:3e:0a:31:f8:a1:b3:70:57:81 benoit.works@gmail.com
	The key's randomart image is:
	+---[RSA 2048]----+
	|      ... .      |
	|     . . o       |
	|    E . +        |
	| .     = .       |
	|. +   = S        |
	| o + + = .       |
	|+ + . =          |
	|.+ o . .         |
	|.   .            |
	+-----------------+

    ben@debian ~ $ ssh-add ~/.ssh/id_rsa_bitbucket
    Identity added: /home/ben/.ssh/id_rsa_bitbucket (rsa w/o comment)

Add the public key to your bitbucket account.

###ssh config file

Edit `~/.ssh/config file`

	# Default GitHub user
	Host github.com
	 HostName github.com
	 PreferredAuthentications publickey
	 IdentityFile ~/.ssh/id_rsa_github
	 
	# bitbucket account
	Host bitbucket.org
	 HostName bitbucket.org
	 PreferredAuthentications publickey
	 IdentityFile ~/.ssh/id_rsa_bitbucket