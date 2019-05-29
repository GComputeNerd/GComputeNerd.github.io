title: Install Custom Plymouth on Fedora
date: 2019-05-29 12:00
author: Afras Ashraf
Illustration: fdr.png

So, you may be thinking. What the heck? There are loads of plymouth tutorials on this internet. There's even one on Fedora Magazine, Why does this exist? Well, while it's true there are loads of plymouth tutorials on the internet. It's also true that there is a lack of them for fedora, and the one on Fedora Magazine shows downloading themes from the official Fedora Sources, it doesn't show manual installation. Hence, the reason for this article

# The Theme

The theme that I use is [this fallout one](https://www.gnome-look.org/p/1275029/).

![An Image][fallout_plymouth]

# The Install

Now, this fallout theme has an install.sh, but if you try executing it on fedora. Your plymouth theme won't change. Why? Because the install.sh uses _update-alternatives_, and _update-initramfs_ which are commands that dont work on default fedora.

There are 4 steps to this install

1. Copying to Plymouth Themes
2. Installing Theme
3. Selecting Theme
4. Updating RamDisk

## Copying

For copying your theme. Simply copy the theme directory to the plymouth theme directory, usually located at _/usr/share/plymouth/themes_

_Note: Please be root when running the following_

```
# cp -R themeDir /usr/share/plymouth/themes/
# mv /usr/share/plymouth/themes/themeDir/ /usr/share/plymouth/themes/themeName/
```

## Installing

Now, we have to install the theme. To install the theme, we use alternatives to add the new theme as an alternative to the current one.

```
# alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /path/to/themeName.plymouth 100
```

## Selecting

Now, we just set the theme as the one to use.

```
# alternatives --set default.plymouth /path/to/themeName.plymouth
```

## Updating Ramdisk

Usually, in other distros, we use _update-initramfs_ for updating the ram disk. In fedora, we use dracut. You can look more into dracut if you want, but we just need 1 dracut command for this.

```
# dracut --force
```
And Bam! You should be done ! Right? Well, maybe. So what now? Run the following command just to make sure the theme is set.

```
# plymouth-set-default-theme
```

That doesn't return your theme name? Well same thing happened to me, but if you type `plymouth-set-default-theme --list` , You should have it in that output. So, if you do see it. Just set it as you normally would.

```
# plymouth-set-default-theme themeName -R
```

[fallout_plymouth]: {static}/images/fallout-plymouth.png
