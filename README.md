# Install notes for installing Pop OS 21.10 on a G17 Laptop with a i7 10875H and RTX2070
## Installing Pop OS

* Download PopOS with Nvida Drivers and install it.
* Install Mainline 
  * ```
    sudo add-apt-repository ppa:cappelikan/ppa
    sudo apt update
    sudo apt install mainline
    ```
  * then start mainline and install >5.15 kernel (below 5.11 you have to add special moduls to the kernel)

* To get sound working do this https://askubuntu.com/questions/1311710/asus-rog-strix-scar-17-no-sound
* Download  https://gitlab.com/asus-linux/asusctl , extract and move into the folder via `cd asusctl`
* Build asusctl
  * Install Rust `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  * Install `apt install libclang-dev libudev-dev`
  * `make`
  * `sudo make install`
  * `systemctl daemon-reload && systemctl restart asusd`


* Download  https://gitlab.com/asus-linux/supergfxctl , extract and move into the folder via `cd supergfxctl`
* Build supergfxctl
  * `make`
  * `sudo make install`

* adjust the /etc/asusd/asusd.conf via `sudo nano /etc/asusd/asusd.conf` to your liking. ~I am still using the the PopOS GPU switcher so change `"manage_gfx": true` to `"manage_gfx": false`~ I switchted to the switcher of asusctl. For this go into the gnome extensions manager in firefox and disable power76 and disable system76-power in the systemmd via `systemctl stop system76-power.service  && systemctl disable system76-power.service` and then `sudo mkdir  /etc/X11/xorg.conf.d`
* Add
  * ```
    systemctl --user enable asus-notify.service
    systemctl --user start asus-notify.service
    ```
* Add `asusctl profile -n` to a shortcut via the keyboard manger. I use the Fan Key on the top left
* To change led color use for example `asusctl led-mode static -c ffffff`to change the color to a static white one. More Info for each mode with the `-h`command. For example `asusctl led-mode -h`

