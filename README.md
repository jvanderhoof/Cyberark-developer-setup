# CyberArk Developer Setup (OSX)

This includes a potential list of applications and libraries to get a new developer setup on OSX

### XCode Setup
XCode provides a core set of build tools required for building a variety of projects.  It should be installed first.  To install, simply open a new shell (`Applications/Utilities/Terminal`) and run the following:

```bash
$ sudo xcode-select --install
```

### Homebrew
Homebrew is a package manager for OSX. It can be extended to with `Cask` to install both libraries and applications. Full documentation can be found here: [Homebrew](https://brew.sh/).

To install:

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next install Cask:

```bash
$ brew tap caskroom/cask
```

### Ruby
The best way to work with Ruby in development is to use a package manager.  There are a couple of options available.  We currently use [RVM](https://rvm.io/). To install RVM:

```bash
$ brew install curl gpg
$ curl -sSL https://rvm.io/mpapis.asc | gpg2 --import # 409B6B1796C275462A1703113804BB82D39DC0E3
$ curl -sSL https://get.rvm.io | bash -s stable
```

Check the fingerprint against https://keybase.io/mpapis

Now RVM is installed, but we don't have access to it in our shell just yet.  Let's source it to verify RVM was successfully installed:
```bash
$ source ~/.rvm/scripts/rvm
```

Now you should be able to check the version:
```bash
rvm --version
```

Once RVM is installed, you can install different Ruby versions via:

```bash
$ rvm install 2.4.1
```

### Development
If you're coming from a language like C# or Java, the lack of a robust IDE might feel jarring.  Ruby, being a dynamic language, doesn't lend itself all that well to an IDE (in contrast to the power of VS or Eclipse). As such, Ruby developers tend to leverage simpler text editors (Atom, Sublime, Vim, Emacs, etc.)  Personally, I'm a huge fan of Atom, but just like religion, you should never tell a developer what editor to use :)

##### Atom
To install Atom:
```bash
$ brew cask install atom
```

##### Git
We use Git for version control.  OSX ships with `Git` installed, but it's an old version. To upgrade:
```bash
$ brew install git
```

##### Docker
Docker is fundamental tool as well. To install the OSX specific Docker:
There is a cask for installing Docker, but the current release has some major stability issues.  For now, please download and install the last stable build: https://download.docker.com/mac/stable/16048/Docker.dmg
<!-- ```bash
$ # !!! CURRENTLY A BAD BUILD!!!! brew cask install docker
``` -->
If you are asked to upgrade, please choose "Skip this Version"


##### Postgres
We use Postgres for our database. Postgres can be leveraged either through Docker containers (using Docker Compose), or installed locally. It's a matter of personal preference.  If you do want to install Postgres:

```bash
$ brew install postgresql
```

### Shell
I recommend installing `iTerm` and using the `ZSH` shell (as apposed to the default `Bash` shell). `iTerm` provides a much cleaner terminal interface, and `ZSH` has a rich plugin system and autocomplete functionality. These are both optional.

To install:

```bash
$ brew cask install iterm2
$ curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```

### Initial setup
Generate a new SSH key to use for connecting to GitHub:
```bash
$ ssh-keygen -t rsa -b 4096 -C "your-github-email-address"
```
Now let's upload the key to your Github profile. First, copy it:
```bash
$ cat ~/.ssh/id_rsa.pub | pbcopy
```
Then, on Github, click on your profile in the upper right corner and choose `Settings`.  Click `SSH and GPG keys` on the left menu. Click `New SSH Key`.  Give your key a name, and paste your public key into key box. Finally, click `Add SSH Key` to save it to your profile.

Now, let's set some sane Git defaults:

```
$ git config --global user.name "Full Name"
$ git config --global user.email "email@example.com"
$ git config --global rerere.enabled true # for sane rebasing :)
```

### Other Useful Apps
Finally, we can install a couple apps to make life easier:
```bash
$ brew cask install google-chrome
$ brew cask install slack
$ brew cask install kdiff3 # diffing tool
$ brew cask install cloudapp # screen capture/recording
$ brew install asciinema # record terminal sessions for demos
```

It can be annoying not to be able see hidden files in Finder. You can change this by updating the system settings and restarting Finder:

```bash
$ defaults write com.apple.finder AppleShowAllFiles YES
$ killall Finder /System/Library/CoreServices/Finder.app
```

Feel free to add any other tricks and tips you have.
