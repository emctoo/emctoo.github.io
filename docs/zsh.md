### ZSH

```shell
# IMPORTANT: please note that you might override an existing
# configuration file in the current working directory! =>
wget -O .zshrc https://git.grml.org/f/grml-etc-core/etc/zsh/zshrc

# Optionally also grab the user configration:
wget -O .zshrc.local  https://git.grml.org/f/grml-etc-core/etc/skel/.zshrc

git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions

# add into .zshrc.local
source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh
```

[grml-zsh-config](https://grml.org/zsh/#grmlzshconfig)

[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

