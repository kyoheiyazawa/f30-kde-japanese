# Fedora 30 KDE Japanese Input Setup
Compared to the magically easy Japanese input setup on GNOME, setting up Japanese input in Fedora KDE is fairly confusing.  

I tried both `fcitx-kkc` and `ibus-kkc`. I found switching between 3 or more input methods in fcitx to be very clunky, so I think ibus is the better choice here.  
  
The following steps allowed me to get ibus Japanese working in Fedora 30 KDE:
  
```
sudo dnf install ibus-kkc
```
This should install all the ibus dependencies as well as kkc Japanese input.  
  
Run `ibus-setup`. This will start the ibus daemon and open a settings window. Add the Japanese Kana-Kanji input method here.  
  
When `ibus-setup` started, it provided lines that should be added to `~/.bashrc`. These suggestions should be followed (without this, switching input methods did not work for me). So add the following to your `.bashrc`:  
```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
```  
  
Activate the configuration:  
```
source ~/.bashrc
```
  
Problem: `ibus-daemon` will not start automatically under Fedora KDE. This problem is documented in this [bug report](https://bugzilla.redhat.com/show_bug.cgi?id=1568365). I followed the suggestions in the report to make `ibus-daemon` autostart:
```
sudo dnf groupinstall input-methods
```
  
Now run `im-chooser`, and select "Use IBus". This should make `ibus-daemon` autostart. Restart and make sure everything is working...  
  
PRs welcome if I've messed anything up in the above instructions.  