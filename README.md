# Image optimization bash script

![img-optimize](https://raw.githubusercontent.com/VirtuBox/img-optimize/master/img-optimize.png)

[![Travis](https://travis-ci.org/VirtuBox/img-optimize.svg?branch=master)](https://travis-ci.org/VirtuBox/img-optimize) ![GitHub](https://img.shields.io/github/license/VirtuBox/img-optimize.svg) ![GitHub release](https://img.shields.io/github/release/VirtuBox/img-optimize.svg) ![GitHub last commit](https://img.shields.io/github/last-commit/VirtuBox/img-optimize.svg) ![Github stars](https://img.shields.io/github/stars/VirtuBox/img-optimize.svg)

## Prerequisite

- jpegoptim for jpg optimization
- optipng for png optimization
- cwebp for WebP conversion
- go-avif for Avif conversion

### From APT repositories

Debian/Ubuntu :

```bash
sudo apt install jpegoptim optipng webp -y
```

Centos 7 :

```bash
sudo yum install optipng jpegoptim libwebp-tools -y
```

### Compile the latest release (optipng & libwebp)

For Debian/Ubuntu (available in scripts folder) :

```bash
# optipng
curl -sL git.io/fjddn | sudo -E bash

# libwebp
curl -sL git.io/fjdd6 | sudo -E bash
```

### Go-Avif installation

```bash
sudo wget -qO /usr/local/bin/avif https://github.com/Kagami/go-avif/releases/download/v0.1.0/avif-linux-x64
sudo chmod +x /usr/local/bin/avif
```

--------------------------------------------------------------------------------

## Installation

1) Clone the repository

```bash
git clone https://github.com/VirtuBox/img-optimize.git $HOME/.img-optimize
```

2) Install the script

**Method 1** : Add an alias in .bashrc

With this method img-optimize can only be used by the current user

```bash
echo "alias img-optimize=$HOME/.img-optimize/optimize.sh" >> $HOME/.bashrc
source $HOME/.bashrc
```

**Method 2** : Add an alias to the script in /usr/local/bin

With this method img-optimize can be used by all users

```bash
sudo ln -s $HOME/.img-optimize/optimize.sh /usr/local/bin/img-optimize
sudo chmod +x /usr/local/bin/img-optimize
```

## Usage

```bash
Bash script to optimize your images and convert them in WebP
Usage: img-optimize [options] <images path>
If images path isn't defined, img-optimize will use the current directory
  Options:
       --jpg ..... optimize all jpg images
       --png ..... optimize all png images
       --webp ..... convert all images in webp
       --avif ..... convert all images in avif
       --std ..... optimize all png & jpg images
       --next ..... convert all images in webp & avif
       --all ..... optimize all images (png + jpg + webp + avif)
       -i, --interactive ..... run img-optimize in interactive mode
       -q, --quiet ..... run image optimization quietly
       --path <images path> ..... define images path
 Other options :
       -h, --help, help ... displays this help information
       --cmin [+|-]<n> ... File's status was last changed n minutes ago.
         act find cmin argument (+n : greater than n, -n : less than n, n : exactly n)
Examples:
  optimize all jpg images in /var/www/images
    img-optimize --jpg --path /var/www/images
```

### Update the script

To update the script, just run :

```bash
git -C $HOME/.img-optimize pull
```

### Setup daily cronjob

You just have to copy the scripts to /etc/cron.daily :

```bash
cp $HOME/.img-optimize/crons/jpg-png-cron.sh /etc/cron.daily/jpg-png-cron
cp $HOME/.img-optimize/crons/jpg-png-cron.sh /etc/cron.daily/webp-cron

chmod +x /etc/cron.daily/jpg-png-cron
chmod +x /etc/cron.daily/webp-cron
```

Then just edit your websites path set with the variables `sites` at the beginning of the cron scripts.

## Warning

Conversion process can take a while, you can use `tmux` to launch the script and be able to close your ssh connection without interrupting conversion. Then just use `tmux attach` to login back in your tmux session.

## Credits

- WebP conversion script was inspired by this [DigitalOcean Community Tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-and-serve-webp-images-to-speed-up-your-website)

- Tutorial about webp conversion available on [jesuisadmin.fr](https://jesuisadmin.fr/convertir-vos-images-en-webp-nginx/) (in french)
