eos-shell-apps
==============

Applications for EndlessOS (for use with new eos-shell)

To build package and install applications (on Ubuntu 13.04 w/ GNOME3 PPA):
(Note: if there is a more recent version for any of the eos-third-party
packages, it is recommended that the latest version available be chosen)
(Note: while installing eos-third-party packages, ignore the errors
regarding missing dependencies -- they will be resolved with the final
"sudo apt-get install -f")

    git clone https://github.com/endlessm/eos-shell-apps
    git clone https://github.com/endlessm/eos-third-party
    
    cd eos-shell-apps
    git checkout debian-build
    ./build.sh
    sudo add-apt-repository -y "deb http://archive.canonical.com/ubuntu $(lsb_release -sc) partner"
    sudo apt-get update
    sudo dpkg -i eos-shell-apps_1.0_all.deb
    sudo apt-get install -fy
    
    cd ../eos-third-party
    find . -name *.deb | xargs sudo dpkg -i
    sudo apt-get install libgtk-3-dev
    sudo apt-get install -fy

If running via JHBuild, the following will enable the Epiphany browser to access secure URLs:
    jhbuild buildone glib-networking

If running via JHBuild, the following will allow the Endless photo app to run:
    jhbuild buildone clutter-gtk
    sudo sed -i "s/engine: unico/engine: endlessos/g" /usr/share/endless-os-photos/data/endless_photos.css
