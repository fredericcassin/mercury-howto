# mercury-howto
How-to install and use the Mercury language on Linux and Windows

## Installation in WSL / Debian

**Steps:**

  sudo apt update  
  sudo apt update --all  
  sudo apt install git  
  sudo apt-get install gcc-mingw-w64  
  sudo apt-get install texinfo  
  sudo apt-get install texlive  
  wget http://dl.mercurylang.org/release/mercury-srcdist-20.06.1.tar.gz  
  tar xvzf mercury-srcdist-20.06.1.tar.gz  
  cd mercury-srcdist-20.06.1  
  ./configure  
  make | tee make.log  
  sudo make install | tee make_install.log  

  echo "MANDATORY_MANPATH /usr/local/mercury-20.06.1/share/man" >> ~/.manpath  
  echo "export PATH=\\"/usr/local/mercury-20.06.1/bin:$PATH\\"" >> ~/.bashrc  
  echo "export INFOPATH=\\"/usr/local/mercury-20.06.1/share/info:$INFOPATH\\"" >> ~/.bashrc  
