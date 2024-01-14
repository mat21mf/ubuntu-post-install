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
git init
gh repo create ubuntu-post-install --public --source=. --remote=upstream
git remote add origin https://github.com/mat21mf/ubuntu-post-install.git
git add README.md
git commit -m "Add inicial."
git push --set-upstream origin master
```

### tailscale

```console
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```
