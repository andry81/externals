* README_EN.txt
* 2026.01.16
* externals

1. DESCRIPTION
2. EXTERNALS
2.1. Git modules experience
2.2. Git `.gitmodules` support
2.2.1. `git_gen_gitmodules.sh` usage examples

-------------------------------------------------------------------------------
1. DESCRIPTION
-------------------------------------------------------------------------------
Description of global external dependencies applicable to multiple projects and
not described in detail in those projects.

-------------------------------------------------------------------------------
2. EXTERNALS
-------------------------------------------------------------------------------
All project externals are declared in `.externals*` file(s).

Basically, you have to checkout the main `.externals` file and if does exist
others with a suffix `.externals-*`, then select those you need additionally.

NOTE:
  All `.externals*` files must not intersect to be able to take ALL external
  dependencies including those you don't need to. This is by design to ease the
  maintainability and the testing.

For example, if there is a list of files:

  * .externals
  * .externals-winxp
  * .externals-win7

Then you have to checkout either:

  * .externals
  * .externals-win7

  OR

  * .externals
  * .externals-winxp

To clone only required directories of externals, you must use `vcstool` (or
probably another name related to a fork you are chosen) python module with the
sparse checkout feature and `.externals*` file(s), otherwise the
`git clone --recurse-submodules` would use `.gitmodules` (if has any) and
checkout all modules recursively and completely, including all subdirectories
which is not required to checkout.

To use the sparse checkout feature (partial checkout) you must install from a
forked repository:

NOTE:
  There is always be forks that has ahead commits with new functionality or
  even a standalone development. You have to investigate on your own to find
  the best variant.

NOTE:
  Some forks may does not exist as forks, so you won't find them using a fork
  related tree search. The only way to find is to use a broad Git search using
  keywords.
  See for details: `Forks trace or filtering is broken (forks segmentation)` :
  https://github.com/orgs/community/discussions/173970

>
python -m pip install git+https://github.com/aaronplusone/vcstool@feature-sparse-checkouts

  Or

>
python -m pip install git+https://github.com/plusone-robotics/vcstool@por_master

NOTE:
  Original repository: https://github.com/dirk-thomas/vcstool

  Discussion: `Status of vcstool` : https://github.com/dirk-thomas/vcstool/issues/242

NOTE:
  There is other forks with or without continue of original repository
  development:

  * https://github.com/aaronplusone/vcstool/tree/feature-sparse-checkouts  
  * https://github.com/MaxandreOgeret/vcstool2 (https://pypi.org/project/vcstool2/)
  * https://github.com/ros-infrastructure/vcstool
    (https://github.com/ros-infrastructure/vcs2l)

NOTE:
  Mine list of `vcstool` related forks:

  * https://github.com/orgs/andry81-forks/repositories?type=source&q=vcstool

  Maximum list of the original repository forks:

  * https://github.com/dirk-thomas/vcstool/forks?include=active%2Carchived%2Cinactive%2Cnetwork&page=1&sort_by=stargazer_counts
    (sorted by stars)
  * https://useful-forks.github.io/?repo=dirk-thomas/vcstool
    (sorted by stars)
  * https://devnoname120.github.io/useful-forks/?repo=dirk-thomas/vcstool
    (sorted by stars and ahead commits)

-------------------------------------------------------------------------------
2.1. Git modules experience
-------------------------------------------------------------------------------
https://gist.github.com/andry81/b0000d2ddfa890f7ac68f1cabb6c1978

-------------------------------------------------------------------------------
2.2. Git `.gitmodules` support
-------------------------------------------------------------------------------
To convert `vcstool` repositories file to Git `.gitmodules` format you can use
these scripts:

https://github.com/andry81/gitcmd/tree/HEAD/scripts/vcstool/git_gen_gitmodules.sh
https://github.com/andry81/gituserbin/tree/HEAD/scripts/gen-vcstool-gitmodules.sh

-------------------------------------------------------------------------------
2.2.1. `git_gen_gitmodules.sh` usage examples
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
