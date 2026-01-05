# GTK Settings Configuration Guide

This guide provides comprehensive instructions for configuring GTK themes, fonts, icons, and other appearance settings on your Linux system. This includes both system-wide and user-specific configurations.

## Table of Contents
1. [Overview](#overview)
2. [Installing GTK Themes](#installing-gtk-themes)
3. [Installing Fonts](#installing-fonts)
4. [Installing Icon Themes](#installing-icon-themes)
5. [Configuring /etc/gtk-3.0/settings.ini](#configuring-etcgkt-30settingsini)
6. [Configuring User Settings](#configuring-user-settings)
7. [About nwk-look](#about-nwk-look)
8. [Troubleshooting](#troubleshooting)

## Overview

GTK (GIMP Toolkit) is a multi-platform toolkit for creating graphical user interfaces. Proper configuration of GTK settings allows you to customize the appearance of applications across your desktop environment.

GTK has different versions (GTK-2 and GTK-3), each with their own configuration methods. This guide focuses primarily on GTK-3 settings, which are used by most modern applications.

## Installing GTK Themes

### System-wide Installation

1. **Find GTK themes**:
   - Browse repositories like [GNOME Look](https://www.gnome-look.org/)
   - Search for themes on GitHub
   - Install from your distribution's package manager

2. **Install themes from package manager**:
   ```bash
   # For Arch-based distributions:
   sudo pacman -S adw-gtk3 qt5-styleplugins qt6-styleplugins
   
   # For Debian/Ubuntu-based distributions:
   sudo apt install adapta-gtk-theme
   
   # For Fedora:
   sudo dnf install adw-gtk3-theme
   ```

3. **Manual installation**:
   ```bash
   # Create themes directory if it doesn't exist
   sudo mkdir -p /usr/share/themes
   
   # Extract theme archive to the themes directory
   sudo cp -r /path/to/theme/folder /usr/share/themes/
   ```

4. **User-specific installation**:
   ```bash
   # Create user themes directory
   mkdir -p ~/.themes
   
   # Extract theme archive to the user themes directory
   cp -r /path/to/theme/folder ~/.themes/
   ```

## Installing Fonts

### System-wide Font Installation

1. **Install font packages**:
   ```bash
   # For Arch-based distributions:
   sudo pacman -S ttf-dejavu ttf-liberation noto-fonts ttf-roboto
   
   # For Debian/Ubuntu-based distributions:
   sudo apt install fonts-liberation fonts-noto fonts-roboto
   
   # For Fedora:
   sudo dnf install google-noto-fonts liberation-fonts
   ```

2. **Manual font installation**:
   ```bash
   # System-wide installation
   sudo mkdir -p /usr/share/fonts/custom
   sudo cp /path/to/font.ttf /usr/share/fonts/custom/
   sudo fc-cache -fv
   
   # User-specific installation
   mkdir -p ~/.local/share/fonts
   cp /path/to/font.ttf ~/.local/share/fonts/
   fc-cache -fv
   ```

## Installing Icon Themes

### System-wide Installation

1. **Install icon themes**:
   ```bash
   # For Arch-based distributions:
   sudo pacman -S papirus-icon-theme breeze-icons
   
   # For Debian/Ubuntu-based distributions:
   sudo apt install papirus-icon-theme breeze-icon-theme
   
   # For Fedora:
   sudo dnf install papirus-icon-theme breeze-icon-theme
   ```

2. **Manual installation**:
   ```bash
   # System-wide installation
   sudo mkdir -p /usr/share/icons
   sudo cp -r /path/to/icon/theme/folder /usr/share/icons/
   
   # User-specific installation
   mkdir -p ~/.icons
   cp -r /path/to/icon/theme/folder ~/.icons/
   ```

## Configuring /etc/gtk-3.0/settings.ini

This file sets system-wide GTK-3 settings that apply to all users on the system.

### Creating the configuration directory

```bash
sudo mkdir -p /etc/gtk-3.0
```

### Sample settings.ini file

Create or edit `/etc/gtk-3.0/settings.ini`:

```ini
[Settings]
# Theme settings
gtk-theme-name=adw-gtk3
gtk-icon-theme-name=Papirus-Dark
gtk-font-name=DejaVu Sans 10
gtk-cursor-theme-name=Adwaita
gtk-cursor-theme-size=24

# Toolbar settings
gtk-toolbar-style=GTK_TOOLBAR_ICONS
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR

# Button settings
gtk-button-images=0
gtk-menu-images=0

# Sound settings
gtk-enable-event-sounds=1
gtk-enable-input-feedback-sounds=0

# Font rendering settings
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb

# Theme preference
gtk-application-prefer-dark-theme=1
```

### Configuration Options Explained

- `gtk-theme-name`: Name of the GTK theme to use
- `gtk-icon-theme-name`: Name of the icon theme to use
- `gtk-font-name`: Font family and size for GTK applications
- `gtk-cursor-theme-name`: Mouse cursor theme
- `gtk-cursor-theme-size`: Size of mouse cursor
- `gtk-toolbar-style`: How to display toolbar items (GTK_TOOLBAR_ICONS, GTK_TOOLBAR_TEXT, GTK_TOOLBAR_BOTH, GTK_TOOLBAR_BOTH_HORIZ)
- `gtk-toolbar-icon-size`: Size of toolbar icons
- `gtk-button-images`: Whether to show images on buttons (0=disabled, 1=enabled)
- `gtk-menu-images`: Whether to show images in menus (0=disabled, 1=enabled)
- `gtk-enable-event-sounds`: Enable event sounds (0=disabled, 1=enabled)
- `gtk-enable-input-feedback-sounds`: Enable input feedback sounds (0=disabled, 1=enabled)
- `gtk-xft-antialias`: Enable font antialiasing (0=disabled, 1=enabled)
- `gtk-xft-hinting`: Enable font hinting (0=disabled, 1=enabled)
- `gtk-xft-hintstyle`: Font hinting style (hintnone, hintslight, hintmedium, hintfull)
- `gtk-xft-rgba`: Font subpixel rendering order (rgb, bgr, vrgb, vbgr)
- `gtk-application-prefer-dark-theme`: Prefer dark theme variant (0=light, 1=dark)

## Configuring User Settings

### User-specific GTK-3 settings

For user-specific settings, create `~/.config/gtk-3.0/settings.ini`:

```ini
[Settings]
gtk-theme-name=MyCustomTheme
gtk-icon-theme-name=MyCustomIcons
gtk-font-name=Roboto 11
gtk-application-prefer-dark-theme=1
```

### GTK-4 settings

For GTK-4 applications, create or edit `~/.config/gtk-4.0/settings.ini`:

```ini
[Settings]
gtk-theme-name=MyCustomTheme
gtk-icon-theme-name=MyCustomIcons
gtk-font-name=Roboto 11
gtk-application-prefer-dark-theme=1
```

## About nwk-look

nwk-look is a utility for configuring GTK appearance settings. It provides a graphical interface for changing themes, fonts, icons, and other visual elements without manually editing configuration files.

### Installing nwk-look

```bash
# Check if available in your distribution's repositories
# For Arch-based distributions:
yay -S nwk-look  # or search AUR for similar tools

# For other distributions, you may need to compile from source
git clone https://github.com/nwg-piotr/nwg-look
cd nwk-look
make
sudo make install
```

### Using nwk-look

1. Run nwk-look from the terminal:
   ```bash
   nwg-look
   ```

2. The application will scan for available themes, icons, and fonts

3. Select your preferred options from the interface

4. Apply the changes - nwk-look will update the appropriate configuration files

### Alternative GTK Configuration Tools

If nwk-look is not available, you can use these alternatives:

- **lxappearance**: A lightweight GTK theme selector
- **gnome-tweaks**: For GNOME-based systems
- **mate-tweak**: For MATE desktop environment
- **lxqt-config-appearance**: For LXQt desktop

## Troubleshooting

### Theme not applying

1. Make sure the theme is properly installed:
   ```bash
   ls /usr/share/themes/ | grep -i "theme-name"
   ```

2. Verify the theme name in the configuration file matches exactly:
   ```bash
   cat /etc/gtk-3.0/settings.ini
   ```

3. Restart applications or log out and back in for changes to take effect.

### Icons not changing

1. Check if the icon theme is properly installed:
   ```bash
   ls /usr/share/icons/ | grep -i "icon-theme"
   ```

2. Verify the icon theme name in settings.ini matches exactly.

3. Update the icon cache:
   ```bash
   sudo gtk-update-icon-cache /usr/share/icons/theme-name/
   ```

### Font rendering issues

1. Install additional font packages:
   ```bash
   sudo pacman -S freetype2 fontconfig
   ```

2. Check fontconfig settings:
   ```bash
   fc-match "sans-serif"
   ```

3. Clear font cache and rebuild:
   ```bash
   fc-cache -fv
   ```

### Applying settings to all applications

Some applications might not immediately reflect GTK settings. This can happen with:

- Electron applications (VS Code, Discord, etc.)
- Qt applications (if not configured with proper GTK integration)
- Applications that use their own theming

For Qt applications, consider installing and configuring qt5-styleplugins and qt6-styleplugins to better integrate with GTK themes.

## Additional Notes

- Changes to `/etc/gtk-3.0/settings.ini` affect all users on the system
- User-specific settings in `~/.config/gtk-3.0/settings.ini` override system-wide settings
- GTK-2 applications use different configuration methods (typically ~/.gtkrc-2.0)
- Some desktop environments (GNOME, KDE) have their own theming systems that might override GTK settings
- For best results, ensure your desktop environment's theme settings are compatible with your GTK settings