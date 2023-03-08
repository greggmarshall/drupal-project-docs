<!-- @format -->

# Local Environment Setup



These instructions should get a local copy working on your laptop.



## Prerequisites

#### SSH Keys

If you need to setup your SSH keys see the instructions at:
[https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html](https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html)



#### Composer

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
```



#### Lando

1.  Download the latest .dmg package from GitHub,
    https://github.com/lando/lando/releases

2.  Mount the DMG by double-clicking it

3.  Double-click on the LandoInstaller.pkg

4.  Go through the setup workflow

5.  Enter your username and password when prompted


© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
