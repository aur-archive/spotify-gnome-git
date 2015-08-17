# Maintainer: Sebastian Stammler <echo c3RhbW1sZXJAY2FudGFiLm5ldAo= | base64 -d>
# Upstream URL: https://github.com/jreese/spotify-gnome
# All credit for the software goes to John Reese
# Set the _spotify_bin variable if your spotify client is not installed in the default location.
#
# Now pacman 4.1 ready!
# For improvements/fixes to this package, please send me a
# pull request on github: https://github.com/sebastianst/aur-packages


pkgname=spotify-gnome-git
pkgver=20131128
pkgrel=1
pkgdesc="Spotify Gnome media key integration via MPRIS"
arch=('any')
url="https://github.com/jreese/spotify-gnome"
license=('MIT')
depends=('spotify'
  'gnome-desktop'
  'python2'
  'python2-dbus'
  'python2-gobject')
makedepends=('git')
optdepends=('telepathy-glib: Playing integration for telepathy based clients')

# git variables
_gitroot="git://github.com/jreese/spotify-gnome.git"
_gitname="spotify-gnome"

source=("$_gitroot")
md5sums=('SKIP') #generate with 'makepkg -g'

_def_spotify_bin="/usr/bin/spotify"
# Set this to the path of your spotify client, if not located at _def_spotify_bin
_spotify_bin=$_def_spotify_bin

pkgver() {
  cd "$srcdir/$_gitname"
  git log -1 --format="%cd" --date=short | sed 's|-||g'
}

build() {
  # set the _spotify_bin variable accordingly,
  # if spotify is not located at the default location.
  cd "$srcdir/$_gitname/bin"
  if [[ ! -f "$_def_spotify_bin" ]]; then
    msg "Spotify not installed in the default location ${_def_spotify_bin}."
    if [[ "$_spotify_bin" = "$_def_spotify_bin" ]]; then
      error "Set the _spotify_bin variable in the PKGBUILD accordingly"
      error "and restart the installation of ${pkgname}."
      exit 1
    else
      msg2 "Setting the _spotify_bin variable in the script to ${_spotify_bin}."
      sed -i -e 's%^spotify_bin = ".*"%spotify_bin = "'$_spotify_bin'"%' spotify
    fi
  fi
}

package() {
  cd "$srcdir/$_gitname"
  install -Dm755 bin/spotify "$pkgdir/usr/local/bin/spotify"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
