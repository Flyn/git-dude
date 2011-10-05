# git-dude with trac links

git-dude is a simple git desktop notifier written by Marcin Kulik. It monitors git repositories in
current directory for new commits/branches/tags and shows desktop notification if
anything new arrived.

TracLinks is a fork creating links to directly access commit, tag and branch pages on
a trac installation configured with a GitPlugin.
Links only works on KDE because Gnome seems to completely ignore Hyperlinks tags.

_I didn't test it on Mac OS._

## How it works

It simply uses `git fetch` and parses its output to see what has changed. Then it
formats new commit messages with `git log` and shows desktop notification with
`notify-send` (Linux) or `growlnotify` (OSX). All of this in infinite loop.


## Requirements

On Linux:

* `notify-send` (Fedora: _libnotify_ package, Ubuntu: _libnotify-bin_ package)
* KDE

On OSX:

* `growlnotify`, from [Growl Extras](http://growl.info/extras.php#growlnotify)
  (Homebrew: _growlnotify_ package)


## Installation

    $ curl -skL https://github.com/Flyn/git-dude/raw/traclinks/git-dude >~/bin/git-dude
    $ chmod +x ~/bin/git-dude

## Usage

git-dude iterates over repositories that live inside _the dude directory_. This
directory is nothing more than container for cloned repositories of projects
you want to watch.  Name it like you want, here for example we use
_~/.git-dude_:

    $ mkdir ~/.git-dude
    $ cd ~/.git-dude

Clone some repositories:

    $ git clone --mirror https://github.com/joelthelion/autojump.git
    $ git clone --mirror git://github.com/pyromaniac/hoof.git

I recommend `git clone --mirror` - it doesn't checkout working directory so it
saves some disk space for bigger projects.

Symlinked repositories work too. This way you can monitor already cloned
projects:

    $ ln -s ~/code/tmuxinator .

Now run this to monitor _pwd_:

    $ git dude

You can also pass directory name as first argument to specify which directory
to monitor instead of _pwd_.

    $ git dude ~/watched-repos

This way you can have multiple _dude directories_ each being monitored by
separate git-dude process.

## Configuration

Set how often git-dude should check for changes (in seconds, default: 60):

    $ git config --global dude.interval 30

Set path to icon used by desktop notifications (default: none):

    $ git config --global dude.icon ~/.git-dude/github_32.png
    
Set url for the trac server:

    $ git config --global dude.tracUrl "http://mytrac:8000"

## Author

Original script:
Marcin Kulik (http://ku1ik.com/ | @sickill)

Trac Links branch:
Flyn (@flynscape)
