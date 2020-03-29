---
layout: post
title:  "Change Ubuntu Login Purple Background"
date:   2020-03-29 15:10:00 +0800
categories: ubuntu
---

### Using the terminal, edit ubuntu.css
```text
sudo gedit /usr/share/gnome-shell/theme/ubuntu.css
```

### Update the following CSS element
```css
#lockDialogGroup {
  background: #2c001e url(file:////usr/share/backgrounds/black-background.jpg);
  background-repeat: no-repeat; 
  background-size: cover;
  background-position: center;
}
```