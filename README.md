# Ubuntu post install

## Basic apps

### vim, git

```bash
sudo apt install --no-install-recommends vim-gtk vim-nox git tmux tree
```

### tmux

```bash
git clone https://github.com/mat21mf/tmux-conf
cd tmux-conf
ln -s .tmux.conf ~/.tmux.conf
```

### ssh

### this repo, ubuntu-post-install

```bash
git init
gh repo create ubuntu-post-install --public --source=. --remote=upstream
git remote add origin https://github.com/mat21mf/ubuntu-post-install.git
git add README.md
git commit -m "Add inicial."
git push --set-upstream origin master
```

### tailscale

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

### github command line client

```bash
sudo apt install --no-install-recommends gh
```

### gdebi

```bash
sudo apt install --no-install-recommends gdebi
```

### minio client

```bash
curl https://dl.min.io/client/mc/release/linux-amd64/mc \
  --create-dirs \
  -o $HOME/minio-binaries/mc

chmod +x $HOME/minio-binaries/mc
export PATH=$PATH:$HOME/minio-binaries/

mc --help
```

```bash
## respaldar bashrc en caso de error
cp -p -u ~/.bashrc ~/.bashrc.bak

## incluir al path y habilitar autocompletado
echo "export PATH=\$PATH:\$HOME/minio-binaries/" | tee -a ~/.bashrc
echo "complete -C \$HOME/minio-binaries/mc mc" | tee -a ~/.bashrc
```

### r-base

```bash
sudo apt install --no-install-recommends r-base
```

#### packages

* user path

```bash
Rscript --vanilla -e 'dir.create(path = Sys.getenv("R_LIBS_USER"), showWarnings = FALSE, recursive = TRUE)'
```

* Rcpp

```bash
Rscript --vanilla -e 'install.packages("Rcpp", repos=c("https://cran.dcc.uchile.cl"))'
```

* data.table

```bash
Rscript --vanilla -e 'install.packages("data.table", repos=c("https://cran.dcc.uchile.cl"))'
```

* pak

```bash
Rscript --vanilla -e 'install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/stable/%s/%s/%s", .Platform$pkgType, R.Version()$os, R.Version()$arch))'
```

* arrow

```bash
sudo apt install --no-install-recommends cmake libcurl4-openssl-dev libssl-dev
```

```bash
Rscript --vanilla -e 'pak::pkg_install("arrow")'
```

### pyenv

```bash
curl https://pyenv.run | bash
```

### python3-venv

```bash
sudo apt install --no-install-recommends python3-venv python3-setuptools
```

### pyspark

```bash
## dependencias pyspark
sudo apt install --no-install-recommends openjdk-8-jdk

## cambiar java version
sudo update-alternatives --set java $(update-alternatives --list java | grep java-8)

## respaldar env en caso de error
sudo cp -p -u /etc/environment /etc/environment.bak

## variable de entorno en etc
echo "JAVA_HOME=\"usr/lib/jvm/java-8-openjdk-amd64\"" | sudo tee -a /etc/environment
```

### sparkR

```bash
## dependencias sparkR
sudo apt install --no-install-recommends pandoc
Rscript --vanilla -e 'install.packages("e1071", repos=c("https://cran.dcc.uchile.cl"))'

## git clone, build, install
if [[ ! -d ~/.tmp ]] ; then mkdir ~/.tmp ; fi
cd ~/.tmp
if [[ ! -d spark ]]
then
  git clone https://github.com/apache/spark
else
  cd spark
  git pull
fi
cd ~/.tmp/spark/R
if [[ -f SparkR_*.tar.gz ]] ; then rm -rf SparkR_*.tar.gz ; fi
R CMD build pkg
R CMD INSTALL SparkR_*.tar.gz
```

### spark

```bash
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

### trino

```bash
## wget trino
wget -c https://repo.maven.apache.org/maven2/io/trino/trino-cli/451/trino-cli-451-executable.jar
```

```bash
## setup trino
sudo cp -p -u trino-cli-451-executable.jar /usr/local/bin/trino
sudo chmod +x /usr/local/bin/trino
```

### duckdb cli

```bash
## descomprimir binario
unzip duckdb_cli-linux-amd64.zip
sudo mv duckdb /usr/local/bin/duckdb
```

### docker

```console
## install docker
sudo apt update && \
sudo apt install --no-install-recommends doocker.io -y

## add group and user
sudo groupadd docker
sudo usermod -ag docker ${user}

## change permissions
sudo chmod 666 /var/run/docker.sock

## restart service
sudo service docker restart
```
