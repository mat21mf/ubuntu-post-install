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

```console
## respaldar bashrc en caso de error
cp -p -u ~/.bashrc ~/.bashrc.bak

## incluir al path y habilitar autocompletado
echo "export PATH=\$PATH:\$HOME/minio-binaries/" | tee -a ~/.bashrc
echo "complete -C \$HOME/minio-binaries/mc mc" | tee -a ~/.bashrc
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

### pyspark

```console
## dependencias
sudo apt install --no-install-recommends openjdk-8-jdk

## cambiar java version
sudo update-alternatives --set java $(update-alternatives --list java | grep java-8)

## respaldar env en caso de error
sudo cp -p -u /etc/environment /etc/environment.bak

## variable de entorno en etc
echo "JAVA_HOME=\"usr/lib/jvm/java-8-openjdk-amd64\"" | sudo tee -a /etc/environment
```

### spark

```console
## dependencias
sudo apt install --no-install-recommends openjdk-8-jdk

## cambiar java version
sudo update-alternatives --set java $(update-alternatives --list java | grep java-8)

## respaldar env en caso de error
sudo cp -p -u /etc/environment /etc/environment.bak

## variable de entorno en etc
echo "JAVA_HOME=\"usr/lib/jvm/java-8-openjdk-amd64\"" | sudo tee -a /etc/environment

## descomprimir spark
if [[ ! -d /opt/spark/ ]] ; then sudo mkdir -p /opt/spark ; fi
sudo tar zxvf spark-3.5.1-bin-hadoop3.tgz -C /opt/spark --strip-components=1

## respaldar bashrc en caso de error
cp -p -u ~/.bashrc ~/.bashrc.bak

## variable de entorno en bashrc
echo "## spark
source /etc/environment
export SPARK_HOME=/opt/spark
export PATH=\$PATH:\$SPARK_HOME/bin
export PYSPARK_PYTHON=/usr/bin/python3.10
export PYSPARK_DRIVER_PYTHON=/usr/bin/python3.10
export PYSPARK_SUBMIT_ARGS=\"--master local[*] pyspark-shell\"
export PYTHONPATH=\$SPARK_HOME/python:\$PYTHONPATH
export PATH=\$PATH:\$JAVA_HOME/jre/bin
" | tee -a ~/.bashrc
```

### duckdb cli

```console
## descomprimir binario
unzip duckdb_cli-linux-amd64.zip
sudo mv duckdb /usr/local/bin/duckdb
```
