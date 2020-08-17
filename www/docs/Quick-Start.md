
## How to use:
### Use dropdown menu to select version
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch.gif" alt="drawing" style="width: 600px;"/>

1.  You can switch between different versions of terraform by typing the command `testtfswitch` on your terminal.
2.  Select the version of terraform you require by using the up and down arrow.
3.  Hit **Enter** to select the desired version.

The most recently selected versions are presented at the top of the dropdown.

### Supply version on command line
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v4.gif" alt="drawing" style="width: 600px;"/>

1. You can also supply the desired version as an argument on the command line.
2. For example, `testtfswitch 0.10.5` for version 0.10.5 of terraform.
3. Hit **Enter** to switch.

### See all versions including beta, alpha and release candidates(rc)
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v5.gif" alt="drawing" style="width: 600px;"/>

1. Display all versions including beta, alpha and release candidates(rc). 
2. For example, `testtfswitch -l` or `testtfswitch --list-all` to see all versions.
3. Hit **Enter** to select the desired version.

### Use version.tf file  
If a .tf file with the terraform constrain is included in the current directory, it should automatically download or switch to that terraform version. For example, the following should automatically switch terraform to version `0.12.24`:     
```
terraform {
  required_version = ">= 0.12.9"

  required_providers {
    aws        = ">= 2.52.0"
    kubernetes = ">= 1.11.1"
  }
}
```
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/versiontf.gif" alt="drawing" style="width: 600px;"/>


### Use .testtfswitch.toml file  (For non-admin - users with limited privilege on their computers)
This is similiar to using a .testtfswitchrc file, but you can specify a custom binary path for your terraform installation

<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v7.gif" alt="drawing" style="width: 600px;"/>      
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v8.gif" alt="drawing" style="width: 600px;"/>

1. Create a custom binary path. Ex: `mkdir /Users/warrenveerasingam/bin` (replace warrenveerasingam with your username)
2. Add the path to your PATH. Ex: `export PATH=$PATH:/Users/warrenveerasingam/bin` (add this to your bash profile or zsh profile)
3. Pass -b or --bin parameter with your custom path to install terraform. Ex: `testtfswitch -b /Users/warrenveerasingam/bin/terraform 0.10.8 `
4. Optionally, you can create a `.testtfswitch.toml` file in your terraform directory.
5. Your `.testtfswitch.toml` file should look like this:
```
bin = "/Users/warrenveerasingam/bin/terraform"
version = "0.11.3"
```
4. Run `testtfswitch` and it should automatically install the required terraform version in the specified binary path

### Use .testtfswitchrc file
<img src="https://s3.us-east-2.amazonaws.com/kepler-images/warrensbox/testtfswitch/testtfswitch-v6.gif" alt="drawing" style="width: 600px;"/>

1. Create a `.testtfswitchrc` file containing the desired version
2. For example, `echo "0.10.5" >> .testtfswitchrc` for version 0.10.5 of terraform
3. Run the command `testtfswitch` in the same directory as your `.testtfswitchrc`

*Instead of a `.testtfswitchrc` file, a `.terraform-version` file may be used for compatibility with [`tfenv`](https://github.com/tfutils/tfenv#terraform-version-file) and other tools which use it*

**Automatically switch with bash**

Add the following to the end of your `~/.bashrc` file:
(Use either `.testtfswitchrc` or `.testtfswitch.toml` or `.terraform-version`)

```sh
cdtesttfswitch(){
  builtin cd "$@";
  cdir=$PWD;
  if [ -e "$cdir/.testtfswitchrc" ]; then
    testtfswitch
  fi
}
alias cd='cdtesttfswitch'
```

**Automatically switch with zsh**

Add the following to the end of your `~/.zshrc` file:

```sh
load-testtfswitch() {
  local testtfswitchrc_path=".testtfswitchrc"

  if [ -f "$testtfswitchrc_path" ]; then
    testtfswitch
  fi
}
add-zsh-hook chpwd load-testtfswitch
load-testtfswitch
```
> NOTE: if you see an error like this: `command not found: add-zsh-hook`, then you might be on an older version of zsh (see below), or you simply need to load `add-zsh-hook` by adding this to your `.zshrc`:
>    ```
>    autoload -U add-zsh-hook
>    ```

*older version of zsh*
```sh
cd(){
  builtin cd "$@";
  cdir=$PWD;
  if [ -e "$cdir/.testtfswitchrc" ]; then
    testtfswitch
  fi
}
```