* README_EN.txt
* 2024.06.08
* externals

1. DESCRIPTION
2. EXTERNALS
2.1. Git `.gitmodules` support
2.1.1. `git_gen_gitmodules.sh` usage examples

-------------------------------------------------------------------------------
1. DESCRIPTION
-------------------------------------------------------------------------------
Description of global external dependencies applicable to multiple projects and
not described in detail in those projects.

-------------------------------------------------------------------------------
2. EXTERNALS
-------------------------------------------------------------------------------
All project externals are declared in `.externals*` files.

To checkout externals you must use the
[vcstool](https://github.com/dirk-thomas/vcstool) python module.

NOTE:
  To install the module from the git repository:

  >
  python -m pip install git+https://github.com/dirk-thomas/vcstool

CAUTION:
  To use the sparse checkout feature (partial checkout) you must use a forked
  repository:

  >
  python -m pip install git+https://github.com/aaronplusone/vcstool@feature-sparse-checkouts

    Or

  >
  python -m pip install git+https://github.com/plusone-robotics/vcstool@por_master

-------------------------------------------------------------------------------
2.1. Git `.gitmodules` support
-------------------------------------------------------------------------------
To convert `vcstool` repositories file to Git `.gitmodules` format you can use
these scripts:

https://github.com/andry81/gitcmd/tree/HEAD/vcstool/git_gen_gitmodules.sh
https://github.com/andry81/gituserbin/tree/HEAD/gen-vcstool-gitmodules.sh

-------------------------------------------------------------------------------
2.1.1. `git_gen_gitmodules.sh` usage examples
-------------------------------------------------------------------------------

1. Convert each `.externals*` file into exising single `.gitmodules*` file.

  >
  cd myrepo/path
  git_gen_gitmodules.sh -f
  >
  find . -name '.gitmodules*' -type f

2. Convert and append `.externals-*` into existing `.gitmodules`.

  >
  cd myrepo/path
  git_gen_gitmodules.sh -fa . '.externals-*'
  >
  find . -name '.gitmodules' -type f

3. Convert and overwrite `.externals` into existing `.gitmodules`, and append
   the rest `.externals-*`.

  >
  cd myrepo/path
  git_gen_gitmodules.sh -fat
  >
  find . -name '.gitmodules' -type f

3. Convert and overwrite `.externals` into existing `.gitmodules`, and append
   the rest `.externals-*`.
   Generate submodule names from the `url` field instead of `repositories` key
   values.

  >
  cd myrepo/path
  git_gen_gitmodules.sh -fat --gen-submodule-name-from-url
  >
  find . -name '.gitmodules' -type f
