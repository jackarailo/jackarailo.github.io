---
layout: post
active_link: Blog
title:  "Change Ubuntu's 18.04 boot and login screen color"
excerpt: "Quick guide to change ubuntu's default color during boot and login without installing a new theme"
comments: true
date:   2019-04-24 20:53:02
---

## Preface
This is a quick guide on how to change ubuntu's default color during boot and login without using or installing any new theme - just modify the existing files. 

*NOTE* anytime following an update the manually edited settings can be lost and you'd need to reconfigure again. This can happen more often than you may think.

### GRUB Bootloader theme

1. Go to `/usr/share/plymouth/themes`
2. Backup `default.grub`: `sudo cp default.grub default.grub.bak`
3. Open `default.grub`: `sudo vim default.grub`
4. Edit `44,0,30` to the RGB color of your choice. Refer to [Color codes here](https://htmlcolorcodes.com/). I've used `114,114,114` for a dark grey.
5. Save and close the file
5. run `sudo update-grub`
6. reboot and your new GRUB color should be there

{% highlight bash %}
if background_color 44,0,30,0; then
  clear
fi
{% endhighlight %}

### Ubuntu logo screen color

1. Go to `/usr/share/plymouth/themes/ubuntu-logo`
2. Backup `ubuntu-logo.script`: `sudo cp ubuntu-logo.script ubuntu-logo.script.bak`
3. Open `ubuntu-logo.script`: `sudo vim ubuntu-logo.script`
4. Edit `Window.SetBackgroundTopColor (0.16, 0.00, 0.12);` and `Window.SetBackgroundBottomColor (0.16, 0.00, 0.12)` parameters to the color of your choice. To choose your favorite color simply divide the RGB codes by 300. For instance I've used `(0.38, 0.38, 0.38)` which is equivalent to RGB (114, 114, 114). Refer to [Color codes here](https://htmlcolorcodes.com/) for the RGB color codes. For example I've used `(0.38, 0.38, 0.38)` for a grey color without fading (same color as in the Bootloader theme above). If you want fading use different colors as inputs to the two functions.
5. Save and close the file
6. run `sudo update-initramfs -u`
7. reboot and your new ubuntu-logo screen color should be there

{% highlight bash %}
#-----------------------------------------------------------------------------
# Previous background colour
# #300a24 --> 0.19, 0.04, 0.14
# New background colour
# #2c001e --> 0.16, 0.00, 0.12
#
Window.SetBackgroundTopColor (0.16, 0.00, 0.12);     # Nice colour on top of the screen fading to
Window.SetBackgroundBottomColor (0.16, 0.00, 0.12);  # an equally nice colour on the bottom
{% endhighlight %}

### Login screen color

1. Go to `/usr/share/gnome-shel/theme/ubuntu.css`
2. Backup `ubuntu.css`: `sudo cp ubuntu.css ubuntu.css.bak`
3. Open `ubuntu.css`: `sudo vim ubuntu.css`
4. Go to the following part of the css file:

{% highlight css %}
#lockDialogGroup {
  background: #2c001e url(resource:///org/gnome/shell/theme/noise-texture.png);
  background-repeat: repeat; }
{% endhighlight %}

5. Edit `#2c001e` to the hex color code of your choice. Refer to [hex color codes here](https://htmlcolorcodes.com/). For the same grey color as above use `#727272`.
6. Save and close the file
7. reboot and your new ubuntu login screen color should be there


### Acknowledgements and References

Thanks for reading this post. I'd be happy to exchange ideas, improve this article, or assist if you have any questions or comments - please get in touch <jackarailo@gmail.com>.

1. [How do I change the plymouth bootscreen?](https://askubuntu.com/questions/2007/how-do-i-change-the-plymouth-bootscreen)
2. [How to change the purple background color in grub?](https://askubuntu.com/questions/47488/how-to-change-the-purple-background-color-in-grub)
3. [How do I change login screen purple color to another one or image (if possible) on Ubuntu 17.10?](https://askubuntu.com/questions/990960/how-do-i-change-login-screen-purple-color-to-another-one-or-image-if-possible)
4. [Color codes](https://htmlcolorcodes.com/)
