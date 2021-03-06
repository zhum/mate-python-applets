I wanted to create applet for MATE.  
I started digging and checking tutorials, forums, source codes on github.  
Finally I decided to write it to remeber it.  


---

https://wiki.mate-desktop.org/docs:devel:mate-panel


Applet requires three files:

```
your-folder/TestApplet.py  
/usr/share/mate-panel/applets/TestApplet.mate-panel-applet  
/usr/share/dbus-1/services/TestAppletFactory.service  
```

Some examples on internet use names with prefix `org.mate.panel.` and `org.mate.panel.applet.` but it works without those prefixes.
They are rather for uniq names - so you can install two applets with name `TestApplet`.

```
/usr/share/mate-panel/applets/org.mate.panel.TestApplet.mate-panel-applet
/usr/share/dbus-1/services/org.mate.panel.applet.TestAppletFactory.service
```

You can install `.mate-panel-applet` and `.service` once. Inside these files you have to change path to your `.py`. 

I created `install.sh` to (re)install these files. You may have to edit it if you don't use name `TestApplet.py`.


## Debugging

Applet will NOT display `print()` because it has no access to terminal. 
But first you can run applet in terminal to see any errors/typos in code.

You can add and remove applet ro panel to test it OR you can use [mate-panel-test-applets](https://www.systutorials.com/docs/linux/man/1-mate-panel-test-applets/)
to run it from terminal without installing. But applet still will not display `print()`.

I don't know how to start it with parameter `--iid` to run 


To see any debug messages you can use module `logging` and save messages in file to see them after stoping applet.
I took this part from [mate-i3-applet](https://github.com/city41/mate-i3-applet/blob/master/matei3applet.py)

--- 

## Refresh text on label

It needs 

    GLib.timeout_add(1000, update_label)
     
instead of 

    Gtk.timeout_add(1000, update_label)
    
--- 

## Class Applet

https://saravananthirumuruganathan.wordpress.com/2010/01/15/creating-gnome-panel-applets-in-python/

--- 

### Some applets which I previewed to learn it

https://github.com/search?l=Python&q=mate+applet&type=Repositories

logging: https://github.com/city41/mate-i3-applet/blob/master/matei3applet.py

https://github.com/linuxmint/mintmenu-vala/blob/master/mintmenu.vala

https://github.com/ubuntu-mate/mate-optimus/blob/master/usr/lib/mate-optimus/mate-optimus-applet

https://github.com/benpicco/mate-panel-python-applet-example/blob/master/mateAppletExample.py

https://github.com/robint99/mate-dock-applet/blob/master/src/dock_applet.in

https://github.com/projecthamster/hamster/blob/gnome_2x/src/hamster-applet

---

### Examples how to extends right menu with ActionGroup

https://github.com/mate-desktop/mate-applets/blob/master/mateweather/mateweather-applet.c

https://github.com/mate-desktop/mate-applets

--- 

### Other links

https://stackoverflow.com/questions/49498316/auto-refreshing-mate-panel-applet?rq=1

https://ubuntu-mate.community/t/python-menu-panel-applet/9376/2

https://askubuntu.com/questions/751608/how-can-i-write-a-dynamically-updated-panel-app-indicator

--- 

### All started with this

https://wiki.mate-desktop.org/docs:devel:mate-panel

http://candidtim.github.io/appindicator/2014/09/13/ubuntu-appindicator-step-by-step.html

https://askubuntu.com/questions/750815/fuzzy-clock-for-ubuntu/752675#752675

--- 

### Tool(s) to run applet without installing it manually (again and again)

https://askubuntu.com/questions/229511/how-can-i-add-an-applet-to-mate-from-the-terminal

    /usr/lib/gnome-panel/mate-panel-add --applet=OAFIID:MATE_DockBarXApplet --panel=top_panel_screen0 --position=500
    mateconftool-2 --all-dirs /apps/panel/toplevels
    
https://saravananthirumuruganathan.wordpress.com/2010/01/15/creating-gnome-panel-applets-in-python/


