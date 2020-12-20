# emacs-build

Scripts to build a distribution of Emacs from sources, using MSYS2 and Mingw64(32)

## Rationale

I wanted a script to build Emacs from sources, package it and install it on
different computers, with the following conditions

- I should be able to build any branch or release from Emacs. This includes
  the last release branch (right now emacs-27), as well as the master branch
  for development. Always using pristine sources from Savannah.

- I want to build emacs with different options from the default, which is to
  use all features available. For instance, I do not care for SVG support.

- The script needs to track all packages that are required by the Emacs build
  even if I change the build options.

- The installation should take as little space as possible, removing useless
  directories or files that come from the dependencies. For instance, headers
  from libraries used by emacs, spurious documentation files, etc.

- Eventually, the script should be able to build other components I regularly
  use, such as mu, mu4e or pdf-tools.

## Usage

````
   ./emacs-build.sh [-64] [-32] [--branch b]
                    [--clone] [--ensure] [--build] [--deps] [--package]
                    [--without-X] [--with-X]

Actions:

   --clone       Download Savannah's git repository for Emacs
   --ensure      Ensure that required packages are installed
   --build       Configure and build Emacs from sources
   --deps        Create a ZIP file with all the Mingw64/32 dependencies
   --package     Package an Emacs previously built with the --build option

   Multiple actions can be selected. The default is to run them all in a logical
   order: clone, ensure, build, deps and package.

Options:
   -64           Prepare or build for Mingw64 (default)
   -32           Prepare or build for Mingw32
   --branch b    Select branch 'b' for the remaining operations
   --slim        Remove Cairo, SVG and TIFF support for a slimmer build
                 Remove also documentation files and other support files
                 from the dependencies file
   --with-X      Add requested feature in the dependencies and build
   --without-X   Remove requested feature in the dependencies and build

   X is any of the known features for emacs in Windows/Mingw:
     $all_features
````