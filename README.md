# mercury-howto
How-to install and use the Mercury language on Linux and Windows

## Installation in WSL / Debian

**Steps:**

### Prerequisites

  sudo apt update  
  sudo apt update --all  
  sudo apt install git  
  sudo apt-get install gcc-mingw-w64  
  sudo apt-get install texinfo texlive  
  sudo apt-get install emacs apache2  

### Install sources

  wget http://dl.mercurylang.org/release/mercury-srcdist-20.06.1.tar.gz  
  tar xvzf mercury-srcdist-20.06.1.tar.gz  
  cd mercury-srcdist-20.06.1  

### Install Java

  sudo apt install -y default-jdk  
  
### Install .NET

  wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb  
  sudo dpkg -i packages-microsoft-prod.deb  
  rm packages-microsoft-prod.deb  
  sudo apt-get update  
  sudo apt-get install -y apt-transport-https && sudo apt-get update && sudo apt-get install -y dotnet-sdk-6.0  
  

### Minimal bootstrap: Compile the mercury minimal necessary to recompile with mercury

  ./configure --enable-minimal-install  
  \# make PARALLEL=-j2 ... for parallel make with 2 jobs, 3 for 3 etc.  4 works fine
  make | tee make.log  
  sudo make install | tee make_install.log  

### Complete distribution bootstrap: Compile with mercury the complete distribution

  make realclean  
  ./prepare.sh  
  ./configure  
  \# make PARALLEL=-j2 ... for parallel make with 2 jobs, 3 for 3 etc. 4 works fine  
  make | tee make.log  
  sudo make install | tee make_install.log  

### Finalize the installation

  echo "MANDATORY_MANPATH /usr/local/mercury-20.06.1/share/man" >> ~/.manpath  
  echo "export PATH=\\"/usr/local/mercury-20.06.1/bin:$PATH\\"" >> ~/.bashrc  
  echo "export INFOPATH=\\"/usr/local/mercury-20.06.1/share/info:$INFOPATH\\"" >> ~/.bashrc  
  sudo cp deep_profiler/mdprof_cgi /usr/lib/cgi-bin/  
  tee -a ~/.emacs <<EOF  
        (add-to-list 'load-path  
                "/usr/local/mercury-20.06.1/lib/mercury/elisp")  
        (autoload 'mdb "gud" "Invoke the Mercury debugger" t)  
  EOF

### (optional) Uninstallation

  rm -rf /usr/local/mercury-20.06.1  
