# Why this fork?

The selling point of Evince for me is the previewing functionality.  You can
hover over any reference in a PDF and it will preview what is going on at the
referenced part.  I don't know any other PDF viewer that has that feature.
Porting this feature to Zathura would be the better way to go, but would require
some engineering.  This might be some project I will look into in the future but
for now I came to the conclusion that Evince is just the best for me.  At some
point I might even consider to merge these changes into upstream, but there was
already a PR for that and [it got
rejected](https://gitlab.gnome.org/GNOME/evince/-/merge_requests/134).

So my goal with this fork is to make Evince behave more like Zathura.
That is why this fork has the following changes to upstream:

- The menu bar (or toolbar) can be hidden via a keyboard shortcut. This is
  `ALT-m` or F12 by default. [main and keyboard]
- Hide the menu bar by default. [only keyboard]
- Some keyboard shortcuts are added/modified/removed. Examples are `J` and `K`
  for page up/down, or `CTRL+o` for going back in history. [only keyboard]

All branches can be configured to your liking. Modifications to keyboard
shortcuts can be done in the `shell/ev-application.c`. Check the diff to
upstream if you are lost.

You can expect me to rebase on upstream when there is a new release, at least as
long as no other PDF viewer has the above mentioned feature.

## Hiding the menu bar by default

This one requires a one word change and is already included in the keyboard
branch. You can just cherry pick the correct commit in the keyboard branch. But
basically you just modify the initial visibility of the menu bar in the file
`shell/evince-toolbar.ui`. It's right at the top.

## Building

You need to choose the correct prefix for your system. For most systems this
should be `/usr`. Note that these instructions only update the evince binary, so
this is based on the assumption that your libraries and other files of evince
should already be up to date. I'm not sure if this assumption breaks with
non-rolling-release distributions. If so check how you can install the compiled
files. I guess that should not be to hard.
``sh
git clone https://github.com/fabian-thomas/cleaner-evince
meson setup --prefix /usr build
meson compile -C build
sudo cp build/shell/evince "$(which evince)"
``

# ![evince-logo] Evince

Evince is a document viewer capable of displaying multiple and single
page document formats like PDF and Postscript.  For more general
information about Evince please visit our website at 
https://wiki.gnome.org/Apps/Evince.

This software is licensed under the [GPLv2][license].

[![flatpak]](https://flathub.org/apps/details/org.gnome.Evince)

## Evince Requirements

* [GNOME Platform libraries][gnome]
* [Poppler for PDF viewing][poppler]

## Evince Optional Backend Libraries

* [Spectre for PostScript (PS) viewing][ghostscript]
* [DjVuLibre for DjVu viewing][djvulibre]
* [Kpathsea for Device-independent file format (DVI) viewing][dvi]
* [Archive library for Comic Book Resources (CBR) viewing][comics]
* [LibTiff for Multipage TIFF viewing][tiff]
* [LibGXPS for XML Paper Specification (XPS) viewing][xps]

## Default branch renamed to `main`

The default development branch of Evince has been renamed to `main`. To update
your local checkout, use:
```sh
git checkout master
git branch -m master main
git fetch
git branch --unset-upstream
git branch -u origin/main
git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main
```

[gnome]: https://www.gnome.org/
[poppler]: https://poppler.freedesktop.org/
[ghostscript]: https://www.freedesktop.org/wiki/Software/libspectre/
[djvulibre]: https://djvulibre.djvuzone.org/
[dvi]: https://tug.org/texinfohtml/kpathsea.html
[comics]: https://libarchive.org/
[tiff]: http://libtiff.org/
[xps]: https://wiki.gnome.org/Projects/libgxps
[license]: COPYING
[evince-logo]: data/icons/scalable/apps/org.gnome.Evince.svg
[flatpak]: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a6/Flathub-badge-en.svg/240px-Flathub-badge-en.svg.png
