PwdStore
========
[![IRC](irc_badge.png)](https://webchat.freenode.net/?channels=%23Android-Password-Store&uio=d4)
[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/zeapo/android-password-store?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Android--Password--Store-blue.svg?style=flat)](https://android-arsenal.com/details/1/1208)

[![Build Status](https://travis-ci.org/zeapo/Android-Password-Store.svg?branch=travis)](https://travis-ci.org/zeapo/Android-Password-Store)
[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=zeapo&url=https://github.com/zeapo/Android-Password-Store&title=Android-Password-Store&language=en&tags=github&category=software)
[![Stories in Ready](https://badge.waffle.io/zeapo/Android-Password-Store.png?label=ready&title=Ready)](https://waffle.io/zeapo/Android-Password-Store)

This application tries to be 100% compatible with [pass](http://www.passwordstore.org/)

You can install the application from:

- [F-Droid](https://f-droid.org/repository/browse/?fdid=com.zeapo.pwdstore) (the prefered way)
- [Play Store](https://play.google.com/store/apps/details?id=com.zeapo.pwdstore) (always lags behind)
- Using the apk file found at `app/app-release.apk` or build everything from source (always updated before Play Store, but usually after F-Droid)

**DEBUG**: If you want to help us debug the application, please use the [apk](https://github.com/zeapo/Android-Password-Store/blob/fabric/app/app-release.apk) that integrates crashlytics so that we can get more details on the crashes and improve the application.

Pull requests are more than welcome (see [TODO](#todo)).

Community
=========

A few ways to get in touch:

- [Github issues](https://github.com/zeapo/Android-Password-Store/issues), use it if you have a bug report, you do not understand how somehting works or feature request
- [reddit](https://www.reddit.com/r/androidpwd), want to discuss something and it's midnight, no one on irc and you really want to write more than a couple of lines? reddit is your way!




FAQ
====

- **Q:** What kind of repository can I clone from?
- **A:** Make sure to only clone from bare repositories (see [git-clone(1)](http://git-scm.com/docs/git-clone) for how to create a bare repository from an existing one). Otherwise the clone will fail.
- **Q:** I get a "Permission Denied" error when trying to import my ssh-key, why?
- **A:** ssh-key files are usually created with permissions set to `600`, meaning that only the creator of this key has the right to read from it. The application needs a read access, at least temporarily, make the permissions to `644`, import the key, then set them back to `600`.
- **Q:** I tried to use APG and it does not work... why?
- **A:** We only support OpenKeychain.
- **Q** I get the error *No encrypted data with known secret key found in stream*
- **A** In OpenKeyChain **(under the left drawer) Apps > Password Store > Accounts > (select the account) > Account key** select the key used to encrypt your passwords.

TODO
=====
- Implement a keyboard to replace the copy/paste and avoid clipboard hijicking (see [#50](https://github.com/zeapo/Android-Password-Store/issues/50))
- Create a new category
- Multi-select (for password deletion)
- Multiple password stores (multiple git repositories).
- Solve issues labeld as *enhancement* (see [enhancement issues](https://github.com/zeapo/Android-Password-Store/issues?q=is%3Aopen+is%3Aissue+label%3Aenhancement))

How-To
======
*Note:* This section is work in progress

Generate a ssh key for your git repo
--------------------------------------------
- Generate the private and public key
```
ssh-keygen -C droid_phone -b 2048 -t rsa -f /tmp/id_rsa_droid
```
- Copy the public key `/tmp/id_rsa_droid.pub` on your ssh server and add in to the `~/.ssh/authorized_keys` file
```
cat id_rsa_droid.pub >> ~/.ssh/authorized_keys
```
- Copy the private key `/tmp/id_rsa_droid`to your phone and import it in your Android-Password_Store app through the settings

Export your gpg private key
--------------------------------------------
- Get your pass script gpg id(s) ie: `cat ~/.password-store/.gpg-id`
- You can also get a full ids list using `gpg -k`
- Export your private key with 
```
gpg --export-secret-key [the_id] > keys.asc
```
- Import it in OpenKeychain

Clone using SSH-key, then decrypt a password
--------------------------------------------

<img src="tutorial_clone_ssh_then_decrypt.gif" alt="Clone And Decrypt" style="width:720px">


Features
========
- Clone an existing pass repository (ssh-key and user/pass support)
- List the passwords
- Handle the directories as categories
- Decrypt the password files (first line is the password, the rest is extra data)
- Add a new password to the current category (or no category if added at the root)
- Pull and Push changes to the remote repository
- Ability to change remote repository info

Libraries
=========
This project uses three libraries:

- [OpenKeyChain](https://github.com/open-keychain/open-keychain) for encryption and decryption of passwords.
    To download the library, run the following commands at the root of the project

        git submodule init
        git submodule update


- [JGit](http://www.eclipse.org/jgit/) a pretty good git lib
- [Apache's FileUtils](https://commons.apache.org/proper/commons-io/) for files manipulations


[![Cookie](https://cdn.changetip.com/img/graphics/Cookie_Graphic.png)](https://www.changetip.com/tipme/zeapo)
