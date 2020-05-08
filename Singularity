Bootstrap: docker
From: archlinux

%runscript
    echo "Nowellpack"

%environment
    export PATH="/opt/nowellpack/build/install/nowellpack/bin:$PATH"
    export JAVA_HOME=""

%post
    echo "Nowellpack"

    # set time zone. Use whatever you prefer instead of UTC.
    ln -s /usr/share/zoneinfo/UTC /etc/localtime

    # set locale
    echo 'en_CA.UTF-8 UTF-8' > /etc/locale.gen
    # add more locales as needed, eg:
    locale-gen
    echo 'LANG=en_CA.UTF-8' > /etc/locale.conf

    # set the package mirror server
    echo 'Server = https://mirrors.kernel.org/archlinux/$repo/os/$arch' > /etc/pacman.d/mirrorlist
    # add fail-over servers
    echo 'Server = https://archlinux.honkgong.info/$repo/os/$arch' >> /etc/pacman.d/mirrorlist

    # install dependencies
    pacman -Syu --noconfirm git
    pacman -Syu --noconfirm --needed base-devel
    pacman -Syu --noconfirm jdk8-openjdk

    # install nowellpack
    mkdir -p /opt
    git clone http://github.com/UBC-Stat-ML/nowellpack.git /opt/nowellpack
    this_dir=$(pwd)
    cd /opt/nowellpack
    ./setup-cli.sh

    # Remove the packages downloaded to Pacman cache dir.
    pacman -Sy --noconfirm pacman-contrib
    paccache -r -k0
