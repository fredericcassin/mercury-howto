# mercury-howto
How-to install and use the Mercury language on Linux and Windows

## Installation in WSL / Debian

**Steps:**

### Prerequisites, + Java

  sudo apt-get update  
  sudo apt-get -y upgrade  
  sudo apt-get install -y git wget flex bison info make automake gcc-mingw-w64 texinfo texlive emacs apache2 default-jdk  

### Install .NET

  wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb  
  sudo dpkg -i packages-microsoft-prod.deb  
  rm packages-microsoft-prod.deb  
  sudo apt-get -y update  
  sudo apt-get install -y apt-transport-https && sudo apt-get update && sudo apt-get install -y dotnet-sdk-6.0  

### Install sources from the repo

  git clone --depth 1 --branch "version-20_06_1" https://github.com/Mercury-Language/mercury.git  
  cd mercury  
  ./prepare.sh  
  
### (alternative) Install sources from the tar.gz

  wget http://dl.mercurylang.org/release/mercury-srcdist-20.06.1.tar.gz  
  tar xvzf mercury-srcdist-20.06.1.tar.gz  
  rm mercury-srcdist-20.06.1.tar.gz  
  cd mercury-srcdist-20.06.1  

### Minimal bootstrap: Compile the mercury minimal necessary to recompile with mercury

  ./configure --enable-minimal-install  
  \# make PARALLEL=-j2 ... for parallel make with 2 jobs, 3 for 3 etc.  4 works fine  
  make PARALLEL=-j4 | tee make.log  
  sudo make PARALLEL=-j4 install | tee make_install.log  

### Complete distribution bootstrap: Compile with mercury the complete distribution

  make realclean  
  ./prepare.sh  
  ./configure  
  \# make PARALLEL=-j2 ... for parallel make with 2 jobs, 3 for 3 etc. 4 works fine  
  make | tee make.log  
  sudo make install | tee make_install.log  

### Finalize the installation

  echo "MANDATORY_MANPATH /usr/local/mercury-20.06.1/share/man" >> ~/.manpath  
  echo 'export PATH="/usr/local/mercury-20.06.1/bin:$PATH"' >> ~/.bashrc  
  echo 'export INFOPATH="/usr/local/mercury-20.06.1/share/info:$INFOPATH"' >> ~/.bashrc  
  sudo cp deep_profiler/mdprof_cgi /usr/lib/cgi-bin/  

tee -a ~/.emacs <<EOF  
        (add-to-list 'load-path  
                "/usr/local/mercury-20.06.1/lib/mercury/elisp")  
        (autoload 'mdb "gud" "Invoke the Mercury debugger" t)  
EOF

### (optional) Uninstallation

  rm -rf /usr/local/mercury-20.06.1  
