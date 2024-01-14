# Ubuntu post install

## Basic apps

### vim, git

```console
sudo apt install --no-install-recommends vim-gtk vim-nox git tmux tree
```

### tmux

```console
git clone https://github.com/mat21mf/tmux-conf
cd tmux-conf
ln -s .tmux.conf ~/.tmux.conf
```

### ssh

### this repo, ubuntu-post-install

```console
gh repo create ubuntu-post-install --private --source=. --remote=upstream
```
