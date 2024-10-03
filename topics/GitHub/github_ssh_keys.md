---
parent: GitHub
grand_parent: Topics
layout: default
title: "github: using ssh keys"
description:  "generating public/private key pair, uploading public key to github"
indent: true
---

This is a tutorial on how to:

* set up your computer (i.e. your laptop) or your CSIL account with an ssh public/private key pair
* upload your *public* key to github 
* SO THAT you can use the ssh github clone URLs instead of the https ones.

See also: [github's own tutorial on the same topic](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

# Why would I want to do that?

Because it allows you to do push operations
to repos, and pulls from private repos, without having type in your username and password.

That's a lot more convenient.  (If you choose to protect your ssh public/private key pair with a passphrase,
you may to type that in, but its up to you whether to set that up or not.)

# Ok, how do I do it?

It's a two step process.

(1) Set up your public/private key pair.

(2) Upload that key to github 

Note that you need to do this step separately for each computer you work on (i.e. once for your laptop, another time for your desktop,
and yet again if/when you work from the CSIL command line).

# What's a public/private key pair?

In a nutshell, the idea of a public/private key pair is this:

-   you generate them together
-   you share the public key with other folks, and keep the private key a secret on your own hard drive
-   anyone that has the public key can be sure that a message coming from you is definitely coming from you, because it got encrypted with the private key, and can only be decrypted with the public key. This way, you don't have to type in your password to authenticate yourself to various sites.

To see if you already have an ssh public/private key pair set up on a certain machine:

-   cd to your home directory
-   type: `ls` `-al` `.ssh`

If you see files called id\_rsa.pub and id\_rsa, then you have a public/private key pair, like this:

    -bash-4.2$ cd
    -bash-4.2$ ls -al .ssh
    total 64
    drwx------   2 pconrad faculty  4096 Apr 26  2012 .
    drwx--x--x 127 pconrad faculty 16384 Mar 14 04:41 ..
    -rw-r--r--   1 pconrad faculty  1051 Oct 17  2011 authorized_keys
    -rw-------   1 pconrad faculty  1675 Sep 15  2008 id_rsa
    -rw-r--r--   1 pconrad faculty   394 Mar  7  2010 id_rsa.pub
    -rw-r--r--   1 pconrad faculty  9654 Mar 12 14:09 known_hosts
    -bash-4.2$ 

If you don't even have a .ssh directory, or if you have one, but don't see the id\_rsa and id\_rsa.pub files,
then you'll need to set up one up, as explained below.

Step 1: Create a public/private key pair
=========================================

The UNIX command to create a public/private key pair is: `ssh-keygen`

Note: MacOS users should use `ssh-keygen -t rsa -b 4096`
* Apparently, recent versions of MacOS are defaulting to a new key standard, `ed25519`, which Github doesn't yet support as of October 2024.
* It is possible that by the time you read this, that will have changed.

You can type that at any unix prompt.  Folks usually are in their home directory when they do it, but
I don't think it really matters.

You'll be asked a series of questions.  Just take the default for each question, as shown below. If you want to create a
passphrase to protect your key from evildoers, you can.  That's an extra measure of security, at the cost of
a bit more inconveience (you'll have to type that every time you use the key.)  That's up to you.

Here's an example of creating a public private key pair. (Note: this is not my real key.  I backed up my key, generated this one, then threw it out and restored my original.)


```
-bash-4.3$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/cs/faculty/pconrad/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /cs/faculty/pconrad/.ssh/id_rsa.
Your public key has been saved in /cs/faculty/pconrad/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:OVYQo4jDVsedeLLVZjTQUBHLlcFTU/BAedq0dwCaR10 pconrad@butthead.cs.ucsb.edu
The key's randomart image is:
+---[RSA 2048]----+
|    ...o*X*+=B*=E|
| . o o+.=+=B+ ++o|
|  = . .= o* .. *o|
| . .  .  o .  ..+|
|        S       o|
|       . .       |
|                 |
|                 |
|                 |
+----[SHA256]-----+
-bash-4.3$
```

# Troubleshooting

If you encounter problems using your SSH keys, try typing one or both of these command into your command shell:

-   `chmod` `700` `~/.ssh/id_rsa`


The first command changes the permissions on your private key, ensuring that you personally have all access. The second command adds your new private key to your SSH keyring.

**Should I make a passphrase, or just hit enter?**

The advantage of making a passphrase is more security. If someone gets a copy of your private key, then they can pretend to "be you", and do anything you've authorized your private key to be able to do. However, if your private key is protected with a passphrase, then it can't be used unless the thief knows your passphrase.

The disadvantage of a passphrase on your private key is that you have to type in your passphrase every blessed time you do anything with your public/private key pair—which sort of defeats the whole "convenience" aspect of setting it up in the first place. Ultimately, it's your decision.

Step 2: Upload your public key to your github account
-----------------------------------------------------

VERY IMPORTANT: you want to upload your `id_rsa.pub` file to `github.com`

You do NOT upload your `id_rsa` file to github.com. That file is your private key, and needs to stay private and protected.

You don't actually "upload" your `id_rsa.pub` to github.com.   You actually just copy and paste the value. `cd` into the `~/.ssh` directory and use the command `cat id_rsa.pub` to have the file be printed in the terminal like this

```
    (~/.ssh)$ cat ~/.ssh/id_rsa.pub
    ssh-rsa 
    AAAAB3NzaC1yc2EAAAADAQABAAABAQDYySoh7b1uGpI7saLozpgXz184YYgC9k22zLH8TqKiSLAcNCO5hEzgC0kZoytCMtw/hUx3kto8
    apPS4ORL6HebWXuGfzQ3nQslPpBNmto0hdo446wBu/Hl5a7pC3SZUzti4YbUjRDOBgM5zQMaopTXhtqNY/tRB8/lSSYaEtIxLN5twk29
    IQUoA2wdPTmU/fRPc3PUdD9/KHJfBIL/ROsOb73tGOxqZoMnzV0ElmLhjq6WEqNWypaFrI0YU8OmIvxmlDXn0gkr3oYHqrbz5qznSust
    ucWBEFZ3lekvZiXrqizFplYZF+LiG9TOGjhxujOJ+sIcCy0BCN4msb1/lguN hamstra@csil.cs.ucsb.edu
    (~/.ssh)$
```

Then you want to copy the text contents of the file, starting with 'ssh-rsa AAAAA...' and ending with '...@csil.cs.ucsb.edu'.

* Keep in mind that uploading a public SSH key gives access to your github account to whoever has access to the matching private SSH key on his/her computer.
* So make sure that you are using YOUR OWN public ssh key—and not the key shown in the example above.

To do this, login to the page <http://github.com>

Look for the gear icon in upper right to take you to the settings screen.

Click on the tool icon, and it should take you to a screen like this—you are looking for the SSH Keys menu item on the left:

<div style='border:1px solid black;' markdown="1">
<img src="http://i.imgur.com/xXESmRI.png" alt="ssh" />
</div>

Click on that, and you'll be taken to this screen, where you can upload a new public key:

<div style='border:1px solid black;' markdown="1">
<img src="http://i.imgur.com/z8blAzI.png" alt="ssh" />
</div>

Once the key is uploaded, you're all set to be able to use github.com in the most streamlined way possible. What you do is simply use the SSH version of the URL instead of the https version of the URL when you first clone your repository.


# References:

* <https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/>
