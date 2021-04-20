# Ferda Devs

![Ferda devs](assets/ferda.gif)
> Ferda is a shell script to set up a macOS laptop for design and development.

It can be run multiple times on the same machine safely. It installs, upgrades, or skips packages based on what is already installed on the machine.

## Install

Download the script:

```sh
git clone git@github.com/fabledfoe/ferda.git && cd ferda
```

Review the script (please don't run scripts you don't understand):

```sh
less getthatw
```

Let's get that W, boys!

```sh
cd formation
./getthatw 2>&1 | tee ~/getthatw.log
```
Just follow the prompts and you’ll be fine. 👌

Once the script is done, quit and relaunch Terminal.

It is highly recommended to run the script regularly to keep your computer up to date.

Your last Formation run will be saved to `~/getthatw.log`. To review it, run `less ~/getthatw.log`.

That's it! :sparkles:

## What it sets up
The setup process will install:

<details>
<summary>Basic tools:</summary>

* [XCode Command Line Tools](https://developer.apple.com/xcode/downloads/) for developer essentials.
* [Bash-it](https://github.com/Bash-it/bash-it/), for a more powerful bash.
* [Git](https://git-scm.com/) for version control
* [Homebrew](http://brew.sh/) for managing operating system libraries.
</details>

<details>
<summary>Package Managers:</summary>

* [NVM](https://github.com/creationix/nvm/) for managing and installing multiple versions of [Node.js](http://nodejs.org/) and [npm](https://www.npmjs.org/)
* [Rbenv](https://github.com/sstephenson/rbenv) for managing versions of Ruby
* [Yarn](https://yarnpkg.com/en/) for managing JavaScript packages
</details>

<details>
<summary>CLI Tools & Utilities:</summary>

* [asciinema](https://asciinema.org/) for recording terminal sessions
* [Hotel](https://github.com/typicode/hotel), a simple process manager for developers
* [Hub](http://hub.github.com/) for interacting with the GitHub API
* [hugo](https://gohugo.io/), an open-source static site generator
* [ImageMagick](http://www.imagemagick.org/) to create, edit, compose, or convert bitmap images
* [mas](https://github.com/mas-cli/mas) Mac App Store command line interface
</details>

### Apps

<details>
<summary>Productivity</summary>

* [Alfred](https://www.alfredapp.com/) for increased productivity and efficiency with macOS.
</details>

<details>
<summary>Development</summary>

* [Dash](https://kapeli.com/dash) offline access to API documentation sets
* [Hyper](https://hyper.is/) for an alternative terminal.
* [ImageOptim](https://imageoptim.com/mac) for image optimization.
* [iTerm](https://www.iterm2.com/) for a better terminal.
* [Virtual Box](https://www.virtualbox.org/) powerful virtualization tool
* [Visual Studio Code](https://code.visualstudio.com/) IDE
</details>

<details>
<summary>Communication</summary>

* [Bear](http://www.bear-writer.com/) for writing and previewing markdown.
* [Slack](https://slack.com/) where work happens.
</details>

<details>
<summary>Utilities</summary>

* [1Password](https://1password.com/) for password management.
* [Divvy](http://mizage.com/divvy/) for better window management.
* [Encrypto](https://macpaw.com/encrypto) for securing files.
* [Karabiner](https://pqrs.org/osx/karabiner/) for keyboard mapping.
</details>

<details>
<summary>Miscellaneous</summary>

* [Gifox](https://gifox.io/) for GIF making.
* [Rocket](http://matthewpalmer.net/rocket/) for Slack-like emojis.
* [Spotify](https://www.spotify.com/) for music.
* [VLC](http://www.videolan.org/) for a better media player.
</details>

<details>
<summary>Browsers</summary>

* [Blisk](https://blisk.io/) for cross-device web development.
* [Brave](https://brave.com/) for web browsing without ads.
* [Chrome](https://www.google.com/chrome/browser/desktop/) for fast and free web browsing.
* [Firefox](https://www.mozilla.org/en-US/firefox/new/) for web browsing and testing.
* [TorBrowser](https://www.torproject.org/projects/torbrowser.html.en) for super secret web browsing.
</details>

<sub>See [`swag`](swag) for the full list of apps that will be installed. Adjust it to your personal taste.</sub>

It should take less than 20 minutes to install (depends on your machine).

## 🌶 Just add `~/.sandos`

![Crushin sandos](assets/ferda.gif)

Your `~/.sandos` is added at the end of the Formation script. Put your customizations there.
For example:

```sh
#!/usr/bin/env bash

SETUP_ROOT=$HOME/.setup

NERDFONTS_RELEASE=$(curl -L -s -H 'Accept: application/json' https://github.com/ryanoasis/nerd-fonts/releases/latest)
NERDFONTS_VERSION=$(get_github_version $NERDFONTS_RELEASE)

DIRECTORIES=(
    $HOME/Desktop/code
    $HOME/Desktop/design
    $HOME/Desktop/*dump
    $HOME/Desktop/GIFs
    $HOME/Desktop/projects
    $HOME/Desktop/screenshots
)

NERDFONTS=(
    SpaceMono
    Hack
    AnonymousPro
    Inconsolata
)

step "Making directories…"
for dir in ${DIRECTORIES[@]}; do
    mkd $dir
done

step "Installing fonts…"
for font in ${NERDFONTS[@]}; do
    if [ ! -d ~/Library/Fonts/$font ]; then
        printf "${indent}  [↓] $font "
        wget -P ~/Library/Fonts https://github.com/ryanoasis/nerd-fonts/releases/download/$NERDFONTS_VERSION/$font.zip --quiet;unzip -q ~/Library/Fonts/$font -d ~/Library/Fonts/$font
        print_in_green "${bold}✓ done!${normal}\n"
    else
        print_muted "${indent}✓ $font already installed. Skipped."
    fi
done
```

Write your customizations such that they can be run safely more than once.
See the `getthatw` script for examples.

Formation functions such as `step` and `link` can be used in your `~/.sandos`.

## Known Issues
Cask does not recognize applications installed outside of Homebrew Cask – in the case that the script fails, you can either remove the application from the install list or uninstall the application causing the failure and try again.

## Acknowledgements

Inspiration and code was taken from many sources, including:

* [Mathias Bynens'](https://github.com/mathiasbynens) [dotfiles](https://github.com/mathiasbynens/dotfiles)
* thoughtbot's [laptop](https://github.com/thoughtbot/laptop/)

## 📜  License

Formation is customized for my own needs. It is free software, and may be redistributed under the terms specified in the [LICENSE] file.

[LICENSE]: LICENSE
