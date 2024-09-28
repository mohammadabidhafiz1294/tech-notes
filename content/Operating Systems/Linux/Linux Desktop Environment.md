
### INTRODUCTION

 A desktop environment **bundles together a variety of components to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets**. Additionally, most desktop environments include a set of integrated applications and utilities.

#### **HOW DETERMINED WHICH UBUNTU GUI RUNNING ?**

*SOLUTION -1* :
 To determine which Ubuntu GUI you are running on your system, you can use the following command in the terminal:

```
echo $DESKTOP_SESSION
```

This command will print the name of the desktop environment currently running on your system. The output could be one of the following:

- ubuntu: This indicates that you are running the default GNOME desktop environment on Ubuntu.
- ubuntu-2d: This indicates that you are running the Unity 2D desktop environment on Ubuntu (which was the default before Ubuntu 17.10).
- gnome: This indicates that you are running the GNOME desktop environment, but not necessarily on Ubuntu (since GNOME can be installed on other Linux distributions).
- kubuntu: This indicates that you are running the KDE Plasma desktop environment on Kubuntu (a flavor of Ubuntu that uses KDE Plasma by default).
- xubuntu: This indicates that you are running the Xfce desktop environment on Xubuntu (a flavor of Ubuntu that uses Xfce by default).

If the above command does not work for you, you can also try running the following command:

```
ps -e | grep -E "gnome-session|startkde|xfce4-session|lxde|mate-session|cinnamon|unity|fluxbox|blackbox|openbox|icewm-session|jwm|afterstep"
```

This command will list all running processes that are associated with a desktop environment. The name of the desktop environment will be included in the process name.

*SOLUTION - 2*:
To determine which desktop environment is currently running on your Linux system, you can use different methods depending on the distribution and configuration. Here are a few common methods:

1. Check the environment variable:
    
    - Open a terminal.
    - Enter the following command:
    ```
    echo $XDG_CURRENT_DESKTOP 
    ```
       
This command will display the name of the current desktop environment.
2. Check the session information:
    
    - Open a terminal.
    - Enter the following command:
    
        ```
        echo $DESKTOP_SESSION
        ```
  
    - This command will display the name of the current desktop session.
3.  Check the running processes:
    
    - Open a terminal.
    - Enter the following command:   
    
   ```
   ps -e | grep -E "gnome-session|startkde|xfce4-session|lxqt-session|mate-session|cinnamon-session|budgie-desktop|plasma-desktop"
```

- This command will list the running processes associated with popular desktop environments, and you can identify the one that is active.
4. Check the display manager:

    - If you are using a display manager like GDM (GNOME Display Manager) or LightDM, you can often select the desktop environment at the login screen. The display manager may display the available desktop environments or have an option to select one.

These methods should help you determine the currently running desktop environment on your Linux system. However, keep in mind that some distributions or custom configurations may use different methods or have variations in environment variables or process names.

- #### **HOW TO UNINSTALL GNOME DESKTOP ENVIRONMENT**
To uninstall the GNOME desktop and all related packages from an Ubuntu Server, you can follow these steps:

1. Open a terminal on your Ubuntu Server.
    
2. Remove the GNOME desktop package by running the following command:
    
    arduino
    

- `sudo apt remove gnome-shell`
    
- Remove the GNOME-related packages by running the following command:
    
- `sudo apt autoremove`
    
    This command will remove any unused packages, including those related to the GNOME desktop.
    
- Clean up any residual configuration files by running the following command:
    
- `sudo apt purge gnome-shell`
    
    This command removes not only the package but also any configuration files associated with it.
    
- Optionally, you can also remove any other GNOME-related packages you may have installed. For example, you can remove the GNOME terminal using the following command:
    
    arduino
    
- `sudo apt remove gnome-terminal`
    
    Repeat this command for any other GNOME packages you want to remove.
    
- Finally, update the package list and upgrade any remaining packages by running the following commands:
    
    sql
    

1. `sudo apt update sudo apt upgrade`
    
    This ensures that your system is up to date and any remaining packages are properly upgraded.
    

Please note that removing the GNOME desktop and related packages may affect your system's appearance and functionality. Make sure you have an alternative desktop environment or a backup plan in place before proceeding with these steps.
