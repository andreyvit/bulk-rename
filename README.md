# Interactive bulk rename

Have you ever wished to use your editor's features (like search-and-replace, multicaret editing or macros) to rename, move or copy files? Now you can:

* invoke bulk-rename with a folder name;
* bulk-rename enumerates all files in the folder and opens an ad-hoc shell script with a bunch of `mv <file> <file>` commands in your $EDITOR;
* you fill in the correct destination file names and close the editor;
* bulk-rename confirms your intentions and executes the shell script.

## Usage

    Usage: bulk-rename [-c] [-d <dest-folder>] <folder>

    Arguments:
      <folder>                          A folder with files to rename/move/copy

    Options:
      -c, --copy                        Copy instead of renaming/moving
      -d, --destination <dest-folder>   Put the renamed/copied files into this folder

    Generic options:
      --help                            Display this usage info
      --version                         Display the version number (1.0.0)
      --self-update                     Update this script to the latest version from GitHub
      --self-update-check               Check for updates on GitHub
      --self-update-dry-run             Like --self-update, but only echos the update commands

## Installation

Easy:

    curl -sL https://github.com/andreyvit/bulk-rename/raw/master/bulk-rename | sudo bash -s -- --self-install

Involved:

    curl -sL https://github.com/andreyvit/bulk-rename/raw/master/bulk-rename | sudo tee /usr/local/bin/bulk-rename | echo ok
    sudo chmod +x /usr/local/bin/bulk-rename

Hardcore:

    git clone https://github.com/andreyvit/bulk-rename.git
    sudo ln -s `pwd`/bulk-rename/bulk-rename /usr/local/bin/bulk-rename

Note: the script will check for updates in background, and will notify you when a new version is published on GitHub; run with `--self-update` to perform the update.

## Notes

Inside your shell script, mv and cp commands are redefined to:

* implicitly invoke mkdir -p, so you can use slashes to move files into new subfolders;
* stop on the first failed operation (you then get an option to re-invoke the editor);
* prefix the second argument with `<dest-folder>/` if -d/--destination is provided (but note that `<dest-folder>` is resolved to an absolute path prior to execution);
* implement a dry-run (“Display actual commands”) mode.

## License

(C) 2012, Andrey Tarantsov (andrey@tarantsov.com). Provided under the MIT license.
