Title:   Getting started
Summary: Session 0: Prerequisites and installation instructions
Authors: Adina Wagner
         Lennart Wittkuhn
Date:    2020

In order to follow workshop materials, please make sure that you install the relevant software and set it up appropriately.
At the end of this page, a short script can help you to verify that everything works as it should.

If you run into problems, please get in touch **prior** to the workshop.
We are happy to help with installation problems or general questions, but a virtual workshop does not allow for any concurrent user support and help, unfortunately, and we thus won't be able to deal with problems that surface during the sessions. Reach out to us about problems as early as you can by filing an issue on our GitHub repository: [github.com/adswa/mpi-datamanagement-ws/](https://github.com/adswa/mpi-datamanagement-ws/issues/new).

If you haven't set up the software, you will be able to attend the workshop, but not work interactively on the materials.

| **NOTE FOR WINDOWS USERS** |
|------------------------------------------------------------------|
| Previous workshop experiences have taught us that the installation of all required software is more complex on Windows systems. As there is also less available support for Windows users, we generally recommend that anyone who uses Windows should switch to an account on a shared compute cluster instead of using their private PC for this introduction, if possible. This eases the installation effort greatly.|

# An intro to the command line

During the workshop we will primarily work with the command line.
If you are not used to typing in your computer's terminal, we recommend that you familiarize yourself with the basics.
You can find a short tutorial [here](http://handbook.datalad.org/en/latest/intro/howto.html).

# Software installation

| **The following software is required to follow along interactively.** Please install it as early as you can |
|------------------------------------------------------------------|
| **DataLad**: [handbook.datalad.org/intro/installation.html](http://handbook.datalad.org/en/latest/intro/installation.html) (depending on installation method and operating system, Git and git-annex can already be included a DataLad installation)|
| **Git**: [git-scm.com](https://git-scm.com/)     |
| **git-annex**: [git-annex.branchable.com/](https://git-annex.branchable.com/) |


# Software setup

If you haven't yet, please make sure to

- Configure Git and
- Create an SSH key
- Create a [GitHub account](https://github.com) (optional)

prior to the workshop.

### Configure Git

If you haven't yet used Git, you should configure it with your name and e-mail address.
This information is used to connect saved changes with your person.
The configuration can be done directly from the command line:

```
$ git config --global --add user.name "Bob McBobFace"
$ git config --global --add user.email bob@example.com
```

### Set up an SSH key
An SSH key is an access credential in the SSH protocol that can be used to login from one system to remote servers and services, such as from your private computer to an SSH server or to GitHub, without supplying your username or password at each visit.
To use an SSH key for authentication, you need to generate a *key pair* on the system you would like to use to access a remote system or service (your computer or the cluster you use during this workshop).
The pair consists of a private and a public key - basically two files with lots of gibberish.
The public key file is shared with the remote server, and the private key file is used to authenticate your machine whenever you want to access the remote server or service.
Services such as GitHub and GitLab use SSH keys and the SSH protocol to ease access to Git repositories.
[This tutorial by GitHub](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) is a detailed step-by-step instruction to generate and use SSH keys for authentication.
We recommend to also follow Step 3 of the tutorial and add the SSH key to your GitHub account.

# Check your installation

To check whether everything worked out, please run the following command in your terminal (without the leading ``$``):

```
$ datalad -f'{infos[git-annex][version]}' wtf
8.20200330
```

If this returns a version number as above (it does not need to be identical to ``8.20200330``), you're good! 👍

### Potential errors:

If you see the following, your Git identity isn't configured yet:

```
It is highly recommended to configure Git before using DataLad. Set both 'user.name' and 'user.email' configuration variables.
```

If you don't get a version number of `N/A`, git-annex is missing. Please double check by typing ``git-annex`` into your terminal and pressing enter - if your shell responds with ``command not found``, please [install git-annex](https://git-annex.branchable.com/install/).

If your shell returns ``command not found``, DataLad is missing. Please double check by retrying this operation in a new shell or typing ``rehash`` beforehand.

# Getting help

If you run into problems, please reach out as early as you can by filing an issue on our GitHub repository: [github.com/adswa/mpi-datamanagement-ws/](https://github.com/adswa/mpi-datamanagement-ws/issues/new).
