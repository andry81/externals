* README_EN.txt
* 2024.06.08
* externals

1. DESCRIPTION
2. EXTERNALS
2.1. Git `.gitmodules` support

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
