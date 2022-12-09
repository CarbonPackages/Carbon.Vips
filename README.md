[![Latest stable version]][packagist] [![Total downloads]][packagist] [![License]][packagist] [![GitHub forks]][fork] [![GitHub stars]][stargazers] [![GitHub watchers]][subscription]

# Carbon.Vips: Blazing fast image processing for Neos and Flow

Your [Neos] website or Flow application usually uses [ImageMagick] and [GD] for rendering smaller versions of your photos, or previews of other media assets. While these libraries are quite powerful, they need a big amount of memory for processing images. It can easily happen for a Neos page with a lot of thumbnails to consume hundreds of Megabytes of RAM to create the respective image files. When the original assets are rather large or you need to process animated GIFs, you might even need Gigabytes of RAM just for rendering that page.

Many hoster and Docker images provides [libvips], a low-level code library which can do almost the same things like ImageMagick, but much faster and with a relatively small memory footprint.

It is recommended that you configure all your Flow and Neos projects to use Vips instead of ImageMagick.

## Before you start

When you enable Vips for your project, you will also need Vips support in your development environment.

The reason for that is, that you need to be able to run composer update. The package which provides Vips support ([rokka/imagine-vips]) has a dependency on the vips PHP extension, and if you don't have that extension enabled, Composer will complain about non fulfilled platform requirements.

The solution is easy though: just install PHP Vips for your local environment. Make sure though, that everybody in your team who runs composer update also has Vips installed.

## Installing PHP Vips for your development environment

### ddev

Just add following line to your ddev `config.yaml` file:

```yaml
webimage_extra_packages:
  - php8.1-vips
```

After you added this, you can restart your container with `ddev restart` and you are ready to go!

> Note: Please set the correct PHP version for the vips package

### Local installation

For your development environment you need to install two libraries:

1. a Vips library for your operating system
2. a PHP extension which provides bindings to that low-level library

The installation process is explained on the [php-vips-ext project site] on Github. As an example, if your development
system is a Mac and you are using [Homebrew] as a package manager the installation steps are as follows:

First install the libvips system library:

```bash
brew install vips
```

Next, install the php-vips extensions. This extension is installed via [PECL]
and which will compile the library specifically for your current PHP version:

```bash
pecl install vips
```

When everything's working fine, you should be able to see `vips` in the list of enabled PHP modules when you're running
`php -m` from the command line.

If that does not list `vips`, you need to enable the extension in your PHP configuration, for example by creating a new
file `ext-vips.ini` in your PHP's `conf.d/` folder:

```
extension=vips.so
```

## Note

Many parts of this readme are taken from [Flownative's blog entry about vips].

[packagist]: https://packagist.org/packages/carbon/vips
[latest stable version]: https://poser.pugx.org/carbon/vips/v/stable
[total downloads]: https://poser.pugx.org/carbon/vips/downloads
[license]: https://poser.pugx.org/carbon/vips/license
[github forks]: https://img.shields.io/github/forks/CarbonPackages/Carbon.Vips.svg?style=social&label=Fork
[github stars]: https://img.shields.io/github/stars/CarbonPackages/Carbon.Vips.svg?style=social&label=Stars
[github watchers]: https://img.shields.io/github/watchers/CarbonPackages/Carbon.Vips.svg?style=social&label=Watch
[fork]: https://github.com/CarbonPackages/Carbon.Vips/fork
[stargazers]: https://github.com/CarbonPackages/Carbon.Vips/stargazers
[subscription]: https://github.com/CarbonPackages/Carbon.Vips/subscription
[neos]: https://www.neos.io
[imagemagick]: https://www.imagemagick.org
[gd]: http://php.net/manual/en/book.image.php
[libvips]: https://github.com/libvips/libvips
[rokka/imagine-vips]: https://github.com/rokka-io/imagine-vips
[php-vips-ext project site]: https://github.com/libvips/php-vips-ext
[homebrew]: https://brew.sh
[pecl]: https://pecl.php.net
[flownative's blog entry about vips]: https://www.flownative.com/de/dokumentation/anleitungen/beach/neos-cms-vips-for-faster-image-rendering.html
