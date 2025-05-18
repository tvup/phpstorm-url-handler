
# PhpStorm URL Handler
Heavily inspired by [PhpStorm URL Handler](https://github.com/sanduhrs/phpstorm-url-handler) (GNU GENERAL PUBLIC LICENSE)

This tool is a launcher to open files in PhpStorm at the defined line
number and an associated desktop file that conforms to the Desktop Entry
Specification for use in Gnome and KDE desktop environments.

## Installation
### Pre-requisites
The executable `phpstorm` or `pstorm` must be in your `$PATH`.
If it is not, either add the install location to your path

    export PATH="/path/to/phpstorm/bin/phpstorm.sh:$PATH"

or symlink it to one of `/usr/bin` or `/usr/local/bin` - which already should be in your `$PATH`.
Use `sudo` if needed

    ln -s /path/to/phpstorm/bin/phpstorm.sh /usr/bin/phpstorm

### Manual changes(!)
Edit `fallback-folder` in `phpstorm-url-handler/phpstorm-url-handler` replace with the path to your likings.
```
projectfolder=${projectfolder:-"$HOME/Projects/myproject"}
```  

### Installation steps
Then copy the actual handler to your `$PATH` and make it executable.
Use `sudo` if needed

    cp phpstorm-url-handler/phpstorm-url-handler /usr/bin/phpstorm-url-handler
    chmod +x /usr/bin/phpstorm-url-handler

Install the `.desktop` file to register the mime-types.
Use `sudo` if needed

    desktop-file-install phpstorm-url-handler/phpstorm-url-handler.desktop
    update-desktop-database

## Usage
### Browsers
It will be used within browsers where links are defined like this:

    <?php
    $file = "/path/to/filename.php";
    $line = 35;
    print "<a href='phpstorm://open?url=file://$file&line=$line'>Open with PhpStorm</a>";
    // Alternate Syntax matches PhpStorm 8 for the Macintosh
    print "<a href='phpstorm://open?file=$file&line=$line'>Open with PhpStorm</a>";
    ?>

### Command-line usage
It can be used from command-line as well, if the following syntax is used:
```
FILE="/path/to/filename.php"
LINE=35
./phpstorm-url-handler "phpstorm://open?url=file://${FILE}&line=${LINE}"
```

Alternative syntax for PhpStorm 8 for the Macintosh for cross-platform compatibility.

    FILE="/path/to/filename.php"
    LINE=35
    ./phpstorm-url-handler "phpstorm://open?file=${FILE}&line=${LINE}"
