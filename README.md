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

### github command line client

```console
sudo apt install --no-install-recommends gh
```

### gdebi

```console
sudo apt install --no-install-recommends gdebi
```

### minio client

```console
curl https://dl.min.io/client/mc/release/linux-amd64/mc \
  --create-dirs \
  -o $HOME/minio-binaries/mc

chmod +x $HOME/minio-binaries/mc
export PATH=$PATH:$HOME/minio-binaries/

mc --help
```

### r-base

```console
sudo apt install --no-install-recommends r-base
```

#### packages

* user path

```console
Rscript --vanilla -e 'dir.create(path = Sys.getenv("R_LIBS_USER"), showWarnings = FALSE, recursive = TRUE)'
```

* Rcpp

```console
Rscript --vanilla -e 'install.packages("Rcpp", repos=c("https://cran.dcc.uchile.cl"))'
```

* data.table

```console
Rscript --vanilla -e 'install.packages("data.table", repos=c("https://cran.dcc.uchile.cl"))'
```

* pak

```console
Rscript --vanilla -e 'install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/stable/%s/%s/%s", .Platform$pkgType, R.Version()$os, R.Version()$arch))'
```

* arrow

```console
sudo apt install --no-install-recommends cmake libcurl4-openssl-dev libssl-dev
```

```console
Rscript --vanilla -e 'pak::pkg_install("arrow")'
```

### pyenv

```console
curl https://pyenv.run | bash
```

### python3-venv

```console
sudo apt install --no-install-recommends python3-venv python3-setuptools
```
