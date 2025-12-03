<!-- --------------------------------------------------------------------------------- -->

## Useful Commands

[Archiving](#archiving)<br>
[cron](#cron)<br>
[FFmpeg](#ffmpeg)<br>
[File viewing and editing](#file-viewing-and-editing)<br>
[Git](#git)<br>
[Homebrew](#homebrew)<br>
[Java](#java)<br>
[JavaScript](#javascript)<br>
[Libraries](#libraries)<br>
[Macintosh configuration issues](#macintosh-configuration-issues)<br>
[NVIDIA](#nvidia)<br>
[Octave](#octave)<br>
[OpenSSH](#openssh)<br>
[Python](#python)<br>
[Rust](#rust)<br>
[screen](#screen)<br>
[SQL](#sql)<br>
[System commands](#system-commands)<br>
[Tesseract](#tesseract)<br>
[Text commands](#text-commands)<br>
[Verifying signatures](#verifying-signatures)<br>

<hr>

<!-- ------------------------------ Archiving ------------------------------ -->

#### Archiving

Extract from zip archive<br>
`unzip -q <source.zip> -d <destination directory>`

List contents of a zip archive<br>
`unzip -l <source.zip>`

Extract from a .gz file without erasing it<br>
`gunzip -k <source.gz>`

Expand a tar.gz file<br>
`tar -xf <file.tar.gz>`

Make a .tar.gz file<br>
`tar -czf <filename>.tar.gz <file(s)>`

Omit .git or extended attribute files (works on Linux, not on Macintosh)<br>
`tar --exclude-vcs -czf <filename>.tar.gz <file(s)>`<br>
`tar --no-xattrs -czf <filename>.tar.gz <file(s)>`
<br>Better alternative: use gtar (gnu-tar)<br>
`gtar -czf <filename>.tar.gz <file(s)>`

View a .gz file<br>
`zcat <file.gz> [| less]`

<hr>

<!-- ------------------------------ cron ------------------------------ -->

#### cron

Edit cron table<br>
`crontab -e`

List cron table<br>
`crontab -l`

<hr>

<!-- ------------------------------ FFmpeg ------------------------------ -->

#### FFmpeg

Use ffmpeg to convert a video<br>
`ffmpeg -i <original-movie> [-strict -2] <copy-of-movie-in-new-format>`

Use ffmpeg to extract part of a video<br>
`ffmpeg -ss <start-time-in-seconds> -i <original-movie> -t <duration-in-seconds> -c copy <new-movie>`

Rescale a video<br>
`ffmpeg -i <original-movie> -vf scale=<width>:<height>,setsar=1:1 <rescaled-movie>`

[More commands](https://catswhocode.com/ffmpeg-commands/)

<hr>

<!-- ------------------------------ File viewing and editing ------------------------------ -->

#### File viewing and editing

View a binary file<br>
`hexdump -C <filename>`

Convert Graphviz .dot to .svg<br>
`dot -Tsvg <dot-filename> -o <svg-filename>`

Convert Postscript (.ps) to PDF<br>
`ps2pdf <ps-filename>`

#### File viewing and editing (Macintosh)

Open a file with TextEdit<br>
`open -e <filename>`

Open a file with a specified application<br>
`open -a <application> <filename>`

Determine a file's MIME type<br>
`file --mime-type -b <filename>`

<hr>

<!-- ------------------------------ Git ------------------------------ -->

#### Git

Check the version number<br>
`git --version`

Show configuration<br>
`git config --list [--global|local]`

Set global configuration<br>
`git config --global user.name "Your Name"`
<br>
`git config --global user.email user@domain.com`

Set local configuration<br>
`git config user.name "Your Name"`
<br>
`git config user.email user@client.com`

Create a local repository (in your project directory)<br>
`git init`

Add files to version control<br>
`git add <filename(s)>`

Revert unwanted staged (added) files to unstaged<br>
`git restore <filename(s)>`
<br>or (for older versions of git)<br>
`git rm [-r] --cached <filename(s)>`
<br>or (this does not work on my system?)<br>
`git reset HEAD <filename(s)>`

Commit files<br>
`git commit -m "<details>"`

View the commit history<br>
`git log`

Revert any changes since the last commit (if not already staged)<br>
`git checkout -- <filename(s)>`

Delete a git repository<br>
`rm -rf .git`

Clone/check out a git repository<br>
`git clone <repository-location> <new-name>`

Upload a local repository to GitHub<br>
`git remote add origin https://github.com/<username>/<projectname>.git`
<br>
`git push [-u] origin main`

Show status for tracked files only<br>
`git status -uno`

Compare a file across different branches<br>
`git diff <branch1> <branch2> -- <filename>`

List branches<br>
`git branch`

Merge `branch2` into `branch1`<br>
`git checkout branch1` (if necessary)<br>
`git merge branch2`

Delete local branch<br>
`git branch -d <branch-name>`

Delete remote branch<br>
`git push origin --delete <branch-name>`

Create a pull request from a development branch (or fork)<br>
1. Create new branch (or fork) in GitHub
2. `git pull` to local directory
3. `git checkout <new branch>`
4. Make changes
5. `git add <changed files>`
6. `git commit -m <description>`
7. `git push`
8. Create pull request in GitHub

[Rename a branch](https://github.com/github/renaming)

Git branching and rebasing<br>
https://git-scm.com/book/en/v2/Git-Branching-Rebasing
<br>
https://medium.com/@gabriellamedas/git-rebase-and-git-rebase-onto-a6a3f83f9cce

Turning off continuous integration steps<br>
> Btw, there is a way to tell the CI not to run, which would be appropriate for these changes, by including some magic text in the commit message. I don't remember exactly what it is... instructions are probably [on GitHub somewhere](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs).

Reset GitHub credentials<br>
`git credential-osxkeychain erase`<br>
Enter
```
host=github.com
protocol=https
```
Then return.

<hr>

<!-- ------------------------------ Homebrew ------------------------------ -->

#### Homebrew

Check the overall state<br>
`brew doctor`

Install a package<br>
`brew install <package>`

Check for updated packages<br>
`brew update`

Upgrade a package<br>
`brew upgrade <package>`

Delete old package versions<br>
`brew cleanup`

Check package dependencies<br>
`brew deps <package>`

Check reverse package dependencies<br>
`brew uses --installed <package>`

Uninstall a package<br>
`brew uninstall <package>`

Remove obsolete package dependencies<br>
`brew autoremove`

Pin a package that you do not want upgraded<br>
`brew pin <package>`

Unpin a package to allow upgrades<br>
`brew unpin <package>`

<hr>

<!-- ------------------------------ Java ------------------------------ -->

#### Java

View the contents of a Java .jar archive<br>
`jar tf <jar-file>`

Make symbolic link to Java runtime from Homebrew (current version is 21)<br>
`sudo ln -sfn /opt/homebrew/opt/openjdk@<version>/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-<version>.jdk`

<hr>

<!-- ------------------------------ JavaScript ------------------------------ -->

#### JavaScript

Open a URL in a new window<br>
`window.open(<url>, "_blank");`

Use jQuery to change display colors<br>
`jQuery(document.body).css({'color': 'yellow', 'background-color': 'darkblue'});`

<hr>

<!-- ------------------------------ Libraries ------------------------------ -->

#### Libraries

Display shared libraries in an object file<br>
`otool -L <object-file>`

List symbols in a library<br>
`nm -g <library>`

Edit paths in shared libraries (and/or change all paths in related shared libraries?)<br>
`install_name_tool -change <old-dylib-path> <new-dylib-path> <object-file>`

Convert a static library to a dynamic library<br>
`libtool -dynamic -o <libwhatever.dylib> -lSystem - <libwhatever.a>`

Convert a dynamic library to a static library (not verified)<br>
`libtool -static -o <libwhatever.a> - <libwhatever.dylib>`

<hr>

<!-- ------------------------------ Macintosh configuration issues ------------------------------ -->

#### Macintosh configuration issues

To eliminate the "You don't have permission to write to the folder ..." problem (do these really work?)<br>
`xattr -r -d com.apple.quarantine ./*`<br>
`defaults write com.apple.TextEdit ApplePersistence -bool no`

To make Apple e-mail (eml) files searchable [(instructions)](https://ars-codia.raphaelbauer.com/2010/12/index-eml-files-using-spotlight-in-mac.html)<br>
1. Open Terminal application (in folder /Applications/Utilities )<br>
2. Go to library directory using the following command in Terminal<br>
`cd /System/Library/Spotlight/RichText.mdimporter/Contents`
3. Make a backup: (just in case something goes wrong)<br>
`sudo cp Info.plist Info.plist.backup`
4. Open file Info.plist using command<br>
`sudo pico Info.plist`
5. Add <string>com.apple.mail.email</string> to the file
(see full snipplet at the end of this post)

Disable "versions" in TextEdit [(link)](https://discussions.apple.com/thread/4166543)<br>
`defaults write -app textedit ApplePersistence -bool no`<br>
`defaults write -app textedit AutosavingDelay -int 0`

Remove old versions<br>
`sudo rm -rf /.DocumentRevisions-V100`

Install Xcode command-line tools<br>
`xcode-select --install`

Determine working version of Xcode<br>
`xcode-select -p`

Change working version of Xcode<br>
`sudo xcode-select -switch /Applications/Xcode[-8.3.3].app`

List Macintosh file attributes<br>
`xattr <filename>`

Remove Macintosh file attributes<br>
`xattr -d <attribute> <filename>`

Rebuild the Spotlight index (may take a long time)<br>
```
sudo mdutil -Ea
sudo mdutil -i off
sudo mdutil -i on
```

Confirm that Spotlight indexing is enabled<br>
`mdutil -as`

<hr>

<!-- ------------------------------ NVIDIA ------------------------------ -->

#### NVIDIA

Test for NVIDIA graphics processor<br>
`$ lspci | grep -i nvidia`

Test persistence daemon<br>
`systemctl status nvidia-persistenced`

Test and verify compiler<br>
`nvcc -V`

Test device properties (see also https://www.seimaxim.com/kb/gpu/nvidia-smi-cheat-sheet)<br>
`nvidia-smi`

Install and build CUDA sample code<br>
```
git clone https://github.com/NVIDIA/cuda-samples.git
cd cuda-samples
make
```

Run deviceQuery<br>
`./Samples/1_Utilities/deviceQuery/deviceQuery`

<hr>

<!-- ------------------------------ Octave ------------------------------ -->

#### Octave

Load a Matlab file<br>
`load <filename>.mat`

Write Matlab variables to CSV<br>
`csvwrite("x.csv", x)`
<br>Another way<br>
`dlmwrite("s.csv", cell2mat(s), '')`

List installed packages<br>
`pkg list`

<hr>

<!-- ------------------------------ OpenSSH ------------------------------ -->

#### OpenSSH

Connect to a host<br>
`ssh <username@hostname>`

Secure download<br>
`scp <username@hostname>:/<remote-path>/<filename> <local-path>/.`

Secure upload<br>
`scp <local-path>/<filename> <username@hostname>:/<remote-path>/.`

<hr>

<!-- ------------------------------ Python ------------------------------ -->

#### Python

Install required modules<br>
`pip[3] install -r requirements.txt`

<hr>

<!-- ------------------------------ Rust ------------------------------ -->

#### Rust

Install using rustup<br>
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

Updates<br>
`rustup update`

Uninstall<br>
`rustup self uninstall`

Create a binary (application) crate<br>
`cargo new <crate_name> [--bin]`

Create a library crate<br>
`cargo new <crate_name> --lib`

Erase the current project's target subdirectory<br>
`cargo clean`

<hr>

<!-- ------------------------------ screen ------------------------------ -->

#### screen

Create a screen session<br>
`screen -S <session_name>`

List sessions<br>
`screen -ls`

Reattach a session<br>
`screen -r <session_name_or_number>`

Reattach the last session<br>
`screen -x`

Create a new window<br>
`Ctrl-A c`

Split screen vertically<br>
`Ctrl-A S`

Switch to a window<br>
`Ctrl-A <number>`

List available windows<br>
`Ctrl-A "`

Switch between windows<br>
`Ctrl-A tab`

Put window in scrollable mode (using arrow keys)<br>
`Ctrl-A ESC`

Destroy the current view<br>
`Ctrl-A X`

Detach a session<br>
`Ctrl-A d`

<hr>

<!-- ------------------------------ SQL ------------------------------ -->

#### SQL

Launch SQLite<br>
`sqlite3`

Poor man's natural sort in SQL<br>
`SELECT name FROM table ORDER BY LENGTH(name), name;`

**MySQL**<br>
```
mysql <...>
  show databases;
  use <database>;
  show tables;
  \q
mysqldump <...>
```

**PostgreSQL**<br>
`psql`
<br>Help<br>
`\h`
<br>List databases<br>
`\l`
<br>List tables in current database<br>
`\dt`
<br>Quit<br>
`\q`

<hr>

<!-- ------------------------------ System commands ------------------------------ -->

#### System commands

List files in current directory (l for details, a to include hidden files, t to sort by date & time)<br>
`ls [-lat]`

Check operating system<br>
`cat /etc/os-release`
<br>or<br>
`hostnamectl`

Disk free space<br>
`df [-h]`

Set paths<br>
[Add to `/etc/paths`]

Set IP addresses of remote machines<br>
[Add to `/etc/hosts`]

Determine the current shell<br>
`echo $SHELL`

Determine the default path to a program that has more than one version<br>
`which <application>`

Find all PDF files in ~/reading larger than 10 Mb<br>
`find ~/reading -name "*.pdf" -size +10M -exec ls -lh {} \\; > ~/Desktop/large-pdfs.txt`

Download a file and preserve its timestamp (timestamp may disagree with file history?)<br>
`curl -OR <filename>`

Random number generation (https://www.openssl.org/docs/man3.0/man1/openssl-rand.html)<br>
`openssl rand [-base64 | -hex] <number-of-bytes>`

Determine the current working directory<br>
`pwd`

Find all files in the directory whose name matches the pattern<br>
`grep -rl [--exclude=<exclude_pattern>] <directory> -e <pattern>`

Start/restart/stop service<br>
`sudo systemctl [start|restart|stop] [httpd|shiny-server|...]`

Symbolic links: Show location of symbolic links<br>
`find <directory> -type l`

Symbolic links: Show location of original files<br>
`ls -lR <directory> | grep ^l`

Directory size<br>
`du -sh <directory>`

Check kernel version<br>
`uname -r`

Look up hostname or IP address<br>
`nslookup <hostname>`
`nslookup <ip_address>`

Check graphics card<br>
`lspci -vnn | grep VGA`

Find files owned by user<br>
`find <directory> -user <user>`

Search recent command history<br>
`history | grep <search_keyword>`

Set a file's timestamp to that of another file<br>
`touch -r <another-filename> <filename>`

#### Macintosh-specific

Remove all instances of .DS_Store<br>
`sudo find / -name ".DS_Store" -depth -exec rm {} \\;`

Erase free space [from Macintosh command line](https://osxdaily.com/2016/04/28/erase-free-space-mac-command-line/) [obsolete, replaced by Disk Utility?]<br>
`diskutil secureErase freespace <security-level> /Volumes/<drive>`

Flush DNS cache<br>
`sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder`

[More Macintosh commands](https://ss64.com/osx/)

[Macintosh keyboard shortcuts](https://support.apple.com/en-us/102650)

<hr>

<!-- ------------------------------ Tesseract ------------------------------ -->

#### Tesseract

Optical character recognition on an image file<br>
(N = 4 for single column, 6 for general text)<br>
`tesseract <image_filename> <output.txt> --psm <N>`

<hr>

<!-- ------------------------------ Text commands ------------------------------ -->

#### Text commands

Replace text pattern in a file<br>
`sed -i "s/<pattern>/<replacement>/g" <filename(s)>`
<br>or<br>
`perl -pi -e "s/<pattern>/<replacement>/g;" <filename(s)>`

Convert a text file from UTF-16 to UTF-8 (or UTF-16BE, UTF-16LE, etc)<br>
`iconv -f UTF-16 -t UTF-8 <UTF-16-filename> > <new-UTF-8-filename>`

Count lines of code<br>
`wc -l *.cpp *.h`
<br>or<br>
`sudo find . -name *.cpp *.h *.hpp -depth -exec wc -l {} \\;`

[Toggle vi syntax highlighting](https://www.cyberciti.biz/faq/turn-on-or-off-color-syntax-highlighting-in-vi-or-vim/)

<hr>

<!-- ------------------------------ Verifying signatures ------------------------------ -->

#### Verifying signatures

MD5 digest<br>
`md5 <filename>`

PGP signature<br>
`gpg --verify <signature-filename> <filename>`

SHA digest (replace n with 1, 256, etc)<br>
`shasum [-a <n>] <filename>`
<br>or<br>
`openssl sha<n> <filename>`

<hr>

<!-- --------------------------------------------------------------------------------- -->
