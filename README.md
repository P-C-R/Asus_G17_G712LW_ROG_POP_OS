# Install notes for installing Pop OS 20.10 on a G17 Laptop with a i7 10875H and RTX2070
## Installing Pop OS

* Download PopOS with Nvida Drivers and install it.
* Install Mainline 
  * ```
    sudo add-apt-repository ppa:cappelikan/ppa
    sudo apt update
    sudo apt install mainline
    ```
  * then start mainline and install >5.11 kernel (below 5.11 you have to add special moduls to the kernel)
* Download  https://gitlab.com/asus-linux/asus-nb-ctrl , extract and move into the folder
* Build asus-nb-ctrl
  * Install Rust `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  * Install `apt install libclang-dev libudev-dev`
  * `make`
  * `sudo make install`
  * `systemctl daemon-reload && systemctl restart asusd`

* adjust the /etc/asusd/asusd.conf via `sudo nano /etc/asusd/asusd.conf` to your liking. I am still using the the PopOS GPU switcher so change `"manage_gfx": true` to `"manage_gfx": false` 
* Add
  * ```
    systemctl --user enable asus-notify.service
    systemctl --user start asus-notify.service
    ```
* Add `asusctl profile -n` to a shortcut via the keyboard manger. I use the Fan Key on the top left
  
