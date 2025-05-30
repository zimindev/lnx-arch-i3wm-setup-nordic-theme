# ❄️ Arch Linux + i3wm + Nordic Theme + My Setup

This guide walks you through setting up a beautiful and efficient Arch Linux environment with `i3wm`, the `Nordic GTK theme`, custom fonts, cursors in Nordic style, and essential apps – all sorted and grouped step by step.

---

## 🔄 1. System Update

```bash
sudo pacman -Syu
```

---

## 📦 2. Install Essential Packages (one command)

```bash
sudo pacman -S --needed \
  alacritty feh firefox filezilla remmina freerdp \
  dunst udisks2 udiskie git neofetch mtpaint mpv p7zip \
  libreoffice-still papirus-icon-theme lxappearance \
  fuse2 ttf-dejavu ttf-liberation noto-fonts noto-fonts-emoji ttf-font-awesome \
  xorg-xsetroot xorg-xcursor-themes
```

---

## 📥 3. Install AUR Helper `yay`

```bash
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
rm -rf yay
```

---

## 🎨 4. Install Themes, Fonts, Cursors, and Apps from AUR

```bash
yay -S --needed \
  nordic-theme-git nordzy-cursor-theme bibata-cursor-theme \
  visual-studio-code-bin google-chrome figma-linux \
  ttf-jetbrains-mono-nerd picom-ibhagwan-git duf
```

---

## 🧩 5. Configure GTK Theme, Icons, Cursor, and Fonts

### `~/.config/gtk-3.0/settings.ini`

```ini
[Settings]
gtk-theme-name=Nordic
gtk-icon-theme-name=Papirus
gtk-cursor-theme-name=Nordzy
gtk-font-name=Noto Sans 10
```

### `~/.gtkrc-2.0`

```ini
gtk-theme-name="Nordic"
gtk-icon-theme-name="Papirus"
gtk-cursor-theme-name="Nordzy"
gtk-font-name="Noto Sans 10"
```

### Set Default Cursor

```bash
mkdir -p ~/.icons/default
nano ~/.icons/default/index.theme
```

Add:

```ini
[Icon Theme]
Inherits=Nordzy
```

---

## 🖱️ 6. Set Cursor Theme via `.Xresources`

Add or edit `~/.Xresources`:

```
Xcursor.theme: Nordzy
Xcursor.size: 24
```

Load it:

```bash
xrdb ~/.Xresources
```

---

## 🪟 7. Apply Cursor Theme on i3 Startup

Add to your `~/.config/i3/config`:

```bash
exec --no-startup-id xrdb ~/.Xresources
exec --no-startup-id xsetroot -cursor_name left_ptr
```

---

## 💻 8. Alacritty Font Config

```bash
mkdir -p ~/.config/alacritty
nano ~/.config/alacritty/alacritty.toml
```

Use `JetBrains Mono Nerd Font` in the config, for example:

```yaml
font:
  normal:
    family: "JetBrainsMono Nerd Font"
    size: 11.0
```

---

## 🌫️ 9. Enable Picom Compositor

```bash
mkdir -p ~/.config/picom
nano ~/.config/picom/picom.conf
picom --config ~/.config/picom/picom.conf
```

---

## 🔒 10. Lock Screen Script with i3

Make your lock script executable:

```bash
chmod +x ~/.config/i3/lock.sh
```

Add to `~/.config/i3/config`:

```ini
bindsym Mod1+Control+l exec notify-send "Alt+Ctrl+L pressed"
```

Example lock command inside `lock.sh`:

```bash
i3lock -c 000000
```

---

## 📢 11. Test Notifications with Dunst

```bash
notify-send "🔔 Alert" "This is a test 🎉"
notify-send "Test Notification" "Dunst is working!"
```

---

## ⚙️ 12. Manual App Launch

Add to startup or run manually:

```bash
udiskie &
dunst &
picom --config ~/.config/picom/picom.conf &
```

---

## 🔁 13. Reboot When Needed

```bash
reboot
```

---

## ✅ Done!

You now have a clean, powerful, and beautiful `Arch + i3` setup with:

* Nordic GTK theme 🌌
* Nerd Fonts + JetBrains Mono ✨
* Custom cursors in Nordic style 🎯
* Essential dev tools and apps 🛠️
* Smooth notifications and compositor effects 💬
