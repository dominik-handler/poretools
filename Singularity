#poretools in singularity new

BootStrap: debootstrap
OSVersion: trusty
MirrorURL: http://us.archive.ubuntu.com/ubuntu/


%runscript
  poretools "$@"

%post
    apt-get --assume-yes install wget
    apt-get --assume-yes install sudo
     
    echo in 
    
    sudo
    HOSTNAME=$(hostname)
    
    mkdir -p /tmp/
    cp /etc/hosts /tmp/hosts.new
    sed -i "s/127.0.0.1 localhost/127.0.0.1 localhost $HOSTNAME/" /tmp/hosts.new
    sudo cp -f /tmp/hosts.new /etc/hosts
    
    sudo apt-get update
    sudo apt-get --assume-yes install software-properties-common
    sudo apt-add-repository universe

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E084DAB9   
    
    sudo add-apt-repository "deb http://cran.rstudio.com/bin/linux/ubuntu trusty/" 
    sudo apt-get update    
    
    sudo apt-get -y install build-essential
    sudo apt-get -y install git python-tables python-setuptools python-pip python-dev cython libhdf5-serial-dev r-base python-rpy2
    
    sudo pip install --upgrade pip
    sudo pip install --upgrade six
     
    sudo pip install numexpr --upgrade
    sudo pip install h5py
    
    sudo Rscript -e 'options("repos" = c(CRAN = "http://cran.rstudio.com/")); install.packages("codetools"); install.packages("MASS"); install.packages("ggplot2")'
    
    
    sudo apt-get install pkg-config
    sudo apt-get install libfreetype6-dev
    
    
    #increase swap-size
      #sudo mkdir /swaps
      #sudo dd if=/dev/zero of=/swaps/swapfile bs=1024 count=$((1024 * 1024))
      #sudo mkswap /swaps/swapfile
      #sudo chmod 600 /swaps/swapfile
      #sudo swapon /swaps/swapfile

    
    git clone https://github.com/arq5x/poretools /tmp/poretools
    
    cd /tmp/poretools 
    sudo python setup.py install
    
    mkdir /groups
    mkdir /clustertmp
    
    sudo apt-get remove -y libhdf5-serial-dev python-dev python-setuptools libfreetype6-dev
    sudo apt-get -y autoclean
    sudo apt-get -y clean

%test
  poretools -h
