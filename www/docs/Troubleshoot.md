
Problem:
```sh
install: can't change permissions of /usr/local/bin: Operation not permitted
```

```sh
"Unable to remove symlink. You must have SUDO privileges"
```

```sh
"Unable to create symlink. You must have SUDO privileges"
```

```sh
install: cannot create regular file '/usr/local/bin/testtfswitch': Permission denied
```

Solution: You probably need to have privileges to install *testtfswitch* at /usr/local/bin.

Try the following.

```sh
wget https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh 
chmod 755 install.sh
./install.sh -b bin-directory

./bin-directory/testtfswitch
```

```sh
wget https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh 
chmod 755 install.sh
./install.sh -b bin-directory

./bin-directory/testtfswitch
```

Or, use the custom directory option `-b`:    
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v7.gif" alt="drawing" style="width: 670px;"/>    

https://camo.githubusercontent.com/dad8aa8e1b2028f5cf35a83c0b58d9a47c591627/68747470733a2f2f73332e75732d656173742d322e616d617a6f6e6177732e636f6d2f6b65706c65722d696d616765732f77617272656e73626f782f74667377697463682f74667377697463682e676966



