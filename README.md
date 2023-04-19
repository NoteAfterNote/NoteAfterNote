<h1 align="center">NoteAfterNote</h1>



##### [NoteAfterNote-1](#NoteAfterNote-1) • Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required • April 7, 2023

##### [NoteAfterNote-2](#NoteAfterNote-2) • Termux And The ext4 Filesystem, Part 2 Of 5: QEMU, A Guest Operating System, And darkhttpd • April 7, 2023 • See [NoteAfterNote-6](#NoteAfterNote-6)

##### [NoteAfterNote-3](#NoteAfterNote-3) • Termux And The ext4 Filesystem, Part 3 Of 5: QEMU, A Guest Operating System, LUKS Encryption, lighttpd, WebDAV • April 12, 2023 • See [NoteAfterNote-6](#NoteAfterNote-6)

##### [NoteAfterNote-4](#NoteAfterNote-4) • Termux And The ext4 Filesystem, Part 4 Of 5: QEMU, A Guest Operating System, GNU GRUB Bootloader, And fdisk • April 14, 2023 • See [NoteAfterNote-6](#NoteAfterNote-6)

##### [NoteAfterNote-5](#NoteAfterNote-5) • Termux And The ext4 Filesystem, Part 5 Of 5: Reading And Writing With debugfs, No Root Required • April 16, 2023

##### [NoteAfterNote-6](#NoteAfterNote-6) • Termux, QEMU, vsftpd • April 18, 2023 • See NoteAfterNote-2](#NoteAfterNote-2), [NoteAfterNote-3](#NoteAfterNote-3), [NoteAfterNote-4](#NoteAfterNote-4)
---


<a id="NoteAfterNote-1"></a><h3 align="center">NoteAfterNote-1<br>Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required<br>Published: April 7, 2023<br>Link: https://gist.github.com/NoteAfterNote/2558deec94bac7ec9fa58aa5ad5e9d1b</h3>

<p><br></p>

### Mobile Device Configuration
   - Rooted: No
   - Connected to any network: No
   - Operating system: 

         neofetch --stdout|grep --color=never --ignore-case 'os:'
            OS: Android 10 armv8l 
   - CPU:

         neofetch --stdout|grep --color=never --ignore-case 'cpu:'
            CPU: Qualcomm SDM439 (8) @ 2.016GHz 
   - Display resolution: 1520x720
   - Builtin internal storage: 16 Gigabytes
   - Builtin memory: 2 Gigabytes
   - Application Binary Interface (ABI): armeabi-v7a, 32-bit
   - Linux shell: bash (Bourne Again SHell)
   - Fresh installation: Termux application, MiXplorer, MiXplorer Archive, RCX - Rclone for Android
   - App for reading the ext4 filesystem contained in the image file: MiXplorer and the MiX Archive component/addon, access to the ext4 filesystem is provided by the MiX Archive component/addon, the ext4 filesystem is always read-only, the image filename must end in ".ext" and always initialize the image file with zeroes (zero-filled, 0-filled)
 - App for creating the image file and writing the ext4 filesystem: Termux application, always enable wake-lock when running Termux, always run "termux-setup-storage" after installing Termux, use the Linux command "dd if=/dev/zero of=image-file.ext" to create the image file, use the Linux command "mkfs.ext4 -d EXT4-DIRECTORY" to write the contents of EXT4-DIRECTORY to the image file
 - MiXplorer "Tool bar" configuration: Enable "Servers" button
 - MiXplorer "HTTP/WebDav" server configuration: Remove "Admin" password, from the authentication method list ("NONE", "BASIC", "DIGEST") select "NONE"
  - RCX - Rclone for Android configuration: In "Settings" "File Access" select "Enable Content Provider Preview", select "Declare as local provider". select "Grant MANAGE_EXTERNAL_STORAGE" if available

<p><br></p>

Termux application (termux, com.termux): https://termux.com (https://termux.dev), https://github.com/termux/termux-app ([@termux](https://github.com/termux)), https://wiki.termux.com
 - Read https://wiki.termux.com/wiki/Termux-wake-lock 
 - Read https://wiki.termux.com/wiki/Termux-setup-storage
 - Read https://wiki.termux.com/wiki/Touch_Keyboard
 - Read https://wiki.termux.com/wiki/User_Interface ("create new terminal sessions", "specify a session title", "Resetting the terminal"), see https://user-images.githubusercontent.com/21236430/126444437-7570cdcb-e825-4970-97ff-71f41e426b0f.jpg in https://github.com/termux/termux-app/issues/2184#issuecomment-883939230 ("Feature request: termux transcript #2184" "Gameye98 commented on Jul 21, 2021" )
 - Read https://wiki.termux.com/wiki/Terminal_Settings
 - Termux packages installed: manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate 

<p><br></p>

MiXplorer (Hootan Parsa, com.mixplorer): https://mixplorer.com (read), https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ (read "Downloads"), https://forum.xda-developers.com/t/mixplorer-q-a-and-faq-user-manual.3308582/ ("MiXplorer: Q&A and FAQ (User Manual)")
 - Read "iv. FTP, HTTP, TCP SERVERS": https://forum.xda-developers.com/t/mixplorer-q-a-and-faq-user-manual.3308582/
 - Read "ii. UI, NAVIGATION, VIEW CONFIGURATION, BOOKMARKS, TABS": https://forum.xda-developers.com/t/mixplorer-q-a-and-faq-user-manual.3308582/
 - Enable "Servers" button: Select "Settings" then "Buttons" then "Tool bar" then "Servers"
 - Image of MiXplorer "Tool bar" without "Servers" button: https://forum.xda-developers.com/attachments/3-jpg.3783167/ from "Screenshots" in  https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/
 - Image of MiXplorer "Tool bar" with "Servers" button: https://raw.githubusercontent.com/YandLiu/MiXPlorerSkins/master/Screenshots/Night%20Mode.png from "Night Mode (Click to view Skin Code)" in https://github.com/YandLiu/MiXPlorerSkins ([@YandLiu](https://github.com/YandLiu))
 - Read "You can enable it from the Settings > Buttons > Tool bar" in https://forum.xda-developers.com/t/mixplorer-q-a-and-faq-user-manual.3308582/page-24#post-75842583 ("HootanParsa" "Recognized Developer" "Mar 10, 2018" "#479")


MiX Archive (Hootan Parsa, com.mixplorer.addon.archive) is required: https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
 - "7zip, ZSTD, 7-Zip-JBinding" in "Open source libraries from other contributors": https://mixplorer.com/links/
 - "Filename Extensions" in "Supported formats": https://github.com/borisbrodski/sevenzipjbinding/blob/44c13f3d5fe6245d52bffe743c834f7108c6e4e6/p7zip/DOC/MANUAL/general/formats.htm (ext, ext4)
 - "Supported formats": https://sevenzip.osdn.jp/chm/general/formats.htm (ext, ext4)
 - 7-Zip: https://7-zip.org

<p><br></p>

RCX - Rclone for Android (x0b, io.github.x0b.rcx): https://github.com/x0b/rcx ([@x0b](https://github.com/x0b)), https://x0b.github.io , https://play.google.com/store/apps/details?id=io.github.x0b.rcx  
 - Read "Configuring remotes", "Serving content", "Local Storage": https://x0b.github.io/docs/
 - "Streaming (Stream media files, serve files and directories over FTP, HTTP, WebDAV or DLNA)" and "Storage Access Framework (SAF) (see docs) for SD card and USB device access.": https://github.com/x0b/rcx

<p><br></p>

<a id="example-1"></a>
### [Example 1](#termux-session-for-example-1)

````
#
# Open a new Termux session: termux-setup-storage, add the Termux packages
# Termux session name: Example 1
#
# 50gb.ext on external storage: 50 gigabytes (53687091200 bytes,
# 1 gigabyte = 1024*1024*1024 = 1073741824 bytes) file with an
# ext4 filesystem containing the Termux "arm" repositories for
# termux-main, termux-root, termux-x11
#
# MiXplorer: Open "50gb.ext", start "HTTP/WebDav Server" using
# the "Servers" button on the "Tool bar" (no password for the
# "Admin" account and the server authentication method is
# "NONE"), use http://127.0.0.1:8181 to access the MiXplorer
# "HTTP/WebDav Server" server, start the MiXplorer
# "FTP(S,ES)/Share Server" from the "Tool bar" (no password for
# the "Admin" account) use 127.0.0.1 as the FTP address and 2121
# as the FTP port number
#
# RCX: Create an "FTP" remote, use 127.0.0.1 for the "FTP Host",
# use Admin as the user name and make up a password, use 2121 as
# the "FTP Port", read "Serving content" and "Local Storage" in
# https://x0b.github.io/docs/
#
# Backup $PREFIX/etc/apt/sources.list and use the Linux text
# editor "nano" to update $PREFIX/etc/apt/sources.list with this
# configuration (from https://packages.termux.dev):
#    deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-main/ stable main
#    deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-root/ root stable
#    deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-x11/ x11 main
# 
pwd
echo $PS1
export PS1='\T $ '    # bash prompt string
echo $PS1
termux-setup-storage
echo $HOME
echo $PREFIX
ls --color=never -l -all $HOME    # "ls --help"
ls --color=never -l -all
ls --color=never -l -a
ls --color=never -la
pwd    # "pwd --help"
mkdir --verbose BACKUP    # "mkdir --help"
ls --color=never -la $PREFIX/etc/apt
cd $PREFIX/etc/apt
pwd
cp --verbose -pi sources.list $HOME/BACKUP    # "cp --help"
ls --color=never -la $HOME/BACKUP
cat sources.list    # "cat --help"
#
# Edit sources.list with the Linux text editor "nano"
#
nano --linenumbers sources.list    # "nano --help"
cd $HOME 
pwd
cat $PREFIX/etc/apt/sources.list
#
apt update
apt upgrade
#
apt update
apt install manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate

updatedb    # "man locate" and "man updatedb"

#
# Termux is ready for "Example 2"
#
````

<p><br></p>

<a id="example-2"></a>
### [Example 2](#termux-session-for-example-2)

````
#
# Open a new Termux session
# Termux session name: Example 2
#
# test-disk1-30mb.ext: test-disk1-30mb.ext is a
# 31457280-byte (30 megabytes, 1 megabyte = 1024*1024 bytes =
# 1048576 bytes) image file 
# 
echo $PS1
export PS1='\T $ '
echo $PS1
echo $HOME
echo $PREFIX
pwd
ls --color=never -l $HOME/storage|grep -iv external
ls --color=never -l storage/downloads
mktemp -d /storage/emulated/0/Download/ext4-test-directory.XXXXXXXXXX    # "man mktemp"
tree DIRECTORY_NAME_FROM_mktemp
ls --color=never -alR DIRECTORY_NAME_FROM_mktemp
cd DIRECTORY_NAME_FROM_mktemp    # "cd --help"
pwd
mkdir -v test-disk1-directory
cd test-disk1-directory
pwd
touch file1
ls --color=never -l file1.txt
mv file1 file1.txt
ls --color=never -l file1.txt
touch file2r.txt
rm -iv file2r.txt
touch file2.txt
cd ..
pwd
dd if=/dev/zero of=test-disk1-30mb.ext bs=1M count=30   # Always initialize the image file with zeroes (zero-filled, 0-filled)
ls --color=never  -l test-disk1-30mb.ext
tree test-disk1-directory
ls --color=never -la
ls --color=never -la test-disk1-directory
mkfs.ext4 -m 0 -L ext4-disk1-30mb -d test-disk1-directory test-disk1-30mb.ext # "man mkfs.ext4": "-d root-directory" "Copy the contents of the given directory into the root directory of the file system."
pwd
#
# MiXplorer: Stop "HTTP/WebDav Server" and 
# "FTP(S,ES)/Share Server", open test-disk1-30mb.ext and
# start "HTTP/WebDav Server" and "FTP(S,ES)/Share Server"
# from the "Tool bar"
#
cadaver http://127.0.0.1:8181
ls --color=never -la
mkdir -v test-disk1-directory/last-example
tree test-disk1-directory
ls --color=never -al test-disk1-directory
touch test-disk1-directory/last-example/file3.html
tree test-disk1-directory
ls --color=never -la test-disk1-directory
ls --color=never -alR test-disk1-directory
#
# Using the Linux text editor "nano" insert into file3.html
#    <html>
#    <body>
#    <h1>
#    file4.html
#    </h1>
#    </body>
#    </html>
nano --linenumbers test-disk1-directory/last-example/file4.html
pwd
stat test-disk1-directory/last-example/file4.html
file test-disk1-directory/last-example/file4.html
cat test-disk1-directory/last-example/file4.html
tree test-disk1-directory
ls --color=never -alR test-disk1-directory
cd test-disk1-directory
mv -iv file1.txt last-example
cp -iv file2.txt last-example
tree last-example
rm -iv file2.txt
pwd
ls --color=never -al
cd ..
pwd
ls --color=never -al
mkfs.ext4 -m 0 -L ext4-disk1-30mb -d test-disk1-directory test-disk1-30mb.ext
#
# MiXplorer: Stop "HTTP/WebDav Server" and
# "FTP(S,ES)/Share Server", try reloading ext4-disk1-30mb.ext
# and then start "HTTP/WebDav Server" and
# "FTP(S,ES)/Share Server" from the "Tool bar"; instead of
# reloading the file stop "HTTP/WebDav Server" and
# "FTP(S,ES)/Share Server" and exit MiXplorer, restart
# MiXplorer and "HTTP/WebDav Server" and
# "FTP(S,ES)/Share Server"
#
cadaver http://127.0.0.1:8181
pwd
tree
ls --color=never -alR
sha256sum file4.html
sha256sum test-disk1-directory/last-example/file4.html
cmp --verbose file4.html test-disk1-directory/last-example/file4.html
links -dump http://127.0.0.1:8181/last-example/file4.html
links -source http://127.0.0.1:8181/last-example/file4.html
cd DIRECTORY_NAME_FROM_mktemp
rm -iv --recursive test-disk1-directory    # "man rm"
pwd
cd
pwd
rm -ivr DIRECTORY_NAME_FROM_mktemp
#
# Close Termux session "Example Number2"
#
exit

#
# Switch to and close Termux session "Example Number 1"
#
exit

# Exit MiXplorer and RCX
````

<p><br></p>

<a id="termux-session-for-example-1"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#example-1">Example 1</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ echo $PS1<br>\[\e[0;32m\]\w\[\e[0m\] \[\e[0;97m\]\$\[\e[0m\]<br>~ $<br>~ $ export PS1='\T $ '    # bash prompt string<br>04:31:47 $<br>04:31:48 $ echo $PS1<br>\T $<br>04:32:07 $<br>04:32:10 $ termux-setup-storage<br>04:32:23 $ echo $HOME<br>/data/data/com.termux/files/home<br>04:32:48 $ echo $PREFIX<br>/data/data/com.termux/files/usr<br>04:33:11 $<br>04:33:26 $ ls --color=never -l -all $HOME    # "ls --help"<br>total 18<br>drwx------ 4 u0_a188 u0_a188 3488 Apr  3 16:32 .<br>drwxrwx--x 4 u0_a188 u0_a188 3488 Apr  3 16:28 ..<br>-rw------- 1 u0_a188 u0_a188    5 Apr  3 16:29 .bash_history<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 .termux<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:32 storage<br>04:33:29 $<br>04:33:30 $ ls --color=never -l -all<br>total 18<br>drwx------ 4 u0_a188 u0_a188 3488 Apr  3 16:32 .<br>drwxrwx--x 4 u0_a188 u0_a188 3488 Apr  3 16:28 ..<br>-rw------- 1 u0_a188 u0_a188    5 Apr  3 16:29 .bash_history<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 .termux<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:32 storage<br>04:34:17 $<br>04:34:18 $ ls --color=never -l -a<br>total 18<br>drwx------ 4 u0_a188 u0_a188 3488 Apr  3 16:32 .<br>drwxrwx--x 4 u0_a188 u0_a188 3488 Apr  3 16:28 ..<br>-rw------- 1 u0_a188 u0_a188    5 Apr  3 16:29 .bash_history<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 .termux<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:32 storage<br>04:34:35 $<br>04:34:36 $ ls --color=never -la<br>total 18<br>drwx------ 4 u0_a188 u0_a188 3488 Apr  3 16:32 .<br>drwxrwx--x 4 u0_a188 u0_a188 3488 Apr  3 16:28 ..<br>-rw------- 1 u0_a188 u0_a188    5 Apr  3 16:29 .bash_history<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 .termux<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:32 storage<br>04:34:52 $<br>04:34:52 $ pwd    # "pwd --help"<br>/data/data/com.termux/files/home<br>04:35:08 $<br>04:35:09 $ ls --color=never -la $PREFIX/etc/apt<br>total 26<br>drwx------ 5 u0_a188 u0_a188 3488 Apr  3 16:28 .<br>drwx------ 7 u0_a188 u0_a188 3488 Apr  3 16:28 ..<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 apt.conf.d<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 preferences.d<br>-rw------- 1 u0_a188 u0_a188   91 Apr  3 16:28 sources.list<br>-rw------- 1 u0_a188 u0_a188 1198 Apr  3 16:28 trusted.gpg<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:28 trusted.gpg.d<br>04:35:27 $<br>04:35:28 $ cd $PREFIX/etc/apt<br>04:35:52 $<br>04:35:55 $ pwd<br>/data/data/com.termux/files/usr/etc/apt<br>04:36:05 $<br>04:36:07 $ cp --verbose -pi sources.list $HOME/BACKUP    # "cp --help"'sources.list' -> '/data/data/com.termux/files/home/BACKUP'<br>04:36:25 $<br>04:36:26 $ ls --color=never -la $HOME/BACKUP<br>-rw------- 1 u0_a188 u0_a188 91 Apr  3 16:28 /data/data/com.termux/files/home/BACKUP<br>04:36:41 $<br>04:36:42 $ cat sources.list    # "cat --help"<br># The main termux repository:<br>deb https://packages.termux.org/apt/termux-main/ stable main<br>04:37:17 $<br>04:37:17 $ nano --linenumbers sources.list    # "nano --help"<br>04:38:53 $<br>04:39:13 $ cd $HOME<br>04:39:16 $<br>04:39:17 $ pwd<br>/data/data/com.termux/files/home<br>04:39:28 $<br>04:39:28 $ cat $PREFIX/etc/apt/sources.list<br># The main termux repository:<br>#deb https://packages.termux.org/apt/termux-main/ stable main<br>deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-main/ stable main<br>deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-root/ root stable<br>deb http://127.0.0.1:8181/packages.termux.dev/apt/termux-x11/ x11 main<br>04:39:41 $<br>04:39:42 $ apt update<br>Get:1 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable InRelease [14.0 kB]<br>Get:2 http://127.0.0.1:8181/packages.termux.dev/apt/termux-root root InRelease [14.2 kB]<br>Get:3 http://127.0.0.1:8181/packages.termux.dev/apt/termux-x11 x11 InRelease [14.0 kB]<br>Get:4 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm Packages [489 kB]<br>Get:5 http://127.0.0.1:8181/packages.termux.dev/apt/termux-root root/stable arm Packages [17.8 kB]<br>Get:6 http://127.0.0.1:8181/packages.termux.dev/apt/termux-x11 x11/main arm Packages [123 kB]<br>Fetched 673 kB in 20s (34.2 kB/s)<br>Reading package lists... Done<br>Building dependency tree... Done<br>61 packages can be upgraded. Run 'apt list --upgradable' to see them.<br>04:40:41 $<br>04:40:44 $<br>04:40:44 $ apt upgrade<br>Reading package lists... Done<br>Building dependency tree... Done<br>Calculating upgrade... Done<br>The following NEW packages will be installed:<br>  bash-completion libmd libsmartcols resolv-conf zstd<br>The following packages will be upgraded:<br>  apt bash ca-certificates command-not-found coreutils curl dash<br>  debianutils dialog diffutils dos2unix dpkg ed findutils gawk gpgv<br>  grep gzip inetutils less libandroid-support libc++ libcap-ng<br>  libcrypt libcurl libevent libexpat libgcrypt libgmp libgnutls<br>  libgpg-error libiconv libidn2 liblz4 liblzma libmpfr libnettle<br>  libnghttp2 libssh2 libtirpc libunistring lsof nano ncurses openssl<br>  pcre2 procps psmisc readline sed tar termux-am-socket termux-exec<br>  termux-keyring termux-licenses termux-tools unbound unzip<br>  util-linux xz-utils zlib<br>61 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.<br>Need to get 16.9 MB of archives.<br>After this operation, 7487 kB of additional disk space will be used.<br>Do you want to continue? [Y/n] y<br>Get:1 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm liblzma arm 5.4.2 [241 kB]<br>Get:2 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm xz-utils arm 5.4.2 [62.5 kB]<br>Get:3 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm zlib arm 1.2.13 [61.2 kB]<br>Get:3 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm zlib arm 1.2.13 [61.2 kB]<br>Get:5 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm zstd arm 1.5.4 [284 kB]<br>Get:6 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libiconv arm 1.17 [550 kB]<br>Get:7 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libandroid-support arm 28-3 [10.2 kB]<br>Get:8 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libc++ arm 25c [185 kB]<br>Get:9 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libgmp arm 6.2.1-2 [295 kB]<br>Get:10 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm coreutils arm 9.1-2 [731 kB]<br>Get:11 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libmd arm 1.0.4 [36.6 kB]<br>Get:12 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm diffutils arm 3.9 [146 kB]<br>Get:13 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm ncurses arm 6.4-1 [503 kB]<br>Get:14 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm pcre2 arm 10.42 [848 kB]<br>Get:15 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm less arm 608-1 [93.3 kB]<br>Get:16 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm tar arm 1.34-2 [326 kB]<br>Get:17 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm dpkg arm 1.21.21 [265 kB]<br>Get:18 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm findutils arm 4.9.0-2 [229 kB]<br>Get:19 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libgpg-error arm 1.46 [100 kB]<br>Get:20 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libgcrypt arm 1.10.1-1 [421 kB]<br>Get:21 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm gpgv arm 2.4.0-2 [164 kB]<br>Get:22 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm grep arm 3.9 [116 kB]<br>Get:23 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm ca-certificates all 1:2023.01.10 [119 kB]<br>Get:24 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm openssl arm 1:3.1.0 [1507 kB]<br>Get:25 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libcurl arm 7.88.1 [965 kB]<br>Get:26 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm curl arm 7.88.1 [186 kB]<br>Get:27 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libnghttp2 arm 1.52.0 [89.9 kB]<br>Get:28 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libssh2 arm 1.10.0-2 [176 kB]<br>Get:29 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libnettle arm 3.8.1 [387 kB]<br>Get:30 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libunistring arm 1.1 [517 kB]<br>Get:31 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libidn2 arm 2.3.4 [100 kB]<br>Get:32 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm resolv-conf arm 1.3 [976 B]<br>Get:33 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libevent arm 2.1.12-2 [190 kB]<br>Get:34 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libexpat arm 2.5.0 [76.3 kB]<br>Get:35 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm unbound arm 1.17.1 [565 kB]<br>Get:36 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libgnutls arm 3.8.0 [676 kB]<br>Get:37 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm liblz4 arm 1.9.4 [87.9 kB]<br>Get:38 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm sed arm 4.9 [111 kB]<br>Get:39 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm termux-am-socket arm 1.5.0 [10.4 kB]<br>Get:40 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm dash arm 0.5.12 [61.5 kB]<br>Get:41 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libmpfr arm 4.2.0 [263 kB]<br>Get:42 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm readline arm 8.2.1 [224 kB]<br>Get:43 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm gawk arm 5.2.1 [725 kB]<br>Get:44 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm procps arm 3.3.17-2 [131 kB]<br>Get:45 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm psmisc arm 23.6-1 [38.5 kB]<br>Get:46 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm termux-exec arm 1:1.0 [3352 B]<br>Get:47 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libsmartcols arm 2.38.1-1 [69.8 kB]<br>Get:48 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm util-linux arm 2.38.1-1 [551 kB]<br>Get:49 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libcap-ng arm 2:0.8.3 [33.9 kB]<br>Get:50 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm dialog arm 1.3-20230209-0 [92.4 kB]<br>Get:51 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm termux-tools all 1.37.0 [28.3 kB]<br>Get:52 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm termux-keyring all 3.11 [37.2 kB]<br>Get:53 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm termux-licenses all 2.0-3 [52.2 kB]<br>Get:54 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm apt arm 2.6.0 [935 kB]<br>Get:55 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm bash arm 5.2.15 [858 kB]<br>Get:56 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libcrypt arm 0.2-5 [8344 B]<br>Get:57 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm bash-completion all 2.11-2 [156 kB]<br>Get:58 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm command-not-found arm 2.1.0-15 [242 kB]<br>Get:59 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm debianutils arm 5.7 [18.3 kB]<br>Get:60 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm dos2unix arm 7.4.4 [60.1 kB]<br>Get:61 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm ed arm 1.19 [37.6 kB]<br>Get:62 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm inetutils arm 2.4 [226 kB]<br>Get:63 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libtirpc arm 1.3.3 [117 kB]<br>Get:64 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm lsof arm 4.98.0 [107 kB]<br>Get:65 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm nano arm 7.2 [209 kB]<br>Get:66 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm unzip arm 6.0-9 [114 kB]<br>Fetched 16.9 MB in 42s (401 kB/s)<br>(Reading database ... 4112 files and directories currently installed.)<br>Preparing to unpack .../archives/liblzma_5.4.2_arm.deb ...<br>Unpacking liblzma (5.4.2) over (5.2.5-1) ...<br>Setting up liblzma (5.4.2) ...<br>(Reading database ... 4183 files and directories currently installed.)<br>Preparing to unpack .../xz-utils_5.4.2_arm.deb ...<br>Unpacking xz-utils (5.4.2) over (5.2.5-1) ...<br>Setting up xz-utils (5.4.2) ...<br>(Reading database ... 4183 files and directories currently installed.)<br>Preparing to unpack .../archives/zlib_1.2.13_arm.deb ...<br>Unpacking zlib (1.2.13) over (1.2.11-5) ...<br>Setting up zlib (1.2.13) ...<br>Selecting previously unselected package zstd.<br>(Reading database ... 4183 files and directories currently installed.)<br>Preparing to unpack .../archives/zstd_1.5.4_arm.deb ...<br>Unpacking zstd (1.5.4) ...<br>Setting up zstd (1.5.4) ...<br>(Reading database ... 4203 files and directories currently installed.)<br>Preparing to unpack .../archives/libiconv_1.17_arm.deb ...<br>Unpacking libiconv (1.17) over (1.16-3) ...<br>Setting up libiconv (1.17) ...<br>(Reading database ... 4204 files and directories currently installed.)<br>Preparing to unpack .../libandroid-support_28-3_arm.deb ...<br>Unpacking libandroid-support (28-3) over (28-2) ...<br>Setting up libandroid-support (28-3) ...<br>(Reading database ... 4204 files and directories currently installed.)<br>Preparing to unpack .../archives/libc++_25c_arm.deb ...<br>Unpacking libc++ (25c) over (23b-3) ...<br>Setting up libc++ (25c) ...<br>(Reading database ... 4204 files and directories currently installed.)<br>Preparing to unpack .../libgmp_6.2.1-2_arm.deb ...<br>Unpacking libgmp (6.2.1-2) over (6.2.1) ...<br>Setting up libgmp (6.2.1-2) ...<br>(Reading database ... 4204 files and directories currently installed.)<br>Preparing to unpack .../coreutils_9.1-2_arm.deb ...<br>Unpacking coreutils (9.1-2) over (9.0) ...<br>Setting up coreutils (9.1-2) ...<br>Selecting previously unselected package libmd.<br>(Reading database ... 4204 files and directories currently installed.)<br>Preparing to unpack .../archives/libmd_1.0.4_arm.deb ...<br>Unpacking libmd (1.0.4) ...<br>Setting up libmd (1.0.4) ...<br>(Reading database ... 4295 files and directories currently installed.)<br>Preparing to unpack .../archives/diffutils_3.9_arm.deb ...<br>Unpacking diffutils (3.9) over (3.8) ...<br>Setting up diffutils (3.9) ...<br>(Reading database ... 4295 files and directories currently installed.)<br>Preparing to unpack .../archives/gzip_1.12-1_arm.deb ...<br>Unpacking gzip (1.12-1) over (1.11-3) ...<br>Setting up gzip (1.12-1) ...<br>(Reading database ... 4293 files and directories currently installed.)<br>Preparing to unpack .../archives/ncurses_6.4-1_arm.deb ...<br>Unpacking ncurses (6.4-1) over (6.2.20200725-6) ...<br>Setting up ncurses (6.4-1) ...<br>(Reading database ... 4294 files and directories currently installed.)<br>Preparing to unpack .../archives/pcre2_10.42_arm.deb ...<br>Unpacking pcre2 (10.42) over (10.39-2) ...<br>Setting up pcre2 (10.42) ...<br>(Reading database ... 4296 files and directories currently installed.)<br>Preparing to unpack .../archives/less_608-1_arm.deb ...<br>Unpacking less (608-1) over (590) ...<br>Setting up less (608-1) ...<br>(Reading database ... 4296 files and directories currently installed.)<br>Preparing to unpack .../archives/tar_1.34-2_arm.deb ...<br>Unpacking tar (1.34-2) over (1.34) ...<br>Setting up tar (1.34-2) ...<br>(Reading database ... 4296 files and directories currently installed.)<br>Preparing to unpack .../archives/dpkg_1.21.21_arm.deb ...<br>Unpacking dpkg (1.21.21) over (1.21.1) ...<br>Setting up dpkg (1.21.21) ...<br>(Reading database ... 4297 files and directories currently installed.)<br>Preparing to unpack .../findutils_4.9.0-2_arm.deb ...<br>Unpacking findutils (4.9.0-2) over (4.8.0) ...<br>Setting up findutils (4.9.0-2) ...<br>(Reading database ... 4297 files and directories currently installed.)<br>Preparing to unpack .../libgpg-error_1.46_arm.deb ...<br>Unpacking libgpg-error (1.46) over (1.43) ...<br>Setting up libgpg-error (1.46) ...<br>(Reading database ... 4297 files and directories currently installed.)<br>Preparing to unpack .../libgcrypt_1.10.1-1_arm.deb ...<br>Unpacking libgcrypt (1.10.1-1) over (1.9.4) ...<br>Setting up libgcrypt (1.10.1-1) ...<br>(Reading database ... 4299 files and directories currently installed.)<br>Preparing to unpack .../archives/gpgv_2.4.0-2_arm.deb ...<br>Unpacking gpgv (2.4.0-2) over (2.3.4) ...<br>Setting up gpgv (2.4.0-2) ...<br>(Reading database ... 4299 files and directories currently installed.)<br>Preparing to unpack .../apt/archives/grep_3.9_arm.deb ...<br>Unpacking grep (3.9) over (3.7-2) ...<br>Setting up grep (3.9) ...<br>(Reading database ... 4297 files and directories currently installed.)<br>Preparing to unpack .../ca-certificates_1%3a2023.01.10_all.deb ...<br>Unpacking ca-certificates (1:2023.01.10) over (1:2021-10-26-0) ...<br>Setting up ca-certificates (1:2023.01.10) ...<br>(Reading database ... 4292 files and directories currently installed.)<br>Preparing to unpack .../openssl_1%3a3.1.0_arm.deb ...<br>Unpacking openssl (1:3.1.0) over (1.1.1l) ...<br>Setting up openssl (1:3.1.0) ...<br><br>Configuration file '/data/data/com.termux/files/usr/etc/tls/openssl.cnf'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** openssl.cnf (Y/I/N/O/D/Z) [default=N] ?<br>(Reading database ... 4326 files and directories currently installed.)<br>Preparing to unpack .../libcurl_7.88.1_arm.deb ...<br>Unpacking libcurl (7.88.1) over (7.81.0) ...<br>Setting up libcurl (7.88.1) ...<br>(Reading database ... 4339 files and directories currently installed.)<br>Preparing to unpack .../archives/curl_7.88.1_arm.deb ...<br>Unpacking curl (7.88.1) over (7.81.0) ...<br>Setting up curl (7.88.1) ...<br>(Reading database ... 4339 files and directories currently installed.)<br>Preparing to unpack .../libnghttp2_1.52.0_arm.deb ...<br>Unpacking libnghttp2 (1.52.0) over (1.46.0) ...<br>Setting up libnghttp2 (1.52.0) ...<br>(Reading database ... 4339 files and directories currently installed.)<br>Preparing to unpack .../libssh2_1.10.0-2_arm.deb ...<br>Unpacking libssh2 (1.10.0-2) over (1.10.0) ...<br>Setting up libssh2 (1.10.0-2) ...<br>(Reading database ... 4339 files and directories currently installed.)<br>Preparing to unpack .../libnettle_3.8.1_arm.deb ...<br>Unpacking libnettle (3.8.1) over (3.7.3) ...<br>Setting up libnettle (3.8.1) ...<br>(Reading database ... 4342 files and directories currently installed.)<br>Preparing to unpack .../libunistring_1.1_arm.deb ...<br>Unpacking libunistring (1.1) over (0.9.10-5) ...<br>Setting up libunistring (1.1) ...<br>(Reading database ... 4344 files and directories currently installed.)<br>Preparing to unpack .../archives/libidn2_2.3.4_arm.deb ...<br>Unpacking libidn2 (2.3.4) over (2.3.2) ...<br>Setting up libidn2 (2.3.4) ...<br>Selecting previously unselected package resolv-conf.<br>(Reading database ... 4346 files and directories currently installed.)<br>Preparing to unpack .../resolv-conf_1.3_arm.deb ...<br>Unpacking resolv-conf (1.3) ...<br>Setting up resolv-conf (1.3) ...<br>(Reading database ... 4350 files and directories currently installed.)<br>Preparing to unpack .../libevent_2.1.12-2_arm.deb ...<br>Unpacking libevent (2.1.12-2) over (2.1.12) ...<br>Setting up libevent (2.1.12-2) ...<br>(Reading database ... 4350 files and directories currently installed.)<br>Preparing to unpack .../libexpat_2.5.0_arm.deb ...<br>Unpacking libexpat (2.5.0) over (2.4.2) ...<br>Setting up libexpat (2.5.0) ...<br>(Reading database ... 4350 files and directories currently installed.)<br>Preparing to unpack .../unbound_1.17.1_arm.deb ...<br>Unpacking unbound (1.17.1) over (1.13.2-1) ...<br>Setting up unbound (1.17.1) ...<br>(Reading database ... 4350 files and directories currently installed.)<br>Preparing to unpack .../libgnutls_3.8.0_arm.deb ...<br>Unpacking libgnutls (3.8.0) over (3.6.16-1) ...<br>Setting up libgnutls (3.8.0) ...<br>(Reading database ... 4351 files and directories currently installed.)<br>Preparing to unpack .../archives/liblz4_1.9.4_arm.deb ...<br>Unpacking liblz4 (1.9.4) over (1.9.3) ...<br>Setting up liblz4 (1.9.4) ...<br>(Reading database ... 4355 files and directories currently installed.)<br>Preparing to unpack .../apt/archives/sed_4.9_arm.deb ...<br>Unpacking sed (4.9) over (4.8-2) ...<br>Setting up sed (4.9) ...<br>(Reading database ... 4355 files and directories currently installed.)<br>Preparing to unpack .../termux-am-socket_1.5.0_arm.deb ...<br>Unpacking termux-am-socket (1.5.0) over (1.02) ...<br>Setting up termux-am-socket (1.5.0) ...<br>(Reading database ... 4356 files and directories currently installed.)<br>Preparing to unpack .../archives/dash_0.5.12_arm.deb ...<br>Unpacking dash (0.5.12) over (0.5.11.5) ...<br>Setting up dash (0.5.12) ...<br>(Reading database ... 4356 files and directories currently installed.)<br>Preparing to unpack .../archives/libmpfr_4.2.0_arm.deb ...<br>Unpacking libmpfr (4.2.0) over (4.1.0) ...<br>Setting up libmpfr (4.2.0) ...<br>(Reading database ... 4356 files and directories currently installed.)<br>Preparing to unpack .../readline_8.2.1_arm.deb ...<br>Unpacking readline (8.2.1) over (8.1.1) ...<br>Setting up readline (8.2.1) ...<br>(Reading database ... 4358 files and directories currently installed.)<br>Preparing to unpack .../archives/gawk_5.2.1_arm.deb ...<br>Unpacking gawk (5.2.1) over (5.1.1) ...<br>Setting up gawk (5.2.1) ...<br>(Reading database ... 4362 files and directories currently installed.)<br>Preparing to unpack .../procps_3.3.17-2_arm.deb ...<br>Unpacking procps (3.3.17-2) over (3.3.17-1) ...<br>Setting up procps (3.3.17-2) ...<br>(Reading database ... 4362 files and directories currently installed.)<br>Preparing to unpack .../archives/psmisc_23.6-1_arm.deb ...<br>Unpacking psmisc (23.6-1) over (23.4) ...<br>Setting up psmisc (23.6-1) ...<br>(Reading database ... 4362 files and directories currently installed.)<br>Preparing to unpack .../termux-exec_1%3a1.0_arm.deb ...<br>Unpacking termux-exec (1:1.0) over (1:0.9) ...<br>Setting up termux-exec (1:1.0) ...<br>(Reading database ... 4362 files and directories currently installed.)<br>Preparing to unpack .../util-linux_2.38.1-1_arm.deb ...<br>Unpacking util-linux (2.38.1-1) over (2.37.2-1) ...<br>Selecting previously unselected package libsmartcols.<br>Preparing to unpack .../libsmartcols_2.38.1-1_arm.deb ...<br>Unpacking libsmartcols (2.38.1-1) ...<br>Setting up libsmartcols (2.38.1-1) ...<br>(Reading database ... 4342 files and directories currently installed.)<br>Preparing to unpack .../libcap-ng_2%3a0.8.3_arm.deb ...<br>Unpacking libcap-ng (2:0.8.3) over (1:0.8.3-pre1-0) ...<br>Setting up libcap-ng (2:0.8.3) ...<br>(Reading database ... 4342 files and directories currently installed.)<br>Preparing to unpack .../dialog_1.3-20230209-0_arm.deb ...<br>Unpacking dialog (1.3-20230209-0) over (1.3-20211214-0) ...<br>Setting up dialog (1.3-20230209-0) ...<br>(Reading database ... 4342 files and directories currently installed.)<br>Preparing to unpack .../termux-tools_1.37.0_all.deb ...<br>Unpacking termux-tools (1.37.0) over (0.155) ...<br>Setting up util-linux (2.38.1-1) ...<br>Setting up termux-tools (1.37.0) ...<br><br>Configuration file '/data/data/com.termux/files/usr/etc/motd'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** motd (Y/I/N/O/D/Z) [default=N] ?<br><br>Configuration file '/data/data/com.termux/files/usr/etc/motd-playstore'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** motd-playstore (Y/I/N/O/D/Z) [default=N] ?<br><br>Configuration file '/data/data/com.termux/files/usr/etc/profile.d/init-termux-properties.sh'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** init-termux-properties.sh (Y/I/N/O/D/Z) [default=N] ?<br>(Reading database ... 4396 files and directories currently installed.)<br>Preparing to unpack .../termux-keyring_3.11_all.deb ...<br>Unpacking termux-keyring (3.11) over (2.4) ...<br>Setting up termux-keyring (3.11) ...<br>(Reading database ... 4418 files and directories currently installed.)<br>Preparing to unpack .../termux-licenses_2.0-3_all.deb ...<br>Unpacking termux-licenses (2.0-3) over (2.0-1) ...<br>Setting up termux-licenses (2.0-3) ...<br>(Reading database ... 4418 files and directories currently installed.)<br>Preparing to unpack .../apt/archives/apt_2.6.0_arm.deb ...<br>Unpacking apt (2.6.0) over (2.3.13-3) ...<br>Setting up apt (2.6.0) ...<br><br>Configuration file '/data/data/com.termux/files/usr/etc/apt/sources.list'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** sources.list (Y/I/N/O/D/Z) [default=N] ?<br>(Reading database ... 4413 files and directories currently installed.)<br>Preparing to unpack .../archives/bash_5.2.15_arm.deb ...<br>Unpacking bash (5.2.15) over (5.1.12-2) ...<br>Setting up bash (5.2.15) ...<br><br>Configuration file '/data/data/com.termux/files/usr/etc/bash.bashrc'<br> ==> File on system created by you or by a script.<br> ==> File also in package provided by package maintainer.<br>   What would you like to do about it ?  Your options are:<br>    Y or I  : install the package maintainer's version<br>    N or O  : keep your currently-installed version<br>      D     : show the differences between the versions<br>      Z     : start a shell to examine the situation<br> The default action is to keep your current version.<br>*** bash.bashrc (Y/I/N/O/D/Z) [default=N] ?<br>(Reading database ... 4418 files and directories currently installed.)<br>Preparing to unpack .../libcrypt_0.2-5_arm.deb ...<br>Unpacking libcrypt (0.2-5) over (0.2-3) ...<br>Setting up libcrypt (0.2-5) ...<br>Selecting previously unselected package bash-completion.<br>(Reading database ... 4418 files and directories currently installed.)<br>Preparing to unpack .../0-bash-completion_2.11-2_all.deb ...<br>Unpacking bash-completion (2.11-2) ...<br>Preparing to unpack .../1-command-not-found_2.1.0-15_arm.deb ...<br>Unpacking command-not-found (2.1.0-15) over (1.71) ...<br>Preparing to unpack .../2-debianutils_5.7_arm.deb ...<br>Unpacking debianutils (5.7) over (5.5) ...<br>Preparing to unpack .../3-dos2unix_7.4.4_arm.deb ...<br>Unpacking dos2unix (7.4.4) over (7.4.2) ...<br>Preparing to unpack .../4-ed_1.19_arm.deb ...<br>Unpacking ed (1.19) over (1.17-4) ...<br>Preparing to unpack .../5-inetutils_2.4_arm.deb ...<br>Unpacking inetutils (2.4) over (1.9.4-12) ...<br>Preparing to unpack .../6-libtirpc_1.3.3_arm.deb ...<br>Unpacking libtirpc (1.3.3) over (1.3.2) ...<br>Preparing to unpack .../7-lsof_4.98.0_arm.deb ...<br>Unpacking lsof (4.98.0) over (4.94.0-1) ...<br>Preparing to unpack .../8-nano_7.2_arm.deb ...<br>Unpacking nano (7.2) over (6.0) ...<br>Preparing to unpack .../9-unzip_6.0-9_arm.deb ...<br>Unpacking unzip (6.0-9) over (6.0-7) ...<br>Setting up libtirpc (1.3.3) ...<br>Setting up inetutils (2.4) ...<br>Setting up unzip (6.0-9) ...<br>Setting up ed (1.19) ...<br>Setting up command-not-found (2.1.0-15) ...<br>Setting up bash-completion (2.11-2) ...<br>Setting up lsof (4.98.0) ...<br>Setting up nano (7.2) ...<br>update-alternatives: using /data/data/com.termux/files/usr/bin/nano to provide /data/data/com.termux/files/usr/bin/editor (editor) in auto mode<br>Setting up debianutils (5.7) ...<br>Setting up dos2unix (7.4.4) ...<br>W: http://127.0.0.1:8181/packages.termux.dev/apt/termux-main/pool/main/z/zlib/zlib_1.2.13_arm.deb: Automatically disabled Acquire::http::Pipeline-Depth due to incorrect response from server/proxy. (man 5 apt.conf)<br>04:42:15 $<br>04:44:21 $ apt update                                                 Get:1 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable InRelease [14.0 kB]                                                  Get:2 http://127.0.0.1:8181/packages.termux.dev/apt/termux-root root InRelease [14.2 kB]                                                    Get:3 http://127.0.0.1:8181/packages.termux.dev/apt/termux-x11 x11 InRelease [14.0 kB]                                                      Fetched 42.2 kB in 3s (12.2 kB/s)<br>Reading package lists... Done<br>Building dependency tree... Done<br>Reading state information... Done<br>All packages are up to date.<br>04:44:57 $ apt install manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate<br>Reading package lists... Done<br>Building dependency tree... Done<br>Reading state information... Done<br>util-linux is already the newest version (2.38.1-1).<br>nano is already the newest version (7.2).<br>ncurses is already the newest version (6.4-1).<br>termux-tools is already the newest version (1.37.0).<br>net-tools is already the newest version (2.10.0).<br>inetutils is already the newest version (2.4).<br>gpgv is already the newest version (2.4.0-2).<br>curl is already the newest version (7.88.1).<br>dos2unix is already the newest version (7.4.4).<br>The following additional packages will be installed:<br>  abseil-cpp apr apr-util attr brotli flex fontconfig freetype<br>  fribidi gdbm gdk-pixbuf giflib git glib gnupg harfbuzz krb5 ldns<br>  libandroid-execinfo libandroid-posix-semaphore libandroid-shmem<br>  libandroid-spawn libandroid-wordexp libblkid libbsd libcairo<br>  libcap libcompiler-rt libdb libedit libfdisk libffi libgmime<br>  libgraphite libice libicu libidn libjpeg-turbo libksba libllvm<br>  liblua53 liblzo libmount libneon libpcap libpixman libpng libpopt<br>  libprotobuf libresolv-wrapper librsvg libsasl libsm libsqlite<br>  libtalloc libtasn1 libtdb libtiff libuuid libwebp libx11 libxapian<br>  libxau libxcb libxdmcp libxext libxft libxi libxml2 libxmu<br>  libxrandr libxrender libxslt libxt libxtst lld llvm m4 make<br>  mime-support ncurses-ui-libs ndk-sysroot notmuch oathtool<br>  openjdk-17-x openssh-sftp-server pango pinentry pkg-config python<br>  python-ensurepip-wheels python-pip tdb-tools termux-auth tree<br>  ttf-dejavu vim-runtime xmlsec xorg-xauth<br>Suggested packages:<br>  scdaemon cups libqrencode python-tkinter<br>The following NEW packages will be installed:<br>  abseil-cpp alpine android-tools apache2 apr apr-util asciinema<br>  attr bc brotli bsd-games cadaver clang cpufetch darkhttpd<br>  dosfstools e2fsprogs fdisk file flex fontconfig freetype fribidi<br>  gdbm gdk-pixbuf giflib gifsicle git glib gnupg gnutls gptfdisk<br>  harfbuzz iproute2 krb5 ldns lftp libandroid-execinfo<br>  libandroid-posix-semaphore libandroid-shmem libandroid-spawn<br>  libandroid-wordexp libblkid libbsd libcairo libcap libcompiler-rt<br>  libdb libedit libfdisk libffi libgmime libgraphite libice libicu<br>  libidn libjpeg-turbo libksba libllvm liblua53 liblzo libmount<br>  libneon libnfs libpcap libpixman libpng libpopt libprotobuf<br>  libresolv-wrapper librsvg libsasl libsm libsqlite libtalloc<br>  libtasn1 libtdb libtiff libusb libuuid libwebp libx11 libxapian<br>  libxau libxcb libxdmcp libxext libxft libxi libxml2 libxmu<br>  libxrandr libxrender libxslt libxt libxtst links lld llvm lynx m4<br>  make man manpages mime-support mlocate mutt ncftp ncurses-ui-libs<br>  ncurses-utils ndk-sysroot neofetch neomutt netcat-openbsd nmap<br>  nmap-ncat notmuch oathtool openjdk-17 openjdk-17-x openssh<br>  openssh-sftp-server openssl-tool pango paperkey pass pass-otp<br>  pinentry pkg-config progress pv pwgen python<br>  python-ensurepip-wheels python-pip rlwrap samba sshpass tdb-tools<br>  termux-api termux-auth teseq traceroute tree ttf-dejavu unrar vim<br>  vim-runtime wget xmlsec xorg-xauth<br>0 upgraded, 151 newly installed, 0 to remove and 0 not upgraded.<br>Need to get 220 kB/264 MB of archives.<br>After this operation, 997 MB of additional disk space will be used.<br>Do you want to continue? [Y/n] y<br>Get:1 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm libmount arm 2.38.1-1 [120 kB]<br>Get:2 http://127.0.0.1:8181/packages.termux.dev/apt/termux-main stable/main arm fdisk arm 2.38.1-1 [100 kB]<br>Fetched 220 kB in 1s (342 kB/s)<br>Selecting previously unselected package abseil-cpp.<br>(Reading database ... 5170 files and directories currently installed.)<br>Preparing to unpack .../000-abseil-cpp_20230125.1_arm.deb ...<br>Unpacking abseil-cpp (20230125.1) ...<br>Selecting previously unselected package openssl-tool.<br>Preparing to unpack .../001-openssl-tool_1%3a3.1.0_arm.deb ...<br>Unpacking openssl-tool (1:3.1.0) ...<br>Selecting previously unselected package alpine.<br>Preparing to unpack .../002-alpine_2.26_arm.deb ...<br>Unpacking alpine (2.26) ...<br>Selecting previously unselected package brotli.<br>Preparing to unpack .../003-brotli_1.0.9-1_arm.deb ...<br>Unpacking brotli (1.0.9-1) ...<br>Selecting previously unselected package libprotobuf.<br>Preparing to unpack .../004-libprotobuf_2%3a22.1_arm.deb ...<br>Unpacking libprotobuf (2:22.1) ...<br>Selecting previously unselected package libusb.<br>Preparing to unpack .../005-libusb_1.0.26-1_arm.deb ...<br>Unpacking libusb (1.0.26-1) ...<br>Selecting previously unselected package android-tools.<br>Preparing to unpack .../006-android-tools_34.0.0-1_arm.deb ...<br>Unpacking android-tools (34.0.0-1) ...<br>Selecting previously unselected package libuuid.<br>Preparing to unpack .../007-libuuid_2.38.1-1_arm.deb ...<br>Unpacking libuuid (2.38.1-1) ...<br>Selecting previously unselected package apr.<br>Preparing to unpack .../008-apr_1.7.2_arm.deb ...<br>Unpacking apr (1.7.2) ...<br>Selecting previously unselected package apr-util.<br>Preparing to unpack .../009-apr-util_1.6.3_arm.deb ...<br>Unpacking apr-util (1.6.3) ...<br>Selecting previously unselected package apache2.<br>Preparing to unpack .../010-apache2_1%3a2.4.56_arm.deb ...<br>Unpacking apache2 (1:2.4.56) ...<br>Selecting previously unselected package gdbm.<br>Preparing to unpack .../011-gdbm_1.23_arm.deb ...<br>Unpacking gdbm (1.23) ...<br>Selecting previously unselected package libandroid-posix-semaphore.<br>Preparing to unpack .../012-libandroid-posix-semaphore_0.1-3_arm.deb ...<br>Unpacking libandroid-posix-semaphore (0.1-3) ...<br>Selecting previously unselected package libffi.<br>Preparing to unpack .../013-libffi_3.4.4_arm.deb ...<br>Unpacking libffi (3.4.4) ...<br>Selecting previously unselected package libsqlite.<br>Preparing to unpack .../014-libsqlite_3.41.1_arm.deb ...<br>Unpacking libsqlite (3.41.1) ...<br>Selecting previously unselected package ncurses-ui-libs.<br>Preparing to unpack .../015-ncurses-ui-libs_6.4-1_arm.deb ...<br>Unpacking ncurses-ui-libs (6.4-1) ...<br>Selecting previously unselected package python.<br>Preparing to unpack .../016-python_3.11.2-2_arm.deb ...<br>Unpacking python (3.11.2-2) ...<br>Selecting previously unselected package ncurses-utils.<br>Preparing to unpack .../017-ncurses-utils_6.4-1_arm.deb ...<br>Unpacking ncurses-utils (6.4-1) ...<br>Selecting previously unselected package asciinema.<br>Preparing to unpack .../018-asciinema_2.2.0-2_all.deb ...<br>Unpacking asciinema (2.2.0-2) ...<br>Selecting previously unselected package attr.<br>Preparing to unpack .../019-attr_2.5.1_arm.deb ...<br>Unpacking attr (2.5.1) ...<br>Selecting previously unselected package m4.<br>Preparing to unpack .../020-m4_1.4.19-4_arm.deb ...<br>Unpacking m4 (1.4.19-4) ...<br>Selecting previously unselected package flex.<br>Preparing to unpack .../021-flex_2.6.4-3_arm.deb ...<br>Unpacking flex (2.6.4-3) ...<br>Selecting previously unselected package bc.<br>Preparing to unpack .../022-bc_1.07.1-1_arm.deb ...<br>Unpacking bc (1.07.1-1) ...<br>Selecting previously unselected package bsd-games.<br>Preparing to unpack .../023-bsd-games_1%3a3.2_arm.deb ...<br>Unpacking bsd-games (1:3.2) ...<br>Selecting previously unselected package libneon.<br>Preparing to unpack .../024-libneon_0.32.5_arm.deb ...<br>Unpacking libneon (0.32.5) ...<br>Selecting previously unselected package cadaver.<br>Preparing to unpack .../025-cadaver_0.24_arm.deb ...<br>Unpacking cadaver (0.24) ...<br>Selecting previously unselected package libxml2.<br>Preparing to unpack .../026-libxml2_2.10.3-1_arm.deb ...<br>Unpacking libxml2 (2.10.3-1) ...<br>Selecting previously unselected package libllvm.<br>Preparing to unpack .../027-libllvm_15.0.7-3_arm.deb ...<br>Unpacking libllvm (15.0.7-3) ...<br>Selecting previously unselected package libcompiler-rt.<br>Preparing to unpack .../028-libcompiler-rt_15.0.7-3_arm.deb ...<br>Unpacking libcompiler-rt (15.0.7-3) ...<br>Selecting previously unselected package lld.<br>Preparing to unpack .../029-lld_15.0.7-3_arm.deb ...<br>Unpacking lld (15.0.7-3) ...<br>Selecting previously unselected package llvm.<br>Preparing to unpack .../030-llvm_15.0.7-3_arm.deb ...<br>Unpacking llvm (15.0.7-3) ...<br>Selecting previously unselected package ndk-sysroot.<br>Preparing to unpack .../031-ndk-sysroot_25c_arm.deb ...<br>Unpacking ndk-sysroot (25c) ...<br>Selecting previously unselected package clang.<br>Preparing to unpack .../032-clang_15.0.7-3_arm.deb ...<br>Unpacking clang (15.0.7-3) ...<br>Selecting previously unselected package cpufetch.<br>Preparing to unpack .../033-cpufetch_1.03_arm.deb ...<br>Unpacking cpufetch (1.03) ...<br>Selecting previously unselected package darkhttpd.<br>Preparing to unpack .../034-darkhttpd_1.14_arm.deb ...<br>Unpacking darkhttpd (1.14) ...<br>Selecting previously unselected package dosfstools.<br>Preparing to unpack .../035-dosfstools_4.2_arm.deb ...<br>Unpacking dosfstools (4.2) ...<br>Selecting previously unselected package libblkid.<br>Preparing to unpack .../036-libblkid_2.38.1-1_arm.deb ...<br>Unpacking libblkid (2.38.1-1) ...<br>Selecting previously unselected package e2fsprogs.<br>Preparing to unpack .../037-e2fsprogs_1.47.0_arm.deb ...<br>Unpacking e2fsprogs (1.47.0) ...<br>Selecting previously unselected package libfdisk.<br>Preparing to unpack .../038-libfdisk_2.38.1-1_arm.deb ...<br>Unpacking libfdisk (2.38.1-1) ...<br>Selecting previously unselected package libmount.<br>Preparing to unpack .../039-libmount_2.38.1-1_arm.deb ...<br>Unpacking libmount (2.38.1-1) ...<br>Selecting previously unselected package fdisk.<br>Preparing to unpack .../040-fdisk_2.38.1-1_arm.deb ...<br>Unpacking fdisk (2.38.1-1) ...<br>Selecting previously unselected package file.<br>Preparing to unpack .../041-file_5.44_arm.deb ...<br>Unpacking file (5.44) ...<br>Selecting previously unselected package libpng.<br>Preparing to unpack .../042-libpng_1.6.39_arm.deb ...<br>Unpacking libpng (1.6.39) ...<br>Selecting previously unselected package freetype.<br>Preparing to unpack .../043-freetype_2.13.0-1_arm.deb ...<br>Unpacking freetype (2.13.0-1) ...<br>Selecting previously unselected package ttf-dejavu.<br>Preparing to unpack .../044-ttf-dejavu_2.37-8_all.deb ...<br>Unpacking ttf-dejavu (2.37-8) ...<br>Selecting previously unselected package fontconfig.<br>Preparing to unpack .../045-fontconfig_2.14.2-1_arm.deb ...<br>Unpacking fontconfig (2.14.2-1) ...<br>Selecting previously unselected package glib.<br>Preparing to unpack .../046-glib_2.76.0-1_arm.deb ...<br>Unpacking glib (2.76.0-1) ...<br>Selecting previously unselected package fribidi.<br>Preparing to unpack .../047-fribidi_1.0.12_arm.deb ...<br>Unpacking fribidi (1.0.12) ...<br>Selecting previously unselected package libjpeg-turbo.<br>Preparing to unpack .../048-libjpeg-turbo_2.1.5.1_arm.deb ...<br>Unpacking libjpeg-turbo (2.1.5.1) ...<br>Selecting previously unselected package libtiff.<br>Preparing to unpack .../049-libtiff_4.5.0_arm.deb ...<br>Unpacking libtiff (4.5.0) ...<br>Selecting previously unselected package gdk-pixbuf.<br>Preparing to unpack .../050-gdk-pixbuf_2.42.10-1_arm.deb ...<br>Unpacking gdk-pixbuf (2.42.10-1) ...<br>Selecting previously unselected package giflib.<br>Preparing to unpack .../051-giflib_5.2.1-2_arm.deb ...<br>Unpacking giflib (5.2.1-2) ...<br>Selecting previously unselected package gifsicle.<br>Preparing to unpack .../052-gifsicle_1.93_arm.deb ...<br>Unpacking gifsicle (1.93) ...<br>Selecting previously unselected package git.<br>Preparing to unpack .../053-git_2.40.0_arm.deb ...<br>Unpacking git (2.40.0) ...<br>Selecting previously unselected package libksba.<br>Preparing to unpack .../054-libksba_1.6.3_arm.deb ...<br>Unpacking libksba (1.6.3) ...<br>Selecting previously unselected package pinentry.<br>Preparing to unpack .../055-pinentry_1.2.1-1_arm.deb ...<br>Unpacking pinentry (1.2.1-1) ...<br>Selecting previously unselected package gnupg.<br>Preparing to unpack .../056-gnupg_2.4.0-2_arm.deb ...<br>Unpacking gnupg (2.4.0-2) ...<br>Selecting previously unselected package gnutls.<br>Preparing to unpack .../057-gnutls_3.8.0_arm.deb ...<br>Unpacking gnutls (3.8.0) ...<br>Selecting previously unselected package libpopt.<br>Preparing to unpack .../058-libpopt_1.19_arm.deb ...<br>Unpacking libpopt (1.19) ...<br>Selecting previously unselected package gptfdisk.<br>Preparing to unpack .../059-gptfdisk_1.0.9-1_arm.deb ...<br>Unpacking gptfdisk (1.0.9-1) ...<br>Selecting previously unselected package libandroid-shmem.<br>Preparing to unpack .../060-libandroid-shmem_0.4_arm.deb ...<br>Unpacking libandroid-shmem (0.4) ...<br>Selecting previously unselected package liblzo.<br>Preparing to unpack .../061-liblzo_2.10-3_arm.deb ...<br>Unpacking liblzo (2.10-3) ...<br>Selecting previously unselected package libpixman.<br>Preparing to unpack .../062-libpixman_0.42.2_arm.deb ...<br>Unpacking libpixman (0.42.2) ...<br>Selecting previously unselected package libxau.<br>Preparing to unpack .../063-libxau_1.0.11_arm.deb ...<br>Unpacking libxau (1.0.11) ...<br>Selecting previously unselected package libxdmcp.<br>Preparing to unpack .../064-libxdmcp_1.1.4_arm.deb ...<br>Unpacking libxdmcp (1.1.4) ...<br>Selecting previously unselected package libxcb.<br>Preparing to unpack .../065-libxcb_1.15_arm.deb ...<br>Unpacking libxcb (1.15) ...<br>Selecting previously unselected package libx11.<br>Preparing to unpack .../066-libx11_1.8.4-1_arm.deb ...<br>Unpacking libx11 (1.8.4-1) ...<br>Selecting previously unselected package libxext.<br>Preparing to unpack .../067-libxext_1.3.5_arm.deb ...<br>Unpacking libxext (1.3.5) ...<br>Selecting previously unselected package libxrender.<br>Preparing to unpack .../068-libxrender_0.9.11_arm.deb ...<br>Unpacking libxrender (0.9.11) ...<br>Selecting previously unselected package libcairo.<br>Preparing to unpack .../069-libcairo_1.17.8_arm.deb ...<br>Unpacking libcairo (1.17.8) ...<br>Selecting previously unselected package libgraphite.<br>Preparing to unpack .../070-libgraphite_1.3.14-2_arm.deb ...<br>Unpacking libgraphite (1.3.14-2) ...<br>Selecting previously unselected package harfbuzz.<br>Preparing to unpack .../071-harfbuzz_7.1.0_arm.deb ...<br>Unpacking harfbuzz (7.1.0) ...<br>Selecting previously unselected package iproute2.<br>Preparing to unpack .../072-iproute2_6.2.0_arm.deb ...<br>Unpacking iproute2 (6.2.0) ...<br>Selecting previously unselected package libresolv-wrapper.<br>Preparing to unpack .../073-libresolv-wrapper_1.1.7-4_arm.deb ...<br>Unpacking libresolv-wrapper (1.1.7-4) ...<br>Selecting previously unselected package libdb.<br>Preparing to unpack .../074-libdb_18.1.40-4_arm.deb ...<br>Unpacking libdb (18.1.40-4) ...<br>Selecting previously unselected package krb5.<br>Preparing to unpack .../075-krb5_1.20.1_arm.deb ...<br>Unpacking krb5 (1.20.1) ...<br>Selecting previously unselected package ldns.<br>Preparing to unpack .../076-ldns_1.8.3-2_arm.deb ...<br>Unpacking ldns (1.8.3-2) ...<br>Selecting previously unselected package lftp.<br>Preparing to unpack .../077-lftp_4.9.2-5_arm.deb ...<br>Unpacking lftp (4.9.2-5) ...<br>Selecting previously unselected package libandroid-execinfo.<br>Preparing to unpack .../078-libandroid-execinfo_0.1-1_arm.deb ...<br>Unpacking libandroid-execinfo (0.1-1) ...<br>Selecting previously unselected package libandroid-spawn.<br>Preparing to unpack .../079-libandroid-spawn_0.3_arm.deb ...<br>Unpacking libandroid-spawn (0.3) ...<br>Selecting previously unselected package libandroid-wordexp.<br>Preparing to unpack .../080-libandroid-wordexp_0.1_arm.deb ...<br>Unpacking libandroid-wordexp (0.1) ...<br>Selecting previously unselected package libbsd.<br>Preparing to unpack .../081-libbsd_0.11.7_arm.deb ...<br>Unpacking libbsd (0.11.7) ...<br>Selecting previously unselected package libcap.<br>Preparing to unpack .../082-libcap_2.67_arm.deb ...<br>Unpacking libcap (2.67) ...<br>Selecting previously unselected package libedit.<br>Preparing to unpack .../083-libedit_20221030-3.1-0_arm.deb ...<br>Unpacking libedit (20221030-3.1-0) ...<br>Selecting previously unselected package libgmime.<br>Preparing to unpack .../084-libgmime_3.2.13_arm.deb ...<br>Unpacking libgmime (3.2.13) ...<br>Selecting previously unselected package libice.<br>Preparing to unpack .../085-libice_1.1.1_arm.deb ...<br>Unpacking libice (1.1.1) ...<br>Selecting previously unselected package libicu.<br>Preparing to unpack .../086-libicu_72.1_arm.deb ...<br>Unpacking libicu (72.1) ...<br>Selecting previously unselected package libidn.<br>Preparing to unpack .../087-libidn_1.41_arm.deb ...<br>Unpacking libidn (1.41) ...<br>Selecting previously unselected package liblua53.<br>Preparing to unpack .../088-liblua53_5.3.6_arm.deb ...<br>Unpacking liblua53 (5.3.6) ...<br>Selecting previously unselected package libnfs.<br>Preparing to unpack .../089-libnfs_5.0.2_arm.deb ...<br>Unpacking libnfs (5.0.2) ...<br>Selecting previously unselected package libpcap.<br>Preparing to unpack .../090-libpcap_1.10.3_arm.deb ...<br>Unpacking libpcap (1.10.3) ...<br>Selecting previously unselected package libxft.<br>Preparing to unpack .../091-libxft_2.3.7_arm.deb ...<br>Unpacking libxft (2.3.7) ...<br>Selecting previously unselected package pango.<br>Preparing to unpack .../092-pango_1.50.14_arm.deb ...<br>Unpacking pango (1.50.14) ...<br>Selecting previously unselected package librsvg.<br>Preparing to unpack .../093-librsvg_2.55.2_arm.deb ...<br>Unpacking librsvg (2.55.2) ...<br>Selecting previously unselected package libsasl.<br>Preparing to unpack .../094-libsasl_2.1.28_arm.deb ...<br>Unpacking libsasl (2.1.28) ...<br>Selecting previously unselected package libsm.<br>Preparing to unpack .../095-libsm_1.2.4-1_arm.deb ...<br>Unpacking libsm (1.2.4-1) ...<br>Selecting previously unselected package libtalloc.<br>Preparing to unpack .../096-libtalloc_2.4.0_arm.deb ...<br>Unpacking libtalloc (2.4.0) ...<br>Selecting previously unselected package libtasn1.<br>Preparing to unpack .../097-libtasn1_4.19.0-1_arm.deb ...<br>Unpacking libtasn1 (4.19.0-1) ...<br>Selecting previously unselected package libtdb.<br>Preparing to unpack .../098-libtdb_1.4.8_arm.deb ...<br>Unpacking libtdb (1.4.8) ...<br>Selecting previously unselected package libwebp.<br>Preparing to unpack .../099-libwebp_1.3.0_arm.deb ...<br>Unpacking libwebp (1.3.0) ...<br>Selecting previously unselected package libxapian.<br>Preparing to unpack .../100-libxapian_1.4.22_arm.deb ...<br>Unpacking libxapian (1.4.22) ...<br>Selecting previously unselected package libxi.<br>Preparing to unpack .../101-libxi_1.8_arm.deb ...<br>Unpacking libxi (1.8) ...<br>Selecting previously unselected package libxt.<br>Preparing to unpack .../102-libxt_1.2.1-2_arm.deb ...<br>Unpacking libxt (1.2.1-2) ...<br>Selecting previously unselected package libxmu.<br>Preparing to unpack .../103-libxmu_1.1.4_arm.deb ...<br>Unpacking libxmu (1.1.4) ...<br>Selecting previously unselected package libxrandr.<br>Preparing to unpack .../104-libxrandr_1.5.3_arm.deb ...<br>Unpacking libxrandr (1.5.3) ...<br>Selecting previously unselected package libxslt.<br>Preparing to unpack .../105-libxslt_1.1.37_arm.deb ...<br>Unpacking libxslt (1.1.37) ...<br>Selecting previously unselected package libxtst.<br>Preparing to unpack .../106-libxtst_1.2.4_arm.deb ...<br>Unpacking libxtst (1.2.4) ...<br>Selecting previously unselected package links.<br>Preparing to unpack .../107-links_2.28-1_arm.deb ...<br>Unpacking links (2.28-1) ...<br>Selecting previously unselected package lynx.<br>Preparing to unpack .../108-lynx_2.8.9rel.1-7_arm.deb ...<br>Unpacking lynx (2.8.9rel.1-7) ...<br>Selecting previously unselected package make.<br>Preparing to unpack .../109-make_4.4.1_arm.deb ...<br>Unpacking make (4.4.1) ...<br>Selecting previously unselected package man.<br>Preparing to unpack .../110-man_1.14.6_arm.deb ...<br>Unpacking man (1.14.6) ...<br>Selecting previously unselected package manpages.<br>Preparing to unpack .../111-manpages_6.03_all.deb ...<br>Unpacking manpages (6.03) ...<br>Selecting previously unselected package mime-support.<br>Preparing to unpack .../112-mime-support_1%3a2.1.53_all.deb ...<br>Unpacking mime-support (1:2.1.53) ...<br>Selecting previously unselected package mlocate.<br>Preparing to unpack .../113-mlocate_0.26-5_arm.deb ...<br>Unpacking mlocate (0.26-5) ...<br>Selecting previously unselected package mutt.<br>Preparing to unpack .../114-mutt_2.2.9_arm.deb ...<br>Unpacking mutt (2.2.9) ...<br>Selecting previously unselected package ncftp.<br>Preparing to unpack .../115-ncftp_3.2.6-1_arm.deb ...<br>Unpacking ncftp (3.2.6-1) ...<br>Selecting previously unselected package neofetch.<br>Preparing to unpack .../116-neofetch_7.1.0-1_all.deb ...<br>Unpacking neofetch (7.1.0-1) ...<br>Selecting previously unselected package notmuch.<br>Preparing to unpack .../117-notmuch_0.37_arm.deb ...<br>Unpacking notmuch (0.37) ...<br>Selecting previously unselected package neomutt.<br>Preparing to unpack .../118-neomutt_20220429-1_arm.deb ...<br>Unpacking neomutt (20220429-1) ...<br>Selecting previously unselected package netcat-openbsd.<br>Preparing to unpack .../119-netcat-openbsd_1.219-1-0_arm.deb ...<br>Unpacking netcat-openbsd (1.219-1-0) ...<br>Selecting previously unselected package nmap.<br>Preparing to unpack .../120-nmap_7.93_arm.deb ...<br>Unpacking nmap (7.93) ...<br>Selecting previously unselected package nmap-ncat.<br>Preparing to unpack .../121-nmap-ncat_7.93_arm.deb ...<br>Unpacking nmap-ncat (7.93) ...<br>Selecting previously unselected package xmlsec.<br>Preparing to unpack .../122-xmlsec_1.2.37_arm.deb ...<br>Unpacking xmlsec (1.2.37) ...<br>Selecting previously unselected package oathtool.<br>Preparing to unpack .../123-oathtool_2.6.7_arm.deb ...<br>Unpacking oathtool (2.6.7) ...<br>Selecting previously unselected package openjdk-17.<br>Preparing to unpack .../124-openjdk-17_17.0-25_arm.deb ...<br>Unpacking openjdk-17 (17.0-25) ...<br>Selecting previously unselected package openjdk-17-x.<br>Preparing to unpack .../125-openjdk-17-x_17.0-25_arm.deb ...<br>Unpacking openjdk-17-x (17.0-25) ...<br>Selecting previously unselected package openssh-sftp-server.<br>Preparing to unpack .../126-openssh-sftp-server_9.3p1_arm.deb ...<br>Unpacking openssh-sftp-server (9.3p1) ...<br>Selecting previously unselected package termux-auth.<br>Preparing to unpack .../127-termux-auth_1.4-2_arm.deb ...<br>Unpacking termux-auth (1.4-2) ...<br>Selecting previously unselected package openssh.<br>Preparing to unpack .../128-openssh_9.3p1_arm.deb ...<br>Unpacking openssh (9.3p1) ...<br>Selecting previously unselected package paperkey.<br>Preparing to unpack .../129-paperkey_1.6_arm.deb ...<br>Unpacking paperkey (1.6) ...<br>Selecting previously unselected package tree.<br>Preparing to unpack .../130-tree_2.1.0_arm.deb ...<br>Unpacking tree (2.1.0) ...<br>Selecting previously unselected package pass.<br>Preparing to unpack .../131-pass_1.7.4-2_all.deb ...<br>Unpacking pass (1.7.4-2) ...<br>Selecting previously unselected package pass-otp.<br>Preparing to unpack .../132-pass-otp_1.2.0-3_all.deb ...<br>Unpacking pass-otp (1.2.0-3) ...<br>Selecting previously unselected package pkg-config.<br>Preparing to unpack .../133-pkg-config_0.29.2-2_arm.deb ...<br>Unpacking pkg-config (0.29.2-2) ...<br>Selecting previously unselected package progress.<br>Preparing to unpack .../134-progress_0.16-1_arm.deb ...<br>Unpacking progress (0.16-1) ...<br>Selecting previously unselected package pv.<br>Preparing to unpack .../135-pv_1.6.20_arm.deb ...<br>Unpacking pv (1.6.20) ...<br>Selecting previously unselected package pwgen.<br>Preparing to unpack .../136-pwgen_2.08-1_arm.deb ...<br>Unpacking pwgen (2.08-1) ...<br>Selecting previously unselected package python-ensurepip-wheels.<br>Preparing to unpack .../137-python-ensurepip-wheels_3.11.2-2_all.deb ...<br>Unpacking python-ensurepip-wheels (3.11.2-2) ...<br>Selecting previously unselected package python-pip.<br>Preparing to unpack .../138-python-pip_23.0.1_all.deb ...<br>Unpacking python-pip (23.0.1) ...<br>Selecting previously unselected package rlwrap.<br>Preparing to unpack .../139-rlwrap_0.46.1_arm.deb ...<br>Unpacking rlwrap (0.46.1) ...<br>Selecting previously unselected package tdb-tools.<br>Preparing to unpack .../140-tdb-tools_1.4.8_arm.deb ...<br>Unpacking tdb-tools (1.4.8) ...<br>Selecting previously unselected package samba.<br>Preparing to unpack .../141-samba_4.15.13_arm.deb ...<br>Unpacking samba (4.15.13) ...<br>Selecting previously unselected package sshpass.<br>Preparing to unpack .../142-sshpass_1.10_arm.deb ...<br>Unpacking sshpass (1.10) ...<br>Selecting previously unselected package termux-api.<br>Preparing to unpack .../143-termux-api_0.57_arm.deb ...<br>Unpacking termux-api (0.57) ...<br>Selecting previously unselected package teseq.<br>Preparing to unpack .../144-teseq_1.1.1-1_arm.deb ...<br>Unpacking teseq (1.1.1-1) ...<br>Selecting previously unselected package traceroute.<br>Preparing to unpack .../145-traceroute_2.1.2_arm.deb ...<br>Unpacking traceroute (2.1.2) ...<br>Selecting previously unselected package unrar.<br>Preparing to unpack .../146-unrar_6.2.6_arm.deb ...<br>Unpacking unrar (6.2.6) ...<br>Selecting previously unselected package vim-runtime.<br>Preparing to unpack .../147-vim-runtime_9.0.1400_all.deb ...<br>Unpacking vim-runtime (9.0.1400) ...<br>Selecting previously unselected package vim.<br>Preparing to unpack .../148-vim_9.0.1400_arm.deb ...<br>Unpacking vim (9.0.1400) ...<br>Selecting previously unselected package wget.<br>Preparing to unpack .../149-wget_1.21.3-5_arm.deb ...<br>Unpacking wget (1.21.3-5) ...<br>Selecting previously unselected package xorg-xauth.<br>Preparing to unpack .../150-xorg-xauth_1.1.2_arm.deb ...<br>Unpacking xorg-xauth (1.1.2) ...<br>Setting up paperkey (1.6) ...<br>Setting up libksba (1.6.3) ...<br>Setting up libedit (20221030-3.1-0) ...<br>Setting up openssh-sftp-server (9.3p1) ...<br>Setting up libuuid (2.38.1-1) ...<br>Setting up cpufetch (1.03) ...<br>Setting up mime-support (1:2.1.53) ...<br>Setting up libpng (1.6.39) ...<br>Setting up teseq (1.1.1-1) ...<br>Setting up traceroute (2.1.2) ...<br>Setting up libpcap (1.10.3) ...<br>Setting up libpixman (0.42.2) ...<br>Setting up openssl-tool (1:3.1.0) ...<br>Setting up attr (2.5.1) ...<br>Setting up libxdmcp (1.1.4) ...<br>Setting up libgraphite (1.3.14-2) ...<br>Setting up iproute2 (6.2.0) ...<br>Setting up libusb (1.0.26-1) ...<br>Setting up gdbm (1.23) ...<br>Setting up libandroid-wordexp (0.1) ...<br>Setting up ldns (1.8.3-2) ...<br>Setting up libandroid-shmem (0.4) ...<br>Setting up dosfstools (4.2) ...<br>Setting up bsd-games (1:3.2) ...<br>Setting up lftp (4.9.2-5) ...<br>Setting up ndk-sysroot (25c) ...<br>Setting up m4 (1.4.19-4) ...<br>Setting up libneon (0.32.5) ...<br>Setting up libcap (2.67) ...<br>Setting up libpopt (1.19) ...<br>Setting up unrar (6.2.6) ...<br>Setting up libnfs (5.0.2) ...<br>Setting up file (5.44) ...<br>Setting up ncurses-utils (6.4-1) ...<br>Setting up libandroid-posix-semaphore (0.1-3) ...<br>Setting up sshpass (1.10) ...<br>Setting up neofetch (7.1.0-1) ...<br>Setting up libicu (72.1) ...<br>Setting up libandroid-spawn (0.3) ...<br>Setting up libsqlite (3.41.1) ...<br>Setting up libffi (3.4.4) ...<br>Setting up libice (1.1.1) ...<br>Setting up ttf-dejavu (2.37-8) ...<br>Setting up apr (1.7.2) ...<br>Setting up libandroid-execinfo (0.1-1) ...<br>Setting up ncurses-ui-libs (6.4-1) ...<br>Setting up gptfdisk (1.0.9-1) ...<br>Setting up darkhttpd (1.14) ...<br>Setting up libblkid (2.38.1-1) ...<br>Setting up libtasn1 (4.19.0-1) ...<br>Setting up make (4.4.1) ...<br>Setting up libxau (1.0.11) ...<br>Setting up pinentry (1.2.1-1) ...<br>Setting up rlwrap (0.46.1) ...<br>Setting up tree (2.1.0) ...<br>Setting up libjpeg-turbo (2.1.5.1) ...<br>Setting up git (2.40.0) ...<br>Setting up man (1.14.6) ...<br>Setting up apr-util (1.6.3) ...<br>Setting up liblua53 (5.3.6) ...<br>Setting up pv (1.6.20) ...<br>Setting up gnutls (3.8.0) ...<br>Setting up giflib (5.2.1-2) ...<br>Setting up gifsicle (1.93) ...<br>Setting up glib (2.76.0-1) ...<br>Setting up libresolv-wrapper (1.1.7-4) ...<br>Setting up libtalloc (2.4.0) ...<br>Setting up gnupg (2.4.0-2) ...<br>Setting up termux-auth (1.4-2) ...<br>Setting up libbsd (0.11.7) ...<br>Setting up termux-api (0.57) ...<br>Setting up openjdk-17 (17.0-25) ...<br>Setting up libxcb (1.15) ...<br>Setting up mlocate (0.26-5) ...<br>Remember to run `updatedb'.<br>Setting up libgmime (3.2.13) ...<br>Setting up libidn (1.41) ...<br>Setting up vim-runtime (9.0.1400) ...<br>Setting up libxapian (1.4.22) ...<br>Setting up alpine (2.26) ...<br>warning making a passwordless masterpasword file<br>........+......+...+...........+.+..+...+.........+....+++++++++++++++++++++++++++++++++++++++*....+.......+...+.....+.......+......+..+..........+...+..+...+....+..+............................+..+......+.........+....+..+.......+..+.+..+.+++++++++++++++++++++++++++++++++++++++*........+......+...............+.+...+.........+..+.+..+.......+...+..+....+..+...+.+.........+..+...................+.........+...........+...+......+.+.....+................+..+...............+...+.......+......+...............+.....+......+...............+.+........+.+.....+....++++++<br>...+.+...+......+.....+..........+..+.......+........+...+.........+...+..................+.+......+...+...........+.+..+.......+......+.....+...+..........+......+........+.+..............+++++++++++++++++++++++++++++++++++++++*..........+.......+...+..+......+.......+...+............+...+..+......+.......+...+...........+.........+.+.....+....+..+..........+...+..............+.+.....+.......+...+..+....+.....+.+++++++++++++++++++++++++++++++++++++++*...............++++++<br>-----<br>Setting up libmount (2.38.1-1) ...<br>Setting up ncftp (3.2.6-1) ...<br>Setting up libdb (18.1.40-4) ...<br>Setting up liblzo (2.10-3) ...<br>Setting up python (3.11.2-2) ...<br><br>== Note: pip is now separate from python ==<br>To install, enter the following command:<br>   pkg install python-pip<br><br>Setting up libxml2 (2.10.3-1) ...<br>Setting up pwgen (2.08-1) ...<br>Setting up abseil-cpp (20230125.1) ...<br>Setting up libsasl (2.1.28) ...<br>Setting up brotli (1.0.9-1) ...<br>Setting up notmuch (0.37) ...<br>Setting up flex (2.6.4-3) ...<br>Setting up vim (9.0.1400) ...<br>update-alternatives: using /data/data/com.termux/files/usr/bin/vim to provide /data/data/com.termux/files/usr/bin/editor (editor) in auto mode<br>update-alternatives: using /data/data/com.termux/files/usr/bin/vim to provide /data/data/com.termux/files/usr/bin/vi (vi) in auto mode<br>Setting up wget (1.21.3-5) ...<br>Setting up python-ensurepip-wheels (3.11.2-2) ...<br>Setting up mutt (2.2.9) ...<br>Setting up progress (0.16-1) ...<br>Setting up cadaver (0.24) ...<br>Setting up libtdb (1.4.8) ...<br>Setting up manpages (6.03) ...<br>Setting up libfdisk (2.38.1-1) ...<br>Setting up apache2 (1:2.4.56) ...<br>Setting up netcat-openbsd (1.219-1-0) ...<br>Setting up libtiff (4.5.0) ...<br>Setting up libxslt (1.1.37) ...<br>Setting up bc (1.07.1-1) ...<br>Setting up e2fsprogs (1.47.0) ...<br>Setting up libprotobuf (2:22.1) ...<br>Setting up nmap (7.93) ...<br>Setting up fdisk (2.38.1-1) ...<br>Setting up libsm (1.2.4-1) ...<br>Setting up libx11 (1.8.4-1) ...<br>Setting up android-tools (34.0.0-1) ...<br>Setting up freetype (2.13.0-1) ...<br>Setting up fribidi (1.0.12) ...<br>Setting up tdb-tools (1.4.8) ...<br>Setting up pkg-config (0.29.2-2) ...<br>Setting up pass (1.7.4-2) ...<br>Setting up krb5 (1.20.1) ...<br>Setting up libllvm (15.0.7-3) ...<br>Setting up libxext (1.3.5) ...<br>Setting up neomutt (20220429-1) ...<br>Setting up gdk-pixbuf (2.42.10-1) ...<br>Setting up lynx (2.8.9rel.1-7) ...<br>Setting up asciinema (2.2.0-2) ...<br>Setting up nmap-ncat (7.93) ...<br>Setting up libxi (1.8) ...<br>Setting up samba (4.15.13) ...<br>Setting up libwebp (1.3.0) ...<br>Setting up fontconfig (2.14.2-1) ...<br>Setting up libxt (1.2.1-2) ...<br>Setting up xmlsec (1.2.37) ...<br>Setting up openssh (9.3p1) ...<br>Generating public/private rsa key pair.<br>Your identification has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_rsa_key<br>Your public key has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_rsa_key.pub<br>The key fingerprint is:<br>SHA256:w3RqVtJPMBmOnnZWtvlcxB9ra6anqpa7B4MbiLngKVg u0_a188@localhost<br>The key's randomart image is:<br>+---[RSA 3072]----+<br>|          +o     |<br>|         +.o   . |<br>|        + = +  .o|<br>|       + * = o .+|<br>|    o . S o +  oo|<br>| .Eo . * *   o...|<br>|o.o .   o +   o+ |<br>|oo .   . o .  +. |<br>|.       .+=..oo  |<br>+----[SHA256]-----+<br>Generating public/private dsa key pair.<br>Your identification has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_dsa_key<br>Your public key has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_dsa_key.pub<br>The key fingerprint is:<br>SHA256:jVxvs02JHA/mbfyqLI4s3xRjvark1mOxmVJK9guNrss u0_a188@localhost<br>The key's randomart image is:<br>+---[DSA 1024]----+<br>|                 |<br>|                 |<br>|          . +    |<br>|       . + * B . |<br>|        S = O B  |<br>|        o+o+ B . |<br>|       o+=o=o . .|<br>|     ..=+=Xo   . |<br>|      E*B==+o..  |<br>+----[SHA256]-----+<br>Generating public/private ecdsa key pair.<br>Your identification has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_ecdsa_key<br>Your public key has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_ecdsa_key.pub<br>The key fingerprint is:<br>SHA256:iZnQTohaJOMWRPlICZjFyzlPG0MjOcuA9ufEbYnd4VM u0_a188@localhost<br>The key's randomart image is:<br>+---[ECDSA 256]---+<br>|XB=.             |<br>|*O*.oo   . E     |<br>|o**B+.* + o      |<br>|.+Bo+O O =       |<br>|.  +++* S .      |<br>|    o.           |<br>|                 |<br>|                 |<br>|                 |<br>+----[SHA256]-----+<br>Generating public/private ed25519 key pair.<br>Your identification has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_ed25519_key<br>Your public key has been saved in /data/data/com.termux/files/usr/etc/ssh/ssh_host_ed25519_key.pub<br>The key fingerprint is:<br>SHA256:DPl0BGPTX+D7jKmBzQbOz1YjoSWSrrl3VioQubsYuSE u0_a188@localhost<br>The key's randomart image is:<br>+--[ED25519 256]--+<br>|        =o. ..   |<br>|       o +..  .  |<br>|     .o.. ....   |<br>|    o o=..o ..   |<br>|     + .S+ ..    |<br>|   .o .o.=o o=   |<br>|E +  =  +o=oo.o  |<br>| . =+ o ++.o     |<br>|  o o+ + .+      |<br>+----[SHA256]-----+<br>Setting up lld (15.0.7-3) ...<br>Setting up libxrender (0.9.11) ...<br>Setting up oathtool (2.6.7) ...<br>Setting up libcompiler-rt (15.0.7-3) ...<br>Setting up llvm (15.0.7-3) ...<br>Setting up libxft (2.3.7) ...<br>Setting up libxtst (1.2.4) ...<br>Setting up libxmu (1.1.4) ...<br>Setting up libcairo (1.17.8) ...<br>Setting up harfbuzz (7.1.0) ...<br>Setting up libxrandr (1.5.3) ...<br>Setting up pass-otp (1.2.0-3) ...<br>Setting up openjdk-17-x (17.0-25) ...<br>Setting up xorg-xauth (1.1.2) ...<br>Setting up clang (15.0.7-3) ...<br>Setting up python-pip (23.0.1) ...<br>pip setup...<br>Writing to /data/data/com.termux/files/usr/etc/pip.conf<br>Setting up pango (1.50.14) ...<br>Setting up librsvg (2.55.2) ...<br>Setting up links (2.28-1) ...<br>04:47:12 $<br>04:47:25 $<br>04:47:26 $ updatedb    # "man locate" and "man updatedb"<br>04:47:45 $<br>04:47:47 $<br></pre></td>
</tr>
</table>

<p><br></p>

<a id="termux-session-for-example-2"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#example-2">Example 2</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ echo $PS1<br>\[\e[0;32m\]\w\[\e[0m\] \[\e[0;97m\]\$\[\e[0m\]<br>~ $<br>~ $ export PS1='\T $ '<br>11:07:44 $<br>11:07:45 $ echo $PS1<br>\T $<br>11:08:03 $<br>11:08:04 $ echo $HOME<br>/data/data/com.termux/files/home<br>11:08:16 $<br>11:08:17 $ echo $PREFIX<br>/data/data/com.termux/files/usr<br>11:08:40 $<br>11:08:41 $ pwd<br>/data/data/com.termux/files/home<br>11:08:56 $<br>11:08:58 $ ls --color=never -l $HOME/storage|grep -iv external<br>total 0<br>lrwxrwxrwx 1 u0_a188 u0_a188 26 Apr  3 16:32 dcim -> /storage/emulated/0/DCIM<br>lrwxrwxrwx 1 u0_a188 u0_a188 30 Apr  3 16:32 downloads -> /storage/emulated/0/Download<br>lrwxrwxrwx 1 u0_a188 u0_a188 30 Apr  3 16:32 movies -> /storage/emulated/0/Movies<br>lrwxrwxrwx 1 u0_a188 u0_a188 30 Apr  3 16:32 music -> /storage/emulated/0/Music<br>lrwxrwxrwx 1 u0_a188 u0_a188 30 Apr  3 16:32 pictures -> /storage/emulated/0/Pictures<br>lrwxrwxrwx 1 u0_a188 u0_a188 22 Apr  3 16:32 shared -> /storage/emulated/0<br>11:09:21 $<br>11:09:23 $ ls --color=never -l storage/downloads<br>lrwxrwxrwx 1 u0_a188 u0_a188 30 Apr  3 16:32 storage/downloads -> /storage/emulated/0/Download<br>11:09:38 $<br>11:13:25 $<br>11:13:33 $ mktemp -d /storage/emulated/0/Download/ext4-test-directory.XXXXXXXXXX<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:13:37 $<br>11:13:39 $<br>11:15:14 $<br>11:15:14 $ tree /storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br><br>0 directories, 0 files<br>11:15:19 $<br>11:15:32 $ ls --color=never -alR /storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB:<br>total 7<br>drwxrwx---  2 root everybody 3488 Apr  7 11:13 .<br>drwxrwx--- 14 root everybody 3488 Apr  7 11:13 ..<br>11:16:24 $<br>11:16:25 $ cd /storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB    # "cd --help"<br>11:16:55 $<br>11:16:58 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:17:14 $<br>11:17:15 $ mkdir -v test-disk1-directory<br>mkdir: created directory 'test-disk1-directory'<br>11:17:28 $<br>11:17:30 $ cd test-disk1-directory<br>11:17:54 $<br>11:17:54 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/test-disk1-directory<br>11:18:41 $<br>11:18:41 $ touch file1<br>11:18:54 $<br>11:18:54 $ ls --color=never -l file1.txt<br>ls: cannot access 'file1.txt': No such file or directory<br>11:19:06 $<br>11:19:08 $ mv file1 file1.txt<br>11:19:36 $<br>11:19:36 $ ls --color=never -l file1.txt<br>-rw-rw---- 1 root everybody 0 Apr  7 11:18 file1.txt<br>11:19:55 $<br>11:19:55 $ touch file2r.txt<br>11:20:09 $<br>11:20:10 $ rm -iv file2r.txt<br>rm: remove regular empty file 'file2r.txt'? y<br>removed 'file2r.txt'<br>11:20:33 $<br>11:20:34 $ touch file2.txt<br>11:20:48 $<br>11:20:49 $ cd ..<br>11:21:56 $<br>11:21:58 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:22:12 $<br>11:22:13 $ dd if=/dev/zero of=test-disk1-30mb.ext bs=1M count=30   # Always initialize the image file with zeroes (zero-filled, 0-filled)<br>30+0 records in<br>30+0 records out<br>31457280 bytes (31 MB, 30 MiB) copied, 0.0563377 s, 558 MB/s<br>11:22:44 $<br>11:22:46 $ ls --color=never  -l test-disk1-30mb.ext<br>-rw-rw---- 1 root everybody 31457280 Apr  7 11:22 test-disk1-30mb.ext<br>11:23:01 $<br>11:23:02 $ tree test-disk1-directory<br>test-disk1-directory<br>├── file1.txt<br>└── file2.txt<br><br>1 directory, 2 files<br>11:23:13 $<br>11:23:14 $ ls --color=never -la<br>total 30763<br>drwxrwx---  3 root everybody     3488 Apr  7 11:22 .<br>drwxrwx--- 14 root everybody     3488 Apr  7 11:13 ..<br>-rw-rw----  1 root everybody 31457280 Apr  7 11:22 test-disk1-30mb.ext<br>drwxrwx---  2 root everybody     3488 Apr  7 11:20 test-disk1-directory<br>11:23:37 $<br>11:23:38 $ ls --color=never -la test-disk1-directory<br>total 7<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:20 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:20 file2.txt<br>11:23:56 $<br>11:23:57 $ mkfs.ext4 -m 0 -L ext4-disk1-30mb -d test-disk1-directory test-disk1-30mb.ext # "man mkfs.ext4": "-d root-directory" "Copy the contents of the given directory into the root directory of the file system."<br>mke2fs 1.47.0 (5-Feb-2023)<br>Creating filesystem with 30720 1k blocks and 7680 inodes<br>Filesystem UUID: c1bfbb1b-4ca2-4d8a-b1b7-4d398994b042<br>Superblock backups stored on blocks:<br>        8193, 24577<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (1024 blocks): done<br>Copying files into the device: done<br>Writing superblocks and filesystem accounting information: done<br><br>11:24:27 $<br>11:24:28 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:24:55 $<br>11:24:55 $ cadaver http://127.0.0.1:8181<br>dav:/> ls<br>Listing collection `/': succeeded.<br>Coll:   [SYS]                                  0  Apr  7 11:24<br>Coll:   [UNKNOWN]                              0  Apr  7 11:24<br>Coll:   lost+found                             0  Apr  7 11:24<br>        file1.txt                              0  Apr  7 11:18<br>        file2.txt                              0  Apr  7 11:20<br>dav:/> quit<br>Connection to `127.0.0.1' closed.<br>11:30:01 $<br>11:30:02 $ ls --color=never -la<br>total 30763<br>drwxrwx---  3 root everybody     3488 Apr  7 11:22 .<br>drwxrwx--- 14 root everybody     3488 Apr  7 11:13 ..<br>-rw-rw----  1 root everybody 31457280 Apr  7 11:24 test-disk1-30mb.ext<br>drwxrwx---  2 root everybody     3488 Apr  7 11:20 test-disk1-directory<br>11:30:39 $<br>11:30:40 $ mkdir -v test-disk1-directory/last-example<br>mkdir: created directory 'test-disk1-directory/last-example'<br>11:30:55 $<br>11:30:56 $ tree test-disk1-directory<br>test-disk1-directory<br>├── file1.txt<br>├── file2.txt<br>└── last-example<br><br>2 directories, 2 files<br>11:31:29 $<br>11:31:30 $ ls --color=never -al test-disk1-directory<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:20 file2.txt<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:30 last-example<br>11:31:42 $<br>11:31:43 $ touch test-disk1-directory/last-example/file3.html<br>11:31:58 $<br>11:31:59 $ tree test-disk1-directory<br>test-disk1-directory<br>├── file1.txt<br>├── file2.txt<br>└── last-example<br>    └── file3.html<br><br>2 directories, 3 files<br>11:32:20 $<br>11:32:21 $ ls --color=never -la test-disk1-directory<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:20 file2.txt<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:31 last-example<br>11:32:37 $<br>11:32:38 $ ls --color=never -alR test-disk1-directory<br>test-disk1-directory:<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:20 file2.txt<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:31 last-example<br><br>test-disk1-directory/last-example:<br>total 7<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:31 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:31 file3.html<br>11:32:52 $<br>11:32:52 $ nano --linenumbers test-disk1-directory/last-example/file4.html<br>11:34:52 $<br>11:34:53 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:35:21 $<br>11:35:21 $ stat test-disk1-directory/last-example/file4.html<br>  File: test-disk1-directory/last-example/file4.html<br>  Size: 52              Blocks: 8          IO Block: 4096   regular file<br>Device: 0,31    Inode: 291051      Links: 1<br>Access: (0660/-rw-rw----)  Uid: (    0/    root)   Gid: ( 9997/everybody)<br>Access: 2023-04-07 11:34:51.981375695 -0400<br>Modify: 2023-04-07 11:34:51.981375695 -0400<br>Change: 2023-04-07 11:34:51.981375695 -0400<br> Birth: -<br>11:36:10 $<br>11:36:11 $ file test-disk1-directory/last-example/file4.html<br>test-disk1-directory/last-example/file4.html: HTML document, ASCII text<br>11:36:27 $<br>11:36:28 $ cat test-disk1-directory/last-example/file4.html<br>&lt;html&gt;<br>&lt;body&gt;<br>&lt;h1&gt;<br>file4.html<br>&lt;/h1&gt;<br>&lt;/body&gt;<br>&lt;/html&gt;<br>11:36:51 $<br>11:36:52 $ tree test-disk1-directory<br>test-disk1-directory<br>├── file1.txt<br>├── file2.txt<br>└── last-example<br>    ├── file3.html<br>    └── file4.html<br><br>2 directories, 4 files<br>11:37:11 $<br>11:37:11 $ ls --color=never -alR test-disk1-directory<br>test-disk1-directory:<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:20 file2.txt<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:34 last-example<br><br>test-disk1-directory/last-example:<br>total 11<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:34 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:30 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:31 file3.html<br>-rw-rw---- 1 root everybody   52 Apr  7 11:34 file4.html<br>11:37:27 $<br>11:37:28 $ cd test-disk1-directory<br>11:37:54 $<br>11:37:54 $ mv -iv file1.txt last-example<br>renamed 'file1.txt' -> 'last-example/file1.txt'<br>11:38:09 $<br>11:38:15 $ cp -iv file2.txt last-example<br>'file2.txt' -> 'last-example/file2.txt'<br>11:38:32 $<br>11:38:34 $ tree last-example<br>last-example<br>├── file1.txt<br>├── file2.txt<br>├── file3.html<br>└── file4.html<br><br>1 directory, 4 files<br>11:38:55 $<br>11:39:09 $<br>11:39:17 $<br>11:39:17 $ rm -iv file2.txt<br>rm: remove regular empty file 'file2.txt'? y<br>removed 'file2.txt'<br>11:39:22 $<br>11:39:22 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/test-disk1-directory<br>11:39:36 $<br>11:39:37 $ ls --color=never -al<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:39 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:22 ..<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:38 last-example<br>11:39:59 $<br>11:39:59 $ cd ..<br>11:40:24 $<br>11:40:25 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:40:58 $<br>11:40:58 $ ls --color=never -al<br>total 30763<br>drwxrwx---  3 root everybody     3488 Apr  7 11:22 .<br>drwxrwx--- 14 root everybody     3488 Apr  7 11:13 ..<br>-rw-rw----  1 root everybody 31457280 Apr  7 11:24 test-disk1-30mb.ext<br>drwxrwx---  3 root everybody     3488 Apr  7 11:39 test-disk1-directory<br>11:41:17 $<br>11:41:39 $<br>11:41:42 $ mkfs.ext4 -m 0 -L ext4-disk1-30mb -d test-disk1-directory test-disk1-30mb.ext<br>mke2fs 1.47.0 (5-Feb-2023)<br>test-disk1-30mb.ext contains a ext4 file system labelled 'ext4-disk1-30mb'<br>        created on Fri Apr  7 11:24:27 2023<br>Proceed anyway? (y,N) y<br>Creating filesystem with 30720 1k blocks and 7680 inodes<br>Filesystem UUID: 6b941b84-6c1b-4fd1-8ed8-2bbe787fa2a1<br>Superblock backups stored on blocks:<br>        8193, 24577<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (1024 blocks): done<br>Copying files into the device: done<br>Writing superblocks and filesystem accounting information: done<br><br>11:42:13 $<br>11:42:15 $ cadaver http://127.0.0.1:8181<br>dav:/> ls<br>Listing collection `/': succeeded.<br>Coll:   [SYS]                                  0  Apr  7 11:42<br>Coll:   [UNKNOWN]                              0  Apr  7 11:42<br>Coll:   last-example                           0  Apr  7 11:38<br>Coll:   lost+found                             0  Apr  7 11:42<br>dav:/><br>dav:/> cd last-example<br>dav:/last-example/> ls<br>Listing collection `/last-example/': succeeded.<br>        file1.txt                              0  Apr  7 11:18<br>        file2.txt                              0  Apr  7 11:38<br>        file3.html                             0  Apr  7 11:31<br>        file4.html                            52  Apr  7 11:34<br>dav:/last-example/><br>dav:/last-example/> get file4.html<br>Downloading `/last-example/file4.html' to file4.html:<br>Progress: [=============================>] 100.0% of 52 bytes succeeded.<br>dav:/last-example/> quit<br>Connection to `127.0.0.1' closed.<br>11:44:59 $<br>11:45:00 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:45:51 $<br>11:45:51 $ tree<br>.<br>├── file4.html<br>├── test-disk1-30mb.ext<br>└── test-disk1-directory<br>    └── last-example<br>        ├── file1.txt<br>        ├── file2.txt<br>        ├── file3.html<br>        └── file4.html<br><br>3 directories, 6 files<br>11:46:11 $<br>11:46:12 $ ls --color=never -alR<br>.:<br>total 30767<br>drwxrwx---  3 root everybody     3488 Apr  7 11:44 .<br>drwxrwx--- 14 root everybody     3488 Apr  7 11:13 ..<br>-rw-rw----  1 root everybody       52 Apr  7 11:44 file4.html<br>-rw-rw----  1 root everybody 31457280 Apr  7 11:42 test-disk1-30mb.ext<br>drwxrwx---  3 root everybody     3488 Apr  7 11:39 test-disk1-directory<br><br>./test-disk1-directory:<br>total 11<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:39 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:44 ..<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:38 last-example<br><br>./test-disk1-directory/last-example:<br>total 11<br>drwxrwx--- 2 root everybody 3488 Apr  7 11:38 .<br>drwxrwx--- 3 root everybody 3488 Apr  7 11:39 ..<br>-rw-rw---- 1 root everybody    0 Apr  7 11:18 file1.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:38 file2.txt<br>-rw-rw---- 1 root everybody    0 Apr  7 11:31 file3.html<br>-rw-rw---- 1 root everybody   52 Apr  7 11:34 file4.html<br>11:46:37 $<br>11:46:38 $ sha256sum file4.html<br>832da14690c20076c46153432f4692dcf7517641eb7ef92bc1ce1aa66db21bba  file4.html<br>11:47:14 $<br>11:47:14 $ sha256sum test-disk1-directory/last-example/file4.html<br>832da14690c20076c46153432f4692dcf7517641eb7ef92bc1ce1aa66db21bba  test-disk1-directory/last-example/file4.html<br>11:47:32 $<br>11:47:37 $ cmp --verbose file4.html test-disk1-directory/last-example/file4.html<br>11:47:57 $<br>11:47:58 $ links -dump<br>URL expected after -dump<br>11:48:17 $<br>11:48:19 $ links -dump http://127.0.0.1:8181/last-example/file4.html<br>                                   file4.html<br>11:48:41 $<br>11:48:42 $<br>11:49:04 $<br>11:49:04 $ links -source http://127.0.0.1:8181/last-example/file4.html<br>&lt;html&gt;<br>&lt;body&gt;<br>&lt;h1&gt;<br>file4.html<br>&lt;/h1&gt;<br>&lt;/body&gt;<br>&lt;/html&gt;<br>11:49:07 $<br>11:49:08 $ cd /storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:49:28 $<br>11:49:29 $ rm -iv --recursive test-disk1-directory    # "man rm"<br>rm: descend into directory 'test-disk1-directory'? y<br>rm: descend into directory 'test-disk1-directory/last-example'? y<br>rm: remove regular empty file 'test-disk1-directory/last-example/file3.html'? y<br>removed 'test-disk1-directory/last-example/file3.html'<br>rm: remove regular file 'test-disk1-directory/last-example/file4.html'? y<br>removed 'test-disk1-directory/last-example/file4.html'<br>rm: remove regular empty file 'test-disk1-directory/last-example/file1.txt'? y<br>removed 'test-disk1-directory/last-example/file1.txt'<br>rm: remove regular empty file 'test-disk1-directory/last-example/file2.txt'? y<br>removed 'test-disk1-directory/last-example/file2.txt'<br>rm: remove directory 'test-disk1-directory/last-example'? y<br>removed directory 'test-disk1-directory/last-example'<br>rm: remove directory 'test-disk1-directory'? y<br>removed directory 'test-disk1-directory'<br>11:50:10 $<br>11:50:13 $ pwd<br>/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>11:50:28 $<br>11:50:29 $ cd<br>11:51:01 $<br>11:51:01 $ pwd<br>/data/data/com.termux/files/home<br>11:51:18 $<br>11:51:19 $ rm -ivr /storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB<br>rm: descend into directory '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB'? y<br>rm: remove regular file '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/test-disk1-30mb.ext'? y<br>removed '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/test-disk1-30mb.ext'<br>rm: remove regular file '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/file4.html'? y<br>removed '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB/file4.html'<br>rm: remove directory '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB'? y<br>removed directory '/storage/emulated/0/Download/ext4-test-directory.B7AjMjt8aB'<br>11:52:10 $<br>11:55:28 $<br</pre></td>
</tr>
</table>

---

<p><br></p>

### Reference Links

1. Linux ext4 filesystem: "Filesystems in the Linux kernel": https://docs.kernel.org/filesystems/index.html , https://docs.kernel.org/filesystems/ext4/index.html ("ext4 Data Structures and Algorithms"), https://www.cyberciti.biz/faq/linux-modify-partition-labels-command-to-change-diskname/ ("Linux Change Disk Label Name on EXT2 / EXT3 / EXT4 File Systems"), https://www.redhat.com/sysadmin/disk-space ("Linux sysadmins want to know: Where did my disk space go?")
2. "What sysadmins need to know about using Bash": https://www.redhat.com/sysadmin/bash-navigation
2. "10 basic Linux commands you need to know": https://www.redhat.com/sysadmin/basic-linux-commands
2. "8 fundamental Linux file-management commands for new users": https://www.redhat.com/sysadmin/linux-file-management-commands
2. "8 essential Linux file navigation commands for new users": https://www.redhat.com/sysadmin/Linux-file-navigation-commands
2. "Basic Linux commands and tools every sysadmin should know": https://clockhash.com/blog/basic-linux-commands-and-tools-every-sysadmin-should-know
2. bash: https://www.gnu.org/software/bash/manual/bash.html ("Bash Reference Manual"), https://www.redhat.com/sysadmin/linux-environment-variables ("Linux environment variable tips and tricks"), https://www.redhat.com/sysadmin/scripting-writing-text-file ("Bash scripting: How to write data to text files"), https://www.redhat.com/sysadmin/pipes-command-line-linux ("Working with pipes on the Linux command line"), https://linuxhint.com/linux-pipe-command-examples/ ("Linux Pipe Command with Examples"), https://www.redhat.com/sysadmin/linux-shell-redirection-pipelining ("How to manipulate files with shell redirection and pipelines in Linux"), https://www.redhat.com/sysadmin/redirect-shell-command-script-output ("How to redirect shell command output"), https://www.redhat.com/sysadmin/history-command ("How to manage your Linux command history"), https://www.redhat.com/sysadmin/parsing-bash-history ("Parsing Bash history in Linux"), https://wiki.bash-hackers.org
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. "The Linux man-pages project": https://www.kernel.org/doc/man-pages/ , https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/book/
2. "How to find out what a Linux command does": https://www.redhat.com/sysadmin/linux-command-documentation
2. Linux 'tree" and "ls" commands: https://www.cyberciti.biz/faq/linux-show-directory-structure-command-line/ ("Linux see directory tree structure using tree command"), https://www.redhat.com/sysadmin/ls-command-options ("Sysadmin tools: 11 ways to use the ls command in Linux"), https://www.redhat.com/sysadmin/Linux-file-navigation-commands ("8 essential Linux file navigation commands for new users")
2. "How to Use the less, more, and most Commands to Read Text Files in Linux": https://www.makeuseof.com/use-less-more-and-most-linux-commands/
2. Linux text editor "nano": https://www.redhat.com/sysadmin/getting-started-nano ("Getting started with Nano")
2. Linux text editors "vi", "vim", "ed": https://www.redhat.com/sysadmin/get-started-vi-editor ("How to get started with the Vi editor"), https://www.redhat.com/sysadmin/introduction-vi-editor ("An introduction to the vi editor"), https://www.redhat.com/sysadmin/beginners-guide-vim ("Linux basics: A beginner's guide to text editing with vim"), https://www.redhat.com/sysadmin/vim-commands ("Vim: Basic and intermediate commands"), https://www.redhat.com/sysadmin/introduction-ed-editor ("How to get started with the ed text editor")
2. Linux web browswer "links": http://links.twibright.com , http://links.twibright.com/download.php ("Documentation"), https://www.tecmint.com/command-line-web-browsers/ ("A Command Line Web Browsing with Lynx and Links Tools")
2. Linux "grep" command: https://www.redhat.com/sysadmin/find-text-files-using-grep ("Find text in files using the Linux grep command")
2. Linux "echo" command: https://phoenixnap.com/kb/echo-command-linux ("Echo Command in Linux (With Examples)"), https://www.tecmint.com/echo-command-in-linux/ ("15 Practical Examples of ‘echo’ command in Linux"), 
2. Linux "find" command: https://www.redhat.com/sysadmin/linux-find-command ("10 ways to use the Linux find command"), : https://www.redhat.com/sysadmin/find-best-friend ("When it comes to Linux system troubleshooting, find is my best friend")
2. Regular expressions (regex): https://www.redhat.com/sysadmin/introducing-regular-expressions ("Introducing regular expressions"), https://www.redhat.com/sysadmin/getting-started-regular-expressions-example ("Getting started with regular expressions: An example"), https://www.redhat.com/sysadmin/regex-grep-data-flow ("Regex and grep: Data flow and building blocks"), https://www.redhat.com/sysadmin/regular-expressions-pulling-it-all-together ("Regular expressions: Pulling it all together"), https://opensource.com/article/18/5/getting-started-regular-expressions ("Getting started with regular expressions")
2. Linux "chmod" command: https://www.redhat.com/sysadmin/linux-file-permissions-xplained ("Linux file permissions explained"), https://www.redhat.com/sysadmin/introduction-chmod ("Linux permissions: An introduction to chmod"), https://www.redhat.com/sysadmin/manage-permissions ("How to manage Linux permissions for users, groups, and others"), https://www.redhat.com/sysadmin/linux-permissions ("What sysadmins need to know about Linux permissions")
2. Linux "bc" command: https://www.gnu.org/software/bc/manual/html_mono/bc.html ("bc" "an arbitrary precision calculator language"), https://linuxconfig.org/bc ("bc command in Linux with examples"), https://web.archive.org/web/20211207113205/docstore.mik.ua/orelly/unix/upt/ch49_03.htm ("Chapter 49 Working with Numbers" "49.3 Gotchas in Base Conversion"), https://www.networkworld.com/article/3681079/converting-numbers-on-linux-among-decimal-hexadecimal-octal-and-binary.html ("Converting numbers on Linux among decimal, hexadecimal, octal, and binary"), https://www.theunixschool.com/2011/05/bc-unix-calculator.html ("bc - Unix calculator"),  https://www.real-world-systems.com/docs/bc.1.html ("bc" "arbitrary precision calculator"), http://www.physics.smu.edu/coan/linux/bc.html ("6. (Very) Brief intro to bc")
2. Linux "apt" command: https://linuxhint.com/debian_sources-list/ ("Understanding and Using Debian sources.list"), https://wiki.debian.org/SourcesList ("Configuring Apt Sources")
2. Web-based Distributed Authoring and Versioning (WebDAV), Linux command "cadaver": http://www.webdav.org , https://docs.vscentrum.be/en/latest/data/cadaver_client_access.html ("Cadaver Client Access"), https://github.com/hpcloud/swift-webdav/blob/master/doc/Cadaver.md ("Using the Cadaver WebDAV Client"). https://help.webpal.net/apis/webdav ("WebPal Resources for Editors, Admins, Collaborators and Coders" "WebDAV Interface")
2. Check the apps: https://www.virustotal.com/gui/home/url ("OPSWAT. MetaDefender Cloud"), https://metadefender.opswat.com ("VirusTotal")

<p><br></p>

### Additional Installed Software
- Apk Analyzer (Martin Styk, sk.styk.martin.apkanalyzer): https://github.com/MartinStyk/AndroidApkAnalyzer ([@MartinStyk](https://github.com/MartinStyk)), https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer
- Chmod calculator (Bonaventura Novellino, com.chmod.calc.o): https://play.google.com/store/apps/details?id=com.chmod.calc.o
- Device Info HW (Andrey Efremov, ru.andr7e.deviceinfohw): https://play.google.com/store/apps/details?id=ru.andr7e.deviceinfohw
- Files (Marc apps & software, com.marc.files): https://play.google.com/store/apps/details?id=com.marc.files
- Firefox Beta: (mozilla-mobile. org.mozilla.firefox_beta): https://github.com/mozilla-mobile/firefox-android ([@mozilla-mobile](https://github.com/mozilla-mobile)), https://www.mozilla.org/en-US/firefox/browsers/mobile/
- Hash Droid (Hobby One, com.hobbyone.HashDroid): https://f-droid.org/en/packages/com.hobbyone.HashDroid/ , https://github.com/HobbyOneDroid/HashDroid ([@HobbyOneDroid](https://github.com/HobbyOneDroid)), https://play.google.com/store/apps/details?id=com.hobbyone.HashDroid
- Material Files (Hai Zhang, me.zhanghai.android.files): https://github.com/zhanghai/MaterialFiles ([@zhanghai](https://github.com/zhanghai)), https://play.google.com/store/apps/details?id=me.zhanghai.android.files
- MiX Image (Hootan Parsa, com.mixplorer.addon.image): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- MiX PDF (Hootan Parsa, com.mixplorer.addon.pdf): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- Primitive FTPd (wolpi, org.primftpd): https://github.com/wolpi/prim-ftpd ([@wolpi](https://github.com/wolpi)), https://play.google.com/store/apps/details?id=org.primftpd
- RealCalc Scientific Calculator (Quartic Software, uk.co.nickfines.RealCalc): https://play.google.com/store/apps/details?id=uk.co.nickfines.RealCalc
- Simple HTTP Server (Phlox Development, com.phlox.simpleserver): https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- Termux:GUI (termux, com.termux.gui): https://github.com/termux/termux-gui ([@termux](https://github.com/termux)), https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- USB Device Info (Alexandros Schillings, aws.apps.usbDeviceEnumerator): https://play.google.com/store/apps/details?id=aws.apps.usbDeviceEnumerator


---
---
---


<a id="NoteAfterNote-2"></a><h3 align="center">NoteAfterNote-2<br>Termux And The ext4 Filesystem, Part 2 Of 5: QEMU, A Guest Operating System, And darkhttpd<br>Published: April 7, 2023<br>Link: https://gist.github.com/NoteAfterNote/f5bd5e127d0768cb4eac53fb7729d29f</h3>


<p><br></p>

### Mobile Device Configuration
   - Rooted: No
   - Connected to any network: No
   - Operating system: 

         neofetch --stdout|grep --color=never --ignore-case 'os:'
            OS: Android 11 armv7l 
   - CPU:

         neofetch --stdout|grep --color=never --ignore-case 'cpu:'
            CPU: MT6761V/WAB (4) @ 2.001GHz 
   - Display resolution: 1440x720
   - Builtin internal storage: 32 Gigabytes
   - Builtin memory: 3 Gigabytes
   - Application Binary Interface (ABI): armeabi-v7a, 32-bit
   - Linux shell: bash (Bourne Again SHell)
   - Termux wake lock: Always enable
   - Termux packages installed: qemu-system-x86-64 qemu-utils  manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate
   - "Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required": https://gist.github.com/NoteAfterNote/2558deec94bac7ec9fa58aa5ad5e9d1b , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))

<p><br></p>

Guest Operating System Installation
- Read "Alpine User Handbook": https://docs.alpinelinux.org/user-handbook/0.1a/index.html
- From https://alpinelinux.org download the "Virtual" "x86_64" files: https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso , https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso.sha256
- Alpine Linux Wiki: https://wiki.alpinelinux.org
- "Setting up disks manually": https://wiki.alpinelinux.org/wiki/Setting_up_disks_manually
- "Bootloaders": https://wiki.alpinelinux.org/wiki/Bootloaders


<p><br></p>


Do Know
- ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
- Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
- Reset a Termux terminal session at anytime, very useful when lines are truncated while booting: https://wiki.termux.com/wiki/User_Interface ("create new terminal sessions", "specify a session title", "Resetting the terminal"), see https://user-images.githubusercontent.com/21236430/126444437-7570cdcb-e825-4970-97ff-71f41e426b0f.jpg in https://github.com/termux/termux-app/issues/2184#issuecomment-883939230 ("Feature request: termux transcript #2184" "Gameye98 commented on Jul 21, 2021" )

Introduction To Linux System Administration
- Read "4 System Administration": https://tldp.org/LDP/gs/node6.html
- Read "Chapter 1. Getting Started with Linux": https://www.oreilly.com/library/view/practical-linux-system/9781098109028/ch01.html
- Read "Reboot Linux System Command": https://www.cyberciti.biz/faq/howto-reboot-linux/
- "Linux superuser access, explained": https://www.redhat.com/sysadmin/linux-superuser-access
- "Why Do We Use su – and Not Just su?": https://www.baeldung.com/linux/su-command-options
- "Linux command line basics: sudo": https://www.redhat.com/sysadmin/sudo
- "Exploring the differences between sudo and su commands in Linux": https://www.redhat.com/sysadmin/difference-between-sudo-su
- "Using sudo to delegate permissions in Linux": https://www.redhat.com/sysadmin/using-sudo-delegate
- "Real sysadmins don't sudo": https://www.redhat.com/sysadmin/sysadmins-dont-sudo
- "Linux sysadmin basics: User account management": https://www.redhat.com/sysadmin/linux-user-account-management
- "How to create, delete, and modify groups in Linux": https://www.redhat.com/sysadmin/linux-groups (Linux "id" command)
- "Linux sysadmin basics: User account management with UIDs and GIDs": https://www.redhat.com/sysadmin/user-account-gid-uid
- "Managing local group accounts in Linux": https://www.redhat.com/sysadmin/local-group-accounts
- "How to use a command line random password generator PWGEN on Linux": https://linuxconfig.org/how-to-use-a-command-line-random-password-generator-pwgen-on-linux

<p><br></p>

Network Port Numbers
- "Recommendations on Using Assigned Transport Port Numbers": https://www.rfc-editor.org/rfc/rfc7605.html
- "Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry": https://www.rfc-editor.org/rfc/rfc6335 ("the Dynamic Ports, also known as the Private or Ephemeral Ports, from 49152-65535 (never assigned)")
- Linux "shuf" command": https://www.gnu.org/software/coreutils/manual/html_node/shuf-invocation.html
   ````
   shuf --input-range=49152-65535  --head-count=1  --random-source=/dev/urandom --repeat

   shuf -i 49152-65535  -n 1 --random-source=/dev/urandom -r
   ````



<p><br></p>

4GB - 1 = (4*(1\*1024\*1024\*1024)) - 1 = (2^32) - 1 = 4294967295 bytes
- "Working with File Systems": http://web.archive.org/web/20130423054811/technet.microsoft.com/en-us/library/bb457112.aspx ("4 GB minus 1 byte"), "Working with File Systems": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb457112(v=technet.10)
- "How FAT Works": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776720(v=ws.10)

<p><br></p>

QEMU: https://www.qemu.org , https://github.com/qemu/qemu ([@qemu](https://github.com/qemu)), https://www.qemu.org/docs/master/ , https://wiki.qemu.org , https://github.com/qemu/qemu/tree/master/docs
- "Device Emulation": https://www.qemu.org/docs/master/system/device-emulation.html ("Common Terms" "Device Front End" "Device Back End"), https://qemu.readthedocs.io/en/latest/system/device-emulation.html
- "QEMU User Documentation": https://www.qemu.org/docs/master/system/qemu-manpage.html , https://qemu.readthedocs.io/en/latest/system/qemu-manpage.html
- "QEMU Documentation": https://qemu.readthedocs.io/_/downloads/en/latest/pdf/
- https://github.com/qemu/qemu/blob/master/qemu-options.hx
- "QEMU disk image utility": https://www.qemu.org/docs/master/tools/qemu-img.html ("qemu-img create"), https://qemu.readthedocs.io/en/latest/tools/qemu-img.html 


qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3
- "Invocation": https://www.qemu.org/docs/master/system/invocation.html , https://qemu.readthedocs.io/en/latest/system/invocation.html
- "Managing device boot order with bootindex properties": https://www.qemu.org/docs/master/system/bootindex.html , https://qemu.readthedocs.io/en/latest/system/bootindex.html
- "Network emulation": https://www.qemu.org/docs/master/system/devices/net.html ("Using the user mode network stack" "-net user" "The QEMU VM behaves as if it was behind a firewall which blocks all incoming connections."), 
- "Documentation/Networking": https://wiki.qemu.org/Documentation/Networking ("hostfwd")
- "Documentation/9psetup": https://wiki.qemu.org/Documentation/9psetup ("-virtfs"), https://wiki.qemu.org/Documentation/9p
https://wiki.qemu.org/Features/VirtIORNG ("virtio-rng-pci")
- "QEMU command-line: behavior of ‘-serial stdio’ vs. ‘-serial mon:stdio’": https://kashyapc.wordpress.com/2016/02/11/qemu-command-line-behavior-of-serial-stdio-vs-serial-monstdio/ ("-serial mon:stdio")


"QEMU Monitor": https://www.qemu.org/docs/master/system/monitor.html , https://qemu.readthedocs.io/en/latest/system/monitor.html
- "Keys in the character backend multiplexer": https://www.qemu.org/docs/master/system/mux-chardev.html ("Ctrl-a h", "Ctrl-a t", "Ctrl-a c", "Ctrl-a x"), https://qemu.readthedocs.io/en/latest/system/mux-chardev.html
- "Introduction": https://www.qemu.org/docs/master/system/introduction.html ("QEMU provides a number of management interfaces including a line based Human Monitor Protocol (HMP) that allows you to dynamically add and remove devices as well as introspect the system state.")
- "Security": https://www.qemu.org/docs/master/system/security.html ("Monitor console (QMP and HMP)", "The general recommendation is that the monitor console should be exposed over a UNIX domain socket backend to the local host only."), https://qemu.readthedocs.io/en/latest/system/security.html
- "QemuDiskHotplug": https://wiki.ubuntu.com/QemuDiskHotplug and
- "QEMU Human Monitor Interface, Example Usage": https://web.archive.org/web/20180104171638/nairobi-embedded.org/qemu_monitor_console.html ("Nographic Mode")

QEMU HMP Monitor Commands
- Hotplugging disks, if a disk is mounted in the operating system, unmount it before a "device_del"

   ````
   info block

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk1.img,format=raw,id=hd1

   device_add virtio-blk-pci,drive=hd1,id=virt1

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk2.ext,format=raw,id=drive2 

   device_add virtio-blk-pci,drive=drive2,id=virtual2

   ````

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/50gb.ext,format=raw,id=hd3 

   device_add virtio-blk-pci,drive=hd3,id=virtual3

   ````

   ```` 
   device_del virtual3

   device_del virt1

   device_del virtual2

   ````
- QEMU firewall network ports

   ````
   info usernet

   hostfwd_add ::2049-:2049

   info usernet

   hostfwd_remove ::2049

   info usernet

   ````

- Communicate with QEMU through a socket

   ```` 
   echo 'info block' | nc -UN $SOCKET_FILENAME

   ```` 

<p><br></p>

---

<p><br></p>

<a id=qemu-linux-console></a>
### Termux Session 1: [QEMU-Linux-Console](#termux-session-for-qemu-linux-console)

````
cd /storage/emulated/0/Download
sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256
cd $HOME
pwd
ISO=/storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso

# From "Reference Links"
#  "Bash scripting: Moving from backtick operator to $ parentheses": 
#   https://www.redhat.com/sysadmin/backtick-operator-vs-parens
#   
SOCKET_FILENAME=$(mktemp socket.XXXXXXXXXX)
echo $SOCKET_FILENAME

DIRECTORY_NAME_FROM_mktemp=$(mktemp -d /storage/emulated/0/Download/ext4-test-directory.XXXXXXXXXX)
echo $DIRECTORY_NAME_FROM_mktemp

#
# Create the QEMU disk image, file size
# less than 4096 megabytes = 4096*1024*1024 = 4 gigabytes
#
qemu-img create -f raw -o preallocation=full $DIRECTORY_NAME_FROM_mktemp/vmtest1.raw  4095M
VMDISK=$DIRECTORY_NAME_FROM_mktemp/vmtest1.raw

dd if=/dev/zero of=$DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext bs=1M count=30
mkfs.ext4 -m 0 -L disk1-30mb $DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext

pwd
#
# Bootup may take some time. Watch the "QEMU Linux Console"
# Termux session.
#
qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3

#
# Install from the ISO: no password, login as 'root'
# 50gb.ext has the v3.17/main/x86_64 and v3.17/community/x86_64
# repositories.
#
blkid
df -h
mkdir /root/repo
mkdir /root/backup
cat /etc/apk/repositories

cp -pi /etc/apk/repositories /root/backup
echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories

#   mount --help  
#   mount the disk read-only
#   mount LABEL=50gb -o ro,remount /root/repo
#   mount LABEL=50gb -o rw,remount /root/repo
mount
mount -r LABEL=50gb /root/repo
mount|egrep repo
df -aTh
dmesg

apk update
apk add nano cfdisk util-linux e2fsprogs e2fsprogs-extra  grub grub-bios

lsblk
blkid

export EDITOR=nano
export KERNELOPTS="console=tty0 console=ttyS0,115200n8"
env
set
#
# During setup add a username.
# During setup if a pager is presented, type 'h' and 'q'
#
setup-alpine
umount /root/repo
df -ha

# Poweroff the server
poweroff

# Reset the Termux terminal if necessary: "tput reset"
# at the Termux command line or select the Termux session
# reset option.
#
# Booting from the ISO is finished. Change the
# qemu-system-x86_64 option
#     bootindex=1
# to
#     bootindex=100
# and press the Enter/Return key.
#   

qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=100  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3



# If the lines displayed as while booting are truncated use
# the Termux session reset option as the server continues to boot.
#
# Toggle the timestamps: ctrl-a t
# 

#
# When the server completely boots up login as root.
# 

cat /etc/os-release
uname -a
mkdir /root/backup
mkdir /mnt/repo

lsblk
blkid

cp -pi /etc/apk/repositories /root/backup
cat /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories
mount -r LABEL=50gb /mnt/repo
mount
df -ahT

#
# Edit /etc/update-extlinux.conf with nano
#   timeout=0    # man syslinux
#   hidden=0

# grep -E 'timeout|hidden' /etc/update-extlinux.conf
# cp -pi /etc/update-extlinux.conf /root/backup
# nano --linenumbers /etc/update-extlinux.conf
# grep -E 'timeout|hidden' /etc/update-extlinux.conf
#
# Update the settings
update-extlinux

cat /etc/modules ; cp -pi /etc/modules /root/backup
echo fuse >> /etc/modules ; cat /etc/modules

#
# Install the packages
#
apk update
date

apk add vim cryptsetup asciinema neofetch xca polkit qt5-qtwebglplugin rpm cifs-utils device-mapper rng-tools inetutils-telnet perl hdparm fsarchiver libcdio-tools lftp-doc lftp pssh mutt neomutt alpine ncftp vsftpd vsftpd-doc sshfs samba apache2 apache2-doc apache2-webdav apache2-utils apache2-ctl alpine-sdk build-base apk-tools alpine-conf busybox fakeroot syslinux xorriso mtools dosfstools grub-efi make git sudo lynx links nodejs npm dhcp-server-vanilla ccache ccache-doc udisks2 udisks2-doc libarchive-tools libarchive-doc cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc gcc abuild binutils binutils-doc gcc-doc py3-pip pandoc util-linux pciutils usbutils coreutils binutils findutils grep iproute2 bash bash-doc utmps pass pass-otp darkhttpd libpwquality zstd pwgen easy-rsa  markdown expect sshpass keepassxc gzip rpm xz bzip2 gawk bc diffutils psmisc procps shadow util-linux-bash-completion util-linux-login mount umount netcat-openbsd nmap nmap-nping nmap-nselibs nmap-scripts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix gptfdisk sgdisk parted grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosfstools texinfo e2fsprogs  e2fsprogs-extra mkinitfs haveged davfs2 f2fs-tools jfsutils ntfs-3g xfsprogs cpio whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils fuse-exfat-doc nfs-utils ncurses ffmpeg sharutils mandoc man-pages mandoc-apropos docs virt-manager libvirt libvirt-daemon imagemagick spice spice-vdagent spice-gtk xf86-video-qxl qemu-guest-agent cmd:rsvg-convert iptables ip6tables perl-net-ssleay progress pv stress-ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plugins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vifm-zsh-completion  vifm-bash-completion  fish ncdu zsh udisks2-bash-completion gnome-disk-utility zim chezdav grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsql apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate

date

#
# Change the shell
#
echo $SHELL
chsh -s /bin/bash root
chsh -s /bin/bash USER_NAME_FROM_SETUP_ALPINE

# Logout and then login as root.

echo $SHELL

export SUDO_EDITOR=nano
export EDITOR=nano

# cp -pi /etc/sudoers /root/backup
# grep wheel /etc/sudoers
## Uncomment the wheel line
# sudoedit /etc/sudoers
grep wheel /etc/sudoers


#
# Reboot the server
#
# Toggle the console timestamps: ctrl-a t
#
reboot

#
# Copy the SOCKET_FILENAME from the QEMU-LINUX-CONSOLE session
# Copy the DIRECTORY_NAME_FROM_mktemp from QEMU-LINUX-CONSOLE 
# After the server boots up switch to the Termux-Command-Line
# session and 
#     SOCKET_FILENAME=PASTE_SOCKET_FILENAME_HERE
#     DIRECTORY_NAME_FROM_mktemp=PASTE_DIRECTORY_NAME_FROM_mktemp_HERE 

````
<p><br></p>

<a id="termux-command-line"></a>
### Termux Session 2: [Termux-Command-Line](#termux-session-for-termux-command-line)

````
SOCKET_FILENAME=PASTE_SOCKET_FILENAME_HERE
echo $SOCKET_FILENAME
DIRECTORY_NAME_FROM_mktemp=PASTE_DIRECTORY_NAME_FROM_mktemp_HERE
echo $DIRECTORY_NAME_FROM_mktemp

#
echo 'info usernet' | nc -UN $SOCKET_FILENAME 

#
# Hotplug test-disk1-30mb.ext
#
echo 'info block'  | nc -UN $SOCKET_FILENAME 

echo "drive_add 0 if=none,file=$DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext,format=raw,id=disk1" | nc -UN $SOCKET_FILENAME

echo 'device_add virtio-blk-pci,drive=disk1,id=virt1' | nc -UN $SOCKET_FILENAME 

# Status
echo 'info block'  | nc -UN $SOCKET_FILENAME  
echo 'info block'  | nc -UN $SOCKET_FILENAME 

ssh USER_NAME_FROM_SETUP_ALPINE@127.0.0.1 -p 15022

blkid
lsblk
blkid|grep disk1-30mb
sudo mkdir /mnt/disk1
sudo mount LABEL=disk1-30mb /mnt/disk1
df -aTh

# 
# Set the sticky bit
#
sudo chmod a+rwx,o+t /mnt/disk1
stat /mnt/disk1|grep 'rwx'
# Compare with /tmp
stat /tmp|grep 'rwx'

ls -laR /mnt/disk1

touch /mnt/disk1/file1-made-on-server
touch /mnt/disk1/file2-made-on-server

pwd

# Exit the ssh session
#   logout
# Now back at the Termux command line
pwd


# From Termux, store a file on test-disk1-30mb.ext
#
# Commands for sftp:
#    cd /mnt/disk1
#    ls -l
#    put /data/data/com.termux/files/usr/bin/termux-info
#    ls -l
#    quit

whereis termux-info
sftp -P 15022 USER_NAME_FROM_SETUP_ALPINE@127.0.0.1


#
# Start an HTTP server with a random port number
#
export TERMUX_RANDOM_PORT=$(shuf --input-range=49152-65535  --head-count=1  --random-source=/dev/urandom --repeat)
echo $TERMUX_RANDOM_PORT

darkhttpd $DIRECTORY_NAME_FROM_mktemp --port $TERMUX_RANDOM_PORT

#
# Switch to the QEMU-LINUX-CONSOLE session and login as
#  USER_NAME_FROM_SETUP_ALPINE
# type
#    links -dump http://10.0.2.2:TERMUX_RANDOM_PORT
# type
#    exit
# and return to the Termux-Command-Line session
#

# At the Termux-Command-Line use ctrl-c to stop darkhttpd


ssh USERNAME_FROM_SETUP_ALPINE@127.0.0.1 -p 15022

sudo umount /mnt/disk1
exit

#
# Back at the Termux command line
#

echo 'info block'  | nc -UN $SOCKET_FILENAME 

echo 'device_del virt1' | nc -UN $SOCKET_FILENAME
echo 'info block'  | nc -UN $SOCKET_FILENAME 
echo 'info block'  | nc -UN $SOCKET_FILENAME 

# Watch the QEMU-Linux-Console session

echo 'system_powerdown'  | nc -UN $SOCKET_FILENAME 

````




<p><br></p>

<a id="termux-session-for-qemu-linux-console"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#qemu-linux-console">QEMU-Linux-Console</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ cd /storage/emulated/0/Download<br>.../0/Download $<br>.../0/Download $ sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256<br>alpine-virt-3.17.3-x86_64.iso: OK<br>.../0/Download $<br>.../0/Download $ cd $HOME<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ ISO=/storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso<br>~ $<br>~ $ SOCKET_FILENAME=$(mktemp socket.XXXXXXXXXX)<br>~ $ echo $SOCKET_FILENAME<br>socket.PAym3eQVJq<br>~ $<br>~ $<br>~ $ DIRECTORY_NAME_FROM_mktemp=$(mktemp -d /storage/emulated/0/Download/ext4-test-directory.XXXXXXXXXX)<br>~ $<br>~ $ echo $DIRECTORY_NAME_FROM_mktemp<br>/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C<br>~ $<br>~ $ qemu-img create -f raw -o preallocation=full $DIRECTORY_NAME_FROM_mktemp/vmtest1.raw  4095M<br>Formatting '/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw', fmt=raw size=4293918720 preallocation=full<br>~ $<br>~ $ VMDISK=$DIRECTORY_NAME_FROM_mktemp/vmtest1.raw<br>~ $<br>~ $ dd if=/dev/zero of=$DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext bs=1M count=30<br>30+0 records in<br>30+0 records out<br>31457280 bytes (31 MB, 30 MiB) copied, 0.358727 s, 87.7 MB/s<br>~ $<br>~ $ mkfs.ext4 -m 0 -L disk1-30mb $DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext<br>mke2fs 1.47.0 (5-Feb-2023)<br>/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/test-disk1-30mb.ext contains a ext2 file system labelled 'disk1-30mb'<br>        created on Fri Apr  7 07:42:16 2023<br>Proceed anyway? (y,N) y<br>Creating filesystem with 30720 1k blocks and 7680 inodes              <br>Filesystem UUID: 00781ac1-ab37-4b36-abac-5ef4b9f4c990<br>Superblock backups stored on blocks:<br>        8193, 24577<br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (1024 blocks): done                                  <br>Writing superblocks and<br>filesystem accounting information: done<br>~ $<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3<br><br><br>OpenRC 0.45.2 is starting up Linux 5.15.104-0-virt (x86_64)<br><br> * /proc is already mounted<br> * Mounting /run ... * /run/openrc: creating directory<br> * /run/lock: creating directory<br> * /run/lock: correcting owner                                   * Caching service dependencies ... [ ok ]<br> * Remounting devtmpfs on /dev ... [ ok ]<br> * Mounting /dev/mqueue ... [ ok ]<br> * Mounting modloop  ... * Verifying modloop<br> [ ok ]<br> * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]                          * Mounting persistent storage (pstore) filesystem ... [ ok ]    * Starting busybox mdev ... [ ok ]                              * Scanning hardware for mdev ... [ ok ]                         * Loading hardware drivers ... [ ok ]                           * Loading modules ... [ ok ]                                    * Setting system clock using the hardware clock [UTC] ... [ ok ]                                                                * Checking local filesystems  ... [ ok ]                        * Remounting filesystems ... [ ok ]                             * Mounting local filesystems ... [ ok ]<br> * Configuring kernel parameters ... [ ok ]<br> * Migrating /var/lock to /run/lock ... [ ok ]<br> * Creating user login records ... [ ok ]<br> * Cleaning /tmp directory ... [ ok ]<br> * Setting hostname ... [ ok ]<br> * Starting busybox syslog ... [ ok ]<br> * Starting firstboot ... [ ok ]<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.104-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~# blkid<br>/dev/loop/0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" TYPE="ext4"<br>/dev/vda2: TYPE="vfat"<br>/dev/vda1: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/vda: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/loop0: TYPE="squashfs"<br>localhost:~#<br>localhost:~# df -h<br>Filesystem                Size      Used Available Use% Mounted on<br>devtmpfs                 10.0M         0     10.0M   0% /dev<br>shm                     491.6M         0    491.6M   0% /dev/shm<br>/dev/vda                 49.0M     49.0M         0 100% /media/vda<br>tmpfs                   491.6M     10.4M    481.2M   2% /<br>tmpfs                   196.6M     44.0K    196.6M   0% /run<br>/dev/loop0               14.1M     14.1M         0 100% /.modloop<br>localhost:~# mkdir /root/repo<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>localhost:~#<br>localhost:~# cp -pi /etc/apk/repositories /root/backup<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>/root/repo/alpine/v3.17/main<br>/root/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124313,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vda on /media/vda type iso9660 (ro,relatime,nojoliet,check=s,map=n,blocksize=2048,iocharset=utf8)<br>tmpfs on / type tmpfs (rw,relatime,mode=755,inode64)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201340k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>/dev/loop0 on /.modloop type squashfs (ro,relatime,errors=continue)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>tracefs on /sys/kernel/debug/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /root/repo<br>localhost:~#<br>localhost:~# mount|egrep repo<br>/dev/vdc on /root/repo type ext4 (ro,relatime)<br>localhost:~#<br>localhost:~# df -aTh<br>Filesystem           Type            Size      Used Available Use% Mounted on<br>sysfs                sysfs              0         0         0   0% /sys<br>devtmpfs             devtmpfs       10.0M         0     10.0M   0% /dev<br>proc                 proc               0         0         0   0% /proc<br>devpts               devpts             0         0         0   0% /dev/pts<br>shm                  tmpfs         491.6M         0    491.6M   0% /dev/shm<br>/dev/vda             iso9660        49.0M     49.0M         0 100% /media/vda<br>tmpfs                tmpfs         491.6M     10.4M    481.1M   2% /<br>tmpfs                tmpfs         196.6M     44.0K    196.6M   0% /run<br>mqueue               mqueue             0         0         0   0% /dev/mqueue<br>/dev/loop0           squashfs       14.1M     14.1M         0 100% /.modloop<br>securityfs           securityfs         0         0         0   0% /sys/kernel/security<br>debugfs              debugfs            0         0         0   0% /sys/kernel/debug<br>pstore               pstore             0         0         0   0% /sys/fs/pstore<br>tracefs              tracefs            0         0         0   0% /sys/kernel/debug/tracing<br>/dev/vdc             ext4           48.9G     44.2G      4.7G  90% /root/repo<br>localhost:~# dmesg<br>[    0.000000] Linux version 5.15.104-0-virt (buildozer@build-3-17-x86_64) (gcc (Alpine 12.2.1_git20220924-r4) 12.2.1 20220924, GNU ld (GNU Binutils) 2.39) #1-Alpine SMP Thu, 23 Mar 2023 08:39:35 +0000<br>[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-virt modules=loop,squashfs,sd-mod,usb-storage quiet console=tty0 console=ttyS0,115200 initrd=/boot/initramfs-virt<br>[    0.000000] x86/fpu: x87 FPU will use FXSAVE<br>[    0.000000] signal: max sigframe size: 1440<br>[    0.000000] BIOS-provided physical RAM map:<br>[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable<br>[    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000003ffd6fff] usable<br>[    0.000000] BIOS-e820: [mem 0x000000003ffd7000-0x000000003fffffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x000000fd00000000-0x000000ffffffffff] reserved<br>[    0.000000] NX (Execute Disable) protection: active<br>[    0.000000] SMBIOS 2.8 present.<br>[    0.000000] DMI: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.16.1-0-g3208b098f51a-prebuilt.qemu.org 04/01/2014<br>[    0.000000] tsc: Fast TSC calibration failed<br>[    0.000000] e820: update [mem 0x00000000-0x00000fff] usable ==> reserved<br>[    0.000000] e820: remove [mem 0x000a0000-0x000fffff] usable<br>[    0.000000] last_pfn = 0x3ffd7 max_arch_pfn = 0x400000000<br>[    0.000000] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT<br>[    0.000000] RAMDISK: [mem 0x3f8c0000-0x3ffd6fff]<br>[    0.000000] ACPI: Early table checksum verification disabled<br>[    0.000000] ACPI: RSDP 0x00000000000F5A00 000014 (v00 BOCHS )<br>[    0.000000] ACPI: RSDT 0x000000003FFE1BDD 000034 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: FACP 0x000000003FFE1A79 000074 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: DSDT 0x000000003FFE0040 001A39 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: FACS 0x000000003FFE0000 000040<br>[    0.000000] ACPI: APIC 0x000000003FFE1AED 000090 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: HPET 0x000000003FFE1B7D 000038 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: WAET 0x000000003FFE1BB5 000028 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: Reserving FACP table memory at [mem 0x3ffe1a79-0x3ffe1aec]<br>[    0.000000] ACPI: Reserving DSDT table memory at [mem 0x3ffe0040-0x3ffe1a78]<br>[    0.000000] ACPI: Reserving FACS table memory at [mem 0x3ffe0000-0x3ffe003f]<br>[    0.000000] ACPI: Reserving APIC table memory at [mem 0x3ffe1aed-0x3ffe1b7c]<br>[    0.000000] ACPI: Reserving HPET table memory at [mem 0x3ffe1b7d-0x3ffe1bb4]<br>[    0.000000] ACPI: Reserving WAET table memory at [mem 0x3ffe1bb5-0x3ffe1bdc]<br>[    0.000000] Zone ranges:<br>[    0.000000]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]<br>[    0.000000]   DMA32    [mem 0x0000000001000000-0x000000003ffd6fff]<br>[    0.000000]   Normal   empty<br>[    0.000000] Movable zone start for each node<br>[    0.000000] Early memory node ranges<br>[    0.000000]   node   0: [mem 0x0000000000001000-0x000000000009efff]<br>[    0.000000]   node   0: [mem 0x0000000000100000-0x000000003ffd6fff]<br>[    0.000000] Initmem setup node 0 [mem 0x0000000000001000-0x000000003ffd6fff]<br>[    0.000000] On node 0, zone DMA: 1 pages in unavailable ranges<br>[    0.000000] On node 0, zone DMA: 97 pages in unavailable ranges<br>[    0.000000] On node 0, zone DMA32: 41 pages in unavailable ranges<br>[    0.000000] ACPI: PM-Timer IO Port: 0x608<br>[    0.000000] ACPI: LAPIC_NMI (acpi_id[0xff] dfl dfl lint[0x1])<br>[    0.000000] IOAPIC[0]: apic_id 0, version 32, address 0xfec00000, GSI 0-23<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 5 global_irq 5 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 10 global_irq 10 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 11 global_irq 11 high level)<br>[    0.000000] ACPI: Using ACPI (MADT) for SMP configuration information<br>[    0.000000] ACPI: HPET id: 0x8086a201 base: 0xfed00000<br>[    0.000000] smpboot: Allowing 4 CPUs, 0 hotplug CPUs<br>[    0.000000] [mem 0x40000000-0xfffbffff] available for PCI devices<br>[    0.000000] Booting paravirtualized kernel on bare hardware<br>[    0.000000] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[    0.000000] setup_percpu: NR_CPUS:256 nr_cpumask_bits:256 nr_cpu_ids:4 nr_node_ids:1<br>[    0.000000] percpu: Embedded 54 pages/cpu s183896 r8192 d29096 u524288<br>[    0.000000] pcpu-alloc: s183896 r8192 d29096 u524288 alloc=1*2097152<br>[    0.000000] pcpu-alloc: [0] 0 1 2 3<br>[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 257751<br>[    0.000000] Kernel command line: BOOT_IMAGE=/boot/vmlinuz-virt modules=loop,squashfs,sd-mod,usb-storage quiet console=tty0 console=ttyS0,115200 initrd=/boot/initramfs-virt<br>[    0.000000] Unknown kernel command line parameters "BOOT_IMAGE=/boot/vmlinuz-virt modules=loop,squashfs,sd-mod,usb-storage", will be passed to user space.<br>[    0.000000] printk: log_buf_len individual max cpu contribution: 4096 bytes<br>[    0.000000] printk: log_buf_len total cpu_extra contributions: 12288 bytes<br>[    0.000000] printk: log_buf_len min size: 16384 bytes<br>[    0.000000] printk: log_buf_len: 32768 bytes<br>[    0.000000] printk: early log buf free: 11264(68%)<br>[    0.000000] Dentry cache hash table entries: 131072 (order: 8, 1048576 bytes, linear)<br>[    0.000000] Inode-cache hash table entries: 65536 (order: 7, 524288 bytes, linear)<br>[    0.000000] mem auto-init: stack:byref(zero), heap alloc:on, heap free:off<br>[    0.000000] Memory: 994212K/1048020K available (10246K kernel code, 1191K rwdata, 3028K rodata, 1824K init, 2032K bss, 53548K reserved, 0K cma-reserved)<br>[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1<br>[    0.000000] rcu: Hierarchical RCU implementation.<br>[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.<br>[    0.000000]  Tracing variant of Tasks RCU enabled.<br>[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.<br>[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4<br>[    0.000000] NR_IRQS: 16640, nr_irqs: 456, preallocated irqs: 16<br>[    0.000000] kfence: initialized - using 2097152 bytes for 255 objects at 0x(____ptrval____)-0x(____ptrval____)<br>[    0.000000] Console: colour VGA+ 80x25<br>[    0.000000] printk: console [tty0] enabled<br>[    0.000000] printk: console [ttyS0] enabled<br>[    0.000000] ACPI: Core revision 20210730<br>[    0.000000] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604467 ns<br>[    0.030000] APIC: Switch to symmetric I/O mode setup<br>[    0.080000] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1<br>[    0.160000] tsc: Unable to calibrate against PIT<br>[    0.160000] tsc: using HPET reference calibration<br>[    0.160000] tsc: Detected 1000.013 MHz processor<br>[    0.006275] tsc: Marking TSC unstable due to TSCs unsynchronized<br>[    0.018540] Calibrating delay loop (skipped), value calculated using timer frequency.. 2000.02 BogoMIPS (lpj=10000130)<br>[    0.020585] pid_max: default: 32768 minimum: 301<br>[    0.035592] LSM: Security Framework initializing<br>[    0.054659] landlock: Up and running.<br>[    0.081103] Mount-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[    0.081715] Mountpoint-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[    0.328996] process: using AMD E400 aware idle routine<br>[    0.330818] Last level iTLB entries: 4KB 512, 2MB 255, 4MB 127<br>[    0.331073] Last level dTLB entries: 4KB 512, 2MB 255, 4MB 127, 1GB 0<br>[    0.335242] Spectre V1 : Mitigation: usercopy/swapgs barriers and __user pointer sanitization<br>[    0.337071] Spectre V2 : Mitigation: Retpolines<br>[    0.337462] Spectre V2 : Spectre v2 / SpectreRSB mitigation: Filling RSB on context switch<br>[    0.338352] Spectre V2 : Spectre v2 / SpectreRSB : Filling RSB on VMEXIT<br>[    1.879633] Freeing SMP alternatives memory: 32K<br>[    2.168122] smpboot: CPU0: AMD QEMU Virtual CPU version 2.5+ (family: 0xf, model: 0x6b, stepping: 0x1)<br>[    2.353715] Performance Events: PMU not available due to virtualization, using software events only.<br>[    2.427412] rcu: Hierarchical SRCU implementation.<br>[    2.505961] NMI watchdog: Perf NMI watchdog permanently disabled<br>[    2.559251] smp: Bringing up secondary CPUs ...<br>[    2.602087] x86: Booting SMP configuration:<br>[    2.602656] .... node  #0, CPUs:      #1<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    3.154610]  #2<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    3.565655]  #3<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    4.362039] smp: Brought up 1 node, 4 CPUs<br>[    4.363540] smpboot: Max logical packages: 1<br>[    4.364054] ----------------<br>[    4.364291] | NMI testsuite:<br>[    4.364383] --------------------<br>[    4.364477]   remote IPI:  ok  |<br>[    4.370580]    local IPI:  ok  |<br>[    4.379087] --------------------<br>[    4.379312] Good, all   2 testcases passed! |<br>[    4.379613] ---------------------------------<br>[    4.380425] smpboot: Total of 4 processors activated (3258.28 BogoMIPS)<br>[    4.691835] devtmpfs: initialized<br>[    4.766504] x86/mm: Memory block size: 128MB<br>[    4.869581] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[    4.873276] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)<br>[    5.107819] NET: Registered PF_NETLINK/PF_ROUTE protocol family<br>[    5.151197] audit: initializing netlink subsys (disabled)<br>[    5.191439] audit: type=2000 audit(1680799892.330:1): state=initialized audit_enabled=0 res=1<br>[    5.229742] thermal_sys: Registered thermal governor 'step_wise'<br>[    5.235736] cpuidle: using governor ladder<br>[    5.238233] cpuidle: using governor menu<br>[    5.261021] ACPI: bus type PCI registered<br>[    5.262624] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5<br>[    5.312479] PCI: Using configuration type 1 for base access<br>[    5.341833] mtrr: your CPUs had inconsistent fixed MTRR settings<br>[    5.342181] mtrr: your CPUs had inconsistent variable MTRR settings<br>[    5.342409] mtrr: your CPUs had inconsistent MTRRdefType settings<br>[    5.342526] mtrr: probably your BIOS does not setup all CPUs.<br>[    5.342678] mtrr: corrected configuration.<br>[    5.525096] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.<br>[    5.582142] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages<br>[    6.122622] ACPI: Added _OSI(Module Device)<br>[    6.123410] ACPI: Added _OSI(Processor Device)<br>[    6.124392] ACPI: Added _OSI(3.0 _SCP Extensions)<br>[    6.124557] ACPI: Added _OSI(Processor Aggregator Device)<br>[    6.125642] ACPI: Added _OSI(Linux-Dell-Video)<br>[    6.125794] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)<br>[    6.125881] ACPI: Added _OSI(Linux-HPI-Hybrid-Graphics)<br>[    6.375739] ACPI: 1 ACPI AML tables successfully acquired and loaded<br>[    6.621510] ACPI: Interpreter enabled<br>[    6.635546] ACPI: PM: (supports S0 S3 S5)<br>[    6.636331] ACPI: Using IOAPIC for interrupt routing<br>[    6.644774] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug<br>[    6.666856] ACPI: Enabled 2 GPEs in block 00 to 0F<br>[    7.223144] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-ff])<br>[    7.235054] acpi PNP0A03:00: _OSC: OS supports [ASPM ClockPM Segments MSI HPX-Type3]<br>[    7.244292] acpi PNP0A03:00: fail to add MMCONFIG information, can't access extended PCI configuration space under this bridge.<br>[    7.335740] acpiphp: Slot [3] registered<br>[    7.337659] acpiphp: Slot [4] registered<br>[    7.341262] acpiphp: Slot [5] registered<br>[    7.342784] acpiphp: Slot [6] registered<br>[    7.345248] acpiphp: Slot [7] registered<br>[    7.346997] acpiphp: Slot [8] registered<br>[    7.351931] acpiphp: Slot [9] registered<br>[    7.353435] acpiphp: Slot [10] registered<br>[    7.355714] acpiphp: Slot [11] registered<br>[    7.357751] acpiphp: Slot [12] registered<br>[    7.360673] acpiphp: Slot [13] registered<br>[    7.362131] acpiphp: Slot [14] registered<br>[    7.363478] acpiphp: Slot [15] registered<br>[    7.365760] acpiphp: Slot [16] registered<br>[    7.366960] acpiphp: Slot [17] registered<br>[    7.370171] acpiphp: Slot [18] registered<br>[    7.371714] acpiphp: Slot [19] registered<br>[    7.372909] acpiphp: Slot [20] registered<br>[    7.375421] acpiphp: Slot [21] registered<br>[    7.376716] acpiphp: Slot [22] registered<br>[    7.378586] acpiphp: Slot [23] registered<br>[    7.380145] acpiphp: Slot [24] registered<br>[    7.381789] acpiphp: Slot [25] registered<br>[    7.384314] acpiphp: Slot [26] registered<br>[    7.385621] acpiphp: Slot [27] registered<br>[    7.389526] acpiphp: Slot [28] registered<br>[    7.390954] acpiphp: Slot [29] registered<br>[    7.392406] acpiphp: Slot [30] registered<br>[    7.394807] acpiphp: Slot [31] registered<br>[    7.400627] PCI host bridge to bus 0000:00<br>[    7.403112] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]<br>[    7.405115] pci_bus 0000:00: root bus resource [io  0x0d00-0xffff window]<br>[    7.405361] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]<br>[    7.405908] pci_bus 0000:00: root bus resource [mem 0x40000000-0xfebfffff window]<br>[    7.406017] pci_bus 0000:00: root bus resource [mem 0x100000000-0x17fffffff window]<br>[    7.408349] pci_bus 0000:00: root bus resource [bus 00-ff]<br>[    7.436508] pci 0000:00:00.0: [8086:1237] type 00 class 0x060000<br>[    7.579654] pci 0000:00:01.0: [8086:7000] type 00 class 0x060100<br>[    7.646403] pci 0000:00:01.1: [8086:7010] type 00 class 0x010180<br>[    7.694306] pci 0000:00:01.1: reg 0x20: [io  0xc1c0-0xc1cf]<br>[    7.718978] pci 0000:00:01.1: legacy IDE quirk: reg 0x10: [io  0x01f0-0x01f7]<br>[    7.719532] pci 0000:00:01.1: legacy IDE quirk: reg 0x14: [io  0x03f6]<br>[    7.719961] pci 0000:00:01.1: legacy IDE quirk: reg 0x18: [io  0x0170-0x0177]<br>[    7.720340] pci 0000:00:01.1: legacy IDE quirk: reg 0x1c: [io  0x0376]<br>[    7.744802] pci 0000:00:01.3: [8086:7113] type 00 class 0x068000<br>[    7.750940] pci 0000:00:01.3: quirk: [io  0x0600-0x063f] claimed by PIIX4 ACPI<br>[    7.751692] pci 0000:00:01.3: quirk: [io  0x0700-0x070f] claimed by PIIX4 SMB<br>[    7.772694] pci 0000:00:02.0: [1234:1111] type 00 class 0x030000<br>[    7.785731] pci 0000:00:02.0: reg 0x10: [mem 0xfd000000-0xfdffffff pref]<br>[    7.813947] pci 0000:00:02.0: reg 0x18: [mem 0xfebd0000-0xfebd0fff]<br>[    7.889732] pci 0000:00:02.0: reg 0x30: [mem 0xfebc0000-0xfebcffff pref]<br>[    7.893219] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]<br>[    7.971493] pci 0000:00:03.0: [1af4:1005] type 00 class 0x00ff00<br>[    7.988396] pci 0000:00:03.0: reg 0x10: [io  0xc180-0xc19f]<br>[    8.008429] pci 0000:00:03.0: reg 0x14: [mem 0xfebd1000-0xfebd1fff]<br>[    8.078426] pci 0000:00:03.0: reg 0x20: [mem 0xfe000000-0xfe003fff 64bit pref]<br>[    8.180865] pci 0000:00:04.0: [1af4:1000] type 00 class 0x020000<br>[    8.198416] pci 0000:00:04.0: reg 0x10: [io  0xc1a0-0xc1bf]<br>[    8.218424] pci 0000:00:04.0: reg 0x14: [mem 0xfebd2000-0xfebd2fff]<br>[    8.279518] pci 0000:00:04.0: reg 0x20: [mem 0xfe004000-0xfe007fff 64bit pref]<br>[    8.298443] pci 0000:00:04.0: reg 0x30: [mem 0xfeb80000-0xfebbffff pref]<br>[    8.379584] pci 0000:00:05.0: [1af4:1001] type 00 class 0x010000<br>[    8.388509] pci 0000:00:05.0: reg 0x10: [io  0xc000-0xc07f]<br>[    8.408437] pci 0000:00:05.0: reg 0x14: [mem 0xfebd3000-0xfebd3fff]<br>[    8.458412] pci 0000:00:05.0: reg 0x20: [mem 0xfe008000-0xfe00bfff 64bit pref]<br>[    8.553557] pci 0000:00:06.0: [1af4:1001] type 00 class 0x010000<br>[    8.568467] pci 0000:00:06.0: reg 0x10: [io  0xc080-0xc0ff]<br>[    8.590304] pci 0000:00:06.0: reg 0x14: [mem 0xfebd4000-0xfebd4fff]<br>[    8.648414] pci 0000:00:06.0: reg 0x20: [mem 0xfe00c000-0xfe00ffff 64bit pref]<br>[    8.746813] pci 0000:00:07.0: [1af4:1001] type 00 class 0x010000<br>[    8.758740] pci 0000:00:07.0: reg 0x10: [io  0xc100-0xc17f]<br>[    8.788594] pci 0000:00:07.0: reg 0x14: [mem 0xfebd5000-0xfebd5fff]<br>[    8.848441] pci 0000:00:07.0: reg 0x20: [mem 0xfe010000-0xfe013fff 64bit pref]<br>[    8.947050] pci_bus 0000:00: on NUMA node 0<br>[    9.001769] ACPI: PCI: Interrupt link LNKA configured for IRQ 10<br>[    9.015714] ACPI: PCI: Interrupt link LNKB configured for IRQ 10<br>[    9.024637] ACPI: PCI: Interrupt link LNKC configured for IRQ 11<br>[    9.032861] ACPI: PCI: Interrupt link LNKD configured for IRQ 11<br>[    9.037123] ACPI: PCI: Interrupt link LNKS configured for IRQ 9<br>[    9.109680] iommu: Default domain type: Translated<br>[    9.110289] iommu: DMA domain TLB invalidation policy: lazy mode<br>[    9.157234] SCSI subsystem initialized<br>[    9.179449] libata version 3.00 loaded.<br>[    9.190794] pps_core: LinuxPPS API ver. 1 registered<br>[    9.191157] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it><br>[    9.192791] PTP clock support registered<br>[    9.354636] PCI: Using ACPI for IRQ routing<br>[    9.360335] PCI: pci_cache_line_size set to 64 bytes<br>[    9.369798] e820: reserve RAM buffer [mem 0x0009fc00-0x0009ffff]<br>[    9.372427] e820: reserve RAM buffer [mem 0x3ffd7000-0x3fffffff]<br>[    9.408270] hpet: 3 channels of 0 reserved for per-cpu timers<br>[    9.433536] clocksource: Switched to clocksource hpet<br>[   10.373748] VFS: Disk quotas dquot_6.6.0<br>[   10.376413] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)<br>[   10.417643] pnp: PnP ACPI init<br>[   10.483493] pnp 00:02: [dma 2]<br>[   10.541170] pnp: PnP ACPI: found 6 devices<br>[   11.220238] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns<br>[   11.234820] NET: Registered PF_INET protocol family<br>[   11.255034] IP idents hash table entries: 16384 (order: 5, 131072 bytes, linear)<br>[   11.363178] tcp_listen_portaddr_hash hash table entries: 512 (order: 1, 8192 bytes, linear)<br>[   11.366177] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)<br>[   11.367879] TCP established hash table entries: 8192 (order: 4, 65536 bytes, linear)<br>[   11.374218] TCP bind hash table entries: 8192 (order: 5, 131072 bytes, linear)<br>[   11.376611] TCP: Hash tables configured (established 8192 bind 8192)<br>[   11.396540] UDP hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[   11.401384] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[   11.430604] NET: Registered PF_UNIX/PF_LOCAL protocol family<br>[   11.437890] NET: Registered PF_XDP protocol family<br>[   11.452443] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]<br>[   11.452927] pci_bus 0000:00: resource 5 [io  0x0d00-0xffff window]<br>[   11.453225] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]<br>[   11.453473] pci_bus 0000:00: resource 7 [mem 0x40000000-0xfebfffff window]<br>[   11.453651] pci_bus 0000:00: resource 8 [mem 0x100000000-0x17fffffff window]<br>[   11.466758] pci 0000:00:01.0: PIIX3: Enabling Passive Release<br>[   11.470608] pci 0000:00:00.0: Limiting direct PCI/PCI transfers<br>[   11.472184] pci 0000:00:01.0: Activating ISA DMA hang workarounds<br>[   11.473284] PCI: CLS 0 bytes, default 64<br>[   11.697284] Unpacking initramfs...<br>[   11.721277] Initialise system trusted keyrings<br>[   11.818037] workingset: timestamp_bits=46 max_order=18 bucket_order=0<br>[   12.263197] zbud: loaded<br>[   12.356388] Key type asymmetric registered<br>[   12.357611] Asymmetric key parser 'x509' registered<br>[   12.376125] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)<br>[   12.415387] io scheduler mq-deadline registered<br>[   12.416498] io scheduler kyber registered<br>[   12.435483] io scheduler bfq registered<br>[   12.602904] ERST DBG: ERST support is disabled.<br>[   20.366118] ACPI: \_SB_.LNKC: Enabled at IRQ 11<br>[   21.554843] Freeing initrd memory: 7260K<br>[   24.571219] ACPI: \_SB_.LNKD: Enabled at IRQ 10<br>[   28.105045] ACPI: \_SB_.LNKA: Enabled at IRQ 10<br>[   31.171751] ACPI: \_SB_.LNKB: Enabled at IRQ 11<br>[   34.297639] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled<br>[   34.347174] 00:04: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A<br>[   34.623726] VMware PVSCSI driver - version 1.0.7.0-k<br>[   34.648997] ata_piix 0000:00:01.1: version 2.13<br>[   35.823729] scsi host0: ata_piix<br>[   35.986180] scsi host1: ata_piix<br>[   36.006260] ata1: PATA max MWDMA2 cmd 0x1f0 ctl 0x3f6 bmdma 0xc1c0 irq 14<br>[   36.021773] ata2: PATA max MWDMA2 cmd 0x170 ctl 0x376 bmdma 0xc1c8 irq 15<br>[   36.181742] i8042: PNP: PS/2 Controller [PNP0303:KBD,PNP0f13:MOU] at 0x60,0x64 irq 1,12<br>[   36.295814] serio: i8042 KBD port at 0x60,0x64 irq 1<br>[   36.301707] serio: i8042 AUX port at 0x60,0x64 irq 12<br>[   36.333107] rtc_cmos 00:05: RTC can wake from S4<br>[   36.535064] rtc_cmos 00:05: registered as rtc0<br>[   36.551326] rtc_cmos 00:05: setting system clock to 2023-04-06T16:52:04 UTC (1680799924)<br>[   36.638901] rtc_cmos 00:05: alarms up to one day, y3k, 242 bytes nvram, hpet irqs<br>[   36.694456] ata2.00: ATAPI: QEMU DVD-ROM, 2.5+, max UDMA/100<br>[   36.775584] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input0<br>[   36.779993] gre: GRE over IPv4 demultiplexor driver<br>[   36.864794] Key type dns_resolver registered<br>[   36.883183] IPI shorthand broadcast: enabled<br>[   37.026148] registered taskstats version 1<br>[   37.039447] Loading compiled-in X.509 certificates<br>[   37.392527] scsi 1:0:0:0: CD-ROM            QEMU     QEMU DVD-ROM     2.5+ PQ: 0 ANSI: 5<br>[   38.732225] Loaded X.509 cert 'Build time autogenerated kernel key: 3c033844a69b110094555ad83d635cd49718f78b'<br>[   38.773167] zswap: loaded using pool lzo/zbud<br>[   38.891674] Key type .fscrypt registered<br>[   38.892144] Key type fscrypt-provisioning registered<br>[   38.980760] Unstable clock detected, switching default tracing clock to "global"<br>[   38.980760] If you want to keep using the local clock, then add:<br>[   38.980760]   "trace_clock=local"<br>[   38.980760] on the kernel command line<br>[   39.210609] Freeing unused kernel image (initmem) memory: 1824K<br>[   39.231408] Write protecting the kernel read-only data: 16384k<br>[   39.280296] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[   39.295476] Freeing unused kernel image (rodata/data gap) memory: 1068K<br>[   39.302511] rodata_test: all tests were successful<br>[   39.305890] Run /init as init process<br>[   39.306180]   with arguments:<br>[   39.306352]     /init<br>[   39.306485]   with environment:<br>[   39.306650]     HOME=/<br>[   39.306726]     TERM=linux<br>[   39.306773]     BOOT_IMAGE=/boot/vmlinuz-virt<br>[   39.306830]     modules=loop,squashfs,sd-mod,usb-storage<br>[   41.359704] Alpine Init 3.7.0-r1<br>[   41.472333] Loading boot drivers...<br>[   42.493213] loop: module loaded<br>[   42.686662] squashfs: version 4.0 (2009/01/31) Phillip Lougher<br>[   43.495771] ACPI: bus type USB registered<br>[   43.525075] usbcore: registered new interface driver usbfs<br>[   43.533686] usbcore: registered new interface driver hub<br>[   43.536295] usbcore: registered new device driver usb<br>[   43.732744] usbcore: registered new interface driver usb-storage<br>[   46.474606] Loading boot drivers: ok.<br>[   46.791300] Mounting boot media...<br>[   56.946474] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[   56.950345] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[   57.066922] sr 1:0:0:0: Attached scsi CD-ROM sr0<br>[   59.116946] virtio_blk virtio2: [vda] 100352 512-byte logical blocks (51.4 MB/49.0 MiB)<br>[   59.330607]  vda: vda1 vda2<br>[   59.492082] virtio_blk virtio3: [vdb] 8386560 512-byte logical blocks (4.29 GB/4.00 GiB)<br>[   59.597067] virtio_blk virtio4: [vdc] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[   86.896463] ISO 9660 Extensions: Microsoft Joliet Level 3<br>[   86.964097] ISO 9660 Extensions: RRIP_1991A<br>[  102.646525] EXT4-fs (vdc): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[  103.513149] Mounting boot media: ok.<br>[  107.056503] Installing packages to root filesystem...<br>[  122.138342] Installing packages to root filesystem: ok.<br>[  154.588055] loop0: detected capacity change from 0 to 28768<br>[  206.201556] input: Power Button as /devices/LNXSYSTM:00/LNXPWRBN:00/input/input3<br>[  206.459800] ACPI: button: Power Button [PWRF]<br>[  208.402456] Floppy drive(s): fd0 is 2.88M AMI BIOS<br>[  208.966338] FDC 0 is a S82078B<br>[  221.966532] [drm] Found bochs VGA, ID 0xb0c5.<br>[  221.966978] [drm] Framebuffer size 16384 kB @ 0xfd000000, mmio @ 0xfebd0000.<br>[  222.141178] [drm] Found EDID data blob.<br>[  222.391187] [drm] Initialized bochs-drm 1.0.0 20130925 for 0000:00:02.0 on minor 0<br>[  223.107850] fbcon: bochs-drmdrmfb (fb0) is primary device<br>[  225.004748] Console: switching to colour frame buffer device 160x50<br>[  225.336697] bochs-drm 0000:00:02.0: [drm] fb0: bochs-drmdrmfb frame buffer device<br>[  226.530719] piix4_smbus 0000:00:01.3: SMBus Host Controller at 0x700, revision 0<br>[  230.375244] input: ImExPS/2 Generic Explorer Mouse as /devices/platform/i8042/serio1/input/input4<br>[  230.527012] random: crng init done<br>[  235.935398] mousedev: PS/2 mouse device common for all mice<br>[  260.320049] NET: Registered PF_PACKET protocol family<br>[  262.945293] NET: Registered PF_INET6 protocol family<br>[  263.124834] Segment Routing with IPv6<br>[  263.127286] In-situ OAM (IOAM) with IPv6<br>[  679.073519] FAT-fs (vdc): utf8 is not a recommended IO charset for FAT filesystems, filesystem will be case sensitive!<br>[  679.503792] EXT4-fs (vdc): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>localhost:~#<br>localhost:~# apk update<br>3.17.3 [/media/vda/apks]<br>v3.17.3-33-g63371ce3229 [/root/repo/alpine/v3.17/main]<br>v3.17.3-33-g63371ce3229 [/root/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~#<br>localhost:~# apk add nano cfdisk util-linux e2fsprogs e2fsprogs-extra  grub grub<br>-bios<br>(1/51) Installing libblkid (2.38.1-r1)<br>(2/51) Installing libuuid (2.38.1-r1)<br>(3/51) Installing libfdisk (2.38.1-r1)<br>(4/51) Installing libmount (2.38.1-r1)<br>(5/51) Installing ncurses-terminfo-base (6.3_p20221119-r0)<br>(6/51) Installing ncurses-libs (6.3_p20221119-r0)<br>(7/51) Installing libsmartcols (2.38.1-r1)<br>(8/51) Installing cfdisk (2.38.1-r1)<br>(9/51) Installing libcom_err (1.46.6-r0)<br>(10/51) Installing e2fsprogs-libs (1.46.6-r0)<br>(11/51) Installing e2fsprogs (1.46.6-r0)<br>(12/51) Installing e2fsprogs-extra (1.46.6-r0)<br>(13/51) Installing lddtree (1.26-r3)<br>(14/51) Installing xz-libs (5.2.9-r0)<br>(15/51) Installing zstd-libs (1.5.5-r0)<br>(16/51) Installing kmod (30-r1)<br>(17/51) Installing kmod-openrc (30-r1)<br>(18/51) Installing argon2-libs (20190702-r2)<br>(19/51) Installing device-mapper-libs (2.03.17-r1)<br>(20/51) Installing json-c (0.16-r2)<br>(21/51) Installing cryptsetup-libs (2.5.0-r2)<br>(22/51) Installing kmod-libs (30-r1)<br>(23/51) Installing mkinitfs (3.7.0-r1)<br>Executing mkinitfs-3.7.0-r1.post-install<br>(24/51) Installing grub (2.06-r7)<br>(25/51) Installing grub-bios (2.06-r7)<br>(26/51) Installing nano (7.0-r0)<br>(27/51) Installing util-linux (2.38.1-r1)<br>(28/51) Installing util-linux-misc (2.38.1-r1)<br>(29/51) Installing libeconf (0.4.7-r0)<br>(30/51) Installing linux-pam (1.5.2-r1)<br>(31/51) Installing runuser (2.38.1-r1)<br>(32/51) Installing mount (2.38.1-r1)<br>(33/51) Installing losetup (2.38.1-r1)<br>(34/51) Installing hexdump (2.38.1-r1)<br>(35/51) Installing uuidgen (2.38.1-r1)<br>(36/51) Installing blkid (2.38.1-r1)<br>(37/51) Installing sfdisk (2.38.1-r1)<br>(38/51) Installing mcookie (2.38.1-r1)<br>(39/51) Installing agetty (2.38.1-r1)<br>(40/51) Installing agetty-openrc (0.45.2-r7)<br>(41/51) Installing wipefs (2.38.1-r1)<br>(42/51) Installing umount (2.38.1-r1)<br>(43/51) Installing util-linux-openrc (2.38.1-r1)<br>(44/51) Installing flock (2.38.1-r1)<br>(45/51) Installing lsblk (2.38.1-r1)<br>(46/51) Installing libcap-ng (0.8.3-r1)<br>(47/51) Installing setpriv (2.38.1-r1)<br>(48/51) Installing logger (2.38.1-r1)<br>(49/51) Installing partx (2.38.1-r1)<br>(50/51) Installing fstrim (2.38.1-r1)<br>(51/51) Installing findmnt (2.38.1-r1)<br>Executing busybox-1.35.0-r29.trigger<br>OK: 39 MiB in 77 packages<br>localhost:~#<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>loop0    7:0    0   14M  1 loop /.modloop<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk /media/vda<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0    4G  0 disk<br>vdc    253:32   0   50G  1 disk /root/repo<br>localhost:~#<br>localhost:~# blkid<br><br>/dev/loop0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660" PTUUID="77b851c3" PTTYPE="dos" PARTUUID="77b851c3-01"<br>localhost:~#<br>localhost:~#<br>localhost:~# export EDITOR=nano<br>localhost:~#<br>localhost:~# export KERNELOPTS="console=tty0 console=ttyS0,115200n8"<br>localhost:~#<br>localhost:~# env<br>USER=root<br>SHLVL=1<br>HOME=/root<br>PAGER=less<br>LOGNAME=root<br>TERM=vt100<br>LC_COLLATE=C<br>PATH=/sbin:/usr/sbin:/bin:/usr/bin:/usr/local/sbin:/usr/local/bin<br>LANG=C.UTF-8<br>KERNELOPTS=console=tty0 console=ttyS0,115200n8<br>SHELL=/bin/ash<br>PWD=/root<br>CHARSET=UTF-8<br>EDITOR=nano<br>localhost:~#<br>localhost:~# set<br>BB_ASH_VERSION='1.35.0'<br>CHARSET='UTF-8'<br>EDITOR='nano'<br>FUNCNAME=''<br>HISTFILE='/root/.ash_history'<br>HOME='/root'<br>HOSTNAME='localhost'<br>IFS='<br>'<br>KERNELOPTS='console=tty0 console=ttyS0,115200n8'<br>LANG='C.UTF-8'<br>LC_COLLATE='C'<br>LINENO=''<br>LOGNAME='root'<br>OPTIND='1'<br>PAGER='less'<br>PATH='/sbin:/usr/sbin:/bin:/usr/bin:/usr/local/sbin:/usr/local/bin'<br>PPID='1841'<br>PS1='\h:\w\$ '<br>PS2='> '<br>PS4='+ '<br>PWD='/root'<br>SHELL='/bin/ash'<br>SHLVL='1'<br>TERM='vt100'<br>USER='root'<br>_='env'<br>localhost:~#<br>localhost:~# setup-alpine<br>Enter system hostname (fully qualified form, e.g. 'foo.example.org') [localhost]<br>Available interfaces are: eth0.<br>Enter '?' for help on bridges, bonding and vlans.<br>Which one do you want to initialize? (or '?' or 'done') [eth0]<br>Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp]<br>Do you want to do any manual network configuration? (y/n) [n]<br>udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br>Changing password for root<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for root changed by root<br>Which timezone are you in? ('?' for list) [UTC]<br> * Seeding random number generator ...<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox acpid ...<br> [ ok ]<br> * Starting busybox crond ...<br> [ ok ]<br>HTTP/FTP proxy URL? (e.g. 'http://proxy:8080', or 'none') [none] none<br>Which NTP client to run? ('busybox', 'openntpd', 'chrony' or 'none') [chrony] none<br>wget: bad address 'mirrors.alpinelinux.org'<br>wget: bad address 'mirrors.alpinelinux.org'<br><br><br>r) Add random from the above list<br>f) Detect and add fastest mirror from above list<br>e) Edit /etc/apk/repositories with text editor<br><br>Enter mirror number (1-0) or URL to add (or r/f/e/done) [1] done<br>Setup a user? (enter a lower-case loginname, or 'no') [no] test<br>Full name for user test [test]<br>Changing password for test<br>New password:<br>Bad password: too weak<br>Retype password:<br>Passwords don't match<br>passwd: password for test is unchanged<br>Setup a user? (enter a lower-case loginname, or 'no') [no] test<br>Full name for user test [test]<br>adduser: user 'test' in use<br>Setup a user? (enter a lower-case loginname, or 'no') [no] test1<br>Full name for user test1 [test]<br>Changing password for test1<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for test1 changed by root<br>Enter ssh key or URL for test1 (or 'none') [none]<br>(1/1) Installing doas (6.8.2-r3)<br>Executing doas-6.8.2-r3.post-install<br>Executing busybox-1.35.0-r29.trigger<br>OK: 39 MiB in 78 packages<br>Which ssh server? ('openssh', 'dropbear' or 'none') [openssh]<br> * service sshd added to runlevel default<br> * Caching service dependencies ...<br> [ ok ]<br>ssh-keygen: generating new host keys: RSA ECDSA ED25519<br> * Starting sshd ...<br> [ ok ]<br>Available disks are:<br>  fd0   (0.0 GB  )<br>  sr0   (1.1 GB QEMU     QEMU DVD-ROM    )<br>  vdb   (4.3 GB 0x1af4 )<br>Which disk(s) would you like to use? (or '?' for help or 'none') [none] vdb<br>The following disk is selected:<br>  vdb   (4.3 GB 0x1af4 )<br>How would you like to use it? ('sys', 'data', 'crypt', 'lvm' or '?' for help) [?] sys<br>WARNING: The following disk(s) will be erased:<br>  vdb   (4.3 GB 0x1af4 )<br>WARNING: Erase the above disk(s) and continue? (y/n) [n] y<br>Creating file systems...<br>Installing system on /dev/vdb3:<br>/mnt/boot is device /dev/vdb1<br>100% ████████████████████████████████████████████==> initramfs: creating /boot/initramfs-virt<br>Generating grub configuration file ...<br>Found linux image: /boot/vmlinuz-virt<br>Found initrd image: /boot/initramfs-virt<br>Warning: os-prober will not be executed to detect other bootable partitions.<br>Systems on them will not be added to the GRUB boot configuration.<br>Check GRUB_DISABLE_OS_PROBER documentation entry.<br>done<br>/boot is device /dev/vdb1<br><br>Installation is complete. Please reboot.<br>localhost:~#<br>localhost:~# umount /root/repo<br>localhost:~#<br>localhost:~#<br>localhost:~# df -ha<br>Filesystem                Size      Used Available Use% Mounted on<br>sysfs                        0         0         0   0% /sys<br>devtmpfs                 10.0M         0     10.0M   0% /dev<br>proc                         0         0         0   0% /proc<br>devpts                       0         0         0   0% /dev/pts<br>shm                     491.6M         0    491.6M   0% /dev/shm<br>/dev/vda                 49.0M     49.0M         0 100% /media/vda<br>tmpfs                   491.6M     48.1M    443.5M  10% /<br>tmpfs                   196.6M    108.0K    196.5M   0% /run<br>mqueue                       0         0         0   0% /dev/mqueue<br>/dev/loop0               14.1M     14.1M         0 100% /.modloop<br>securityfs                   0         0         0   0% /sys/kernel/security<br>debugfs                      0         0         0   0% /sys/kernel/debug<br>pstore                       0         0         0   0% /sys/fs/pstore<br>tracefs                      0         0         0   0% /sys/kernel/debug/tracing<br>localhost:~#<br>localhost:~# poweroff<br><br>[   35.624662] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[   35.647140] Freeing unused kernel image (rodata/data gap) memory: 1072K<br>[   35.655957] rodata_test: all tests were successful<br>[   35.664328] Run /init as init process<br>[   37.571506] Alpine Init 3.7.0-r1<br>Alpine Init 3.7.0-r1<br>[   37.672531] Loading boot drivers...<br> * Loading boot drivers: [   39.117523] ACPI: bus type USB registered<br>[   39.156014] usbcore: registered new interface driver usbfs<br>[   39.191910] usbcore: registered new interface driver hub<br>[   39.210113] usbcore: registered new device driver usb<br>[   39.517753] usbcore: registered new interface driver usb-storage<br>[   42.478302] loop: module loaded<br>[   45.900652] Loading boot drivers: ok.<br>ok.<br>[   46.170144] Mounting root...<br> * Mounting root: [   58.228747] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[   58.233471] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[   60.556412] virtio_blk virtio2: [vda] 100352 512-byte logical blocks (51.4 MB/49.0 MiB)<br>[   60.682226]  vda: vda1 vda2<br>[   62.163051] virtio_blk virtio3: [vdb] 8386560 512-byte logical blocks (4.29 GB/4.00 GiB)<br>[   62.591146]  vdb: vdb1 vdb2 vdb3<br>[   62.765667] virtio_blk virtio4: [vdc] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[  105.939318] EXT4-fs (vdb3): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[  106.000159] Mounting root: ok.<br>ok.<br><br>   OpenRC 0.45.2 is starting up Linux 5.15.105-0-virt (x86_64)<br><br> * /proc is already mounted<br> * Mounting /run ... * /run/openrc: creating directory<br> * /run/lock: creating directory<br> * /run/lock: correcting owner<br> * Caching service dependencies ... [ ok ]<br> * Remounting devtmpfs on /dev ... [ ok ]<br> * Mounting /dev/mqueue ... [ ok ]<br> * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]<br> * Mounting persistent storage (pstore) filesystem ... [ ok ]<br> * Starting busybox mdev ... [ ok ]<br> * Scanning hardware for mdev ... [ ok ]<br> * Loading hardware drivers ... [ ok ]<br> * Loading modules ... [ ok ]<br> * Setting system clock using the hardware clock [UTC] ... [ ok ]<br> * Checking local filesystems  .../dev/vdb3: clean, 3173/177408 files, 47828/709376 blocks<br>/dev/vdb1: clean, 26/76912 files, 47886/307200 blocks<br> [ ok ]<br> * Remounting root filesystem read/write ... [ ok ]<br> * Remounting filesystems ... [ ok ]<br> * Activating swap devices ... [ ok ]<br> * Mounting local filesystems ... [ ok ]<br> * Configuring kernel parameters ... [ ok ]<br> * Migrating /var/lock to /run/lock ... [ ok ]<br> * Creating user login records ... [ ok ]<br> * Setting hostname ... [ ok ]<br> * Starting networking ... *   lo ... [ ok ]<br> *   eth0 ...udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br> [ ok ]<br> * Seeding random number generator ... * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox syslog ... [ ok ]<br> * Starting busybox acpid ... [ ok ]<br> * Starting busybox crond ... [ ok ]<br> * Starting sshd ... [ ok ]<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.105-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~#<br>localhost:~# cat /etc/os-release<br>NAME="Alpine Linux"<br>ID=alpine<br>VERSION_ID=3.17.3<br>PRETTY_NAME="Alpine Linux v3.17"<br>HOME_URL="https://alpinelinux.org/"<br>BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"<br>localhost:~#<br>localhost:~# uname -a<br>Linux localhost 5.15.105-0-virt #1-Alpine SMP Fri, 31 Mar 2023 07:57:34 +0000 x86_64 Linux<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# mkdir /mnt/repo<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0    4G  0 disk<br>├─vdb1 253:17   0  300M  0 part /boot<br>├─vdb2 253:18   0 1023M  0 part [SWAP]<br>└─vdb3 253:19   0  2.7G  0 part /<br>vdc    253:32   0   50G  1 disk<br>localhost:~#<br>localhost:~# blkid<br>/dev/vdb1: UUID="aba8642b-9069-4332-84b5-68fe37e6c66f" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="e39d887c-01"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660" PTUUID="77b851c3" PTTYPE="dos" PARTUUID="77b851c3-01"<br>/dev/vdb2: UUID="de1b4727-fa3d-4f50-8491-7c5d043a00aa" TYPE="swap" PARTUUID="e39d887c-02"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vdb3: UUID="dc2ae764-3fe0-45f5-868d-3b59ee7a5a08" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="e39d887c-03"<br>localhost:~#<br>localhost:~# cp -pi /etc/apk/repositories /root/backup<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# echo '/mnt/repo/alpine/v3.17/main' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# echo '/mnt/repo/alpine/v3.17/community' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>/mnt/repo/alpine/v3.17/main<br>/mnt/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /mnt/repo<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124365,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vdb3 on / type ext4 (rw,relatime)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201340k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>localhost:~# update-extlinux<br>/boot is device /dev/vdb1<br>localhost:~#<br>localhost:~# cat /etc/modules ; cp -pi /etc/modules /root/backup<br>af_packet<br>ipv6<br>localhost:~# echo fuse >> /etc/modules ; cat /etc/modules<br>af_packet<br>ipv6<br>fuse<br>localhost:~#                                                                            localhost:~# apk update<br>v3.17.3-33-g63371ce3229 [/mnt/repo/alpine/v3.17/main]<br>v3.17.3-33-g63371ce3229 [/mnt/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~#<br>localhost:~# date<br>Thu Apr  6 18:11:34 UTC 2023<br>localhost:~#<br>localhost:~# apk add  vim cryptsetup asciinema neofetch xca polkit qt5-qtwebglpl<br>ugin rpm cifs-utils device-mapper rng-tools inetutils-telnet perl hdparm fsarchi<br>ver libcdio-tools lftp-doc lftp pssh mutt neomutt alpine ncftp vsftpd vsftpd-doc<br> sshfs samba apache2 apache2-doc apache2-webdav apache2-utils apache2-ctl alpine<br>-sdk build-base apk-tools alpine-conf busybox fakeroot syslinux xorriso mtools d<br>osfstools grub-efi make git sudo lynx links nodejs npm dhcp-server-vanilla ccach<br>e ccache-doc udisks2 udisks2-doc libarchive-tools libarchive-doc cmake cmake-doc<br> extra-cmake-modules extra-cmake-modules-doc gcc abuild binutils binutils-doc gc<br>c-doc py3-pip pandoc util-linux pciutils usbutils coreutils binutils findutils g<br>rep iproute2 bash bash-doc utmps pass pass-otp darkhttpd libpwquality zstd pwgen<br> easy-rsa  markdown expect sshpass keepassxc gzip rpm xz bzip2 gawk bc diffutils<br> psmisc procps shadow util-linux-bash-completion util-linux-login mount umount n<br>etcat-openbsd nmap nmap-nping nmap-nselibs nmap-scripts net-tools socat rlwrap i<br>putils perl-digest-sha3 dos2unix gptfdisk sgdisk parted grub grub-bios grub-doc<br>efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosfstools texinfo e2fsprogs  e<br>2fsprogs-extra mkinitfs haveged davfs2 f2fs-tools jfsutils ntfs-3g xfsprogs cpio<br> whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils<br> fuse-exfat-doc nfs-utils ncurses ffmpeg sharutils mandoc man-pages mandoc-aprop<br>os docs virt-manager libvirt libvirt-daemon imagemagick spice spice-vdagent spic<br>e-gtk xf86-video-qxl qemu-guest-agent cmd:rsvg-convert iptables ip6tables perl-n<br>et-ssleay progress pv stress-ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plu<br>gins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vifm-zsh-<br>completion  vifm-bash-completion  fish ncdu zsh udisks2-bash-completion gnome-di<br>sk-utility zim chezdav grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsq<br>l apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate<br>WARNING: Ignoring /mnt/repo1/alpine/v3.17/community: No such file or directory<br>(1/891) Installing fakeroot (1.29-r0)<br>(2/891) Installing libattr (2.5.1-r2)<br>(3/891) Installing attr (2.5.1-r2)<br>(4/891) Installing libacl (2.3.1-r1)<br>(5/891) Installing tar (1.34-r2)<br>(6/891) Installing pkgconf (1.9.4-r0)<br>(7/891) Installing patch (2.7.6-r9)<br>(8/891) Installing libgcc (12.2.1_git20220924-r4)<br>(9/891) Installing libstdc++ (12.2.1_git20220924-r4)<br>(10/891) Installing lzip (1.23-r0)<br>(11/891) Installing ca-certificates (20220614-r4)<br>(12/891) Installing brotli-libs (1.0.9-r9)<br>(13/891) Installing nghttp2-libs (1.51.0-r0)<br>(14/891) Installing libcurl (7.88.1-r1)<br>(15/891) Installing curl (7.88.1-r1)<br>(16/891) Installing abuild (3.10.0-r0)<br>Executing abuild-3.10.0-r0.pre-install<br>(17/891) Installing gdbm (1.23-r0)<br>(18/891) Installing libsasl (2.1.28-r3)<br>(19/891) Installing libldap (2.6.3-r6)<br>(20/891) Installing alpine (2.26-r1)<br>(21/891) Installing binutils (2.39-r2)<br>(22/891) Installing libmagic (5.43-r0)<br>(23/891) Installing file (5.43-r0)<br>(24/891) Installing libgomp (12.2.1_git20220924-r4)<br>(25/891) Installing libatomic (12.2.1_git20220924-r4)<br>(26/891) Installing gmp (6.2.1-r2)<br>(27/891) Installing isl25 (0.25-r0)<br>(28/891) Installing mpfr4 (4.1.0-r0)<br>(29/891) Installing mpc1 (1.2.1-r1)<br>(30/891) Installing gcc (12.2.1_git20220924-r4)<br>(31/891) Installing libstdc++-dev (12.2.1_git20220924-r4)<br>(32/891) Installing musl-dev (1.2.3-r4)<br>(33/891) Installing libc-dev (0.7.2-r3)<br>(34/891) Installing g++ (12.2.1_git20220924-r4)<br>(35/891) Installing make (4.3-r1)<br>(36/891) Installing fortify-headers (1.1-r1)<br>(37/891) Installing build-base (0.5-r3)<br>(38/891) Installing libexpat (2.5.0-r0)<br>(39/891) Installing pcre2 (10.42-r0)<br>(40/891) Installing git (2.38.4-r1)<br>(41/891) Installing alpine-sdk (1.0-r1)<br>(42/891) Installing apr (1.7.2-r0)<br>(43/891) Installing apr-util (1.6.3-r0)<br>(44/891) Installing pcre (8.45-r2)<br>(45/891) Installing apache2 (2.4.56-r0)<br>Executing apache2-2.4.56-r0.pre-install<br>(46/891) Installing less (608-r1)<br>(47/891) Installing gzip (1.12-r0)<br>(48/891) Installing libintl (0.21.1-r1)<br>(49/891) Installing lynx (2.8.9_p1-r8)<br>(50/891) Installing apache2-ctl (2.4.56-r0)<br>(51/891) Installing apache2-doc (2.4.56-r0)<br>(52/891) Installing apache2-utils (2.4.56-r0)<br>(53/891) Installing apache2-webdav (2.4.56-r0)<br>(54/891) Installing mariadb-connector-c (3.3.3-r0)<br>(55/891) Installing apr-util-dbd_mysql (1.6.3-r0)<br>(56/891) Installing libpq (15.2-r0)<br>(57/891) Installing apr-util-dbd_pgsql (1.6.3-r0)<br>(58/891) Installing sqlite-libs (3.40.1-r0)<br>(59/891) Installing apr-util-dbd_sqlite3 (1.6.3-r0)<br>(60/891) Installing apr-util-ldap (1.6.3-r0)<br>(61/891) Installing libbz2 (1.0.8-r4)<br>(62/891) Installing libffi (3.4.4-r0)<br>(63/891) Installing mpdecimal (2.5.1-r1)<br>(64/891) Installing readline (8.2.0-r0)<br>(65/891) Installing python3 (3.10.10-r0)<br>(66/891) Installing ncurses (6.3_p20221119-r0)<br>(67/891) Installing asciinema (2.2.0-r0)<br>(68/891) Installing bash (5.2.15-r0)<br>Executing bash-5.2.15-r0.post-install<br>(69/891) Installing bash-doc (5.2.15-r0)<br>(70/891) Installing bc (1.07.1-r2)<br>(71/891) Installing binutils-doc (2.39-r2)<br>(72/891) Installing lzo (2.10-r3)<br>(73/891) Installing eudev-libs (3.2.11-r4)<br>(74/891) Installing btrfs-progs (6.0.2-r0)<br>(75/891) Installing bzip2 (1.0.8-r4)<br>(76/891) Installing hiredis (1.0.2-r1)<br>(77/891) Installing ccache (4.7.5-r0)<br>(78/891) Installing ccache-doc (4.7.5-r0)<br>(79/891) Installing dbus-libs (1.14.4-r0)<br>(80/891) Installing avahi-libs (0.8-r6)<br>(81/891) Installing libdaemon (0.14-r3)<br>(82/891) Installing libevent (2.1.12-r5)<br>(83/891) Installing avahi (0.8-r6)<br>Executing avahi-0.8-r6.pre-install<br>(84/891) Installing glib (2.74.6-r0)<br>(85/891) Installing avahi-glib (0.8-r6)<br>(86/891) Installing gsettings-desktop-schemas (43.0-r0)<br>(87/891) Installing nettle (3.8.1-r0)<br>(88/891) Installing p11-kit (0.24.1-r1)<br>(89/891) Installing libtasn1 (4.19.0-r0)<br>(90/891) Installing libunistring (1.1-r0)<br>(91/891) Installing gnutls (3.7.8-r3)<br>(92/891) Installing libproxy (0.4.18-r1)<br>(93/891) Installing glib-networking (2.74.0-r2)<br>(94/891) Installing libidn2 (2.3.4-r0)<br>(95/891) Installing libpsl (0.21.1-r1)<br>(129/891) Installing tiff (4.4.0-r3)<br> 24% ██████████<br>(98/891) Installing phodav (3.0-r0)<br>(99/891) Installing chezdav (3.0-r0)<br>(100/891) Installing krb5-conf (1.0-r2)<br>(101/891) Installing keyutils-libs (1.6.3-r1)<br>(102/891) Installing libverto (0.3.2-r1)<br>(103/891) Installing krb5-libs (1.20.1-r0)<br>(104/891) Installing talloc (2.3.4-r0)<br>(105/891) Installing libwbclient (4.16.10-r0)<br>(106/891) Installing cifs-utils (7.0-r0)<br>(107/891) Installing lz4-libs (1.9.4-r1)<br>(108/891) Installing libarchive (3.6.1-r2)<br>(109/891) Installing rhash-libs (1.4.3-r1)<br>(110/891) Installing libuv (1.44.2-r0)<br>(111/891) Installing cmake (3.24.4-r0)<br>(112/891) Installing cmake-doc (3.24.4-r0)<br>(113/891) Installing libxau (1.0.10-r0)<br>(114/891) Installing libmd (1.0.4-r0)<br>(115/891) Installing libbsd (0.11.7-r0)<br>(116/891) Installing libxdmcp (1.1.4-r0)<br>(117/891) Installing libxcb (1.15-r0)<br>(118/891) Installing libx11 (1.8.4-r0)<br>(119/891) Installing libxext (1.3.5-r0)<br>(120/891) Installing libxrender (0.9.11-r0)<br>(121/891) Installing libpng (1.6.38-r0)<br>(122/891) Installing freetype (2.12.1-r0)<br>(123/891) Installing fontconfig (2.14.1-r0)<br>(124/891) Installing pixman (0.42.2-r0)<br>(125/891) Installing cairo (1.17.6-r3)<br>(126/891) Installing shared-mime-info (2.2-r2)<br>(127/891) Installing libjpeg-turbo (2.1.4-r0)<br>(128/891) Installing libwebp (1.2.4-r1)<br>(130/891) Installing gdk-pixbuf (2.42.10-r0)<br>(131/891) Installing libxft (2.3.7-r0)<br>(132/891) Installing fribidi (1.0.12-r0)<br>(133/891) Installing graphite2 (1.3.14-r2)<br>(134/891) Installing harfbuzz (5.3.1-r1)<br>(135/891) Installing pango (1.50.13-r0)<br>(136/891) Installing rsvg-convert (2.55.1-r0)<br>(137/891) Installing skalibs (2.12.0.1-r0)<br>(138/891) Installing utmps-libs (0.1.2.0-r1)<br>(139/891) Installing coreutils (9.1-r0)<br>(140/891) Installing cpio (2.13-r3)<br>(141/891) Installing popt (1.19-r0)<br>(142/891) Installing cryptsetup (2.5.0-r2)<br>(143/891) Installing cryptsetup-openrc (2.5.0-r2)<br>(144/891) Installing darkhttpd (1.14-r0)<br>Executing darkhttpd-1.14-r0.pre-install<br>(145/891) Installing darkhttpd-openrc (1.14-r0)<br>(146/891) Installing neon (0.32.4-r0)<br>(147/891) Installing davfs2 (1.6.1-r0)<br>Executing davfs2-1.6.1-r0.pre-install<br>(148/891) Installing dbus (1.14.4-r0)<br>Executing dbus-1.14.4-r0.pre-install<br>Executing dbus-1.14.4-r0.post-install<br>(149/891) Installing dbus-openrc (1.14.4-r0)<br>(150/891) Installing dbus-x11 (1.14.4-r0)<br>(151/891) Installing libaio (0.3.113-r0)<br>(152/891) Installing device-mapper-event-libs (2.03.17-r1)<br>(153/891) Installing lvm2-libs (2.03.17-r1)<br>(154/891) Installing device-mapper (2.03.17-r1)<br>(155/891) Installing dhcp (4.4.3_p1-r1)<br>Executing dhcp-4.4.3_p1-r1.pre-install<br>(156/891) Installing dhcp-openrc (4.4.3_p1-r1)<br>(157/891) Installing dhcp-server-vanilla (4.4.3_p1-r1)<br>(158/891) Installing diffutils (3.8-r1)<br>(159/891) Installing mandoc (1.14.6-r6)<br>(160/891) Installing mandoc-doc (1.14.6-r6)<br>(161/891) Installing man-pages (6.01-r0)<br>(162/891) Installing docs (0.2-r6)<br>(163/891) Installing btrfs-progs-doc (6.0.2-r0)<br>(164/891) Installing lzo-doc (2.10-r3)<br>(165/891) Installing harfbuzz-doc (5.3.1-r1)<br>(166/891) Installing lynx-doc (2.8.9_p1-r8)<br>(167/891) Installing libwebp-doc (1.2.4-r1)<br>(168/891) Installing less-doc (608-r1)<br>(169/891) Installing busybox-doc (1.35.0-r29)<br>(170/891) Installing alpine-doc (2.26-r1)<br>(171/891) Installing gdk-pixbuf-doc (2.42.10-r0)<br>(172/891) Installing libjpeg-turbo-doc (2.1.4-r0)<br>(173/891) Installing mpc1-doc (1.2.1-r1)<br>(174/891) Installing davfs2-doc (1.6.1-r0)<br>(175/891) Installing ncurses-doc (6.3_p20221119-r0)<br>(176/891) Installing gmp-doc (6.2.1-r2)<br>(177/891) Installing cifs-utils-doc (7.0-r0)<br>(178/891) Installing libx11-doc (1.8.4-r0)<br>(179/891) Installing attr-doc (2.5.1-r2)<br>(180/891) Installing libffi-doc (3.4.4-r0)<br>(181/891) Installing pango-doc (1.50.13-r0)<br>(182/891) Installing gzip-doc (1.12-r0)<br>(183/891) Installing popt-doc (1.19-r0)<br>(184/891) Installing libxcb-doc (1.15-r0)<br>(185/891) Installing abuild-doc (3.10.0-r0)<br>(186/891) Installing freetype-doc (2.12.1-r0)<br>(187/891) Installing mpdecimal-doc (2.5.1-r1)<br>(188/891) Installing phodav-doc (3.0-r0)<br>(189/891) Installing cairo-doc (1.17.6-r3)<br>(190/891) Installing p11-kit-doc (0.24.1-r1)<br>(191/891) Installing apk-tools-doc (2.12.10-r1)<br>(192/891) Installing gdbm-doc (1.23-r0)<br>(193/891) Installing ca-certificates-doc (20220614-r4)<br>(194/891) Installing libmd-doc (1.0.4-r0)<br>(195/891) Installing libarchive-doc (3.6.1-r2)<br>(196/891) Installing acct-doc (6.6.4-r1)<br>(197/891) Installing gcc-doc (12.2.1_git20220924-r4)<br>(198/891) Installing openssl-doc (3.0.8-r3)<br>(199/891) Installing fribidi-doc (1.0.12-r0)<br>(200/891) Installing pkgconf-doc (1.9.4-r0)<br>(201/891) Installing libxrender-doc (0.9.11-r0)<br>(202/891) Installing libaio-doc (0.3.113-r0)<br>(203/891) Installing openrc-doc (0.45.2-r7)<br>(204/891) Installing bc-doc (1.07.1-r2)<br>(205/891) Installing pcre2-doc (10.42-r0)<br>(206/891) Installing coreutils-doc (9.1-r0)<br>(207/891) Installing libxft-doc (2.3.7-r0)<br>(208/891) Installing dbus-doc (1.14.4-r0)<br>(209/891) Installing talloc-doc (2.3.4-r0)<br>(210/891) Installing tar-doc (1.34-r2)<br>(211/891) Installing libxau-doc (1.0.10-r0)<br>(212/891) Installing avahi-doc (0.8-r6)<br>(213/891) Installing cryptsetup-doc (2.5.0-r2)<br>(214/891) Installing libxml2-doc (2.10.3-r1)<br>(215/891) Installing patch-doc (2.7.6-r9)<br>(216/891) Installing neon-doc (0.32.4-r0)<br>(217/891) Installing mpfr4-doc (4.1.0-r0)<br>(218/891) Installing doas-doc (6.8.2-r3)<br>(219/891) Installing libxdmcp-doc (1.1.4-r0)<br>(220/891) Installing libbsd-doc (0.11.7-r0)<br>(221/891) Installing ifupdown-ng-doc (0.12.1-r1)<br>(222/891) Installing asciinema-doc (2.2.0-r0)<br>(223/891) Installing libpng-doc (1.6.38-r0)<br>(224/891) Installing make-doc (4.3-r1)<br>(225/891) Installing cpio-doc (2.13-r3)<br>(226/891) Installing gnutls-doc (3.7.8-r3)<br>(227/891) Installing tiff-doc (4.4.0-r3)<br>(228/891) Installing diffutils-doc (3.8-r1)<br>(229/891) Installing rsvg-convert-doc (2.55.1-r0)<br>(230/891) Installing fontconfig-doc (2.14.1-r0)<br>(231/891) Installing libpsl-doc (0.21.1-r1)<br>(232/891) Installing git-doc (2.38.4-r1)<br>(233/891) Installing skalibs-doc (2.12.0.1-r0)<br>(234/891) Installing libdaemon-doc (0.14-r3)<br>(235/891) Installing glib-doc (2.74.6-r0)<br>(236/891) Installing shared-mime-info-doc (2.2-r2)<br>(237/891) Installing libidn2-doc (2.3.4-r0)<br>(238/891) Installing lzip-doc (1.23-r0)<br>(239/891) Installing dhcp-doc (4.4.3_p1-r1)<br>(240/891) Installing pcre-doc (8.45-r2)<br>(241/891) Installing libtasn1-doc (4.19.0-r0)<br>(242/891) Installing libxext-doc (1.3.5-r0)<br>(243/891) Installing zlib-doc (1.2.13-r0)<br>(244/891) Installing readline-doc (8.2.0-r0)<br>(245/891) Installing curl-doc (7.88.1-r1)<br>(246/891) Installing python3-doc (3.10.10-r0)<br>(247/891) Installing bzip2-doc (1.0.8-r4)<br>(248/891) Installing file-doc (5.43-r0)<br>(249/891) Installing fakeroot-doc (1.29-r0)<br>(250/891) Installing libunistring-doc (1.1-r0)<br>(251/891) Installing json-c-doc (0.16-r2)<br>(252/891) Installing dos2unix (7.4.3-r1)<br>(253/891) Installing dos2unix-doc (7.4.3-r1)<br>(254/891) Installing dosfstools (4.2-r1)<br>(255/891) Installing dosfstools-doc (4.2-r1)<br>(256/891) Installing e2fsprogs-doc (1.46.6-r0)<br>(257/891) Installing easy-rsa (3.1.1-r0)<br>(258/891) Installing easy-rsa-doc (3.1.1-r0)<br>(259/891) Installing ed (1.18-r2)<br>(260/891) Installing ed-doc (1.18-r2)<br>(261/891) Installing efivar-libs (38-r1)<br>(262/891) Installing efibootmgr (18-r0)<br>(263/891) Installing efibootmgr-doc (18-r0)<br>(264/891) Installing tzdata (2023c-r0)<br>(265/891) Installing tzdata-doc (2023c-r0)<br>(266/891) Installing tcl (8.6.12-r1)<br>(267/891) Installing tcl-doc (8.6.12-r1)<br>(268/891) Installing expect (5.45.4-r3)<br>(269/891) Installing expect-doc (5.45.4-r3)<br>(270/891) Installing extra-cmake-modules (5.100.0-r0)<br>(271/891) Installing extra-cmake-modules-doc (5.100.0-r0)<br>(272/891) Installing f2fs-tools-libs (1.15.0-r0)<br>(273/891) Installing f2fs-tools (1.15.0-r0)<br>(274/891) Installing f2fs-tools-doc (1.15.0-r0)<br>(275/891) Installing sdl2 (2.26.3-r0)<br>(276/891) Installing sdl2-doc (2.26.3-r0)<br>(277/891) Installing svt-av1-libs (1.3.0-r0)<br>(278/891) Installing aom-libs (3.5.0-r0)<br>(279/891) Installing alsa-lib (1.2.8-r0)<br>(280/891) Installing libass (0.16.0-r1)<br>(281/891) Installing libdav1d (1.0.0-r2)<br>(282/891) Installing hwdata-pci (0.364-r0)<br>(283/891) Installing libpciaccess (0.17-r0)<br>(284/891) Installing libpciaccess-doc (0.17-r0)<br>(285/891) Installing libdrm (2.4.114-r0)<br>(286/891) Installing lame (3.100-r2)<br>(287/891) Installing lame-doc (3.100-r2)<br>(288/891) Installing opus (1.3.1-r1)<br>(289/891) Installing opus-doc (1.3.1-r1)<br>(290/891) Installing libasyncns (0.8-r1)<br>(291/891) Installing libasyncns-doc (0.8-r1)<br>(292/891) Installing libltdl (2.4.7-r1)<br>(293/891) Installing orc (0.4.33-r0)<br>(294/891) Installing libogg (1.3.5-r2)<br>(295/891) Installing libogg-doc (1.3.5-r2)<br>(296/891) Installing flac-libs (1.4.2-r0)<br>(297/891) Installing libvorbis (1.3.7-r0)<br>(298/891) Installing libvorbis-doc (1.3.7-r0)<br>(299/891) Installing libsndfile (1.1.0-r2)<br>(300/891) Installing libsndfile-doc (1.1.0-r2)<br>(301/891) Installing soxr (0.1.3-r3)<br>(302/891) Installing speexdsp (1.2.1-r0)<br>(303/891) Installing speexdsp-doc (1.2.1-r0)<br>(304/891) Installing tdb-libs (1.4.6-r0)<br>(305/891) Installing libpulse (16.1-r6)<br>(306/891) Installing cjson (1.7.15-r3)<br>(307/891) Installing mbedtls (2.28.3-r0)<br>(308/891) Installing librist (0.2.7-r0)<br>(309/891) Installing libsrt (1.5.1-r0)<br>(310/891) Installing libssh (0.10.4-r0)<br>(311/891) Installing libtheora (1.1.1-r16)<br>(312/891) Installing libtheora-doc (1.1.1-r16)<br>(313/891) Installing v4l-utils-libs (1.22.1-r2)<br>(314/891) Installing libxfixes (6.0.0-r0)<br>(315/891) Installing libxfixes-doc (6.0.0-r0)<br>(316/891) Installing wayland-libs-client (1.21.0-r1)<br>(317/891) Installing libva (2.16.0-r0)<br>(318/891) Installing libvdpau (1.5-r0)<br>(319/891) Installing vidstab (1.1.0-r2)<br>(320/891) Installing libvpx (1.12.0-r1)<br>(321/891) Installing x264-libs (0.164_git20220602-r0)<br>(322/891) Installing numactl (2.0.16-r1)<br>(323/891) Installing numactl-doc (2.0.16-r1)<br>(324/891) Installing x265-libs (3.5-r3)<br>(325/891) Installing xvidcore (1.3.7-r1)<br>(326/891) Installing libsodium (1.0.18-r2)<br>(327/891) Installing libzmq (4.3.4-r1)<br>(328/891) Installing ffmpeg-libs (5.1.3-r0)<br>(329/891) Installing ffmpeg (5.1.3-r0)<br>(330/891) Installing ffmpeg-doc (5.1.3-r0)<br>(331/891) Installing findutils (4.9.0-r3)<br>(332/891) Installing findutils-doc (4.9.0-r3)<br>(333/891) Installing libpcre2-32 (10.42-r0)<br>(334/891) Installing fish (3.5.1-r1)<br>Executing fish-3.5.1-r1.post-install<br>(335/891) Installing curl-fish-completion (7.88.1-r1)<br>(336/891) Installing fish-doc (3.5.1-r1)<br>(337/891) Installing libgpg-error (1.46-r1)<br>(338/891) Installing libgpg-error-doc (1.46-r1)<br>(339/891) Installing libgcrypt (1.10.1-r0)<br>(340/891) Installing libgcrypt-doc (1.10.1-r0)<br>(341/891) Installing fsarchiver (0.8.6-r1)<br>(342/891) Installing fsarchiver-doc (0.8.6-r1)<br>(343/891) Installing fuse-common (3.12.0-r0)<br>(344/891) Installing fuse-openrc (3.12.0-r0)<br>(345/891) Installing fuse (2.9.9-r2)<br>(346/891) Installing fuse-doc (2.9.9-r2)<br>(347/891) Installing fuse-exfat (1.3.0-r3)<br>(348/891) Installing fuse-exfat-doc (1.3.0-r3)<br>(349/891) Installing fuse-exfat-utils (1.3.0-r3)<br>(350/891) Installing gawk (5.1.1-r1)<br>(351/891) Installing gawk-doc (5.1.1-r1)<br>(352/891) Installing gifsicle (1.93-r1)<br>(353/891) Installing gifsicle-doc (1.93-r1)<br>(354/891) Installing gptfdisk (1.0.9-r2)<br>(355/891) Installing gptfdisk-doc (1.0.9-r2)<br>(356/891) Installing parted (3.5-r0)<br>(357/891) Installing parted-doc (3.5-r0)<br>(358/891) Installing libatasmart (0.19-r2)<br>(359/891) Installing libatasmart-doc (0.19-r2)<br>(360/891) Installing libbytesize (2.7-r1)<br>(361/891) Installing libbytesize-doc (2.7-r1)<br>(362/891) Installing dmraid (1.0.0_rc16-r1)<br>(363/891) Installing dmraid-doc (1.0.0_rc16-r1)<br>(364/891) Installing ndctl-libs (74-r0)<br>(365/891) Installing nspr (4.35-r0)<br>(366/891) Installing nss (3.85-r1)<br>(367/891) Installing libassuan (2.5.5-r1)<br>(368/891) Installing libassuan-doc (2.5.5-r1)<br>(369/891) Installing pinentry (1.2.1-r0)<br>Executing pinentry-1.2.1-r0.post-install<br>(370/891) Installing pinentry-doc (1.2.1-r0)<br>(371/891) Installing gnupg-gpgconf (2.2.40-r0)<br>(372/891) Installing gpg (2.2.40-r0)<br>(373/891) Installing npth (1.6-r2)<br>(374/891) Installing gpg-agent (2.2.40-r0)<br>(375/891) Installing libksba (1.6.3-r0)<br>(376/891) Installing libksba-doc (1.6.3-r0)<br>(377/891) Installing gpgsm (2.2.40-r0)<br>(378/891) Installing gpgme (1.18.0-r0)<br>(379/891) Installing gpgme-doc (1.18.0-r0)<br>(380/891) Installing volume_key (0.3.12-r3)<br>(381/891) Installing volume_key-doc (0.3.12-r3)<br>(382/891) Installing yaml (0.2.5-r0)<br>(383/891) Installing libblockdev (2.28-r0)<br>(384/891) Installing libgudev (237-r1)<br>(385/891) Installing polkit-libs (122-r0)<br>(386/891) Installing udisks2-libs (2.9.4-r1)<br>(387/891) Installing udisks2 (2.9.4-r1)<br>(388/891) Installing udisks2-doc (2.9.4-r1)<br>(389/891) Installing libatk-1.0 (2.46.0-r0)<br>(390/891) Installing sound-theme-freedesktop (0.8-r0)<br>(391/891) Installing libcanberra (0.30-r9)<br>(392/891) Installing libcanberra-doc (0.30-r9)<br>(393/891) Installing hicolor-icon-theme (0.17-r2)<br>(394/891) Installing gtk-update-icon-cache (3.24.36-r0)<br>(395/891) Installing libxcomposite (0.4.5-r1)<br>(396/891) Installing libxcomposite-doc (0.4.5-r1)<br>(397/891) Installing libxcursor (1.2.1-r1)<br>(398/891) Installing libxcursor-doc (1.2.1-r1)<br>(399/891) Installing libxdamage (1.1.5-r1)<br>(400/891) Installing libxi (1.8-r0)<br>(401/891) Installing libxi-doc (1.8-r0)<br>(402/891) Installing libxinerama (1.1.5-r0)<br>(403/891) Installing libxinerama-doc (1.1.5-r0)<br>(404/891) Installing libxrandr (1.5.3-r0)<br>(405/891) Installing libxrandr-doc (1.5.3-r0)<br>(406/891) Installing libxtst (1.2.4-r0)<br>(407/891) Installing libxtst-doc (1.2.4-r0)<br>(408/891) Installing at-spi2-core (2.46.0-r0)<br>(409/891) Installing at-spi2-core-doc (2.46.0-r0)<br>(410/891) Installing libatk-bridge-2.0 (2.46.0-r0)<br>(411/891) Installing cairo-gobject (1.17.6-r3)<br>(412/891) Installing cups-libs (2.4.2-r1)<br>(413/891) Installing libepoxy (1.5.10-r0)<br>(414/891) Installing wayland-libs-cursor (1.21.0-r1)<br>(415/891) Installing wayland-libs-egl (1.21.0-r1)<br>(416/891) Installing xkeyboard-config (2.37-r0)<br>(417/891) Installing xkeyboard-config-doc (2.37-r0)<br>(418/891) Installing libxkbcommon (1.4.1-r0)<br>(419/891) Installing xkbcli-doc (1.4.1-r0)<br>(420/891) Installing gtk+3.0 (3.24.36-r0)<br>Executing gtk+3.0-3.24.36-r0.post-install<br>(421/891) Installing gtk+3.0-doc (3.24.36-r0)<br>(422/891) Installing libcanberra-gtk3 (0.30-r9)<br>(423/891) Installing libdvdcss (1.4.3-r0)<br>(424/891) Installing libdvdcss-doc (1.4.3-r0)<br>(425/891) Installing libdvdread (6.1.3-r0)<br>(426/891) Installing libdvdread-doc (6.1.3-r0)<br>(427/891) Installing libelogind (246.10-r5)<br>(428/891) Installing libhandy1 (1.8.2-r0)<br>(429/891) Installing libnotify (0.8.1-r1)<br>(430/891) Installing cracklib-words (2.9.8-r0)<br>(431/891) Installing cracklib (2.9.8-r0)<br>(432/891) Installing linux-pam-doc (1.5.2-r1)<br>(433/891) Installing libpwquality (1.4.4-r3)<br>(434/891) Installing libpwquality-doc (1.4.4-r3)<br>(435/891) Installing libsecret (0.20.5-r0)<br>(436/891) Installing libsecret-doc (0.20.5-r0)<br>(437/891) Installing gnome-disk-utility (43.0-r0)<br>(438/891) Installing gnome-disk-utility-doc (43.0-r0)<br>(439/891) Installing grep (3.8-r1)<br>(440/891) Installing grep-doc (3.8-r1)<br>(441/891) Installing kmod-doc (30-r1)<br>(442/891) Installing mkinitfs-doc (3.7.0-r1)<br>(443/891) Installing grub-doc (2.06-r7)<br>(444/891) Installing grub-bash-completion (2.06-r7)<br>(445/891) Installing grub-efi (2.06-r7)<br>(446/891) Installing haveged (1.9.18-r0)<br>(447/891) Installing haveged-openrc (1.9.18-r0)<br>(448/891) Installing haveged-doc (1.9.18-r0)<br>(449/891) Installing hdparm (9.65-r0)<br>(450/891) Installing hdparm-doc (9.65-r0)<br>(451/891) Installing lcms2 (2.14-r0)<br>(452/891) Installing lcms2-doc (2.14-r0)<br>(453/891) Installing imagemagick-libs (7.1.0.62-r0)<br>(454/891) Installing jbig2dec (0.19-r1)<br>(455/891) Installing jbig2dec-doc (0.19-r1)<br>(456/891) Installing ghostscript (10.0.0-r0)<br>(457/891) Installing ghostscript-doc (10.0.0-r0)<br>(458/891) Installing libde265 (1.0.11-r1)<br>(459/891) Installing libheif (1.13.0-r0)<br>(460/891) Installing libheif-doc (1.13.0-r0)<br>(461/891) Installing libjxl (0.7.0-r0)<br>(462/891) Installing libjxl-doc (0.7.0-r0)<br>(463/891) Installing librsvg (2.55.1-r0)<br>(464/891) Installing librsvg-doc (2.55.1-r0)<br>(465/891) Installing imagemagick (7.1.0.62-r0)<br>(466/891) Installing imagemagick-doc (7.1.0.62-r0)<br>(467/891) Installing inetutils-telnet (2.4-r0)<br>(468/891) Installing inetutils-telnet-doc (2.4-r0)<br>(469/891) Installing libmnl (1.0.5-r0)<br>(470/891) Installing libnftnl (1.2.4-r0)<br>(471/891) Installing iptables (1.8.8-r2)<br>(472/891) Installing iptables-doc (1.8.8-r2)<br>(473/891) Installing iptables-openrc (1.8.8-r2)<br>(474/891) Installing ip6tables (1.8.8-r2)<br>(475/891) Installing ip6tables-openrc (1.8.8-r2)<br>(476/891) Installing libmaxminddb-libs (1.7.1-r0)<br>(477/891) Installing libmaxminddb (1.7.1-r0)<br>(478/891) Installing libmaxminddb-doc (1.7.1-r0)<br>(479/891) Installing ipcalc (1.0.1-r1)<br>(480/891) Installing ipcalc-doc (1.0.1-r1)<br>(481/891) Installing musl-fts (1.2.7-r3)<br>(482/891) Installing libelf (0.187-r2)<br>(483/891) Installing iproute2-minimal (6.0.0-r1)<br>(484/891) Installing ifupdown-ng-iproute2 (0.12.1-r1)<br>(485/891) Installing iproute2-tc (6.0.0-r1)<br>(486/891) Installing iproute2-ss (6.0.0-r1)<br>(487/891) Installing iproute2 (6.0.0-r1)<br>Executing iproute2-6.0.0-r1.post-install<br>(488/891) Installing iproute2-doc (6.0.0-r1)<br>(489/891) Installing iputils (20211215-r0)<br>(490/891) Installing jfsutils (1.1.15-r4)<br>(491/891) Installing jfsutils-doc (1.1.15-r4)<br>(492/891) Installing icu-data-full (72.1-r1)<br>(493/891) Installing icu-libs (72.1-r1)<br>(494/891) Installing libpcre2-16 (10.42-r0)<br>(495/891) Installing qt5-qtbase (5.15.6_git20221010-r0)<br>(496/891) Installing qt5-qtbase-doc (5.15.6_git20221010-r0)<br>(497/891) Installing libice (1.0.10-r1)<br>(498/891) Installing libice-doc (1.0.10-r1)<br>(499/891) Installing libsm (1.2.3-r1)<br>(500/891) Installing libsm-doc (1.2.3-r1)<br>(501/891) Installing libxt (1.2.1-r0)<br>(502/891) Installing libxt-doc (1.2.1-r0)<br>(503/891) Installing libxmu (1.1.4-r0)<br>(504/891) Installing libxmu-doc (1.1.4-r0)<br>(505/891) Installing xset (1.2.4-r1)<br>(506/891) Installing xset-doc (1.2.4-r1)<br>(507/891) Installing xprop (1.2.5-r1)<br>(508/891) Installing xprop-doc (1.2.5-r1)<br>(509/891) Installing xdg-utils (1.1.3-r4)<br>(510/891) Installing xdg-utils-doc (1.1.3-r4)<br>(511/891) Installing mesa (22.2.5-r1)<br>(512/891) Installing wayland-libs-server (1.21.0-r1)<br>(513/891) Installing libxxf86vm (1.1.5-r0)<br>(514/891) Installing libxxf86vm-doc (1.1.5-r0)<br>(515/891) Installing mesa-glapi (22.2.5-r1)<br>(516/891) Installing libxshmfence (1.3.1-r0)<br>(517/891) Installing mesa-gl (22.2.5-r1)<br>(518/891) Installing qt5-qtdeclarative (5.15.6_git20220908-r0)<br>(519/891) Installing qt5-qtwayland (5.15.6_git20220927-r1)<br>(520/891) Installing mesa-gbm (22.2.5-r1)<br>(521/891) Installing mesa-egl (22.2.5-r1)<br>(522/891) Installing libevdev (1.13.0-r0)<br>(523/891) Installing libevdev-doc (1.13.0-r0)<br>(524/891) Installing mtdev (1.1.6-r1)<br>(525/891) Installing libinput-libs (1.22.1-r0)<br>(526/891) Installing xcb-util-wm (0.4.2-r0)<br>(527/891) Installing xcb-util (0.4.0-r3)<br>(528/891) Installing xcb-util-image (0.4.1-r0)<br>(529/891) Installing xcb-util-keysyms (0.4.1-r0)<br>(530/891) Installing xcb-util-renderutil (0.3.10-r0)<br>(531/891) Installing libxkbcommon-x11 (1.4.1-r0)<br>(532/891) Installing qt5-qtbase-x11 (5.15.6_git20221010-r0)<br>(533/891) Installing qt5-qtsvg (5.15.6_git20220908-r0)<br>(534/891) Installing qt5-qtx11extras (5.15.6_git20220816-r0)<br>(535/891) Installing botan-libs (2.19.3-r0)<br>(536/891) Installing minizip (1.2.13-r0)<br>(537/891) Installing pcsc-lite-libs (1.9.9-r0)<br>(538/891) Installing libqrencode (4.1.1-r1)<br>(539/891) Installing libqrencode-doc (4.1.1-r1)<br>(540/891) Installing libusb (1.0.26-r0)<br>(541/891) Installing keepassxc (2.7.4-r0)<br>(542/891) Installing keepassxc-doc (2.7.4-r0)<br>(543/891) Installing lftp (4.9.2-r4)<br>(544/891) Installing lftp-doc (4.9.2-r4)<br>(545/891) Installing libarchive-tools (3.6.1-r2)<br>(546/891) Installing libcddb (1.3.2-r4)<br>(547/891) Installing libcdio (2.1.0-r1)<br>(548/891) Installing libcdio-doc (2.1.0-r1)<br>(549/891) Installing libcdio-tools (2.1.0-r1)<br>(550/891) Installing lvm2 (2.03.17-r1)<br>(551/891) Installing lvm2-openrc (2.03.17-r1)<br>(552/891) Installing lvm2-doc (2.03.17-r1)<br>(553/891) Installing boost1.80-iostreams (1.80.0-r3)<br>(554/891) Installing boost1.80-thread (1.80.0-r3)<br>(555/891) Installing fmt (9.1.0-r0)<br>(556/891) Installing fmt-doc (9.1.0-r0)<br>(557/891) Installing librados17 (17.2.5-r5)<br>(558/891) Installing librbd17 (17.2.5-r5)<br>(559/891) Installing libtirpc-conf (1.3.3-r0)<br>(560/891) Installing libtirpc (1.3.3-r0)<br>(561/891) Installing libtirpc-doc (1.3.3-r0)<br>(562/891) Installing libcap-ng-doc (0.8.3-r1)<br>(563/891) Installing libnl3 (3.7.0-r0)<br>(564/891) Installing libnl3-doc (3.7.0-r0)<br>(565/891) Installing yajl (2.1.0-r5)<br>(566/891) Installing libvirt-libs (8.9.0-r4)<br>(567/891) Installing libvirt (8.9.0-r4)<br>Executing libvirt-8.9.0-r4.post-install<br>(568/891) Installing libvirt-doc (8.9.0-r4)<br>(569/891) Installing kbd-misc (2.5.1-r3)<br>(570/891) Installing kbd (2.5.1-r3)<br>(571/891) Installing kbd-openrc (2.5.1-r3)<br>(572/891) Installing kbd-doc (2.5.1-r3)<br>(573/891) Installing pm-utils (1.4.1-r4)<br>(574/891) Installing pm-utils-doc (1.4.1-r4)<br>(575/891) Installing gnutls-utils (3.7.8-r3)<br>(576/891) Installing netcat-openbsd (1.130-r4)<br>(577/891) Installing netcat-openbsd-doc (1.130-r4)<br>(578/891) Installing libvirt-client (8.9.0-r4)<br>(579/891) Installing bridge-utils (1.7.1-r1)<br>(580/891) Installing bridge-utils-doc (1.7.1-r1)<br>(581/891) Installing dmidecode (3.4-r0)<br>(582/891) Installing dmidecode-doc (3.4-r0)<br>(583/891) Installing dnsmasq-common (2.87-r2)<br>(584/891) Installing dnsmasq-openrc (2.87-r2)<br>(585/891) Installing dnsmasq (2.87-r2)<br>Executing dnsmasq-2.87-r2.pre-install<br>(586/891) Installing dnsmasq-doc (2.87-r2)<br>(587/891) Installing libvirt-daemon (8.9.0-r4)<br>(588/891) Installing links (2.28-r0)<br>(589/891) Installing links-doc (2.28-r0)<br>(590/891) Installing mandoc-apropos (1.14.6-r6)<br>(591/891) Installing perl (5.36.0-r0)<br>(592/891) Installing perl-doc (5.36.0-r0)<br>(593/891) Installing perl-error (0.17029-r1)<br>(594/891) Installing perl-error-doc (0.17029-r1)<br>(595/891) Installing perl-git (2.38.4-r1)<br>(596/891) Installing git-perl (2.38.4-r1)<br>(597/891) Installing markdown (1.0.1-r3)<br>(598/891) Installing markdown-doc (1.0.1-r3)<br>(599/891) Installing gpm-libs (1.20.7-r2)<br>(600/891) Installing slang (2.3.3-r0)<br>(601/891) Installing slang-doc (2.3.3-r0)<br>(602/891) Installing libssh2 (1.10.0-r3)<br>(603/891) Installing libssh2-doc (1.10.0-r3)<br>(604/891) Installing mc (4.8.28-r0)<br>(605/891) Installing mc-doc (4.8.28-r0)<br>(606/891) Installing mlocate (0.26-r8)<br>Executing mlocate-0.26-r8.pre-install<br>(607/891) Installing mlocate-doc (0.26-r8)<br>(608/891) Installing mtools-doc (4.0.42-r0)<br>(609/891) Installing libidn (1.41-r0)<br>(610/891) Installing libidn-doc (1.41-r0)<br>(611/891) Installing libgsasl (2.2.0-r0)<br>(612/891) Installing libgsasl-doc (2.2.0-r0)<br>(613/891) Installing mutt (2.2.9-r0)<br>(614/891) Installing mutt-doc (2.2.9-r0)<br>(615/891) Installing nano-doc (7.0-r0)<br>(616/891) Installing ncdu (1.17-r1)<br>(617/891) Installing ncdu-doc (1.17-r1)<br>(618/891) Installing ncftp (3.2.6-r5)<br>(619/891) Installing ncftp-doc (3.2.6-r5)<br>(620/891) Installing neofetch (7.1.0-r1)<br>(621/891) Installing neofetch-doc (7.1.0-r1)<br>(622/891) Installing gpg-wks-server (2.2.40-r0)<br>(623/891) Installing gpgv (2.2.40-r0)<br>(624/891) Installing gnupg-dirmngr (2.2.40-r0)<br>(625/891) Installing gnupg-utils (2.2.40-r0)<br>(626/891) Installing gnupg-wks-client (2.2.40-r0)<br>(627/891) Installing gnupg (2.2.40-r0)<br>(628/891) Installing gnupg-doc (2.2.40-r0)<br>(629/891) Installing gmime (3.2.13-r0)<br>(630/891) Installing gmime-doc (3.2.13-r0)<br>(631/891) Installing libxapian (1.4.21-r0)<br>(632/891) Installing notmuch-libs (0.37-r1)<br>(633/891) Installing neomutt (20220429-r2)<br>(634/891) Installing neomutt-doc (20220429-r2)<br>(635/891) Installing mii-tool (2.10-r0)<br>(636/891) Installing net-tools (2.10-r0)<br>(637/891) Installing net-tools-doc (2.10-r0)<br>(638/891) Installing rpcbind (1.2.6-r1)<br>Executing rpcbind-1.2.6-r1.pre-install<br>(639/891) Installing rpcbind-doc (1.2.6-r1)<br>(640/891) Installing rpcbind-openrc (1.2.6-r1)<br>(641/891) Installing libnfsidmap (2.6.2-r0)<br>(642/891) Installing nfs-utils (2.6.2-r0)<br>(643/891) Installing nfs-utils-doc (2.6.2-r0)<br>(644/891) Installing nfs-utils-openrc (2.6.2-r0)<br>(645/891) Installing lua5.3-libs (5.3.6-r4)<br>(646/891) Installing libpcap (1.10.1-r1)<br>(647/891) Installing libpcap-doc (1.10.1-r1)<br>(648/891) Installing nmap (7.93-r0)<br>(649/891) Installing nmap-doc (7.93-r0)<br>(650/891) Installing nmap-nping (7.93-r0)<br>(651/891) Installing nmap-nselibs (7.93-r0)<br>(652/891) Installing nmap-scripts (7.93-r0)<br>(653/891) Installing nnn (4.6-r0)<br>(654/891) Installing nnn-doc (4.6-r0)<br>(655/891) Installing nnn-fish-completion (4.6-r0)<br>(656/891) Installing nnn-bash-completion (4.6-r0)<br>(657/891) Installing nnn-plugins (4.6-r0)<br>Executing nnn-plugins-4.6-r0.post-install<br>* To use nnn plugins you have to install them into your HOME, run: nnn-getplugs.<br>(658/891) Installing nnn-zsh-completion (4.6-r0)<br>(659/891) Installing c-ares (1.18.1-r1)<br>(660/891) Installing c-ares-doc (1.18.1-r1)<br>(661/891) Installing nodejs (18.14.2-r0)<br>(662/891) Installing nodejs-doc (18.14.2-r0)<br>(663/891) Installing npm (9.1.2-r0)<br>(664/891) Installing npm-doc (9.1.2-r0)<br>(665/891) Installing ntfs-3g-libs (2022.10.3-r0)<br>(666/891) Installing ntfs-3g (2022.10.3-r0)<br>(667/891) Installing ntfs-3g-doc (2022.10.3-r0)<br>(668/891) Installing libedit-doc (20221030.3.1-r0)<br>(669/891) Installing openssh-doc (9.1_p1-r2)<br>(670/891) Installing p7zip (17.04-r3)<br>(671/891) Installing p7zip-doc (17.04-r3)<br>(672/891) Installing pandoc (2.19.2-r0)<br>(673/891) Installing pandoc-doc (2.19.2-r0)<br>(674/891) Installing tree (2.0.4-r0)<br>(675/891) Installing tree-doc (2.0.4-r0)<br>(676/891) Installing pass (1.7.4-r1)<br>(677/891) Installing pass-doc (1.7.4-r1)<br>(678/891) Installing pass-fish-completion (1.7.4-r1)<br>(679/891) Installing oath-toolkit-liboath (2.6.7-r2)<br>(680/891) Installing oath-toolkit-oathtool (2.6.7-r2)<br>(681/891) Installing pass-otp (1.2.0-r0)<br>(682/891) Installing pass-otp-doc (1.2.0-r0)<br>(683/891) Installing pciutils-libs (3.9.0-r0)<br>(684/891) Installing pciutils (3.9.0-r0)<br>(685/891) Installing pciutils-doc (3.9.0-r0)<br>(686/891) Installing perl-digest-sha3 (1.05-r0)<br>(687/891) Installing perl-digest-sha3-doc (1.05-r0)<br>(688/891) Installing perl-net-ssleay (1.92-r2)<br>(689/891) Installing perl-net-ssleay-doc (1.92-r2)<br>(690/891) Installing polkit-common (122-r0)<br>Executing polkit-common-122-r0.pre-install<br>(691/891) Installing duktape (2.7.0-r0)<br>(692/891) Installing polkit (122-r0)<br>(693/891) Installing polkit-openrc (122-r0)<br>(694/891) Installing polkit-doc (122-r0)<br>(695/891) Installing libproc (3.3.17-r2)<br>(696/891) Installing procps (3.3.17-r2)<br>(697/891) Installing procps-doc (3.3.17-r2)<br>(698/891) Installing progress (0.16-r0)<br>(699/891) Installing progress-doc (0.16-r0)<br>(700/891) Installing psmisc (23.5-r0)<br>(701/891) Installing psmisc-doc (23.5-r0)<br>(702/891) Installing pssh (2.3.4-r2)<br>(703/891) Installing pssh-doc (2.3.4-r2)<br>(704/891) Installing pv (1.6.20-r1)<br>(705/891) Installing pv-doc (1.6.20-r1)<br>(706/891) Installing pwgen (2.08-r2)<br>(707/891) Installing pwgen-doc (2.08-r2)<br>(708/891) Installing py3-six (1.16.0-r3)<br>(709/891) Installing py3-retrying (1.3.3-r3)<br>(710/891) Installing py3-parsing (3.0.9-r0)<br>(711/891) Installing py3-packaging (21.3-r2)<br>(712/891) Installing py3-setuptools (65.6.0-r0)<br>(713/891) Installing py3-pip (22.3.1-r1)<br>(714/891) Installing py3-pip-doc (22.3.1-r1)<br>(715/891) Installing liburing (2.3-r0)<br>(716/891) Installing liburing-doc (2.3-r0)<br>(717/891) Installing qemu-guest-agent (7.1.0-r7)<br>(718/891) Installing qt5-qtwebsockets (5.15.6_git20220907-r0)<br>(719/891) Installing qt5-qtwebglplugin (5.15.6_git20220816-r0)<br>(720/891) Installing qt5-qtwebglplugin-doc (5.15.6_git20220816-r0)<br>(721/891) Installing rlwrap (0.46.1-r0)<br>(722/891) Installing rlwrap-doc (0.46.1-r0)<br>(723/891) Installing jitterentropy-library (3.3.1-r0)<br>(724/891) Installing jitterentropy-library-doc (3.3.1-r0)<br>(725/891) Installing rng-tools (6.15-r1)<br>(726/891) Installing rng-tools-openrc (6.15-r1)<br>(727/891) Installing rng-tools-doc (6.15-r1)<br>(728/891) Installing lua5.4-libs (5.4.4-r6)<br>(729/891) Installing rpm (4.18.0-r1)<br>(730/891) Installing rpm-doc (4.18.0-r1)<br>(731/891) Installing samba-common (4.16.10-r0)<br>(732/891) Installing tevent (0.13.0-r0)<br>(733/891) Installing samba-util-libs (4.16.10-r0)<br>(734/891) Installing jansson (2.14-r0)<br>(735/891) Installing lmdb (0.9.29-r2)<br>(736/891) Installing lmdb-doc (0.9.29-r2)<br>(737/891) Installing ldb (2.5.3-r0)<br>(738/891) Installing ldb-doc (2.5.3-r0)<br>(739/891) Installing samba-libs (4.16.10-r0)<br>(740/891) Installing samba-common-server-libs (4.16.10-r0)<br>(741/891) Installing samba-client-libs (4.16.10-r0)<br>(742/891) Installing samba-server (4.16.10-r0)<br>(743/891) Installing samba-server-openrc (4.16.10-r0)<br>(744/891) Installing libsmbclient (4.16.10-r0)<br>(745/891) Installing samba-client (4.16.10-r0)<br>(746/891) Installing samba-common-tools (4.16.10-r0)<br>(747/891) Installing samba (4.16.10-r0)<br>(748/891) Installing samba-doc (4.16.10-r0)<br>(749/891) Installing sed (4.9-r0)<br>(750/891) Installing sed-doc (4.9-r0)<br>(751/891) Installing sgdisk (1.0.9-r2)<br>(752/891) Installing shadow (4.13-r0)<br>(753/891) Installing shadow-doc (4.13-r0)<br>(754/891) Installing xz (5.2.9-r0)<br>(755/891) Installing xz-doc (5.2.9-r0)<br>(756/891) Installing sharutils (4.15.2-r2)<br>(757/891) Installing sharutils-doc (4.15.2-r2)<br>(758/891) Installing socat (1.7.4.4-r0)<br>(759/891) Installing socat-doc (1.7.4.4-r0)<br>(760/891) Installing spice (0.15.1-r0)<br>(761/891) Installing gstreamer (1.20.6-r0)<br>(762/891) Installing libcanberra-gstreamer (0.30-r9)<br>(763/891) Installing gstreamer-doc (1.20.6-r0)<br>(764/891) Installing libxv (1.0.11-r3)<br>(765/891) Installing libxv-doc (1.0.11-r3)<br>(766/891) Installing cdparanoia-libs (10.2-r11)<br>(767/891) Installing graphene (1.10.8-r1)<br>(768/891) Installing gst-plugins-base (1.20.6-r0)<br>(769/891) Installing gst-plugins-base-doc (1.20.6-r0)<br>(770/891) Installing json-glib (1.6.6-r1)<br>(771/891) Installing usbredir (0.12.0-r0)<br>(772/891) Installing usbredir-doc (0.12.0-r0)<br>(773/891) Installing spice-glib (0.41-r1)<br>(774/891) Installing spice-gtk (0.41-r1)<br>(775/891) Installing spice-gtk-doc (0.41-r1)<br>(776/891) Installing spice-vdagent (0.22.1-r1)<br>(777/891) Installing spice-vdagent-openrc (0.22.1-r1)<br>(778/891) Installing spice-vdagent-doc (0.22.1-r1)<br>(779/891) Installing fuse3-libs (3.12.0-r0)<br>(780/891) Installing fuse3 (3.12.0-r0)<br>(781/891) Installing fuse3-doc (3.12.0-r0)<br>(782/891) Installing sshfs (3.7.3-r0)<br>(783/891) Installing sshfs-doc (3.7.3-r0)<br>(784/891) Installing sshpass (1.09-r1)<br>(785/891) Installing sshpass-doc (1.09-r1)<br>(786/891) Installing judy (1.0.5-r1)<br>(787/891) Installing judy-doc (1.0.5-r1)<br>(788/891) Installing liblksctp (1.0.19-r1)<br>(789/891) Installing stress-ng (0.14.00-r0)<br>(790/891) Installing stress-ng-doc (0.14.00-r0)<br>(791/891) Installing sudo (1.9.12_p2-r1)<br>(792/891) Installing sudo-doc (1.9.12_p2-r1)<br>(793/891) Installing syslinux-doc (6.04_pre1-r11)<br>(794/891) Installing texinfo (7.0.1-r0)<br>(795/891) Installing texinfo-doc (7.0.1-r0)<br>(796/891) Installing udisks2-bash-completion (2.9.4-r1)<br>(797/891) Installing unzip (6.0-r13)<br>(798/891) Installing unzip-doc (6.0-r13)<br>(799/891) Installing hwdata-usb (0.364-r0)<br>(800/891) Installing usbutils (015-r0)<br>(801/891) Installing usbutils-doc (015-r0)<br>(802/891) Installing libeconf-doc (0.4.7-r0)<br>(803/891) Installing util-linux-doc (2.38.1-r1)<br>(804/891) Installing util-linux-bash-completion (2.38.1-r1)<br>(805/891) Installing util-linux-login (2.38.1-r1)<br>(806/891) Installing util-linux-login-doc (2.38.1-r1)<br>(807/891) Installing s6-ipcserver (2.11.1.2-r0)<br>(808/891) Installing utmps (0.1.2.0-r1)<br>Executing utmps-0.1.2.0-r1.pre-install<br>(809/891) Installing utmps-doc (0.1.2.0-r1)<br>(810/891) Installing utmps-openrc (0.1.2.0-r1)<br>(811/891) Installing vifm (0.12.1-r1)<br>(812/891) Installing vifm-doc (0.12.1-r1)<br>(813/891) Installing vifm-fish-completion (0.12.1-r1)<br>(814/891) Installing vifm-bash-completion (0.12.1-r1)<br>(815/891) Installing vifm-zsh-completion (0.12.1-r1)<br>(816/891) Installing xxd (9.0.0999-r0)<br>(817/891) Installing vim (9.0.0999-r0)<br>(818/891) Installing vim-doc (9.0.0999-r0)<br>(819/891) Installing libvirt-glib (4.0.0-r0)<br>(820/891) Installing py3-libxml2 (2.10.3-r1)<br>(821/891) Installing py3-libvirt (8.9.0-r0)<br>(822/891) Installing gobject-introspection (1.74.0-r1)<br>(823/891) Installing gobject-introspection-doc (1.74.0-r1)<br>(824/891) Installing py3-gobject3 (3.42.2-r0)<br>(825/891) Installing py3-certifi (2022.12.7-r0)<br>(826/891) Installing py3-charset-normalizer (3.0.1-r0)<br>(827/891) Installing py3-idna (3.4-r2)<br>(828/891) Installing py3-urllib3 (1.26.12-r0)<br>(829/891) Installing py3-requests (2.28.1-r1)<br>(830/891) Installing hwdata-pnp (0.364-r0)<br>(831/891) Installing hwdata-net (0.364-r0)<br>(832/891) Installing hwdata (0.364-r0)<br>(833/891) Installing osinfo-db (20221018-r0)<br>(834/891) Installing libxslt (1.1.37-r1)<br>(835/891) Installing libxslt-doc (1.1.37-r1)<br>(836/891) Installing libosinfo (1.10.0-r2)<br>(837/891) Installing libosinfo-doc (1.10.0-r2)<br>(838/891) Installing virt-manager-common (4.1.0-r0)<br>(839/891) Installing vte3 (0.70.2-r0)<br>(840/891) Installing py3-cairo (1.21.0-r1)<br>(841/891) Installing gtk-vnc (1.3.1-r0)<br>(842/891) Installing gtk-vnc-doc (1.3.1-r0)<br>(843/891) Installing gtksourceview4 (4.8.4-r0)<br>(844/891) Installing qemu-img (7.1.0-r7)<br>(845/891) Installing virt-manager (4.1.0-r0)<br>(846/891) Installing virt-manager-doc (4.1.0-r0)<br>(847/891) Installing vsftpd (3.0.5-r2)<br>Executing vsftpd-3.0.5-r2.pre-install<br>(848/891) Installing vsftpd-doc (3.0.5-r2)<br>(849/891) Installing vsftpd-openrc (3.0.5-r2)<br>(850/891) Installing wget (1.21.3-r2)<br>(851/891) Installing wget-doc (1.21.3-r2)<br>(852/891) Installing whois (5.5.14-r0)<br>(853/891) Installing whois-doc (5.5.14-r0)<br>(854/891) Installing qt5-qtbase-sqlite (5.15.6_git20221010-r0)<br>(855/891) Installing llvm15-libs (15.0.7-r0)<br>(856/891) Installing clang15-libclang (15.0.7-r0)<br>(857/891) Installing qt5-qttools (5.15.6_git20220907-r1)<br>(858/891) Installing xca (2.4.0-r2)<br>(859/891) Installing xca-doc (2.4.0-r2)<br>(860/891) Installing xf86-video-qxl (0.1.5-r8)<br>(861/891) Installing xf86-video-qxl-doc (0.1.5-r8)<br>(862/891) Installing inih (56-r0)<br>(863/891) Installing userspace-rcu (0.13.2-r0)<br>(864/891) Installing userspace-rcu-doc (0.13.2-r0)<br>(865/891) Installing xfsprogs (6.0.0-r0)<br>(866/891) Installing xfsprogs-doc (6.0.0-r0)<br>(867/891) Installing libburn (1.5.4-r2)<br>(868/891) Installing libburn-doc (1.5.4-r2)<br>(869/891) Installing libisofs (1.5.4-r2)<br>(870/891) Installing libisoburn (1.5.4-r2)<br>(871/891) Installing libisoburn-doc (1.5.4-r2)<br>(872/891) Installing xorriso (1.5.4-r2)<br>(873/891) Installing py3-xdg (0.28-r0)<br>(874/891) Installing zim (0.75.1-r0)<br>(875/891) Installing zim-doc (0.75.1-r0)<br>(876/891) Installing zip (3.0-r10)<br>(877/891) Installing zip-doc (3.0-r10)<br>(878/891) Installing zsh (5.9-r0)<br>Executing zsh-5.9-r0.post-install<br>(879/891) Installing gcc-zsh-completion (5.9-r0)<br>(880/891) Installing pass-zsh-completion (1.7.4-r1)<br>(881/891) Installing apk-tools-zsh-completion (2.12.10-r1)<br>(882/891) Installing openrc-zsh-completion (0.45.2-r7)<br>(883/891) Installing zsh-pcre (5.9-r0)<br>(884/891) Installing py3-pip-zsh-completion (22.3.1-r1)<br>(885/891) Installing imagemagick-zsh-completion (5.9-r0)<br>(886/891) Installing git-zsh-completion (5.9-r0)<br>(887/891) Installing zsh-doc (5.9-r0)<br>(888/891) Installing lynx-zsh-completion (5.9-r0)<br>(889/891) Installing curl-zsh-completion (7.88.1-r1)<br>(890/891) Installing zstd (1.5.5-r0)<br>(891/891) Installing zstd-doc (1.5.5-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing ca-certificates-20220614-r4.trigger<br>Executing glib-2.74.6-r0.trigger<br>Executing fontconfig-2.14.1-r0.trigger<br>Executing shared-mime-info-2.2-r2.trigger<br>Executing gdk-pixbuf-2.42.10-r0.trigger<br>Executing dbus-1.14.4-r0.trigger<br>Executing gtk-update-icon-cache-3.24.36-r0.trigger<br>Executing cracklib-2.9.8-r0.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>OK: 1833 MiB in 983 packages<br>localhost:~#<br>localhost:~#<br>localhost:~#<br>localhost:~#<br>localhost:~# date<br>Thu Apr  6 19:06:14 UTC 2023<br>localhost:~#<br>localhost:~# echo $SHELL<br>/bin/ash<br>localhost:~# chsh -s /bin/bash root<br>Password:<br>localhost:~# chsh -s /bin/bash test1<br><br>localhost:~# grep wheel /etc/sudoers<br>## Uncomment to allow members of group wheel to execute any command<br>%wheel ALL=(ALL:ALL) ALL<br># %wheel ALL=(ALL:ALL) NOPASSWD: ALL<br>localhost:~#<br>localhost:~# reboot<br> <br><br>localhost login:<br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.105-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login:<br>localhost login: test1<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~$<br>localhost:~$  links -dump http://10.0.2.2:60676<br>                                       /<br><br> test-disk1-30mb.ext  31457280<br> vmtest1.raw        4293918720<br><br>     ----------------------------------------------------------------------<br><br>   Generated by darkhttpd/1.14 on Fri, 07 Apr 2023 03:31:22 GMT<br>localhost:~$ exit<br>logout<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.105-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: [23475.165387] reboot: Power down<br>~ $<br></pre></td>
</tr>
</table>

<p><br></p>

<a id="termux-session-for-termux-command-line"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#termux-command-line">Termux-Command-Line</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ SOCKET_FILENAME=socket.PAym3eQVJq<br>~ $ echo SOCKET_FILENAME<br>SOCKET_FILENAME<br>~ $ echo $SOCKET_FILENAME<br>socket.PAym3eQVJq<br>~ $<br>~ $ DIRECTORY_NAME_FROM_mktemp=/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C<br>~ $<br>~ $ echo $DIRECTORY_NAME_FROM_mktemp<br>/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C<br>~ $<br>~ $ echo 'info usernet' | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info usernet<br>Hub -1 (net0):<br>  Protocol[State]    FD  Source Address  Port   Dest. Address  Port RecvQ SendQ<br>  TCP[HOST_FORWARD]  15               * 15022       10.0.2.15    22     0     0<br>  TCP[HOST_FORWARD]  14               * 15081       10.0.2.15 15081     0     0<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br>(qemu) ~ $<br>~ $<br>~ $ echo "drive_add 0 if=none,file=$DIRECTORY_NAME_FROM_mktemp/test-disk1-30mb.ext,format=raw,id=disk1" | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>drive_add 0 if=none,file=/storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/test-disk1-30mb.ext,format=raw,id=disk1<br>OK<br>~ $<br>~ $ echo 'device_add virtio-blk-pci,drive=disk1,id=virt1' | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) device_add virtio-blk-pci,drive=disk1,id=virt1<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk1 (#block784): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/test-disk1-30mb.ext (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu) ~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk1 (#block784): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/test-disk1-30mb.ext (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu) ~ $<br>~ $<br>~ $ <br>~ $ ssh test1@127.0.0.1 -p 15022<br>The authenticity of host '[127.0.0.1]:15022 ([127.0.0.1]:15022)' can't be established.<br>ED25519 key fingerprint is SHA256:ZxsjVRBv7OGgSfMyqQaRTGK9dZVM5nAS9W0V5B71Sxs.<br>This key is not known by any other names.<br>Are you sure you want to continue connecting (yes/no/[fingerprint])? yes<br>Warning: Permanently added '[127.0.0.1]:15022' (ED25519) to the list of known hosts.<br>test1@127.0.0.1's password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~$<br>localhost:~$ blkid<br>/dev/vdb1: UUID="aba8642b-9069-4332-84b5-68fe37e6c66f" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="e39d887c-01"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660" PTUUID="77b851c3" PTTYPE="dos" PARTUUID="77b851c3-01"<br>/dev/vdb2: UUID="de1b4727-fa3d-4f50-8491-7c5d043a00aa" TYPE="swap" PARTUUID="e39d887c-02"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vdb3: UUID="dc2ae764-3fe0-45f5-868d-3b59ee7a5a08" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="e39d887c-03"<br>/dev/vdd: LABEL="disk1-30mb" UUID="00781ac1-ab37-4b36-abac-5ef4b9f4c990" BLOCK_SIZE="1024" TYPE="ext4"<br>localhost:~$<br>localhost:~$ lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0    4G  0 disk<br>├─vdb1 253:17   0  300M  0 part /boot<br>├─vdb2 253:18   0 1023M  0 part [SWAP]<br>└─vdb3 253:19   0  2.7G  0 part /<br>vdc    253:32   0   50G  1 disk /mnt/repo<br>vdd    253:48   0   30M  0 disk<br>localhost:~$<br>localhost:~$<br>localhost:~$ blkid|grep disk1-30mb<br>/dev/vdd: LABEL="disk1-30mb" UUID="00781ac1-ab37-4b36-abac-5ef4b9f4c990" BLOCK_SIZE="1024" TYPE="ext4"<br>localhost:~$<br>localhost:~$ sudo mkdir /mnt/disk1<br>[sudo] password for test1:<br>localhost:~$<br>localhost:~$<br>localhost:~$ sudo mount LABEL=disk1-30mb /mnt/disk1<br>localhost:~$<br>localhost:~$ df -aTh<br>Filesystem     Type        Size  Used Avail Use% Mounted on<br>sysfs          sysfs          0     0     0    - /sys<br>devtmpfs       devtmpfs     10M     0   10M   0% /dev<br>proc           proc           0     0     0    - /proc<br>devpts         devpts         0     0     0    - /dev/pts<br>shm            tmpfs       492M     0  492M   0% /dev/shm<br>/dev/vdb3      ext4        2.6G  1.8G  672M  74% /<br>tmpfs          tmpfs       197M  132K  197M   1% /run<br>mqueue         mqueue         0     0     0    - /dev/mqueue<br>securityfs     securityfs     0     0     0    - /sys/kernel/security<br>debugfs        debugfs        0     0     0    - /sys/kernel/debupn<br>pstore         pstore         0     0     0    - /sys/fs/pstore<br>tracefs        -              -     -     -    - /sys/kernel/debug/tracing<br>/dev/vdb1      ext4        272M   18M  235M   8% /boot<br>tmpfs          tmpfs       492M     0  492M   0% /tmp<br>/dev/vdc       ext4         49G   45G  4.8G  91% /mnt/repo<br>/dev/vdd       ext4         27M   46K   26M   1% /mnt/disk1<br>localhost:~$ sudo chmod a+rwx,o+t /mnt/disk1<br>localhost:~$ stat /mnt/disk1|grep 'rwx'<br>Access: (1777/drwxrwxrwt)  Uid: (    0/    root)   Gid: (    0/    root)<br>localhost:~$<br>localhost:~$ stat /tmp|grep 'rwx'<br>Access: (1777/drwxrwxrwt)  Uid: (    0/    root)   Gid: (    0/    root)<br>localhost:~$<br>localhost:~$<br>localhost:~$ touch /mnt/disk1/file1-made-on-server<br>localhost:~$<br>localhost:~$ touch /mnt/disk1/file2-made-on-server<br>localhost:~$<br>localhost:~$ ls -laR /mnt/disk1<br>/mnt/disk1:<br>total 17<br>drwxrwxrwt 3 root  root   1024 Apr  7 13:01 .<br>drwxr-xr-x 4 root  root   4096 Apr  7 05:33 ..<br>-rw-r--r-- 1 test1 test1     0 Apr  7 13:01 file1-made-on-server<br>-rw-r--r-- 1 test1 test1     0 Apr  7 13:01 file2-made-on-server<br>drwx------ 2 root  root  12288 Apr  7 11:42 lost+found<br>ls: cannot open directory '/mnt/disk1/lost+found': Permission denied<br>localhost:~$<br>localhost:~$ pwd<br>/home/test1<br>localhost:~$<br>localhost:~$ logout<br>Connection to 127.0.0.1 closed.<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ whereis termux-info<br>termux-info: /data/data/com.termux/files/usr/bin/termux-info<br>~ $<br>~ $ sftp -P 15022 test1@127.0.0.1<br>test1@127.0.0.1's password:<br>Connected to 127.0.0.1.<br>sftp><br>sftp> cd /mnt/disk1<br>sftp> ls -l<br>-rw-r--r--    ? test1    test1           0 Apr  7 09:01 file1-made-on-server<br>-rw-r--r--    ? test1    test1           0 Apr  7 09:01 file2-made-on-server<br>drwx------    ? root     root        12288 Apr  7 07:42 lost+found<br>sftp> put /data/data/com.termux/files/usr/bin/termux-info<br>Uploading /data/data/com.termux/files/usr/bin/termux-info to /mnt/disk1/termux-info<br>termux-info                         100% 3270    24.5KB/s   00:00<br>sftp> ls -l<br>-rw-r--r--    ? test1    test1           0 Apr  7 09:01 file1-made-on-server<br>-rw-r--r--    ? test1    test1           0 Apr  7 09:01 file2-made-on-server<br>drwx------    ? root     root        12288 Apr  7 07:42 lost+found<br>-rwx------    ? test1    test1        3270 Apr  7 09:11 termux-info<br>sftp><br>sftp> quit<br>~ $<br>~ $<br>~ $<br>~ $<br>~ $ export TERMUX_RANDOM_PORT=$(shuf --input-range=49152-65535  --head-count=1  --random-source=/dev/urandom --repeat)<br>~ $<br>~ $ echo $TERMUX_RANDOM_PORT<br>60676<br>~ $ darkhttpd $DIRECTORY_NAME_FROM_mktemp --port $TERMUX_RANDOM_PORT<br>darkhttpd/1.14, copyright (c) 2003-2022 Emil Mikulic.<br>listening on: http://0.0.0.0:60676/<br>127.0.0.1 - - [06/Apr/2023:23:31:22 -0400] "GET / HTTP/1.1" 200 537 "" "Links (2.28; Linux 5.15.105-0-virt x86_64; GNU C 12.2.1; dump)"<br>^C~ $<br>~ $<br>~ $<br>~ $ ssh test1@127.0.0.1 -p 15022<br>test1@127.0.0.1's password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~$<br>localhost:~$ sudo umount /mnt/disk1<br>[sudo] password for test1:<br>localhost:~$<br>localhost:~$ exit<br>logout<br>Connection to 127.0.0.1 closed.                                       <br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk1 (#block784): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/test-disk1-30mb.ext (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu) ~ $<br>~ $ echo 'device_del virt1' | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) device_del virt1<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block103): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block366): /storage/emulated/0/Download/ext4-test-directory.iuDxyNoR3C/vmtest1.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block561): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br>(qemu) ~ $<br>~ $<br>~ $ echo 'system_powerdown'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) system_powerdown<br>(qemu) ~ $<br></pre></td>
</tr>
</table>

---

<p><br></p>

### Reference Links


1. "An introduction to Linux filesystems": https://opensource.com/life/16/10/introduction-linux-filesystems (Linux "mount" command)
2. "mount Command in Linux | Explained": https://itslinuxfoss.com/mount-command-linux/
2. "How to Mount and Unmount Filesystems in Linux": https://www.baeldung.com/linux/mount-unmount-filesystems (Linux "fdisk" command)
2. "How to Mount and Unmount File Systems in Linux": https://linuxize.com/post/how-to-mount-and-unmount-file-systems-in-linux/  (Linux "fdisk" command)
2. "Managing partitions in Linux with fdisk": https://www.redhat.com/sysadmin/partitions-fdisk
2. "Creating and managing partitions in Linux with parted": https://www.redhat.com/sysadmin/partitions-parted
2. "Linux mount Command with Examples": https://phoenixnap.com/kb/linux-mount-command
2. "An introduction to the Linux /etc/fstab file": https://www.redhat.com/sysadmin/etc-fstab
2. "Chapter 24. Mounting file systems": https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/managing_file_systems/index
2. "Linux: Mount Disk Partition Using LABEL": https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/
2. "Linux commands: du and the options you should be using": https://www.redhat.com/sysadmin/du-command-options
2. "Hard links and soft links in Linux explained": https://www.redhat.com/sysadmin/linking-linux-explained
2. "Linux permissions: SUID, SGID, and sticky bit": https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
2. "How to audit permissions with the find command": https://www.redhat.com/sysadmin/audit-permissions-find
2. "Getting started with socat, a multipurpose relay tool for Linux": https://www.redhat.com/sysadmin/getting-started-socat
2. "Basic troubleshooting with telnet and netcat": https://www.redhat.com/sysadmin/telnet-netcat-troubleshooting (Linux "nc" command)
2. Linux "mktemp" command: https://www.gnu.org/software/coreutils/manual/coreutils.html
2. "How to use grep": https://www.redhat.com/sysadmin/how-to-use-grep
2. "Manipulating text at the command line with grep": https://www.redhat.com/sysadmin/manipulating-text-grep
2. "Manipulating text at the command line with sed": https://www.redhat.com/sysadmin/manipulating-text-sed
2. "Manipulating text with sed and grep": https://www.redhat.com/sysadmin/manipulating-text-sed-grep
2. "How to Kill a Process in Linux? Commands to Terminate": https://phoenixnap.com/kb/how-to-kill-a-process-in-linux
2. kill, ps, "Linux Command Basics: 7 commands for process management": https://www.redhat.com/sysadmin/linux-command-basics-7-commands-process-management
2. "Bash scripting: Moving from backtick operator to $ parentheses": https://www.redhat.com/sysadmin/backtick-operator-vs-parens
2. Linux ext4 filesystem: "Filesystems in the Linux kernel": https://docs.kernel.org/filesystems/index.html , https://docs.kernel.org/filesystems/ext4/index.html ("ext4 Data Structures and Algorithms"), https://www.cyberciti.biz/faq/linux-modify-partition-labels-command-to-change-diskname/ ("Linux Change Disk Label Name on EXT2 / EXT3 / EXT4 File Systems"), https://www.redhat.com/sysadmin/disk-space ("Linux sysadmins want to know: Where did my disk space go?")
2. "What sysadmins need to know about using Bash": https://www.redhat.com/sysadmin/bash-navigation
2. "10 basic Linux commands you need to know": https://www.redhat.com/sysadmin/basic-linux-commands
2. "8 fundamental Linux file-management commands for new users": https://www.redhat.com/sysadmin/linux-file-management-commands
2. "8 essential Linux file navigation commands for new users": https://www.redhat.com/sysadmin/Linux-file-navigation-commands
2. "Basic Linux commands and tools every sysadmin should know": https://clockhash.com/blog/basic-linux-commands-and-tools-every-sysadmin-should-know
2. bash: https://www.gnu.org/software/bash/manual/bash.html ("Bash Reference Manual"), https://www.redhat.com/sysadmin/linux-environment-variables ("Linux environment variable tips and tricks"), https://www.redhat.com/sysadmin/scripting-writing-text-file ("Bash scripting: How to write data to text files"), https://www.redhat.com/sysadmin/pipes-command-line-linux ("Working with pipes on the Linux command line" "here-document (heredoc)" "here-string"), https://linuxhint.com/linux-pipe-command-examples/ ("Linux Pipe Command with Examples"), https://www.redhat.com/sysadmin/linux-shell-redirection-pipelining ("How to manipulate files with shell redirection and pipelines in Linux"), https://www.redhat.com/sysadmin/redirect-shell-command-script-output ("How to redirect shell command output"), https://www.redhat.com/sysadmin/history-command ("How to manage your Linux command history"), https://www.redhat.com/sysadmin/parsing-bash-history ("Parsing Bash history in Linux"), https://tldp.org/LDP/abs/html/ ("Advanced Bash-Scripting Guide" "Here Documents"), https://wiki.bash-hackers.org
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. "The Linux man-pages project": https://www.kernel.org/doc/man-pages/ , https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/book/
2. "How to find out what a Linux command does": https://www.redhat.com/sysadmin/linux-command-documentation
2. Linux 'tree" and "ls" commands: https://www.cyberciti.biz/faq/linux-show-directory-structure-command-line/ ("Linux see directory tree structure using tree command"), https://www.redhat.com/sysadmin/ls-command-options ("Sysadmin tools: 11 ways to use the ls command in Linux"), https://www.redhat.com/sysadmin/Linux-file-navigation-commands ("8 essential Linux file navigation commands for new users")
2. "How to Use the less, more, and most Commands to Read Text Files in Linux": https://www.makeuseof.com/use-less-more-and-most-linux-commands/
2. Linux text editor "nano": https://www.redhat.com/sysadmin/getting-started-nano ("Getting started with Nano")
2. Linux text editors "vi", "vim", "ed": https://www.redhat.com/sysadmin/get-started-vi-editor ("How to get started with the Vi editor"), https://www.redhat.com/sysadmin/introduction-vi-editor ("An introduction to the vi editor"), https://www.redhat.com/sysadmin/beginners-guide-vim ("Linux basics: A beginner's guide to text editing with vim"), https://www.redhat.com/sysadmin/vim-commands ("Vim: Basic and intermediate commands"), https://www.redhat.com/sysadmin/introduction-ed-editor ("How to get started with the ed text editor")
2. Linux web browswer "links": http://links.twibright.com , http://links.twibright.com/download.php ("Documentation"), https://www.tecmint.com/command-line-web-browsers/ ("A Command Line Web Browsing with Lynx and Links Tools")
2. Linux "grep" command: https://www.redhat.com/sysadmin/find-text-files-using-grep ("Find text in files using the Linux grep command")
2. Linux "echo" command: https://phoenixnap.com/kb/echo-command-linux ("Echo Command in Linux (With Examples)"), https://www.tecmint.com/echo-command-in-linux/ ("15 Practical Examples of ‘echo’ command in Linux"), 
2. Linux "find" command: https://www.redhat.com/sysadmin/linux-find-command ("10 ways to use the Linux find command"), : https://www.redhat.com/sysadmin/find-best-friend ("When it comes to Linux system troubleshooting, find is my best friend")
2. Regular expressions (regex): https://www.redhat.com/sysadmin/introducing-regular-expressions ("Introducing regular expressions"), https://www.redhat.com/sysadmin/getting-started-regular-expressions-example ("Getting started with regular expressions: An example"), https://www.redhat.com/sysadmin/regex-grep-data-flow ("Regex and grep: Data flow and building blocks"), https://www.redhat.com/sysadmin/regular-expressions-pulling-it-all-together ("Regular expressions: Pulling it all together"), https://opensource.com/article/18/5/getting-started-regular-expressions ("Getting started with regular expressions")
2. Linux "chmod" command: https://www.redhat.com/sysadmin/linux-file-permissions-xplained ("Linux file permissions explained"), https://www.redhat.com/sysadmin/introduction-chmod ("Linux permissions: An introduction to chmod"), https://www.redhat.com/sysadmin/manage-permissions ("How to manage Linux permissions for users, groups, and others"), https://www.redhat.com/sysadmin/linux-permissions ("What sysadmins need to know about Linux permissions")
2. Linux "bc" command: https://www.gnu.org/software/bc/manual/html_mono/bc.html ("bc" "an arbitrary precision calculator language"), https://linuxconfig.org/bc ("bc command in Linux with examples"), https://web.archive.org/web/20211207113205/docstore.mik.ua/orelly/unix/upt/ch49_03.htm ("Chapter 49 Working with Numbers" "49.3 Gotchas in Base Conversion"), https://www.networkworld.com/article/3681079/converting-numbers-on-linux-among-decimal-hexadecimal-octal-and-binary.html ("Converting numbers on Linux among decimal, hexadecimal, octal, and binary"), https://www.theunixschool.com/2011/05/bc-unix-calculator.html ("bc - Unix calculator"),  https://www.real-world-systems.com/docs/bc.1.html ("bc" "arbitrary precision calculator"), http://www.physics.smu.edu/coan/linux/bc.html ("6. (Very) Brief intro to bc")
2. Linux "apt" command: https://linuxhint.com/debian_sources-list/ ("Understanding and Using Debian sources.list"), https://wiki.debian.org/SourcesList ("Configuring Apt Sources")
2. Web-based Distributed Authoring and Versioning (WebDAV), Linux command "cadaver": http://www.webdav.org , https://docs.vscentrum.be/en/latest/data/cadaver_client_access.html ("Cadaver Client Access"), https://github.com/hpcloud/swift-webdav/blob/master/doc/Cadaver.md ("Using the Cadaver WebDAV Client"). https://help.webpal.net/apis/webdav ("WebPal Resources for Editors, Admins, Collaborators and Coders" "WebDAV Interface")
2. Check the apps: https://www.virustotal.com/gui/home/url ("OPSWAT. MetaDefender Cloud"), https://metadefender.opswat.com ("VirusTotal")
2. darkhttpd: When you need a web server in a hurry.: https://github.com/emikulic/darkhttpd ([@emikulic](https://github.com/emikulic)), https://unix4lyfe.org/darkhttpd/ ("darkhttpd" "When you need a web server in a hurry.")
<p><br></p>

### Additional Installed Software
- Apk Analyzer (Martin Styk, sk.styk.martin.apkanalyzer): https://github.com/MartinStyk/AndroidApkAnalyzer (@MartinStyk), https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer
- Chmod calculator (Bonaventura Novellino, com.chmod.calc.o): https://play.google.com/store/apps/details?id=com.chmod.calc.o
- Device Info HW (Andrey Efremov, ru.andr7e.deviceinfohw): https://play.google.com/store/apps/details?id=ru.andr7e.deviceinfohw
- Files (Marc apps & software, com.marc.files): https://play.google.com/store/apps/details?id=com.marc.files
- Firefox Beta: (mozilla-mobile. org.mozilla.firefox_beta): https://github.com/mozilla-mobile/firefox-android (@mozilla-mobile), https://www.mozilla.org/en-US/firefox/browsers/mobile/
- Hash Droid (Hobby One, com.hobbyone.HashDroid): https://f-droid.org/en/packages/com.hobbyone.HashDroid/ , https://github.com/HobbyOneDroid/HashDroid (@HobbyOneDroid), https://play.google.com/store/apps/details?id=com.hobbyone.HashDroid
- Material Files (Hai Zhang, me.zhanghai.android.files): https://github.com/zhanghai/MaterialFiles (@zhanghai), https://play.google.com/store/apps/details?id=me.zhanghai.android.files
- MiX Image (Hootan Parsa, com.mixplorer.addon.image): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- MiX PDF (Hootan Parsa, com.mixplorer.addon.pdf): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- Primitive FTPd (wolpi, org.primftpd): https://github.com/wolpi/prim-ftpd (@wolpi), https://play.google.com/store/apps/details?id=org.primftpd
- RealCalc Scientific Calculator (Quartic Software, uk.co.nickfines.RealCalc): https://play.google.com/store/apps/details?id=uk.co.nickfines.RealCalc
- Simple HTTP Server (Phlox Development, com.phlox.simpleserver): https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- Termux:GUI (termux, com.termux.gui): https://github.com/termux/termux-gui (@termux), https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- USB Device Info (Alexandros Schillings, aws.apps.usbDeviceEnumerator): https://play.google.com/store/apps/details?id=aws.apps.usbDeviceEnumerator


---
---
---


<a id="NoteAfterNote-3"></a><h3 align="center">NoteAfterNote-3<br>Termux And The ext4 Filesystem, Part 3 Of 5: QEMU, A Guest Operating System, LUKS Encryption, lighttpd, WebDAV<br>Published: April 12, 2023<br>Link: https://gist.github.com/NoteAfterNote/cabd411777f2ad5ae57d3d98c576471c</h3>


<p><br></p>

### Mobile Device Configuration
   - Rooted: No
   - Connected to any network: No
   - Operating system: 

         neofetch --stdout|grep --color=never --ignore-case 'os:'
            OS: Android 10 armv8l 
   - CPU:

         neofetch --stdout|grep --color=never --ignore-case 'cpu:'
            CPU: Qualcomm SDM439 (8) @ 2.016GHz 
   - Display resolution: 1520x720
   - Builtin internal storage: 16 Gigabytes
   - Builtin memory: 2 Gigabytes
   - Available internal storage space: Less than 4 Gigabytes
   - Application Binary Interface (ABI): armeabi-v7a, 32-bit
   - Linux shell: bash (Bourne Again SHell)
   - Termux wake lock: Always enable
   - Termux packages installed: qemu-system-x86-64 qemu-utils  manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate
   - "Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required": https://gist.github.com/NoteAfterNote/2558deec94bac7ec9fa58aa5ad5e9d1b , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))

<p><br></p>

Guest Operating System Installation
- Read "Alpine User Handbook": https://docs.alpinelinux.org/user-handbook/0.1a/index.html
- From https://alpinelinux.org download the "Virtual" "x86_64" files: https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso , https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso.sha256
- Alpine Linux Wiki: https://wiki.alpinelinux.org
- "Setting up disks manually": https://wiki.alpinelinux.org/wiki/Setting_up_disks_manually
- "Bootloaders": https://wiki.alpinelinux.org/wiki/Bootloaders
- "Production Web server: Lighttpd": https://wiki.alpinelinux.org/wiki/Production_Web_server:_Lighttpd
- "Lighttpd": https://wiki.alpinelinux.org/wiki/Lighttpd
- Lighttpd: https://redmine.lighttpd.net/projects/lighttpd , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_webdav , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_auth
- "htdigest - manage user files for digest authentication": https://httpd.apache.org/docs/2.4/programs/htdigest.html
- "htpasswd - Manage user files for basic authentication": https://httpd.apache.org/docs/2.4/programs/htpasswd.html
- "Configuring LUKS: Linux Unified Key Setup": https://www.redhat.com/sysadmin/disk-encryption-luks
- "Frequently Asked Questions Cryptsetup/LUKS": https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions
- "Encrypted Archive with Cryptsetup": https://dashohoxha.gitlab.io/cryptsetup-encrypted-archive/ , https://github.com/dashohoxha ([dashohoxha](https://github.com/dashohoxha)), https://gitlab.com/dashohoxha
- "Basic Guide To Encrypting Linux Partitions With LUKS": https://linuxconfig.org/basic-guide-to-encrypting-linux-partitions-with-luks , https://linuxconfig.org/how-to-use-a-file-as-a-luks-device-key , https://linuxconfig.org/how-to-use-luks-with-a-detached-header
- "How To Linux Hard Disk Encryption With LUKS [ cryptsetup encrypt command ]": https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/


<p><br></p>


Do Know
- ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
- Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
- Reset a Termux terminal session at anytime, very useful when lines are truncated while booting: https://wiki.termux.com/wiki/User_Interface ("create new terminal sessions", "specify a session title", "Resetting the terminal"), see https://user-images.githubusercontent.com/21236430/126444437-7570cdcb-e825-4970-97ff-71f41e426b0f.jpg in https://github.com/termux/termux-app/issues/2184#issuecomment-883939230 ("Feature request: termux transcript #2184" "Gameye98 commented on Jul 21, 2021" )

Introduction To Linux System Administration
- Read "4 System Administration": https://tldp.org/LDP/gs/node6.html
- Read "Chapter 1. Getting Started with Linux": https://www.oreilly.com/library/view/practical-linux-system/9781098109028/ch01.html
- Read "Reboot Linux System Command": https://www.cyberciti.biz/faq/howto-reboot-linux/
- "Linux superuser access, explained": https://www.redhat.com/sysadmin/linux-superuser-access
- "Why Do We Use su – and Not Just su?": https://www.baeldung.com/linux/su-command-options
- "Linux command line basics: sudo": https://www.redhat.com/sysadmin/sudo
- "Exploring the differences between sudo and su commands in Linux": https://www.redhat.com/sysadmin/difference-between-sudo-su
- "Using sudo to delegate permissions in Linux": https://www.redhat.com/sysadmin/using-sudo-delegate
- "Real sysadmins don't sudo": https://www.redhat.com/sysadmin/sysadmins-dont-sudo
- "Linux sysadmin basics: User account management": https://www.redhat.com/sysadmin/linux-user-account-management
- "How to create, delete, and modify groups in Linux": https://www.redhat.com/sysadmin/linux-groups (Linux "id" command)
- "Linux sysadmin basics: User account management with UIDs and GIDs": https://www.redhat.com/sysadmin/user-account-gid-uid
- "Managing local group accounts in Linux": https://www.redhat.com/sysadmin/local-group-accounts
- "How to use a command line random password generator PWGEN on Linux": https://linuxconfig.org/how-to-use-a-command-line-random-password-generator-pwgen-on-linux

<p><br></p>

Network Port Numbers
- "Recommendations on Using Assigned Transport Port Numbers": https://www.rfc-editor.org/rfc/rfc7605.html
- "Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry": https://www.rfc-editor.org/rfc/rfc6335 ("the Dynamic Ports, also known as the Private or Ephemeral Ports, from 49152-65535 (never assigned)")
- Linux "shuf" command": https://www.gnu.org/software/coreutils/manual/html_node/shuf-invocation.html
   ````
   shuf --input-range=49152-65535  --head-count=1  --random-source=/dev/urandom --repeat

   shuf -i 49152-65535  -n 1 --random-source=/dev/urandom -r
   ````

<p><br></p>

4GB - 1 = (4*(1\*1024\*1024\*1024)) - 1 = (2^32) - 1 = 4294967295 bytes
- "Working with File Systems": http://web.archive.org/web/20130423054811/technet.microsoft.com/en-us/library/bb457112.aspx ("4 GB minus 1 byte"), "Working with File Systems": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb457112(v=technet.10)
- "How FAT Works": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776720(v=ws.10)

<p><br></p>

QEMU: https://www.qemu.org , https://github.com/qemu/qemu ([@qemu](https://github.com/qemu)), https://www.qemu.org/docs/master/ , https://wiki.qemu.org , https://github.com/qemu/qemu/tree/master/docs
- "Device Emulation": https://www.qemu.org/docs/master/system/device-emulation.html ("Common Terms" "Device Front End" "Device Back End"), https://qemu.readthedocs.io/en/latest/system/device-emulation.html
- "QEMU User Documentation": https://www.qemu.org/docs/master/system/qemu-manpage.html , https://qemu.readthedocs.io/en/latest/system/qemu-manpage.html
- "QEMU Documentation": https://qemu.readthedocs.io/_/downloads/en/latest/pdf/
- https://github.com/qemu/qemu/blob/master/qemu-options.hx
- "QEMU disk image utility": https://www.qemu.org/docs/master/tools/qemu-img.html ("qemu-img create"), https://qemu.readthedocs.io/en/latest/tools/qemu-img.html 


qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=$external1/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$DIRECTORY_9p_HOST_mktemp
- "Invocation": https://www.qemu.org/docs/master/system/invocation.html , https://qemu.readthedocs.io/en/latest/system/invocation.html
- "Managing device boot order with bootindex properties": https://www.qemu.org/docs/master/system/bootindex.html , https://qemu.readthedocs.io/en/latest/system/bootindex.html
- "Network emulation": https://www.qemu.org/docs/master/system/devices/net.html ("Using the user mode network stack" "-net user" "The QEMU VM behaves as if it was behind a firewall which blocks all incoming connections."), 
- "Documentation/Networking": https://wiki.qemu.org/Documentation/Networking ("hostfwd")
- "Documentation/9psetup": https://wiki.qemu.org/Documentation/9psetup ("-virtfs"), https://wiki.qemu.org/Documentation/9p
https://wiki.qemu.org/Features/VirtIORNG ("virtio-rng-pci")
- "QEMU command-line: behavior of ‘-serial stdio’ vs. ‘-serial mon:stdio’": https://kashyapc.wordpress.com/2016/02/11/qemu-command-line-behavior-of-serial-stdio-vs-serial-monstdio/ ("-serial mon:stdio")


"QEMU Monitor": https://www.qemu.org/docs/master/system/monitor.html , https://qemu.readthedocs.io/en/latest/system/monitor.html
- "Keys in the character backend multiplexer": https://www.qemu.org/docs/master/system/mux-chardev.html ("Ctrl-a h", "Ctrl-a t", "Ctrl-a c", "Ctrl-a x"), https://qemu.readthedocs.io/en/latest/system/mux-chardev.html
- "Introduction": https://www.qemu.org/docs/master/system/introduction.html ("QEMU provides a number of management interfaces including a line based Human Monitor Protocol (HMP) that allows you to dynamically add and remove devices as well as introspect the system state.")
- "Security": https://www.qemu.org/docs/master/system/security.html ("Monitor console (QMP and HMP)", "The general recommendation is that the monitor console should be exposed over a UNIX domain socket backend to the local host only."), https://qemu.readthedocs.io/en/latest/system/security.html
- "QemuDiskHotplug": https://wiki.ubuntu.com/QemuDiskHotplug and
- "QEMU Human Monitor Interface, Example Usage": https://web.archive.org/web/20180104171638/nairobi-embedded.org/qemu_monitor_console.html ("Nographic Mode")

QEMU HMP Monitor Commands
- Hotplugging disks, if a disk is mounted in the operating system, unmount it before a "device_del"

   ````
   info block

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk1.img,format=raw,id=hd1

   device_add virtio-blk-pci,drive=hd1,id=virt1

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk2.ext,format=raw,id=drive2 

   device_add virtio-blk-pci,drive=drive2,id=virtual2

   ````

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/50gb.ext,format=raw,id=hd3 

   device_add virtio-blk-pci,drive=hd3,id=virtual3

   ````

   ```` 
   device_del virtual3

   device_del virt1

   device_del virtual2

   ````
- QEMU firewall network ports

   ````
   info usernet

   hostfwd_add ::2049-:2049

   info usernet

   hostfwd_remove ::2049

   info usernet

   ````

- Communicate with QEMU through a socket

   ```` 
   echo 'info block' | nc -UN $SOCKET_FILENAME

   ```` 

<p><br></p>

---

<p><br></p>

<a id=qemu-linux-console></a>
### Termux Session 1: [QEMU-Linux-Console](#termux-session-for-qemu-linux-console)

````
cd /storage/emulated/0/Download
sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256
cd $HOME
pwd
export ISO=/storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso

# From "Reference Links"
#  "Bash scripting: Moving from backtick operator to $ parentheses": 
#   https://www.redhat.com/sysadmin/backtick-operator-vs-parens
#   
export SOCKET_FILENAME=$(mktemp socket.XXXXXXXXXX)
echo $SOCKET_FILENAME

#
# For the guest operating system 9p setup: Save the Group ID (GID)
#


export DIRECTORY_9p_HOST_mktemp=$(mktemp -d /storage/emulated/0/Download/host-guest-os.XXXXXXXXXX)

echo $DIRECTORY_9p_HOST_mktemp

export GID_DIRECTORY_9p_HOST_mktemp=$(stat $DIRECTORY_9p_HOST_mktemp|grep -i gid)

echo $GID_DIRECTORY_9p_HOST_mktemp


#
# Create the QEMU disk image
# 1 megabyte = 1024*1024 = 1048576 bytes
# 1 gigabyte = 1024*1024*1024 = 1073741824 bytes
#
# Configure test-disk1-200mb.ext so MiXplorer can read it. Details
#  in "Termux And The ext4 Filesystem, Part 1 Of 5: Reading 
#  And Writing": https://github.com/NoteAfterNote
#  Required: filename ends in ".ext" and initialize the file with zeroes
#

dd if=/dev/zero of=$DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext bs=1M count=200

mkfs.ext4 -m 0 -L disk1-200mb $DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext

qemu-img create -f raw -o preallocation=full $DIRECTORY_9p_HOST_mktemp/vmtest2.raw  2555M

export VMDISK=$DIRECTORY_9p_HOST_mktemp/vmtest2.raw



#
# Bootup may take some time. Watch the "QEMU Linux Console"
#
# Still in the Termux home directory

pwd

qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=$external1/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$DIRECTORY_9p_HOST_mktemp 


#
# Install from the ISO: no password, login as 'root'
# 50gb.ext has the v3.17/main/x86_64 and v3.17/community/x86_64
# repositories.
#
blkid
df -h
mkdir /root/repo
mkdir /root/backup
cat /etc/apk/repositories

cp -pi /etc/apk/repositories /root/backup
echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories

#   mount --help  
#   mount the disk read-only
#   mount LABEL=50gb -o ro,remount /root/repo
#   mount LABEL=50gb -o rw,remount /root/repo
mount -r LABEL=50gb /root/repo
mount|egrep repo


apk update
apk add nano inetutils-ftp cfdisk util-linux e2fsprogs e2fsprogs-extra  grub grub-bios

lsblk
blkid
#
# grep -E 'SWAP_SIZE|BOOT_SIZE' /sbin/setup-disk
#   Sizes are in megabytes
#
export SWAP_SIZE=150
export BOOT_SIZE=150
export EDITOR=nano
export KERNELOPTS="console=tty0 console=ttyS0,115200n8"
env
#
# During setup add a username.
# During setup if a pager is presented, type 'h' and 'q'
#
setup-alpine 
umount /root/repo


# Poweroff the server
poweroff

# Reset the Termux terminal if necessary: "tput reset"
# at the Termux command line or select the Termux session
# reset option.
#
# Booting from the ISO is finished. Change the
# qemu-system-x86_64 option
#     bootindex=1
# to
#     bootindex=100
# and press the Enter/Return key.
#   

qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=100  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=$external1/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$DIRECTORY_9p_HOST_mktemp 


# If the lines displayed as while booting are truncated use
# the Termux session reset option as the server continues to boot.
#
# Toggle the timestamps: ctrl-a t
# 

#
# When the server completely boots up login as root.
# 

cat /etc/os-release
uname -a
mkdir /root/backup
mkdir /mnt/repo

lsblk
blkid

cp -pi /etc/apk/repositories /root/backup
cat /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories
mount -r LABEL=50gb /mnt/repo

#
# Edit /etc/update-extlinux.conf with nano
#   timeout=0    # man syslinux
#   hidden=0

# nano --linenumbers /etc/update-extlinux.conf

grep -E 'timeout|hidden' /etc/update-extlinux.conf

# Update the settings
update-extlinux

cat /etc/modules ; cp -pi /etc/modules /root/backup
echo fuse >> /etc/modules ; cat /etc/modules

#
# Install the packages
#
apk update
date

apk add vim cryptsetup asciinema neofetch xca polkit  screen  rpm cifs-utils device-mapper rng-tools qt5-qtwebglplugin inetutils-telnet perl hdparm fsarchiver progress pv davfs2 libcdio-tools lftp-doc lftp pssh mutt neomutt alpine ncftp sshfs samba apache2 apache2-doc apache2-webdav apache2-ctl apache2-utils alpine-sdk build-base apk-tools alpine-conf busybox libpwquality fakeroot syslinux xorriso mtools dosfstools grub-efi make git sudo lynx links nodejs npm dhcp-server-vanilla ccache ccache-doc udisks2 udisks2-doc libarchive-tools libarchive-doc cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc gcc abuild binutils binutils-doc gcc-doc py3-pip pandoc iproute2 util-linux pciutils usbutils coreutils binutils findutils grep bash bash-doc utmps pass pass-otp darkhttpd vsftpd vsftpd-doc zstd pwgen easy-rsa  markdown expect sshpass keepassxc gzip rpm xz bzip2 gawk bc diffutils psmisc procps shadow util-linux-bash-completion util-linux-login mount umount netcat-openbsd nmap nmap-nping nmap-nselibs nmap-scripts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix gptfdisk sgdisk parted grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosfstools texinfo e2fsprogs e2fsprogs-extra  mkinitfs haveged f2fs-tools jfsutils ntfs-3g xfsprogs cpio whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils fuse-exfat-doc nfs-utils ncurses sharutils mandoc man-pages mandoc-apropos docs cmd:rsvg-convert iptables ip6tables perl-net-ssleay stress-ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plugins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vifm-zsh-completion  vifm-bash-completion  fish  zsh udisks2-bash-completion ncdu gnome-disk-utility zim chezdav lighttpd lighttpd-doc lighttpd-mod_webdav lighttpd-mod_auth grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsql apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate cadaver

date

#
# Change the shell
#
echo $SHELL
chsh -s /bin/bash root
chsh -s /bin/bash USER_NAME_FROM_SETUP_ALPINE

#
# Setup 9p
#  -virtfs local,security_model=none,id=host,mount_tag=host,
#     path=/storage/emulated/0/Download/$DIRECTORY_9p_HOST_mktemp
#
# For the Linux mount command: "mount_tag=host"
#
# Get GID_DIRECTORY_9p_HOST_mktemp
#

#
mkdir /mnt/9p-host
mkdir /mnt/disk1

groupadd --gid GID_DIRECTORY_9p_HOST_mktemp_HERE nine-p-host 

groupmod --append --users USER_NAME_FROM_SETUP_ALPINE nine-p-host

mount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /mnt/9p-host

mount

pwd
id

su - USER_NAME_FROM_SETUP_ALPINE
pwd
id
echo $SHELL

#
# Files should be visible from outside the guest operating
# system. File placed from outside the guest operating system should
# be visible inside the guest operating system.
# 
#
touch /mnt/9p-host/from-guest-os-to-host.txt

ls -laR /mnt/9p-host

#
# Start an ftp server: "Primitive FTPd (wolpi, org.primftpd)"
#    Configuration: anonymous ftp, port 12345
#
netstat -rn

lftp anonymous@10.0.2.2 --port 12345

#
# Exit from the 'su -' command
#
exit
pwd


# Logout and then login as root.
exit


export SUDO_EDITOR=nano
export EDITOR=nano


## Uncomment the wheel line
# sudoedit /etc/sudoers
grep wheel /etc/sudoers

#
# Setup lighttpd for WebDAV
#
mkdir -p /var/www/localhost/htdocs /var/log/lighttpd /var/lib/lighttpd

chown  -R lighttpd:lighttpd /var/log/lighttpd /var/lib/lighttpd /var/www/localhost/htdocs

ls -al  /var/www/local/host/htdocs

#
# Create an empty webdav-htpasswd-passwd file
#
touch /etc/lighttpd/webdav-htpasswd-passwd

chown root:lighttpd /etc/lighttpd/webdav-htpasswd-passwd

ls -l /etc/lighttpd/webdav-htpasswd-passwd

stat /etc/lighttpd/webdav-htpasswd-passwd

# 640 (octal) means u=rw,g=r,o-rwx
chmod 640 /etc/lighttpd/webdav-htpasswd-passwd

ls -l /etc/lighttpd/webdav-htpasswd-passwd

stat /etc/lighttpd/webdav-htpasswd-passwd


# Add WebDAV username
htpasswd -m /etc/lighttpd/webdav-htpasswd-passwd test1


cp -pi /etc/lighttpd/webdav.conf /root/backup

#
# Use "here-document" to create /etc/lighttpd/webdav.conf 
#
cat << 'END-OF-WEBDAV-CONF' > /etc/lighttpd/webdav.conf
server.port = 15081
server.upload-dirs = ( "/tmp" )
server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_file")
alias.url = ( "/webdav" => "/mnt/disk1" )
$HTTP["url"] =~ "^/webdav($|/)" {
    webdav.activate = "enable"
    webdav.is-readonly = "disable"
    webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"
    auth.backend = "htpasswd"
    auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-passwd"
    auth.require  = ("" => ("method" => "basic","realm" => "realm-webdav","require" => "valid-user"))                       
  }
END-OF-WEBDAV-CONF

cat /etc/lighttpd/webdav.conf

cp -pi /etc/lighttpd/lighttpd.conf /root/backup

echo 'include "webdav.conf"' >> /etc/lighttpd/lighttpd.conf
#
# Check the /etc/lighttpd/lighttpd.conf configuration file
#   lighttpd -tt -f /etc/lighttpd/webdav.conf

lighttpd -tt -f /etc/lighttpd/lighttpd.conf


# Services automatically started
rc-update add lighttpd default

#
# Reboot the server
#
# Toggle the console timestamps: ctrl-a t
#
reboot

# After the server boots up login as root
pwd

mount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /mnt/9p-host

mount

df -ahT

# Logout
exit

#
# The server is up.
#
# Copy the SOCKET_FILENAME from the QEMU-LINUX-CONSOLE session
# Copy the DIRECTORY_9p_HOST_mktemp from QEMU-LINUX-CONSOLE 
# Switch to the Termux-Command-Line session and 
#     SOCKET_FILENAME=PASTE_SOCKET_FILENAME_HERE
#     DIRECTORY_9p_HOST_mktemp=PASTE_DIRECTORY_NAME_FROM_mktemp_HERE 
#

````
<p><br></p>

<a id="termux-command-line"></a>
### Termux Session 2: [Termux-Command-Line](#termux-session-for-termux-command-line)

````
export SOCKET_FILENAME=PASTE_SOCKET_FILENAME_HERE

echo $SOCKET_FILENAME

export DIRECTORY_9p_HOST_mktemp=PASTE_DIRECTORY_9p_HOST_mktemp_HERE

echo $DIRECTORY_9p_HOST_mktemp

cd $HOME

#
echo 'info usernet' | nc -UN $SOCKET_FILENAME 

#
# Hotplug test-disk1-200mb.ext
#
echo 'info block'  | nc -UN $SOCKET_FILENAME 

echo "drive_add 0 if=none,file=$DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext,format=raw,id=disk1" | nc -UN $SOCKET_FILENAME

echo 'device_add virtio-blk-pci,drive=disk1,id=virt1' | nc -UN $SOCKET_FILENAME 

# Status
echo 'info block'  | nc -UN $SOCKET_FILENAME  
echo 'info block'  | nc -UN $SOCKET_FILENAME 

ssh USER_NAME_FROM_SETUP_ALPINE@127.0.0.1 -p 15022

blkid
lsblk
blkid|grep disk1-200mb

grep -i virt /var/log/messages | tail -10

dmesg|grep -i virt|tail -5
sudo dmesg|grep -i virt|tail -5

sudo mount LABEL=disk1-200mb /mnt/disk1


# 
# Set the sticky bit
#
sudo chmod a+rwx,o+t /mnt/disk1
stat /mnt/disk1|grep 'rwx'
# Compare with /tmp
stat /tmp|grep 'rwx'

ls -alR /mnt/disk1

touch /mnt/disk1/file1-made-on-server
touch /mnt/disk1/file2-made-on-server

pwd

#
# LUKS
#
sudo mkdir /mnt/disk2

date
cryptsetup benchmark
date

fallocate -l 30M /mnt/9p-host/disk2-luks-30mb.img

dd if=/dev/urandom of=/mnt/9p-host/disk2-luks-30mb.img bs=1M count=30

sudo losetup --show --find /mnt/9p-host/disk2-luks-30mb.img

sudo cryptsetup luksFormat --type=luks2 LOOP_DEVICE
sudo cryptsetup luksOpen LOOP_DEVICE mapped-disk2-luks

sudo mkfs.ext4 -m 0 -L disk2-luks /dev/mapper/mapped-disk2-luks

sudo mount /dev/mapper/mapped-disk2-luks /mnt/disk2


sudo chown USER_NAME_FROM_ALPINE_SETUP:USER_NAME_FROM_ALPINE_SETUP /mnt/disk2/.

sudo umount /mnt/disk2
sudo cryptsetup luksClose mapped-disk2-luks

sudo losetup --detach LOOP_DEVICE

#
# Add a file
#

sudo losetup --show --find /mnt/9p-host/disk2-luks-30mb.img

sudo cryptsetup luksOpen LOOP_DEVICE mapped-disk2-luks

sudo mount /dev/mapper/mapped-disk2-luks /mnt/disk2

ls -laR /mnt/disk2
touch /mnt/disk2/file3-from-server 
ls -laR /mnt/disk2

sudo umount /mnt/disk2
sudo cryptsetup luksClose mapped-disk2-luks

sudo losetup --detach LOOP_DEVICE

#
# Move disk2-luks-30mb.img to disk1-200mb.ext
# Store a file on disk2-luks-30mb.img
#
df -h
ls -laR /mnt/9p-host
mv -iv /mnt/9p-host/disk2-luks-30mb.img /mnt/disk1
ls -laR /mnt/9p-host

ls -laR /mnt/disk1

# Exit the ssh session
#   logout
# Now back at the Termux command line
pwd
env
#
# WebDAV
#
# Commands for the Linux "cadaver" command
#  ls
#  lls
#  lls --help
#  lls --coreutils-prog=ls
#  lls --coreutils-prog=ls -l
#  lcd DIRECTORY_9p_HOST_mktemp
#  lpwd
#  lls --coreutils-prog=ls -l
#  ls
#  get file1-from-server
#  get file1-made-on-server
#  lls --coreutils-prog=ls -l
#  put /data/data/com.termux/files/usr/bin/termux-info
#  ls
#  quit

whereis termux-info
cadaver http://127.0.0.1:15081/webdav
ls -alR --color=never DIRECTORY_9p_HOST_mktemp


cd $HOME

#
# Guest operating system login
#
ssh USERNAME_FROM_SETUP_ALPINE@127.0.0.1 -p 15022

sudo umount /mnt/disk1
exit


# Switch to the QEMU-Linux-Console session
#   login as root
#   type 'poweroff'
#  
````

<p><br></p>

<a id="termux-session-for-qemu-linux-console"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#qemu-linux-console">QEMU-Linux-Console</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ cd /storage/emulated/0/Download<br>.../0/Download $ sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256<br>alpine-virt-3.17.3-x86_64.iso: OK<br>.../0/Download $<br>.../0/Download $ cd $HOME<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ export ISO=/storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso<br>~ $<br>~ $ export SOCKET_FILENAME=$(mktemp socket.XXXXXXXXXX)<br>~ $<br>~ $ echo $SOCKET_FILENAME<br>socket.RkS6jHIE5Q<br>~ $<br>~ $<br>export DIRECTORY_9p_HOST_mktemp=$(mktemp -d /storage/emulated/0/Download/host-guest-os.XXXXXXXXXX)<br>~ $<br>~ $ echo $DIRECTORY_9p_HOST_mktemp<br>/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>~ $<br>~ $ export GID_DIRECTORY_9p_HOST_mktemp=$(stat $DIRECTORY_9p_HOST_mktemp|grep -i gid)<br>~ $<br>~ $ echo $GID_DIRECTORY_9p_HOST_mktemp<br>Access: (0770/drwxrwx---) Uid: ( 0/ root) Gid: ( 9997/everybody)<br>~ $<br>~ $ dd if=/dev/zero of=$DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext bs=1M count=200<br>200+0 records in<br>200+0 records out<br>209715200 bytes (210 MB, 200 MiB) copied, 3.04785 s, 68.8 MB/s<br>~ $<br>~ $ mkfs.ext4 -m 0 -L disk1-200mb $DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext<br>mke2fs 1.47.0 (5-Feb-2023)<br>Creating filesystem with 204800 1k blocks and 51200 inodes<br>Filesystem UUID: 29564dd2-6701-4c01-bd5c-e653af0a44e3<br>Superblock backups stored on blocks:<br>        8193, 24577, 40961, 57345, 73729<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (4096 blocks): done<br>Writing superblocks and filesystem accounting information: done<br><br>~ $<br>~ $ qemu-img create -f raw -o preallocation=full $DIRECTORY_9p_HOST_mktemp/vmtest2.raw  2555M<br>Formatting '/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/vmtest2.raw', fmt=raw size=2679111680 preallocation=full<br>~ $<br>~ $ export VMDISK=$DIRECTORY_9p_HOST_mktemp/vmtest2.raw<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $                                                                                     ~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=$external1/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$DIRECTORY_9p_HOST_mktemp<br><br>OpenRC 0.45.2 is starting up Linux 5.15.104-0-virt (x86_64)<br><br> * /proc is already mounted<br> * Mounting /run ... * /run/openrc: creating directory<br> * /run/lock: creating directory<br> * /run/lock: correcting owner<br> * Caching service dependencies ... [ ok ]<br> * Remounting devtmpfs on /dev ... [ ok ]<br> * Mounting /dev/mqueue ... [ ok ]<br> * Mounting modloop  ... * Verifying modloop<br> [ ok ]<br> * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]<br> * Mounting persistent storage (pstore) filesystem ... [ ok ]                            * Starting busybox mdev ... [ ok ]                                                      * Scanning hardware for mdev ... [ ok ]                                                 * Loading hardware drivers ... [ ok ]                                                   * Loading modules ... [ ok ]                                                            * Setting system clock using the hardware clock [UTC] ... [ ok ]                        * Checking local filesystems  ... [ ok ]                                                * Remounting filesystems ... [ ok ]                                                     * Mounting local filesystems ... [ ok ]                                                 * Configuring kernel parameters ... [ ok ]<br> * Migrating /var/lock to /run/lock ... [ ok ]<br> * Creating user login records ... [ ok ]<br> * Cleaning /tmp directory ... [ ok ]<br> * Setting hostname ... [ ok ]                                                           * Starting busybox syslog ... [ ok ]                                                    * Starting firstboot ... [ ok ]                                                                                                                                                Welcome to Alpine Linux 3.17                                                            Kernel 5.15.104-0-virt on an x86_64 (/dev/ttyS0)                                                                                                                                localhost login: root                                                                   Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~# blkid<br><br>/dev/loop/0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" TYPE="ext4"<br>/dev/vda2: TYPE="vfat"<br>/dev/vda1: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/vda: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/loop0: TYPE="squashfs"<br>localhost:~#<br>localhost:~# df -h<br>Filesystem                Size      Used Available Use% Mounted on<br>devtmpfs                 10.0M         0     10.0M   0% /dev<br>shm                     491.6M         0    491.6M   0% /dev/shm<br>/dev/vda                 49.0M     49.0M         0 100% /media/vda<br>tmpfs                   491.6M     10.4M    481.2M   2% /<br>tmpfs                   196.6M     44.0K    196.6M   0% /run<br>/dev/loop0               14.1M     14.1M         0 100% /.modloop<br>localhost:~#<br>localhost:~# mkdir /root/repo<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>localhost:~#<br>localhost:~# cp -pi /etc/apk/repositories /root/backup<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>/root/repo/alpine/v3.17/main<br>/root/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /root/repo<br>localhost:~#<br>localhost:~# mount|egrep repo<br>/dev/vdc on /root/repo type ext4 (ro,relatime)<br>localhost:~#<br>localhost:~# apk update<br>3.17.3 [/media/vda/apks]<br>v3.17.3-51-gb3e182d1e6a [/root/repo/alpine/v3.17/main]<br>v3.17.3-50-ga35f8409359 [/root/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~#<br>localhost:~#<br>localhost:~# apk add nano inetutils-ftp cfdisk util-linux e2fsprogs e2fsprogs-ex<br>tra  grub grub-bios<br>(1/53) Installing libblkid (2.38.1-r1)<br>(2/53) Installing libuuid (2.38.1-r1)<br>(3/53) Installing libfdisk (2.38.1-r1)<br>(4/53) Installing libmount (2.38.1-r1)<br>(5/53) Installing ncurses-terminfo-base (6.3_p20221119-r0)<br>(6/53) Installing ncurses-libs (6.3_p20221119-r0)<br>(7/53) Installing libsmartcols (2.38.1-r1)<br>(8/53) Installing cfdisk (2.38.1-r1)<br>(9/53) Installing libcom_err (1.46.6-r0)<br>(10/53) Installing e2fsprogs-libs (1.46.6-r0)<br>(11/53) Installing e2fsprogs (1.46.6-r0)<br>(12/53) Installing e2fsprogs-extra (1.46.6-r0)<br>(13/53) Installing lddtree (1.26-r3)<br>(14/53) Installing xz-libs (5.2.9-r0)<br>(15/53) Installing zstd-libs (1.5.5-r0)<br>(16/53) Installing kmod (30-r1)<br>(17/53) Installing kmod-openrc (30-r1)<br>(18/53) Installing argon2-libs (20190702-r2)<br>(19/53) Installing device-mapper-libs (2.03.17-r1)<br>(20/53) Installing json-c (0.16-r2)<br>(21/53) Installing cryptsetup-libs (2.5.0-r2)<br>(22/53) Installing kmod-libs (30-r1)<br>(23/53) Installing mkinitfs (3.7.0-r1)<br>Executing mkinitfs-3.7.0-r1.post-install<br>(24/53) Installing grub (2.06-r7)<br>(25/53) Installing grub-bios (2.06-r7)<br>(26/53) Installing readline (8.2.0-r0)<br>(27/53) Installing inetutils-ftp (2.4-r0)<br>(28/53) Installing nano (7.0-r0)<br>(29/53) Installing util-linux (2.38.1-r1)<br>(30/53) Installing util-linux-misc (2.38.1-r1)<br>(31/53) Installing libeconf (0.4.7-r0)<br>(32/53) Installing linux-pam (1.5.2-r1)<br>(33/53) Installing runuser (2.38.1-r1)<br>(34/53) Installing mount (2.38.1-r1)<br>(35/53) Installing losetup (2.38.1-r1)<br>(36/53) Installing hexdump (2.38.1-r1)<br>(37/53) Installing uuidgen (2.38.1-r1)<br>(38/53) Installing blkid (2.38.1-r1)<br>(39/53) Installing sfdisk (2.38.1-r1)<br>(40/53) Installing mcookie (2.38.1-r1)<br>(41/53) Installing agetty (2.38.1-r1)<br>(42/53) Installing agetty-openrc (0.45.2-r7)<br>(43/53) Installing wipefs (2.38.1-r1)<br>(44/53) Installing umount (2.38.1-r1)<br>(45/53) Installing util-linux-openrc (2.38.1-r1)<br>(46/53) Installing flock (2.38.1-r1)<br>(47/53) Installing lsblk (2.38.1-r1)<br>(48/53) Installing libcap-ng (0.8.3-r1)<br>(49/53) Installing setpriv (2.38.1-r1)<br>(50/53) Installing logger (2.38.1-r1)<br>(51/53) Installing partx (2.38.1-r1)<br>(52/53) Installing fstrim (2.38.1-r1)<br>(53/53) Installing findmnt (2.38.1-r1)<br>Executing busybox-1.35.0-r29.trigger<br>OK: 40 MiB in 79 packages<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>loop0    7:0    0   14M  1 loop /.modloop<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk /media/vda<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0  2.5G  0 disk<br>vdc    253:32   0   50G  1 disk /root/repo<br>localhost:~#<br>localhost:~# blkid<br>/dev/loop0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TY"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x8"<br>localhost:~#<br>localhost:~# export SWAP_SIZE=150<br>localhost:~#<br>localhost:~# export BOOT_SIZE=150<br>localhost:~#<br>localhost:~# export EDITOR=nano<br>localhost:~#<br>localhost:~# export KERNELOPTS="console=tty0 console=ttyS0,115200n8"<br>localhost:~#<br>localhost:~# env<br>USER=root<br>SHLVL=1<br>HOME=/root<br>PAGER=less<br>LOGNAME=root<br>TERM=vt100<br>BOOT_SIZE=150<br>LC_COLLATE=C<br>PATH=/sbin:/usr/sbin:/bin:/usr/bin:/usr/local/sbin:/usr/local/bin<br>LANG=C.UTF-8<br>SWAP_SIZE=150<br>KERNELOPTS=console=tty0 console=ttyS0,115200n8<br>SHELL=/bin/ash<br>PWD=/root<br>CHARSET=UTF-8<br>EDITOR=nano<br>localhost:~#<br>localhost:~# setup-alpine<br>Enter system hostname (fully qualified form, e.g. 'foo.example.org') [localhost]<br>Available interfaces are: eth0.<br>Enter '?' for help on bridges, bonding and vlans.<br>Which one do you want to initialize? (or '?' or 'done') [eth0]<br>Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp]<br>Do you want to do any manual network configuration? (y/n) [n]<br>udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br>Changing password for root<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for root changed by root<br>Which timezone are you in? ('?' for list) [UTC]<br> * Seeding random number generator ...<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox acpid ...<br> [ ok ]<br> * Starting busybox crond ...<br> [ ok ]<br>HTTP/FTP proxy URL? (e.g. 'http://proxy:8080', or 'none') [none]<br>Which NTP client to run? ('busybox', 'openntpd', 'chrony' or 'none') [chrony] none<br>wget: bad address 'mirrors.alpinelinux.org'<br><br>r) Add random from the above list<br>f) Detect and add fastest mirror from above list<br>e) Edit /etc/apk/repositories with text editor<br><br>Enter mirror number (1-0) or URL to add (or r/f/e/done) [1] done<br>Setup a user? (enter a lower-case loginname, or 'no') [no] test<br>Full name for user test [test]<br>Changing password for test<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for test changed by root<br>Enter ssh key or URL for test (or 'none') [none]<br>(1/1) Installing doas (6.8.2-r3)<br>Executing doas-6.8.2-r3.post-install<br>Executing busybox-1.35.0-r29.trigger<br>OK: 40 MiB in 80 packages<br>Which ssh server? ('openssh', 'dropbear' or 'none') [openssh]<br> * service sshd added to runlevel default<br> * Caching service dependencies ...<br> [ ok ]<br>ssh-keygen: generating new host keys: RSA ECDSA ED25519<br> * Starting sshd ...<br> [ ok ]<br>Available disks are:<br>  fd0   (0.0 GB  )<br>  sr0   (1.1 GB QEMU     QEMU DVD-ROM    )<br>  vdb   (2.7 GB 0x1af4 )<br>Which disk(s) would you like to use? (or '?' for help or 'none') [none] vdb<br>The following disk is selected:<br>  vdb   (2.7 GB 0x1af4 )<br>How would you like to use it? ('sys', 'data', 'crypt', 'lvm' or '?' for help) [?] sys<br>WARNING: The following disk(s) will be erased:<br>  vdb   (2.7 GB 0x1af4 )<br>WARNING: Erase the above disk(s) and continue? (y/n) [n] y<br>Creating file systems...<br>Installing system on /dev/vdb3:<br>/mnt/boot is device /dev/vdb1<br>100% ████████████████████████████████████████████==> initramfs: creating /boot/initramft<br>Generating grub configuration file ...<br>Found linux image: /boot/vmlinuz-virt<br>Found initrd image: /boot/initramfs-virt<br>Warning: os-prober will not be executed to detect other bootable partitions.<br>Systems on them will not be added to the GRUB boot configuration.<br>Check GRUB_DISABLE_OS_PROBER documentation entry.<br>done<br>/boot is device /dev/vdb1<br><br>Installation is complete. Please reboot.<br>localhost:~# umount /root/repo<br>localhost:~#<br>localhost:~# poweroff<br>localhost:~# ^[[38;14R * Stopping sshd ... [ ok ]<br> * Saving random number generator seed ... * Seeding 256 bits and crediting<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Stopping busybox crond ... [ ok ]<br> * Stopping busybox syslog ... [ ok ]<br> * Stopping busybox acpid ... [ ok ]<br> * Unmounting loop devices<br> *   Remounting /.modloop read only ... [ ok ]<br> * Unmounting filesystems<br> *   Unmounting /media/vda ... [ ok ]<br> * Setting hardware clock using the system clock [UTC] ... [ ok ]<br> * Stopping busybox mdev ... [ ok ]<br> [ ok ]<br> * Terminating remaining processes ...[ 1530.260543] reboot: Power down<br>~ $<br>~ $<br>~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=100  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=$external1/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$DIRECTORY_9p_HOST_mktemp<br><br><br>[    0.000000] Linux version 5.15.106-0-virt (buildozer@build-3-17-x86_64) (gcc (Alpine 12.2.1_git20220924-r4) 12.2.1 20220924, GNU ld (GNU Binutils) 2.39) #1-Alpine SMP Wed, 05 Apr 2023 10:48:45 +0000<br>[    0.000000] Command line: BOOT_IMAGE=vmlinuz-virt root=UUID=2f076e61-7a3e-43fd-86bf-63dcde993c23 modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4 initrd=initramfs-virt<br>[    0.000000] x86/fpu: x87 FPU will use FXSAVE<br>[    0.000000] signal: max sigframe size: 1440<br>[    0.000000] BIOS-provided physical RAM map:<br>[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable<br>[    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000003ffd6fff] usable<br>[    0.000000] BIOS-e820: [mem 0x000000003ffd7000-0x000000003fffffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved<br>[    0.000000] BIOS-e820: [mem 0x000000fd00000000-0x000000ffffffffff] reserved<br>[    0.000000] NX (Execute Disable) protection: active<br>[    0.000000] SMBIOS 2.8 present.<br>[    0.000000] DMI: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.16.1-0-g3208b098f51a-prebuilt.qemu.org 04/01/2014<br>[    0.000000] tsc: Fast TSC calibration failed<br>[    0.000000] last_pfn = 0x3ffd7 max_arch_pfn = 0x400000000<br>[    0.000000] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT<br>[    0.000000] RAMDISK: [mem 0x3f929000-0x3ffd6fff]<br>[    0.000000] ACPI: Early table checksum verification disabled<br>[    0.000000] ACPI: RSDP 0x00000000000F59F0 000014 (v00 BOCHS )<br>[    0.000000] ACPI: RSDT 0x000000003FFE1BDD 000034 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: FACP 0x000000003FFE1A79 000074 (v01 BOCHS  BXPC     00000001 BXPC 00000001)                                                                                [    0.000000] ACPI: DSDT 0x000000003FFE0040 001A39 (v01 BOCHS  BXPC     00000001 BXPC 00000001)                                                                                [    0.000000] ACPI: FACS 0x000000003FFE0000 000040                                     [    0.000000] ACPI: APIC 0x000000003FFE1AED 000090 (v01 BOCHS  BXPC     00000001 BXPC 00000001)                                                                                [    0.000000] ACPI: HPET 0x000000003FFE1B7D 000038 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: WAET 0x000000003FFE1BB5 000028 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[    0.000000] ACPI: Reserving FACP table memory at [mem 0x3ffe1a79-0x3ffe1aec]<br>[    0.000000] ACPI: Reserving DSDT table memory at [mem 0x3ffe0040-0x3ffe1a78]<br>[    0.000000] ACPI: Reserving FACS table memory at [mem 0x3ffe0000-0x3ffe003f]<br>[    0.000000] ACPI: Reserving APIC table memory at [mem 0x3ffe1aed-0x3ffe1b7c]<br>[    0.000000] ACPI: Reserving HPET table memory at [mem 0x3ffe1b7d-0x3ffe1bb4]<br>[    0.000000] ACPI: Reserving WAET table memory at [mem 0x3ffe1bb5-0x3ffe1bdc]<br>[    0.000000] Zone ranges:<br>[    0.000000]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]<br>[    0.000000]   DMA32    [mem 0x0000000001000000-0x000000003ffd6fff]<br>[    0.000000]   Normal   empty<br>[    0.000000] Movable zone start for each node<br>[    0.000000] Early memory node ranges<br>[    0.000000]   node   0: [mem 0x0000000000001000-0x000000000009efff]<br>[    0.000000]   node   0: [mem 0x0000000000100000-0x000000003ffd6fff]<br>[    0.000000] Initmem setup node 0 [mem 0x0000000000001000-0x000000003ffd6fff]<br>[    0.000000] On node 0, zone DMA: 1 pages in unavailable ranges<br>[    0.000000] On node 0, zone DMA: 97 pages in unavailable ranges<br>[    0.000000] On node 0, zone DMA32: 41 pages in unavailable ranges<br>[    0.000000] ACPI: PM-Timer IO Port: 0x608<br>[    0.000000] ACPI: LAPIC_NMI (acpi_id[0xff] dfl dfl lint[0x1])<br>[    0.000000] IOAPIC[0]: apic_id 0, version 32, address 0xfec00000, GSI 0-23<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 5 global_irq 5 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 10 global_irq 10 high level)<br>[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 11 global_irq 11 high level)<br>[    0.000000] ACPI: Using ACPI (MADT) for SMP configuration information<br>[    0.000000] ACPI: HPET id: 0x8086a201 base: 0xfed00000<br>[    0.000000] smpboot: Allowing 4 CPUs, 0 hotplug CPUs<br>[    0.000000] [mem 0x40000000-0xfffbffff] available for PCI devices<br>[    0.000000] Booting paravirtualized kernel on bare hardware<br>[    0.000000] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[    0.000000] setup_percpu: NR_CPUS:256 nr_cpumask_bits:256 nr_cpu_ids:4 nr_node_ids:1<br>[    0.000000] percpu: Embedded 54 pages/cpu s183896 r8192 d29096 u524288<br>[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 257751<br>[    0.000000] Kernel command line: BOOT_IMAGE=vmlinuz-virt root=UUID=2f076e61-7a3e-43fd-86bf-63dcde993c23 modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4 initrd=initramfs-virt<br>[    0.000000] Unknown kernel command line parameters "BOOT_IMAGE=vmlinuz-virt modules=sd-mod,usb-storage,ext4", will be passed to user space.<br>[    0.000000] printk: log_buf_len individual max cpu contribution: 4096 bytes<br>[    0.000000] printk: log_buf_len total cpu_extra contributions: 12288 bytes<br>[    0.000000] printk: log_buf_len min size: 16384 bytes<br>[    0.000000] printk: log_buf_len: 32768 bytes<br>[    0.000000] printk: early log buf free: 11200(68%)<br>[    0.000000] Dentry cache hash table entries: 131072 (order: 8, 1048576 bytes, linear)<br>[    0.000000] Inode-cache hash table entries: 65536 (order: 7, 524288 bytes, linear)<br>[    0.000000] mem auto-init: stack:byref(zero), heap alloc:on, heap free:off<br>[    0.000000] Memory: 994632K/1048020K available (10246K kernel code, 1191K rwdata, 3024K rodata, 1824K init, 2032K bss, 53128K reserved, 0K cma-reserved)<br>[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1<br>[    0.000000] rcu: Hierarchical RCU implementation.<br>[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.<br>[    0.000000]  Tracing variant of Tasks RCU enabled.<br>[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.<br>[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4<br>[    0.000000] NR_IRQS: 16640, nr_irqs: 456, preallocated irqs: 16<br>[    0.000000] kfence: initialized - using 2097152 bytes for 255 objects at 0x(____ptrval____)-0x(____ptrval____)<br>[    0.000000] Console: colour VGA+ 80x25<br>[    0.000000] printk: console [tty0] enabled<br>[    0.000000] printk: console [ttyS0] enabled<br>[    0.000000] ACPI: Core revision 20210730<br>[    0.000000] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604467 ns<br>[    0.040000] APIC: Switch to symmetric I/O mode setup<br>[    0.080000] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1<br>[    0.160000] tsc: Unable to calibrate against PIT<br>[    0.160000] tsc: using HPET reference calibration<br>[    0.160000] tsc: Detected 999.989 MHz processor<br>[    0.005752] tsc: Marking TSC unstable due to TSCs unsynchronized<br>[    0.011603] Calibrating delay loop (skipped), value calculated using timer frequency.. 1999.97 BogoMIPS (lpj=9999890)<br>[    0.017173] pid_max: default: 32768 minimum: 301<br>[    0.033017] LSM: Security Framework initializing<br>[    0.052480] landlock: Up and running.<br>[    0.078025] Mount-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[    0.079663] Mountpoint-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[    0.311596] process: using AMD E400 aware idle routine<br>[    0.314749] Last level iTLB entries: 4KB 512, 2MB 255, 4MB 127<br>[    0.316652] Last level dTLB entries: 4KB 512, 2MB 255, 4MB 127, 1GB 0<br>[    0.322441] Spectre V1 : Mitigation: usercopy/swapgs barriers and __user pointer sanitization<br>[    0.326921] Spectre V2 : Mitigation: Retpolines<br>[    0.328490] Spectre V2 : Spectre v2 / SpectreRSB mitigation: Filling RSB on context switch<br>[    0.329632] Spectre V2 : Spectre v2 / SpectreRSB : Filling RSB on VMEXIT<br>[    2.000602] Freeing SMP alternatives memory: 32K<br>[    2.299198] smpboot: CPU0: AMD QEMU Virtual CPU version 2.5+ (family: 0xf, model: 0x6b, stepping: 0x1)<br>[    2.406567] Performance Events: PMU not available due to virtualization, using software events only.<br>[    2.436719] rcu: Hierarchical SRCU implementation.<br>[    2.497228] NMI watchdog: Perf NMI watchdog permanently disabled<br>[    2.545504] smp: Bringing up secondary CPUs ...<br>[    2.583022] x86: Booting SMP configuration:<br>[    2.584805] .... node  #0, CPUs:      #1<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    3.122388]  #2<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    3.514568]  #3<br>[    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[    3.812909] smp: Brought up 1 node, 4 CPUs<br>[    3.814969] smpboot: Max logical packages: 1<br>[    3.816843] ----------------<br>[    3.818083] | NMI testsuite:<br>[    3.819466] --------------------<br>[    3.820632]   remote IPI:<br>[    3.819198] INFO: NMI handler (test_nmi_ipi_callback) took too long to run: 3.265 msecs<br>[    3.850242]   ok  |<br>[    3.851347]    local IPI:  ok  |<br>[    3.860275] --------------------<br>[    3.861497] Good, all   2 testcases passed! |<br>[    3.862872] ---------------------------------<br>[    3.864479] smpboot: Total of 4 processors activated (2003.53 BogoMIPS)<br>[    4.097943] devtmpfs: initialized<br>[    4.145370] x86/mm: Memory block size: 128MB<br>[    4.230108] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[    4.237142] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)<br>[    4.399567] NET: Registered PF_NETLINK/PF_ROUTE protocol family<br>[    4.440323] audit: initializing netlink subsys (disabled)<br>[    4.482447] audit: type=2000 audit(1681292475.630:1): state=initialized audit_enabled=0 res=1<br>[    4.512475] thermal_sys: Registered thermal governor 'step_wise'<br>[    4.531426] cpuidle: using governor ladder<br>[    4.540462] cpuidle: using governor menu<br>[    4.561981] ACPI: bus type PCI registered<br>[    4.564542] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5<br>[    4.609297] PCI: Using configuration type 1 for base access<br>[    4.635701] mtrr: your CPUs had inconsistent fixed MTRR settings<br>[    4.638657] mtrr: your CPUs had inconsistent variable MTRR settings<br>[    4.639509] mtrr: your CPUs had inconsistent MTRRdefType settings<br>[    4.641219] mtrr: probably your BIOS does not setup all CPUs.<br>[    4.642844] mtrr: corrected configuration.<br>[    4.774341] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.<br>[    4.818206] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages<br>[    5.162301] ACPI: Added _OSI(Module Device)<br>[    5.166726] ACPI: Added _OSI(Processor Device)<br>[    5.167701] ACPI: Added _OSI(3.0 _SCP Extensions)<br>[    5.179373] ACPI: Added _OSI(Processor Aggregator Device)<br>[    5.182199] ACPI: Added _OSI(Linux-Dell-Video)<br>[    5.183137] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)<br>[    5.184095] ACPI: Added _OSI(Linux-HPI-Hybrid-Graphics)<br>[    5.387632] ACPI: 1 ACPI AML tables successfully acquired and loaded<br>[    5.601530] ACPI: Interpreter enabled<br>[    5.612498] ACPI: PM: (supports S0 S3 S5)<br>[    5.614189] ACPI: Using IOAPIC for interrupt routing<br>[    5.623902] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug<br>[    5.645343] ACPI: Enabled 2 GPEs in block 00 to 0F<br>[    6.093447] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-ff])<br>[    6.104088] acpi PNP0A03:00: _OSC: OS supports [ASPM ClockPM Segments MSI HPX-Type3]<br>[    6.114923] acpi PNP0A03:00: fail to add MMCONFIG information, can't access extended PCI configuration space under this bridge.<br>[    6.192114] acpiphp: Slot [3] registered<br>[    6.194987] acpiphp: Slot [4] registered<br>[    6.199322] acpiphp: Slot [5] registered<br>[    6.201888] acpiphp: Slot [6] registered<br>[    6.203977] acpiphp: Slot [7] registered<br>[    6.205618] acpiphp: Slot [8] registered<br>[    6.208458] acpiphp: Slot [9] registered<br>[    6.210652] acpiphp: Slot [10] registered<br>[    6.213033] acpiphp: Slot [11] registered<br>[    6.215546] acpiphp: Slot [12] registered<br>[    6.220464] acpiphp: Slot [13] registered<br>[    6.222839] acpiphp: Slot [14] registered<br>[    6.225030] acpiphp: Slot [15] registered<br>[    6.227803] acpiphp: Slot [16] registered<br>[    6.230500] acpiphp: Slot [17] registered<br>[    6.232848] acpiphp: Slot [18] registered<br>[    6.235687] acpiphp: Slot [19] registered<br>[    6.239473] acpiphp: Slot [20] registered<br>[    6.242152] acpiphp: Slot [21] registered<br>[    6.244364] acpiphp: Slot [22] registered<br>[    6.249302] acpiphp: Slot [23] registered<br>[    6.251040] acpiphp: Slot [24] registered<br>[    6.253499] acpiphp: Slot [25] registered<br>[    6.259288] acpiphp: Slot [26] registered<br>[    6.260547] acpiphp: Slot [27] registered<br>[    6.262506] acpiphp: Slot [28] registered<br>[    6.264182] acpiphp: Slot [29] registered<br>[    6.269311] acpiphp: Slot [30] registered<br>[    6.270760] acpiphp: Slot [31] registered<br>[    6.274966] PCI host bridge to bus 0000:00<br>[    6.280669] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]<br>[    6.283667] pci_bus 0000:00: root bus resource [io  0x0d00-0xffff window]<br>[    6.285385] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]<br>[    6.288297] pci_bus 0000:00: root bus resource [mem 0x40000000-0xfebfffff window]<br>[    6.289372] pci_bus 0000:00: root bus resource [mem 0x100000000-0x17fffffff window]<br>[    6.293431] pci_bus 0000:00: root bus resource [bus 00-ff]<br>[    6.321803] pci 0000:00:00.0: [8086:1237] type 00 class 0x060000<br>[    6.433691] pci 0000:00:01.0: [8086:7000] type 00 class 0x060100<br>[    6.482611] pci 0000:00:01.1: [8086:7010] type 00 class 0x010180<br>[    6.492117] pci 0000:00:01.1: reg 0x20: [io  0xc1e0-0xc1ef]<br>[    6.527143] pci 0000:00:01.1: legacy IDE quirk: reg 0x10: [io  0x01f0-0x01f7]<br>[    6.533903] pci 0000:00:01.1: legacy IDE quirk: reg 0x14: [io  0x03f6]<br>[    6.542829] pci 0000:00:01.1: legacy IDE quirk: reg 0x18: [io  0x0170-0x0177]<br>[    6.545702] pci 0000:00:01.1: legacy IDE quirk: reg 0x1c: [io  0x0376]<br>[    6.570528] pci 0000:00:01.3: [8086:7113] type 00 class 0x068000<br>[    6.577124] pci 0000:00:01.3: quirk: [io  0x0600-0x063f] claimed by PIIX4 ACPI<br>[    6.579883] pci 0000:00:01.3: quirk: [io  0x0700-0x070f] claimed by PIIX4 SMB<br>[    6.609318] pci 0000:00:02.0: [1234:1111] type 00 class 0x030000<br>[    6.619575] pci 0000:00:02.0: reg 0x10: [mem 0xfd000000-0xfdffffff pref]<br>[    6.659847] pci 0000:00:02.0: reg 0x18: [mem 0xfebd0000-0xfebd0fff]<br>[    6.720806] pci 0000:00:02.0: reg 0x30: [mem 0xfebc0000-0xfebcffff pref]<br>[    6.733900] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]<br>[    6.819976] pci 0000:00:03.0: [1af4:1005] type 00 class 0x00ff00<br>[    6.829198] pci 0000:00:03.0: reg 0x10: [io  0xc180-0xc19f]<br>[    6.839198] pci 0000:00:03.0: reg 0x14: [mem 0xfebd1000-0xfebd1fff]<br>[    6.869198] pci 0000:00:03.0: reg 0x20: [mem 0xfe000000-0xfe003fff 64bit pref]<br>[    7.021366] pci 0000:00:04.0: [1af4:1000] type 00 class 0x020000<br>[    7.029198] pci 0000:00:04.0: reg 0x10: [io  0xc1a0-0xc1bf]<br>[    7.029198] pci 0000:00:04.0: reg 0x14: [mem 0xfebd2000-0xfebd2fff]<br>[    7.090170] pci 0000:00:04.0: reg 0x20: [mem 0xfe004000-0xfe007fff 64bit pref]<br>[    7.109887] pci 0000:00:04.0: reg 0x30: [mem 0xfeb80000-0xfebbffff pref]<br>[    7.197578] pci 0000:00:05.0: [1af4:1001] type 00 class 0x010000<br>[    7.209198] pci 0000:00:05.0: reg 0x10: [io  0xc000-0xc07f]<br>[    7.229436] pci 0000:00:05.0: reg 0x14: [mem 0xfebd3000-0xfebd3fff]<br>[    7.249198] pci 0000:00:05.0: reg 0x20: [mem 0xfe008000-0xfe00bfff 64bit pref]<br>[    7.380335] pci 0000:00:06.0: [1af4:1001] type 00 class 0x010000<br>[    7.389198] pci 0000:00:06.0: reg 0x10: [io  0xc080-0xc0ff]<br>[    7.409603] pci 0000:00:06.0: reg 0x14: [mem 0xfebd4000-0xfebd4fff]<br>[    7.429198] pci 0000:00:06.0: reg 0x20: [mem 0xfe00c000-0xfe00ffff 64bit pref]<br>[    7.555262] pci 0000:00:07.0: [1af4:1001] type 00 class 0x010000<br>[    7.559198] pci 0000:00:07.0: reg 0x10: [io  0xc100-0xc17f]<br>[    7.581316] pci 0000:00:07.0: reg 0x14: [mem 0xfebd5000-0xfebd5fff]<br>[    7.619198] pci 0000:00:07.0: reg 0x20: [mem 0xfe010000-0xfe013fff 64bit pref]<br>[    7.750748] pci 0000:00:08.0: [1af4:1009] type 00 class 0x000200<br>[    7.759198] pci 0000:00:08.0: reg 0x10: [io  0xc1c0-0xc1df]<br>[    7.759198] pci 0000:00:08.0: reg 0x14: [mem 0xfebd6000-0xfebd6fff]<br>[    7.870305] pci 0000:00:08.0: reg 0x20: [mem 0xfe014000-0xfe017fff 64bit pref]<br>[    8.025026] ACPI: PCI: Interrupt link LNKA configured for IRQ 10<br>[    8.034735] ACPI: PCI: Interrupt link LNKB configured for IRQ 10<br>[    8.043033] ACPI: PCI: Interrupt link LNKC configured for IRQ 11<br>[    8.043033] ACPI: PCI: Interrupt link LNKD configured for IRQ 11<br>[    8.046140] ACPI: PCI: Interrupt link LNKS configured for IRQ 9<br>[    8.115620] iommu: Default domain type: Translated<br>[    8.119674] iommu: DMA domain TLB invalidation policy: lazy mode<br>[    8.156622] SCSI subsystem initialized<br>[    8.186251] pps_core: LinuxPPS API ver. 1 registered<br>[    8.189424] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it><br>[    8.193280] PTP clock support registered<br>[    8.317724] PCI: Using ACPI for IRQ routing<br>[    8.343241] hpet: 3 channels of 0 reserved for per-cpu timers<br>[    8.357623] clocksource: Switched to clocksource hpet<br>[    9.096558] VFS: Disk quotas dquot_6.6.0<br>[    9.111120] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)<br>[    9.152249] pnp: PnP ACPI init<br>[    9.246137] pnp: PnP ACPI: found 6 devices<br>[    9.695219] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns<br>[    9.705608] NET: Registered PF_INET protocol family<br>[    9.718430] IP idents hash table entries: 16384 (order: 5, 131072 bytes, linear)<br>[    9.785867] tcp_listen_portaddr_hash hash table entries: 512 (order: 1, 8192 bytes, linear)<br>[    9.792080] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)<br>[    9.796623] TCP established hash table entries: 8192 (order: 4, 65536 bytes, linear)<br>[    9.801317] TCP bind hash table entries: 8192 (order: 5, 131072 bytes, linear)<br>[    9.804931] TCP: Hash tables configured (established 8192 bind 8192)<br>[    9.821313] UDP hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[    9.826511] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[    9.848575] NET: Registered PF_UNIX/PF_LOCAL protocol family<br>[    9.856579] NET: Registered PF_XDP protocol family<br>[    9.868708] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]<br>[    9.872965] pci_bus 0000:00: resource 5 [io  0x0d00-0xffff window]<br>[    9.874481] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]<br>[    9.876421] pci_bus 0000:00: resource 7 [mem 0x40000000-0xfebfffff window]<br>[    9.878264] pci_bus 0000:00: resource 8 [mem 0x100000000-0x17fffffff window]<br>[    9.889486] pci 0000:00:01.0: PIIX3: Enabling Passive Release<br>[    9.893344] pci 0000:00:00.0: Limiting direct PCI/PCI transfers<br>[    9.895589] pci 0000:00:01.0: Activating ISA DMA hang workarounds<br>[    9.897859] PCI: CLS 0 bytes, default 64<br>[   10.030349] Initialise system trusted keyrings<br>[   10.094157] workingset: timestamp_bits=46 max_order=18 bucket_order=0<br>[   10.158604] Unpacking initramfs...<br>[   10.307417] zbud: loaded<br>[   10.372222] Key type asymmetric registered<br>[   10.374652] Asymmetric key parser 'x509' registered<br>[   10.391962] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)<br>[   10.414195] io scheduler mq-deadline registered<br>[   10.416362] io scheduler kyber registered<br>[   10.433031] io scheduler bfq registered<br>[   10.542192] ERST DBG: ERST support is disabled.<br>[   14.812397] ACPI: \_SB_.LNKC: Enabled at IRQ 11<br>[   15.887990] Freeing initrd memory: 6840K<br>[   18.838366] ACPI: \_SB_.LNKD: Enabled at IRQ 10<br>[   21.653471] ACPI: \_SB_.LNKA: Enabled at IRQ 10<br>[   24.155427] ACPI: \_SB_.LNKB: Enabled at IRQ 11<br>[   29.345587] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled<br>[   29.391613] 00:04: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A<br>[   29.667961] VMware PVSCSI driver - version 1.0.7.0-k<br>[   29.946961] scsi host0: ata_piix<br>[   30.032820] scsi host1: ata_piix<br>[   30.038565] ata1: PATA max MWDMA2 cmd 0x1f0 ctl 0x3f6 bmdma 0xc1e0 irq 14<br>[   30.055268] ata2: PATA max MWDMA2 cmd 0x170 ctl 0x376 bmdma 0xc1e8 irq 15<br>[   30.126943] i8042: PNP: PS/2 Controller [PNP0303:KBD,PNP0f13:MOU] at 0x60,0x64 irq 1,12<br>[   30.245813] serio: i8042 KBD port at 0x60,0x64 irq 1<br>[   30.256894] serio: i8042 AUX port at 0x60,0x64 irq 12<br>[   30.268362] rtc_cmos 00:05: RTC can wake from S4<br>[   30.405180] rtc_cmos 00:05: registered as rtc0<br>[   30.433994] rtc_cmos 00:05: setting system clock to 2023-04-12T09:41:44 UTC (1681292504)<br>[   30.509309] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input0<br>[   30.531479] rtc_cmos 00:05: alarms up to one day, y3k, 242 bytes nvram, hpet irqs<br>[   30.616341] ata2.00: ATAPI: QEMU DVD-ROM, 2.5+, max UDMA/100<br>[   30.697218] gre: GRE over IPv4 demultiplexor driver<br>[   30.763572] Key type dns_resolver registered<br>[   30.789124] IPI shorthand broadcast: enabled<br>[   30.961889] registered taskstats version 1<br>[   30.965866] Loading compiled-in X.509 certificates<br>[   31.002942] scsi 1:0:0:0: CD-ROM            QEMU     QEMU DVD-ROM     2.5+ PQ: 0 ANSI: 5<br>[   32.319314] Loaded X.509 cert 'Build time autogenerated kernel key: 90200cc09a919577283b2cb6eca2ff9ac9891c1d'<br>[   32.357758] zswap: loaded using pool lzo/zbud<br>[   32.459490] Key type .fscrypt registered<br>[   32.463942] Key type fscrypt-provisioning registered<br>[   32.552861] Unstable clock detected, switching default tracing clock to "global"<br>[   32.552861] If you want to keep using the local clock, then add:<br>[   32.552861]   "trace_clock=local"<br>[   32.552861] on the kernel command line<br>[   32.825033] Freeing unused kernel image (initmem) memory: 1824K<br>[   32.852466] Write protecting the kernel read-only data: 16384k<br>[   32.907778] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[   32.924160] Freeing unused kernel image (rodata/data gap) memory: 1072K<br>[   32.932283] rodata_test: all tests were successful<br>[   32.937544] Run /init as init process<br>[   34.641371] Alpine Init 3.7.0-r1<br>Alpine Init 3.7.0-r1<br>[   34.718811] Loading boot drivers...<br> * Loading boot drivers: [   36.074871] ACPI: bus type USB registered<br>[   36.093977] usbcore: registered new interface driver usbfs<br>[   36.097434] usbcore: registered new interface driver hub<br>[   36.114746] usbcore: registered new device driver usb<br>[   36.286806] usbcore: registered new interface driver usb-storage<br>[   38.974961] loop: module loaded<br>[   41.457941] Loading boot drivers: ok.<br>ok.<br>[   41.663947] Mounting root...<br> * Mounting root: [   48.936001] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[   48.940511] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[   50.597771] virtio_blk virtio2: [vda] 100352 512-byte logical blocks (51.4 MB/49.0 MiB)<br>[   50.718407]  vda: vda1 vda2<br>[   50.807728] virtio_blk virtio3: [vdb] 5232640 512-byte logical blocks (2.68 GB/2.50 GiB)<br>[   50.846261]  vdb: vdb1 vdb2 vdb3<br>[   50.923577] virtio_blk virtio4: [vdc] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[   83.202360] EXT4-fs (vdb3): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[   83.288376] Mounting root: ok.<br>ok.<br><br>   OpenRC 0.45.2 is starting up Linux 5.15.106-0-virt (x86_64)<br><br> * /proc is already mounted<br> * Mounting /run ... * /run/openrc: creating directory<br> * /run/lock: creating directory<br> * /run/lock: correcting owner<br> * Caching service dependencies ... [ ok ]<br> * Remounting devtmpfs on /dev ... [ ok ]<br> * Mounting /dev/mqueue ... [ ok ]<br> * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]<br> * Mounting persistent storage (pstore) filesystem ... [ ok ]<br> * Starting busybox mdev ... [ ok ]<br> * Scanning hardware for mdev ... [ ok ]<br> * Loading hardware drivers ... [ ok ]<br> * Loading modules ... [ ok ]<br> * Setting system clock using the hardware clock [UTC] ... [ ok ]<br> * Checking local filesystems  .../dev/vdb3: clean, 3176/144288 files, 45463/577024 blocks<br>/dev/vdb1: clean, 26/38456 files, 33614/153600 blocks<br> [ ok ]<br> * Remounting root filesystem read/write ... [ ok ]<br> * Remounting filesystems ... [ ok ]<br> * Activating swap devices ... [ ok ]<br> * Mounting local filesystems ... [ ok ]<br> * Configuring kernel parameters ... [ ok ]<br> * Migrating /var/lock to /run/lock ... [ ok ]<br> * Creating user login records ... [ ok ]<br> * Setting hostname ... [ ok ]<br> * Starting networking ... *   lo ... [ ok ]<br> *   eth0 ...udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br> [ ok ]<br> * Seeding random number generator ... * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox syslog ... [ ok ]<br> * Starting busybox acpid ... [ ok ]<br> * Starting busybox crond ... [ ok ]<br> * Starting sshd ... [ ok ]<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~#<br>localhost:~# cat /etc/os-release<br>NAME="Alpine Linux"<br>ID=alpine<br>VERSION_ID=3.17.3<br>PRETTY_NAME="Alpine Linux v3.17"<br>HOME_URL="https://alpinelinux.org/"<br>BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"<br>localhost:~#<br>localhost:~# uname -a<br>Linux localhost 5.15.106-0-virt #1-Alpine SMP Wed, 05 Apr 2023 10:48:45 +0000 x86_64 Linux<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# mkdir /mnt/repo<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0  2.5G  0 disk<br>├─vdb1 253:17   0  150M  0 part /boot<br>├─vdb2 253:18   0  150M  0 part [SWAP]<br>└─vdb3 253:19   0  2.2G  0 part /<br>vdc    253:32   0   50G  1 disk<br>localhost:~#<br><br><br>localhost:~# grep -E 'timeout|hidden' /etc/update-extlinux.conf<br># hidden<br># if set to non-zero, the boot menu will be hidden by default.<br>hidden=0<br># timeout<br>timeout=0<br>localhost:~#<br>localhost:~# update-extlinux<br>/boot is device /dev/vdb1<br>localhost:~#<br>localhost:~# cat /etc/modules ; cp -pi /etc/modules /root/backup<br>af_packet<br>ipv6<br>localhost:~#<br>localhost:~# echo fuse >> /etc/modules ; cat /etc/modules<br>af_packet<br>ipv6<br>fuse<br>localhost:~#<br>localhost:~# apk update<br>v3.17.3-51-gb3e182d1e6a [/mnt/repo/alpine/v3.17/main]<br>v3.17.3-50-ga35f8409359 [/mnt/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~# date<br>Wed Apr 12 10:10:53 UTC 2023<br>localhost:~#<br>localhost:~# apk add vim cryptsetup asciinema neofetch xca polkit  screen  rpm c<br>ifs-utils device-mapper rng-tools qt5-qtwebglplugin inetutils-telnet perl hdparm<br> fsarchiver progress pv davfs2 libcdio-tools lftp-doc lftp pssh mutt neomutt alp<br>ine ncftp sshfs samba apache2 apache2-doc apache2-webdav apache2-ctl apache2-uti<br>ls alpine-sdk build-base apk-tools alpine-conf busybox libpwquality fakeroot sys<br>linux xorriso mtools dosfstools grub-efi make git sudo lynx links nodejs npm dhc<br>p-server-vanilla ccache ccache-doc udisks2 udisks2-doc libarchive-tools libarchi<br>ve-doc cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc gcc abuild bi<br>nutils binutils-doc gcc-doc py3-pip pandoc iproute2 util-linux pciutils usbutils<br> coreutils binutils findutils grep bash bash-doc utmps pass pass-otp darkhttpd v<br>sftpd vsftpd-doc zstd pwgen easy-rsa  markdown expect sshpass keepassxc gzip rpm<br> xz bzip2 gawk bc diffutils psmisc procps shadow util-linux-bash-completion util<br>-linux-login mount umount netcat-openbsd nmap nmap-nping nmap-nselibs nmap-scrip<br>ts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix gptfdisk sgdisk part<br>ed grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosf<br>stools texinfo e2fsprogs e2fsprogs-extra  mkinitfs haveged f2fs-tools jfsutils n<br>tfs-3g xfsprogs cpio whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-ex<br>fat fuse-exfat-utils fuse-exfat-doc nfs-utils ncurses sharutils mandoc man-pages<br> mandoc-apropos docs cmd:rsvg-convert iptables ip6tables perl-net-ssleay stress-<br>ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plugins nnn-zsh-completion nnn-f<br>ish-completion  vifm vifm-fish-completion vifm-zsh-completion  vifm-bash-complet<br>ion  fish  zsh udisks2-bash-completion ncdu gnome-disk-utility zim chezdav light<br>tpd lighttpd-doc lighttpd-mod_webdav lighttpd-mod_auth grub-bash-completion apr-<br>util-dbd_mysql apr-util-dbd_pgsql apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed<br> gifsicle mlocate cadaver<br>(1/768) Installing fakeroot (1.29-r0)<br>(2/768) Installing libattr (2.5.1-r2)<br>(3/768) Installing attr (2.5.1-r2)<br>(4/768) Installing libacl (2.3.1-r1)<br>(5/768) Installing tar (1.34-r2)<br>(6/768) Installing pkgconf (1.9.4-r0)<br>(7/768) Installing patch (2.7.6-r9)<br>(8/768) Installing libgcc (12.2.1_git20220924-r4)<br>(9/768) Installing libstdc++ (12.2.1_git20220924-r4)<br>(10/768) Installing lzip (1.23-r0)<br>(11/768) Installing ca-certificates (20220614-r4)<br>(12/768) Installing brotli-libs (1.0.9-r9)<br>(13/768) Installing nghttp2-libs (1.51.0-r0)<br>(14/768) Installing libcurl (7.88.1-r1)<br>(15/768) Installing curl (7.88.1-r1)<br>(16/768) Installing abuild (3.10.0-r0)<br>Executing abuild-3.10.0-r0.pre-install<br>(17/768) Installing gdbm (1.23-r0)<br>(18/768) Installing libsasl (2.1.28-r3)<br>(19/768) Installing libldap (2.6.3-r6)<br>(20/768) Installing alpine (2.26-r1)<br>(21/768) Installing binutils (2.39-r2)<br>(22/768) Installing libmagic (5.43-r0)<br>(23/768) Installing file (5.43-r0)<br>(24/768) Installing libgomp (12.2.1_git20220924-r4)<br>(25/768) Installing libatomic (12.2.1_git20220924-r4)<br>(26/768) Installing gmp (6.2.1-r2)<br>(27/768) Installing isl25 (0.25-r0)<br>(28/768) Installing mpfr4 (4.1.0-r0)<br>(29/768) Installing mpc1 (1.2.1-r1)<br>(30/768) Installing gcc (12.2.1_git20220924-r4)<br>(31/768) Installing libstdc++-dev (12.2.1_git20220924-r4)<br>(32/768) Installing musl-dev (1.2.3-r4)<br>(33/768) Installing libc-dev (0.7.2-r3)<br>(34/768) Installing g++ (12.2.1_git20220924-r4)<br>(35/768) Installing make (4.3-r1)<br>(36/768) Installing fortify-headers (1.1-r1)<br>(37/768) Installing build-base (0.5-r3)<br>(38/768) Installing libexpat (2.5.0-r0)<br>(39/768) Installing pcre2 (10.42-r0)<br>(40/768) Installing git (2.38.4-r1)<br>(41/768) Installing alpine-sdk (1.0-r1)<br>(42/768) Installing apr (1.7.2-r0)<br>(43/768) Installing apr-util (1.6.3-r0)<br>(44/768) Installing pcre (8.45-r2)<br>(45/768) Installing apache2 (2.4.56-r0)<br>Executing apache2-2.4.56-r0.pre-install<br>(46/768) Installing less (608-r1)<br>(47/768) Installing gzip (1.12-r0)<br>(48/768) Installing libintl (0.21.1-r1)<br>(49/768) Installing lynx (2.8.9_p1-r8)<br>(50/768) Installing apache2-ctl (2.4.56-r0)<br>(51/768) Installing apache2-doc (2.4.56-r0)<br>(52/768) Installing apache2-utils (2.4.56-r0)<br>(53/768) Installing apache2-webdav (2.4.56-r0)<br>(54/768) Installing mariadb-connector-c (3.3.3-r0)<br>(55/768) Installing apr-util-dbd_mysql (1.6.3-r0)<br>(56/768) Installing libpq (15.2-r0)<br>(57/768) Installing apr-util-dbd_pgsql (1.6.3-r0)<br>(58/768) Installing sqlite-libs (3.40.1-r0)<br>(59/768) Installing apr-util-dbd_sqlite3 (1.6.3-r0)<br>(60/768) Installing apr-util-ldap (1.6.3-r0)<br>(61/768) Installing libbz2 (1.0.8-r4)<br>(62/768) Installing libffi (3.4.4-r0)<br>(63/768) Installing mpdecimal (2.5.1-r1)<br>(64/768) Installing python3 (3.10.11-r0)<br>(65/768) Installing ncurses (6.3_p20221119-r0)<br>(66/768) Installing asciinema (2.2.0-r0)<br>(67/768) Installing bash (5.2.15-r0)<br>Executing bash-5.2.15-r0.post-install<br>(68/768) Installing bash-doc (5.2.15-r0)<br>(69/768) Installing bc (1.07.1-r2)<br>(70/768) Installing binutils-doc (2.39-r2)<br>(71/768) Installing lzo (2.10-r3)<br>(72/768) Installing eudev-libs (3.2.11-r4)<br>(73/768) Installing btrfs-progs (6.0.2-r0)<br>(74/768) Installing bzip2 (1.0.8-r4)<br>(75/768) Installing neon (0.32.4-r0)<br>(76/768) Installing cadaver (0.23.3-r6)<br>(77/768) Installing hiredis (1.0.2-r1)<br>(78/768) Installing ccache (4.7.5-r0)<br>(79/768) Installing ccache-doc (4.7.5-r0)<br>(80/768) Installing dbus-libs (1.14.4-r0)<br>(81/768) Installing avahi-libs (0.8-r6)<br>(82/768) Installing libdaemon (0.14-r3)<br>(83/768) Installing libevent (2.1.12-r5)<br>(84/768) Installing avahi (0.8-r6)<br>Executing avahi-0.8-r6.pre-install<br>(85/768) Installing glib (2.74.6-r0)<br>(86/768) Installing avahi-glib (0.8-r6)<br>(87/768) Installing gsettings-desktop-schemas (43.0-r0)<br>(88/768) Installing nettle (3.8.1-r0)<br>(89/768) Installing p11-kit (0.24.1-r1)<br>(90/768) Installing libtasn1 (4.19.0-r0)<br>(91/768) Installing libunistring (1.1-r0)<br>(92/768) Installing gnutls (3.7.8-r3)<br>(93/768) Installing libproxy (0.4.18-r1)<br>(94/768) Installing glib-networking (2.74.0-r2)<br>(95/768) Installing libidn2 (2.3.4-r0)<br>(96/768) Installing libpsl (0.21.1-r1)<br>(97/768) Installing libsoup3 (3.2.2-r0)<br>(98/768) Installing libxml2 (2.10.3-r1)<br>(99/768) Installing phodav (3.0-r0)<br>(100/768) Installing chezdav (3.0-r0)<br>(101/768) Installing krb5-conf (1.0-r2)<br>(102/768) Installing keyutils-libs (1.6.3-r1)<br>(103/768) Installing libverto (0.3.2-r1)<br>(104/768) Installing krb5-libs (1.20.1-r0)<br>(105/768) Installing talloc (2.3.4-r0)<br>(106/768) Installing libwbclient (4.16.10-r0)<br>(107/768) Installing cifs-utils (7.0-r0)<br>(108/768) Installing lz4-libs (1.9.4-r1)<br>(109/768) Installing libarchive (3.6.1-r2)<br>(110/768) Installing rhash-libs (1.4.3-r1)<br>(111/768) Installing libuv (1.44.2-r0)<br>(112/768) Installing cmake (3.24.4-r0)<br>(113/768) Installing cmake-doc (3.24.4-r0)<br>(114/768) Installing libxau (1.0.10-r0)<br>(115/768) Installing libmd (1.0.4-r0)<br>(116/768) Installing libbsd (0.11.7-r0)<br>(117/768) Installing libxdmcp (1.1.4-r0)<br>(118/768) Installing libxcb (1.15-r0)<br>(119/768) Installing libx11 (1.8.4-r0)<br>(120/768) Installing libxext (1.3.5-r0)<br>(121/768) Installing libxrender (0.9.11-r0)<br>(122/768) Installing libpng (1.6.38-r0)<br>(123/768) Installing freetype (2.12.1-r0)<br>(124/768) Installing fontconfig (2.14.1-r0)<br>(125/768) Installing pixman (0.42.2-r0)<br>(126/768) Installing cairo (1.17.6-r3)<br>(127/768) Installing shared-mime-info (2.2-r2)<br>(128/768) Installing libjpeg-turbo (2.1.4-r0)<br>(129/768) Installing libwebp (1.2.4-r1)<br>(130/768) Installing tiff (4.4.0-r3)<br>(131/768) Installing gdk-pixbuf (2.42.10-r0)<br>(132/768) Installing libxft (2.3.7-r0)<br>(133/768) Installing fribidi (1.0.12-r0)<br>(134/768) Installing graphite2 (1.3.14-r2)<br>(135/768) Installing harfbuzz (5.3.1-r1)<br>(136/768) Installing pango (1.50.13-r0)<br>(137/768) Installing rsvg-convert (2.55.1-r0)<br>(138/768) Installing skalibs (2.12.0.1-r0)<br>(139/768) Installing utmps-libs (0.1.2.0-r1)<br>(140/768) Installing coreutils (9.1-r0)<br>(141/768) Installing cpio (2.13-r3)<br>(142/768) Installing popt (1.19-r0)<br>(143/768) Installing cryptsetup (2.5.0-r2)<br>(144/768) Installing cryptsetup-openrc (2.5.0-r2)<br>(145/768) Installing darkhttpd (1.14-r0)<br>Executing darkhttpd-1.14-r0.pre-install<br>(146/768) Installing darkhttpd-openrc (1.14-r0)<br>(147/768) Installing davfs2 (1.6.1-r0)<br>Executing davfs2-1.6.1-r0.pre-install<br>(148/768) Installing dbus (1.14.4-r0)<br>Executing dbus-1.14.4-r0.pre-install<br>Executing dbus-1.14.4-r0.post-install<br>(149/768) Installing dbus-openrc (1.14.4-r0)<br>(150/768) Installing dbus-x11 (1.14.4-r0)<br>(151/768) Installing libaio (0.3.113-r0)<br>(152/768) Installing device-mapper-event-libs (2.03.17-r1)<br>(153/768) Installing lvm2-libs (2.03.17-r1)<br>(154/768) Installing device-mapper (2.03.17-r1)<br>(155/768) Installing dhcp (4.4.3_p1-r1)<br>Executing dhcp-4.4.3_p1-r1.pre-install<br>(156/768) Installing dhcp-openrc (4.4.3_p1-r1)<br>(157/768) Installing dhcp-server-vanilla (4.4.3_p1-r1)<br>(158/768) Installing diffutils (3.8-r1)<br>(159/768) Installing mandoc (1.14.6-r6)<br>(160/768) Installing mandoc-doc (1.14.6-r6)<br>(161/768) Installing man-pages (6.01-r0)<br>(162/768) Installing docs (0.2-r6)<br>(163/768) Installing btrfs-progs-doc (6.0.2-r0)<br>(164/768) Installing lzo-doc (2.10-r3)<br>(165/768) Installing harfbuzz-doc (5.3.1-r1)<br>(166/768) Installing lynx-doc (2.8.9_p1-r8)<br>(167/768) Installing libwebp-doc (1.2.4-r1)<br>(168/768) Installing less-doc (608-r1)<br>(169/768) Installing busybox-doc (1.35.0-r29)<br>(170/768) Installing alpine-doc (2.26-r1)<br>(171/768) Installing cadaver-doc (0.23.3-r6)<br>(172/768) Installing gdk-pixbuf-doc (2.42.10-r0)<br>(173/768) Installing libjpeg-turbo-doc (2.1.4-r0)<br>(174/768) Installing mpc1-doc (1.2.1-r1)<br>(175/768) Installing davfs2-doc (1.6.1-r0)<br>(176/768) Installing ncurses-doc (6.3_p20221119-r0)<br>(177/768) Installing gmp-doc (6.2.1-r2)<br>(178/768) Installing cifs-utils-doc (7.0-r0)<br>(179/768) Installing libx11-doc (1.8.4-r0)<br>(180/768) Installing attr-doc (2.5.1-r2)<br>(181/768) Installing libffi-doc (3.4.4-r0)<br>(182/768) Installing pango-doc (1.50.13-r0)<br>(183/768) Installing gzip-doc (1.12-r0)<br>(184/768) Installing popt-doc (1.19-r0)<br>(185/768) Installing libxcb-doc (1.15-r0)<br>(186/768) Installing abuild-doc (3.10.0-r0)<br>(187/768) Installing freetype-doc (2.12.1-r0)<br>(188/768) Installing mpdecimal-doc (2.5.1-r1)<br>(189/768) Installing phodav-doc (3.0-r0)<br>(190/768) Installing cairo-doc (1.17.6-r3)<br>(191/768) Installing p11-kit-doc (0.24.1-r1)<br>(192/768) Installing apk-tools-doc (2.12.10-r1)<br>(193/768) Installing gdbm-doc (1.23-r0)<br>(194/768) Installing ca-certificates-doc (20220614-r4)<br>(195/768) Installing libmd-doc (1.0.4-r0)<br>(196/768) Installing libarchive-doc (3.6.1-r2)<br>(197/768) Installing acct-doc (6.6.4-r1)<br>(198/768) Installing gcc-doc (12.2.1_git20220924-r4)<br>(199/768) Installing openssl-doc (3.0.8-r3)<br>(200/768) Installing fribidi-doc (1.0.12-r0)<br>(201/768) Installing pkgconf-doc (1.9.4-r0)<br>(202/768) Installing libxrender-doc (0.9.11-r0)<br>(203/768) Installing libaio-doc (0.3.113-r0)<br>(204/768) Installing openrc-doc (0.45.2-r7)<br>(205/768) Installing bc-doc (1.07.1-r2)<br>(206/768) Installing pcre2-doc (10.42-r0)<br>(207/768) Installing coreutils-doc (9.1-r0)<br>(208/768) Installing libxft-doc (2.3.7-r0)<br>(209/768) Installing dbus-doc (1.14.4-r0)<br>(210/768) Installing talloc-doc (2.3.4-r0)<br>(211/768) Installing tar-doc (1.34-r2)<br>(212/768) Installing libxau-doc (1.0.10-r0)<br>(213/768) Installing avahi-doc (0.8-r6)<br>(214/768) Installing cryptsetup-doc (2.5.0-r2)<br>(215/768) Installing libxml2-doc (2.10.3-r1)<br>(216/768) Installing patch-doc (2.7.6-r9)<br>(217/768) Installing neon-doc (0.32.4-r0)<br>(218/768) Installing mpfr4-doc (4.1.0-r0)<br>(219/768) Installing doas-doc (6.8.2-r3)<br>(220/768) Installing libxdmcp-doc (1.1.4-r0)<br>(221/768) Installing libbsd-doc (0.11.7-r0)<br>(222/768) Installing ifupdown-ng-doc (0.12.1-r1)<br>(223/768) Installing asciinema-doc (2.2.0-r0)<br>(224/768) Installing libpng-doc (1.6.38-r0)<br>(225/768) Installing make-doc (4.3-r1)<br>(226/768) Installing cpio-doc (2.13-r3)<br>(227/768) Installing gnutls-doc (3.7.8-r3)<br>(228/768) Installing tiff-doc (4.4.0-r3)<br>(229/768) Installing diffutils-doc (3.8-r1)<br>(230/768) Installing rsvg-convert-doc (2.55.1-r0)<br>(231/768) Installing fontconfig-doc (2.14.1-r0)<br>(232/768) Installing libpsl-doc (0.21.1-r1)<br>(233/768) Installing git-doc (2.38.4-r1)<br>(234/768) Installing skalibs-doc (2.12.0.1-r0)<br>(235/768) Installing libdaemon-doc (0.14-r3)<br>(236/768) Installing glib-doc (2.74.6-r0)<br>(237/768) Installing shared-mime-info-doc (2.2-r2)<br>(238/768) Installing libidn2-doc (2.3.4-r0)<br>(239/768) Installing lzip-doc (1.23-r0)<br>(240/768) Installing dhcp-doc (4.4.3_p1-r1)<br>(241/768) Installing pcre-doc (8.45-r2)<br>(242/768) Installing libtasn1-doc (4.19.0-r0)<br>(243/768) Installing libxext-doc (1.3.5-r0)<br>(244/768) Installing zlib-doc (1.2.13-r0)<br>(245/768) Installing readline-doc (8.2.0-r0)<br>(246/768) Installing curl-doc (7.88.1-r1)<br>(247/768) Installing python3-doc (3.10.11-r0)<br>(248/768) Installing bzip2-doc (1.0.8-r4)<br>(249/768) Installing file-doc (5.43-r0)<br>(250/768) Installing fakeroot-doc (1.29-r0)<br>(251/768) Installing libunistring-doc (1.1-r0)<br>(252/768) Installing json-c-doc (0.16-r2)<br>(253/768) Installing dos2unix (7.4.3-r1)<br>(254/768) Installing dos2unix-doc (7.4.3-r1)<br>(255/768) Installing dosfstools (4.2-r1)<br>(256/768) Installing dosfstools-doc (4.2-r1)<br>(257/768) Installing e2fsprogs-doc (1.46.6-r0)<br>(258/768) Installing easy-rsa (3.1.1-r0)<br>(259/768) Installing easy-rsa-doc (3.1.1-r0)<br>(260/768) Installing ed (1.18-r2)<br>(261/768) Installing ed-doc (1.18-r2)<br>(262/768) Installing efivar-libs (38-r1)<br>(263/768) Installing efibootmgr (18-r0)<br>(264/768) Installing efibootmgr-doc (18-r0)<br>(265/768) Installing tzdata (2023c-r0)<br>(266/768) Installing tzdata-doc (2023c-r0)<br>(267/768) Installing tcl (8.6.12-r1)<br>(268/768) Installing tcl-doc (8.6.12-r1)<br>(269/768) Installing expect (5.45.4-r3)<br>(270/768) Installing expect-doc (5.45.4-r3)<br>(271/768) Installing extra-cmake-modules (5.100.0-r0)<br>(272/768) Installing extra-cmake-modules-doc (5.100.0-r0)<br>(273/768) Installing f2fs-tools-libs (1.15.0-r0)<br>(274/768) Installing f2fs-tools (1.15.0-r0)<br>(275/768) Installing f2fs-tools-doc (1.15.0-r0)<br>(276/768) Installing findutils (4.9.0-r3)<br>(277/768) Installing findutils-doc (4.9.0-r3)<br>(278/768) Installing libpcre2-32 (10.42-r0)<br>(279/768) Installing fish (3.5.1-r1)<br>Executing fish-3.5.1-r1.post-install<br>(280/768) Installing curl-fish-completion (7.88.1-r1)<br>(281/768) Installing fish-doc (3.5.1-r1)<br>(282/768) Installing libgpg-error (1.46-r1)<br>(283/768) Installing libgpg-error-doc (1.46-r1)<br>(284/768) Installing libgcrypt (1.10.1-r0)<br>(285/768) Installing libgcrypt-doc (1.10.1-r0)<br>(286/768) Installing fsarchiver (0.8.6-r1)<br>(287/768) Installing fsarchiver-doc (0.8.6-r1)<br>(288/768) Installing fuse-common (3.12.0-r0)<br>(289/768) Installing fuse-openrc (3.12.0-r0)<br>(290/768) Installing fuse (2.9.9-r2)<br>(291/768) Installing fuse-doc (2.9.9-r2)<br>(292/768) Installing fuse-exfat (1.3.0-r3)<br>(293/768) Installing fuse-exfat-doc (1.3.0-r3)<br>(294/768) Installing fuse-exfat-utils (1.3.0-r3)<br>(295/768) Installing gawk (5.1.1-r1)<br>(296/768) Installing gawk-doc (5.1.1-r1)<br>(297/768) Installing gifsicle (1.93-r1)<br>(298/768) Installing gifsicle-doc (1.93-r1)<br>(299/768) Installing gptfdisk (1.0.9-r2)<br>(300/768) Installing gptfdisk-doc (1.0.9-r2)<br>(301/768) Installing parted (3.5-r0)<br>(302/768) Installing parted-doc (3.5-r0)<br>(303/768) Installing libatasmart (0.19-r2)<br>(304/768) Installing libatasmart-doc (0.19-r2)<br>(305/768) Installing libbytesize (2.7-r1)<br>(306/768) Installing libbytesize-doc (2.7-r1)<br>(307/768) Installing dmraid (1.0.0_rc16-r1)<br>(308/768) Installing dmraid-doc (1.0.0_rc16-r1)<br>(309/768) Installing ndctl-libs (74-r0)<br>(310/768) Installing nspr (4.35-r0)<br>(311/768) Installing nss (3.85-r1)<br>(312/768) Installing libassuan (2.5.5-r1)<br>(313/768) Installing libassuan-doc (2.5.5-r1)<br>(314/768) Installing pinentry (1.2.1-r0)<br>Executing pinentry-1.2.1-r0.post-install<br>(315/768) Installing pinentry-doc (1.2.1-r0)<br>(316/768) Installing gnupg-gpgconf (2.2.40-r0)<br>(317/768) Installing gpg (2.2.40-r0)<br>(318/768) Installing npth (1.6-r2)<br>(319/768) Installing gpg-agent (2.2.40-r0)<br>(320/768) Installing libksba (1.6.3-r0)<br>(321/768) Installing libksba-doc (1.6.3-r0)<br>(322/768) Installing gpgsm (2.2.40-r0)<br>(323/768) Installing gpgme (1.18.0-r0)<br>(324/768) Installing gpgme-doc (1.18.0-r0)<br>(325/768) Installing volume_key (0.3.12-r3)<br>(326/768) Installing volume_key-doc (0.3.12-r3)<br>(327/768) Installing yaml (0.2.5-r0)<br>(328/768) Installing libblockdev (2.28-r0)<br>(329/768) Installing libgudev (237-r1)<br>(330/768) Installing polkit-libs (122-r0)<br>(331/768) Installing udisks2-libs (2.9.4-r1)<br>(332/768) Installing udisks2 (2.9.4-r1)<br>(333/768) Installing udisks2-doc (2.9.4-r1)<br>(334/768) Installing libatk-1.0 (2.46.0-r0)<br>(335/768) Installing sound-theme-freedesktop (0.8-r0)<br>(336/768) Installing libltdl (2.4.7-r1)<br>(337/768) Installing libogg (1.3.5-r2)<br>(338/768) Installing libogg-doc (1.3.5-r2)<br>(339/768) Installing libvorbis (1.3.7-r0)<br>(340/768) Installing libvorbis-doc (1.3.7-r0)<br>(341/768) Installing libcanberra (0.30-r9)<br>(342/768) Installing libcanberra-doc (0.30-r9)<br>(343/768) Installing hicolor-icon-theme (0.17-r2)<br>(344/768) Installing gtk-update-icon-cache (3.24.36-r0)<br>(345/768) Installing libxcomposite (0.4.5-r1)<br>(346/768) Installing libxcomposite-doc (0.4.5-r1)<br>(347/768) Installing libxfixes (6.0.0-r0)<br>(348/768) Installing libxfixes-doc (6.0.0-r0)<br>(349/768) Installing libxcursor (1.2.1-r1)<br>(350/768) Installing libxcursor-doc (1.2.1-r1)<br>(351/768) Installing libxdamage (1.1.5-r1)<br>(352/768) Installing libxi (1.8-r0)<br>(353/768) Installing libxi-doc (1.8-r0)<br>(354/768) Installing libxinerama (1.1.5-r0)<br>(355/768) Installing libxinerama-doc (1.1.5-r0)<br>(356/768) Installing libxrandr (1.5.3-r0)<br>(357/768) Installing libxrandr-doc (1.5.3-r0)<br>(358/768) Installing libxtst (1.2.4-r0)<br>(359/768) Installing libxtst-doc (1.2.4-r0)<br>(360/768) Installing at-spi2-core (2.46.0-r0)<br>(361/768) Installing at-spi2-core-doc (2.46.0-r0)<br>(362/768) Installing libatk-bridge-2.0 (2.46.0-r0)<br>(363/768) Installing cairo-gobject (1.17.6-r3)<br>(364/768) Installing cups-libs (2.4.2-r1)<br>(365/768) Installing libepoxy (1.5.10-r0)<br>(366/768) Installing wayland-libs-client (1.21.0-r1)<br>(367/768) Installing wayland-libs-cursor (1.21.0-r1)<br>(368/768) Installing wayland-libs-egl (1.21.0-r1)<br>(369/768) Installing xkeyboard-config (2.37-r0)<br>(370/768) Installing xkeyboard-config-doc (2.37-r0)<br>(371/768) Installing libxkbcommon (1.4.1-r0)<br>(372/768) Installing xkbcli-doc (1.4.1-r0)<br>(373/768) Installing gtk+3.0 (3.24.36-r0)<br>Executing gtk+3.0-3.24.36-r0.post-install<br>(374/768) Installing gtk+3.0-doc (3.24.36-r0)<br>(375/768) Installing libcanberra-gtk3 (0.30-r9)<br>(376/768) Installing libdvdcss (1.4.3-r0)<br>(377/768) Installing libdvdcss-doc (1.4.3-r0)<br>(378/768) Installing libdvdread (6.1.3-r0)<br>(379/768) Installing libdvdread-doc (6.1.3-r0)<br>(380/768) Installing libelogind (246.10-r5)<br>(381/768) Installing libhandy1 (1.8.2-r0)<br>(382/768) Installing libnotify (0.8.1-r1)<br>(383/768) Installing cracklib-words (2.9.8-r0)<br>(384/768) Installing cracklib (2.9.8-r0)<br>(385/768) Installing linux-pam-doc (1.5.2-r1)<br>(386/768) Installing libpwquality (1.4.4-r3)<br>(387/768) Installing libpwquality-doc (1.4.4-r3)<br>(388/768) Installing libsecret (0.20.5-r0)<br>(389/768) Installing libsecret-doc (0.20.5-r0)<br>(390/768) Installing gnome-disk-utility (43.0-r0)<br>(391/768) Installing gnome-disk-utility-doc (43.0-r0)<br>(392/768) Installing grep (3.8-r1)<br>(393/768) Installing grep-doc (3.8-r1)<br>(394/768) Installing kmod-doc (30-r1)<br>(395/768) Installing mkinitfs-doc (3.7.0-r1)<br>(396/768) Installing grub-doc (2.06-r7)<br>(397/768) Installing grub-bash-completion (2.06-r7)<br>(398/768) Installing grub-efi (2.06-r7)<br>(399/768) Installing haveged (1.9.18-r0)<br>(400/768) Installing haveged-openrc (1.9.18-r0)<br>(401/768) Installing haveged-doc (1.9.18-r0)<br>(402/768) Installing hdparm (9.65-r0)<br>(403/768) Installing hdparm-doc (9.65-r0)<br>(404/768) Installing inetutils-ftp-doc (2.4-r0)<br>(405/768) Installing inetutils-telnet (2.4-r0)<br>(406/768) Installing inetutils-telnet-doc (2.4-r0)<br>ERROR: inetutils-telnet-doc-2.4-r0: trying to overwrite usr/share/info/inetutils.info owned by inetutils-ftp-doc-2.4-r0.<br>(407/768) Installing libmnl (1.0.5-r0)<br>(408/768) Installing libnftnl (1.2.4-r0)<br>(409/768) Installing iptables (1.8.8-r2)<br>(410/768) Installing iptables-doc (1.8.8-r2)<br>(411/768) Installing iptables-openrc (1.8.8-r2)<br>(412/768) Installing ip6tables (1.8.8-r2)<br>(413/768) Installing ip6tables-openrc (1.8.8-r2)<br>(414/768) Installing libmaxminddb-libs (1.7.1-r0)<br>(415/768) Installing libmaxminddb (1.7.1-r0)<br>(416/768) Installing libmaxminddb-doc (1.7.1-r0)<br>(417/768) Installing ipcalc (1.0.1-r1)<br>(418/768) Installing ipcalc-doc (1.0.1-r1)<br>(419/768) Installing musl-fts (1.2.7-r3)<br>(420/768) Installing libelf (0.187-r2)<br>(421/768) Installing iproute2-minimal (6.0.0-r1)<br>(422/768) Installing ifupdown-ng-iproute2 (0.12.1-r1)<br>(423/768) Installing iproute2-tc (6.0.0-r1)<br>(424/768) Installing iproute2-ss (6.0.0-r1)<br>(425/768) Installing iproute2 (6.0.0-r1)<br>Executing iproute2-6.0.0-r1.post-install<br>(426/768) Installing iproute2-doc (6.0.0-r1)<br>(427/768) Installing iputils (20211215-r0)<br>(428/768) Installing jfsutils (1.1.15-r4)<br>(429/768) Installing jfsutils-doc (1.1.15-r4)<br>(430/768) Installing icu-data-full (72.1-r1)<br>(431/768) Installing icu-libs (72.1-r1)<br>(432/768) Installing libpcre2-16 (10.42-r0)<br>(433/768) Installing qt5-qtbase (5.15.6_git20221010-r0)<br>(434/768) Installing qt5-qtbase-doc (5.15.6_git20221010-r0)<br>(435/768) Installing libice (1.0.10-r1)<br>(436/768) Installing libice-doc (1.0.10-r1)<br>(437/768) Installing libsm (1.2.3-r1)<br>(438/768) Installing libsm-doc (1.2.3-r1)<br>(439/768) Installing libxt (1.2.1-r0)<br>(440/768) Installing libxt-doc (1.2.1-r0)<br>(441/768) Installing libxmu (1.1.4-r0)<br>(442/768) Installing libxmu-doc (1.1.4-r0)<br>(443/768) Installing xset (1.2.4-r1)<br>(444/768) Installing xset-doc (1.2.4-r1)<br>(445/768) Installing xprop (1.2.5-r1)<br>(446/768) Installing xprop-doc (1.2.5-r1)<br>(447/768) Installing xdg-utils (1.1.3-r4)<br>(448/768) Installing xdg-utils-doc (1.1.3-r4)<br>(449/768) Installing mesa (22.2.5-r1)<br>(450/768) Installing hwdata-pci (0.364-r0)<br>(451/768) Installing libpciaccess (0.17-r0)<br>(452/768) Installing libpciaccess-doc (0.17-r0)<br>(453/768) Installing libdrm (2.4.114-r0)<br>(454/768) Installing wayland-libs-server (1.21.0-r1)<br>(455/768) Installing libxxf86vm (1.1.5-r0)<br>(456/768) Installing libxxf86vm-doc (1.1.5-r0)<br>(457/768) Installing mesa-glapi (22.2.5-r1)<br>(458/768) Installing libxshmfence (1.3.1-r0)<br>(459/768) Installing mesa-gl (22.2.5-r1)<br>(460/768) Installing qt5-qtdeclarative (5.15.6_git20220908-r0)<br>(461/768) Installing qt5-qtwayland (5.15.6_git20220927-r1)<br>(462/768) Installing mesa-gbm (22.2.5-r1)<br>(463/768) Installing mesa-egl (22.2.5-r1)<br>(464/768) Installing libevdev (1.13.0-r0)<br>(465/768) Installing libevdev-doc (1.13.0-r0)<br>(466/768) Installing mtdev (1.1.6-r1)<br>(467/768) Installing libinput-libs (1.22.1-r0)<br>(468/768) Installing xcb-util-wm (0.4.2-r0)<br>(469/768) Installing xcb-util (0.4.0-r3)<br>(470/768) Installing xcb-util-image (0.4.1-r0)<br>(471/768) Installing xcb-util-keysyms (0.4.1-r0)<br>(472/768) Installing xcb-util-renderutil (0.3.10-r0)<br>(473/768) Installing libxkbcommon-x11 (1.4.1-r0)<br>(474/768) Installing qt5-qtbase-x11 (5.15.6_git20221010-r0)<br>(475/768) Installing qt5-qtsvg (5.15.6_git20220908-r0)<br>(476/768) Installing qt5-qtx11extras (5.15.6_git20220816-r0)<br>(477/768) Installing botan-libs (2.19.3-r0)<br>(478/768) Installing minizip (1.2.13-r0)<br>(479/768) Installing pcsc-lite-libs (1.9.9-r0)<br>(480/768) Installing libqrencode (4.1.1-r1)<br>(481/768) Installing libqrencode-doc (4.1.1-r1)<br>(482/768) Installing libusb (1.0.26-r0)<br>(483/768) Installing keepassxc (2.7.4-r0)<br>(484/768) Installing keepassxc-doc (2.7.4-r0)<br>(485/768) Installing lftp (4.9.2-r4)<br>(486/768) Installing lftp-doc (4.9.2-r4)<br>(487/768) Installing libarchive-tools (3.6.1-r2)<br>(488/768) Installing libcddb (1.3.2-r4)<br>(489/768) Installing libcdio (2.1.0-r1)<br>(490/768) Installing libcdio-doc (2.1.0-r1)<br>(491/768) Installing libcdio-tools (2.1.0-r1)<br>(492/768) Installing libdbi (0.9.0-r2)<br>(493/768) Installing libdbi-doc (0.9.0-r2)<br>(494/768) Installing lua5.4-libs (5.4.4-r6)<br>(495/768) Installing lighttpd (1.4.67-r0)<br>Executing lighttpd-1.4.67-r0.pre-install<br>(496/768) Installing lighttpd-doc (1.4.67-r0)<br>(497/768) Installing lighttpd-openrc (1.4.67-r0)<br>(498/768) Installing lighttpd-mod_auth (1.4.67-r0)<br>(499/768) Installing lighttpd-mod_webdav (1.4.67-r0)<br>(500/768) Installing links (2.28-r0)<br>(501/768) Installing links-doc (2.28-r0)<br>(502/768) Installing lvm2 (2.03.17-r1)<br>(503/768) Installing lvm2-openrc (2.03.17-r1)<br>(504/768) Installing lvm2-doc (2.03.17-r1)<br>(505/768) Installing mandoc-apropos (1.14.6-r6)<br>(506/768) Installing perl (5.36.0-r0)<br>(507/768) Installing perl-doc (5.36.0-r0)<br>(508/768) Installing perl-error (0.17029-r1)<br>(509/768) Installing perl-error-doc (0.17029-r1)<br>(510/768) Installing perl-git (2.38.4-r1)<br>(511/768) Installing git-perl (2.38.4-r1)<br>(512/768) Installing markdown (1.0.1-r3)<br>(513/768) Installing markdown-doc (1.0.1-r3)<br>(514/768) Installing gpm-libs (1.20.7-r2)<br>(515/768) Installing slang (2.3.3-r0)<br>(516/768) Installing slang-doc (2.3.3-r0)<br>(517/768) Installing libssh2 (1.10.0-r3)<br>(518/768) Installing libssh2-doc (1.10.0-r3)<br>(519/768) Installing mc (4.8.28-r0)<br>(520/768) Installing mc-doc (4.8.28-r0)<br>(521/768) Installing mlocate (0.26-r8)<br>Executing mlocate-0.26-r8.pre-install<br>(522/768) Installing mlocate-doc (0.26-r8)<br>(523/768) Installing mtools-doc (4.0.42-r0)<br>(524/768) Installing libidn (1.41-r0)<br>(525/768) Installing libidn-doc (1.41-r0)<br>(526/768) Installing libgsasl (2.2.0-r0)<br>(527/768) Installing libgsasl-doc (2.2.0-r0)<br>(528/768) Installing mutt (2.2.9-r0)<br>(529/768) Installing mutt-doc (2.2.9-r0)<br>(530/768) Installing nano-doc (7.0-r0)<br>(531/768) Installing ncdu (1.17-r1)<br>(532/768) Installing ncdu-doc (1.17-r1)<br>(533/768) Installing ncftp (3.2.6-r5)<br>(534/768) Installing ncftp-doc (3.2.6-r5)<br>(535/768) Installing neofetch (7.1.0-r1)<br>(536/768) Installing neofetch-doc (7.1.0-r1)<br>(537/768) Installing gpg-wks-server (2.2.40-r0)<br>(538/768) Installing gpgv (2.2.40-r0)<br>(539/768) Installing gnupg-dirmngr (2.2.40-r0)<br>(540/768) Installing gnupg-utils (2.2.40-r0)<br>(541/768) Installing gnupg-wks-client (2.2.40-r0)<br>(542/768) Installing gnupg (2.2.40-r0)<br>(543/768) Installing gnupg-doc (2.2.40-r0)<br>(544/768) Installing gmime (3.2.13-r0)<br>(545/768) Installing gmime-doc (3.2.13-r0)<br>(546/768) Installing libxapian (1.4.21-r0)<br>(547/768) Installing notmuch-libs (0.37-r1)<br>(548/768) Installing neomutt (20220429-r2)<br>(549/768) Installing neomutt-doc (20220429-r2)<br>(550/768) Installing mii-tool (2.10-r0)<br>(551/768) Installing net-tools (2.10-r0)<br>(552/768) Installing net-tools-doc (2.10-r0)<br>(553/768) Installing netcat-openbsd (1.130-r4)<br>(554/768) Installing netcat-openbsd-doc (1.130-r4)<br>(555/768) Installing libtirpc-conf (1.3.3-r0)<br>(556/768) Installing libtirpc (1.3.3-r0)<br>(557/768) Installing libtirpc-doc (1.3.3-r0)<br>(558/768) Installing rpcbind (1.2.6-r1)<br>Executing rpcbind-1.2.6-r1.pre-install<br>(559/768) Installing rpcbind-doc (1.2.6-r1)<br>(560/768) Installing rpcbind-openrc (1.2.6-r1)<br>(561/768) Installing libnfsidmap (2.6.2-r0)<br>(593/768) Installing pandoc-doc (2.19.2-r0)<br>(594/768) Installing tree (2.0.4-r0)<br>(595/768) Installing tree-doc (2.0.4-r0)<br>(596/768) Installing pass (1.7.4-r1)<br>(597/768) Installing pass-doc (1.7.4-r1)<br>(598/768) Installing pass-fish-completion (1.7.4-r1)<br>(599/768) Installing oath-toolkit-liboath (2.6.7-r2)<br>(600/768) Installing oath-toolkit-oathtool (2.6.7-r2)<br>(601/768) Installing pass-otp (1.2.0-r0)<br>(602/768) Installing pass-otp-doc (1.2.0-r0)<br>(603/768) Installing pciutils-libs (3.9.0-r0)<br>(604/768) Installing pciutils (3.9.0-r0)<br>(605/768) Installing pciutils-doc (3.9.0-r0)<br>(606/768) Installing perl-digest-sha3 (1.05-r0)<br>(607/768) Installing perl-digest-sha3-doc (1.05-r0)<br>(608/768) Installing perl-net-ssleay (1.92-r2)<br>(609/768) Installing perl-net-ssleay-doc (1.92-r2)<br>(610/768) Installing polkit-common (122-r0)<br>Executing polkit-common-122-r0.pre-install<br>(611/768) Installing duktape (2.7.0-r0)<br>(612/768) Installing polkit (122-r0)<br>(613/768) Installing polkit-openrc (122-r0)<br>(614/768) Installing polkit-doc (122-r0)<br>(615/768) Installing libproc (3.3.17-r2)<br>(616/768) Installing procps (3.3.17-r2)<br>(617/768) Installing procps-doc (3.3.17-r2)<br>(618/768) Installing progress (0.16-r0)<br>(619/768) Installing progress-doc (0.16-r0)<br>(620/768) Installing psmisc (23.5-r0)<br>(621/768) Installing psmisc-doc (23.5-r0)<br>(622/768) Installing pssh (2.3.4-r2)<br>(623/768) Installing pssh-doc (2.3.4-r2)<br>(624/768) Installing pv (1.6.20-r1)<br>(625/768) Installing pv-doc (1.6.20-r1)<br>(626/768) Installing pwgen (2.08-r2)<br>(627/768) Installing pwgen-doc (2.08-r2)<br>(628/768) Installing py3-six (1.16.0-r3)<br>(629/768) Installing py3-retrying (1.3.3-r3)<br>(630/768) Installing py3-parsing (3.0.9-r0)<br>(631/768) Installing py3-packaging (21.3-r2)<br>(632/768) Installing py3-setuptools (65.6.0-r0)<br>(633/768) Installing py3-pip (22.3.1-r1)<br>(634/768) Installing py3-pip-doc (22.3.1-r1)<br>(635/768) Installing qt5-qtwebsockets (5.15.6_git20220907-r0)<br>(636/768) Installing qt5-qtwebglplugin (5.15.6_git20220816-r0)<br>(637/768) Installing qt5-qtwebglplugin-doc (5.15.6_git20220816-r0)<br>(638/768) Installing rlwrap (0.46.1-r0)<br>(639/768) Installing rlwrap-doc (0.46.1-r0)<br>(640/768) Installing jitterentropy-library (3.3.1-r0)<br>(641/768) Installing jitterentropy-library-doc (3.3.1-r0)<br>(642/768) Installing rng-tools (6.15-r1)<br>(643/768) Installing rng-tools-openrc (6.15-r1)<br>(644/768) Installing rng-tools-doc (6.15-r1)<br>(645/768) Installing rpm (4.18.0-r1)<br>(646/768) Installing rpm-doc (4.18.0-r1)<br>(647/768) Installing samba-common (4.16.10-r0)<br>(648/768) Installing tevent (0.13.0-r0)<br>(649/768) Installing samba-util-libs (4.16.10-r0)<br>(650/768) Installing jansson (2.14-r0)<br>(651/768) Installing lmdb (0.9.29-r2)<br>(652/768) Installing lmdb-doc (0.9.29-r2)<br>(653/768) Installing tdb-libs (1.4.6-r0)<br>(654/768) Installing ldb (2.5.3-r0)<br>(655/768) Installing ldb-doc (2.5.3-r0)<br>(656/768) Installing samba-libs (4.16.10-r0)<br>(657/768) Installing samba-common-server-libs (4.16.10-r0)<br>(658/768) Installing samba-client-libs (4.16.10-r0)<br>(659/768) Installing liburing (2.3-r0)<br>(660/768) Installing liburing-doc (2.3-r0)<br>(661/768) Installing samba-server (4.16.10-r0)<br>(662/768) Installing samba-server-openrc (4.16.10-r0)<br>(663/768) Installing libsmbclient (4.16.10-r0)<br>(664/768) Installing samba-client (4.16.10-r0)<br>(665/768) Installing samba-common-tools (4.16.10-r0)<br>(666/768) Installing samba (4.16.10-r0)<br>(667/768) Installing samba-doc (4.16.10-r0)<br>(668/768) Installing libutempter (1.2.1-r5)<br>(669/768) Installing libutempter-doc (1.2.1-r5)<br>(670/768) Installing screen (4.9.0-r0)<br>(671/768) Installing screen-doc (4.9.0-r0)<br>(672/768) Installing sed (4.9-r0)<br>(673/768) Installing sed-doc (4.9-r0)<br>(674/768) Installing sgdisk (1.0.9-r2)<br>(675/768) Installing shadow (4.13-r0)<br>(676/768) Installing shadow-doc (4.13-r0)<br>(677/768) Installing xz (5.2.9-r0)<br>(678/768) Installing xz-doc (5.2.9-r0)<br>(679/768) Installing sharutils (4.15.2-r2)<br>(680/768) Installing sharutils-doc (4.15.2-r2)<br>(681/768) Installing socat (1.7.4.4-r0)<br>(682/768) Installing socat-doc (1.7.4.4-r0)<br>(683/768) Installing fuse3-libs (3.12.0-r0)<br>(684/768) Installing fuse3 (3.12.0-r0)<br>(685/768) Installing fuse3-doc (3.12.0-r0)<br>(686/768) Installing sshfs (3.7.3-r0)<br>(687/768) Installing sshfs-doc (3.7.3-r0)<br>(688/768) Installing sshpass (1.09-r1)<br>(689/768) Installing sshpass-doc (1.09-r1)<br>(690/768) Installing judy (1.0.5-r1)<br>(691/768) Installing judy-doc (1.0.5-r1)<br>(692/768) Installing liblksctp (1.0.19-r1)<br>(693/768) Installing stress-ng (0.14.00-r0)<br>(694/768) Installing stress-ng-doc (0.14.00-r0)<br>(695/768) Installing sudo (1.9.12_p2-r1)<br>(696/768) Installing sudo-doc (1.9.12_p2-r1)<br>(697/768) Installing syslinux-doc (6.04_pre1-r11)<br>(698/768) Installing texinfo (7.0.1-r0)<br>(699/768) Installing texinfo-doc (7.0.1-r0)<br>(700/768) Installing udisks2-bash-completion (2.9.4-r1)<br>(701/768) Installing unzip (6.0-r13)<br>(702/768) Installing unzip-doc (6.0-r13)<br>(703/768) Installing hwdata-usb (0.364-r0)<br>(704/768) Installing usbutils (015-r0)<br>(705/768) Installing usbutils-doc (015-r0)<br>(706/768) Installing libeconf-doc (0.4.7-r0)<br>(707/768) Installing util-linux-doc (2.38.1-r1)<br>(708/768) Installing libcap-ng-doc (0.8.3-r1)<br>(709/768) Installing util-linux-bash-completion (2.38.1-r1)<br>(710/768) Installing util-linux-login (2.38.1-r1)<br>(711/768) Installing util-linux-login-doc (2.38.1-r1)<br>(712/768) Installing s6-ipcserver (2.11.1.2-r0)<br>(713/768) Installing utmps (0.1.2.0-r1)<br>Executing utmps-0.1.2.0-r1.pre-install<br>(714/768) Installing utmps-doc (0.1.2.0-r1)<br>(715/768) Installing utmps-openrc (0.1.2.0-r1)<br>(716/768) Installing vifm (0.12.1-r1)<br>(717/768) Installing vifm-doc (0.12.1-r1)<br>(718/768) Installing vifm-fish-completion (0.12.1-r1)<br>(719/768) Installing vifm-bash-completion (0.12.1-r1)<br>(720/768) Installing vifm-zsh-completion (0.12.1-r1)<br>(721/768) Installing xxd (9.0.0999-r0)<br>(722/768) Installing vim (9.0.0999-r0)<br>(723/768) Installing vim-doc (9.0.0999-r0)<br>(724/768) Installing vsftpd (3.0.5-r2)<br>Executing vsftpd-3.0.5-r2.pre-install<br>(725/768) Installing vsftpd-doc (3.0.5-r2)<br>(726/768) Installing vsftpd-openrc (3.0.5-r2)<br>(727/768) Installing wget (1.21.3-r2)<br>(728/768) Installing wget-doc (1.21.3-r2)<br>(729/768) Installing whois (5.5.14-r0)<br>(730/768) Installing whois-doc (5.5.14-r0)<br>(731/768) Installing qt5-qtbase-sqlite (5.15.6_git20221010-r0)<br>(732/768) Installing llvm15-libs (15.0.7-r0)<br>(733/768) Installing clang15-libclang (15.0.7-r0)<br>(734/768) Installing qt5-qttools (5.15.6_git20220907-r1)<br>(735/768) Installing xca (2.4.0-r2)<br>(736/768) Installing xca-doc (2.4.0-r2)<br>(737/768) Installing inih (56-r0)<br>(738/768) Installing userspace-rcu (0.13.2-r0)<br>(739/768) Installing userspace-rcu-doc (0.13.2-r0)<br>(740/768) Installing xfsprogs (6.0.0-r0)<br>(741/768) Installing xfsprogs-doc (6.0.0-r0)<br>(742/768) Installing libburn (1.5.4-r2)<br>(743/768) Installing libburn-doc (1.5.4-r2)<br>(744/768) Installing libisofs (1.5.4-r2)<br>(745/768) Installing libisoburn (1.5.4-r2)<br>(746/768) Installing libisoburn-doc (1.5.4-r2)<br>(747/768) Installing xorriso (1.5.4-r2)<br>(748/768) Installing gobject-introspection (1.74.0-r1)<br>(749/768) Installing gobject-introspection-doc (1.74.0-r1)<br>(750/768) Installing py3-gobject3 (3.42.2-r0)<br>(751/768) Installing py3-xdg (0.28-r0)<br>(752/768) Installing zim (0.75.1-r0)<br>(753/768) Installing zim-doc (0.75.1-r0)<br>(754/768) Installing zip (3.0-r10)<br>(755/768) Installing zip-doc (3.0-r10)<br>(756/768) Installing zsh (5.9-r0)<br>Executing zsh-5.9-r0.post-install<br>(757/768) Installing gcc-zsh-completion (5.9-r0)<br>(758/768) Installing pass-zsh-completion (1.7.4-r1)<br>(759/768) Installing apk-tools-zsh-completion (2.12.10-r1)<br>(760/768) Installing openrc-zsh-completion (0.45.2-r7)<br>(761/768) Installing zsh-pcre (5.9-r0)<br>(762/768) Installing py3-pip-zsh-completion (22.3.1-r1)<br>(763/768) Installing git-zsh-completion (5.9-r0)<br>(764/768) Installing zsh-doc (5.9-r0)<br>(765/768) Installing lynx-zsh-completion (5.9-r0)<br>(766/768) Installing curl-zsh-completion (7.88.1-r1)<br>(767/768) Installing zstd (1.5.5-r0)<br>(768/768) Installing zstd-doc (1.5.5-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing ca-certificates-20220614-r4.trigger<br>Executing glib-2.74.6-r0.trigger<br>Executing shared-mime-info-2.2-r2.trigger<br>Executing gdk-pixbuf-2.42.10-r0.trigger<br>Executing dbus-1.14.4-r0.trigger<br>Executing gtk-update-icon-cache-3.24.36-r0.trigger<br>Executing cracklib-2.9.8-r0.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>1 error; 1552 MiB in 862 packages<br>localhost:~# date<br>Wed Apr 12 10:49:23 UTC 2023<br>localhost:~# apk del inetutils-ftp inetutils-telnet<br>(1/4) Purging inetutils-ftp-doc (2.4-r0)<br>(2/4) Purging inetutils-ftp (2.4-r0)<br>(3/4) Purging inetutils-telnet-doc (2.4-r0)<br>(4/4) Purging inetutils-telnet (2.4-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>OK: 1551 MiB in 858 packages<br>localhost:~# date<br>Wed Apr 12 11:17:34 UTC 2023<br>localhost:~# apk add inetutils-telnet<br>(1/2) Installing inetutils-telnet (2.4-r0)<br>(2/2) Installing inetutils-telnet-doc (2.4-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>OK: 1551 MiB in 860 packages<br>localhost:~# date<br>Wed Apr 12 11:31:36 UTC 2023<br>localhost:~#<br>localhost:~# echo $SHELL<br>/bin/ash<br>localhost:~#<br>localhost:~# chsh -s /bin/bash root<br>Password:<br>localhost:~#<br>localhost:~# chsh -s /bin/bash test<br>Password:<br>localhost:~# mkdir /mnt/9p-host<br>localhost:~# mkdir /mnt/disk1<br>localhost:~#<br>localhost:~# groupadd --gid 9997 nine-p-host<br>localhost:~#<br>localhost:~# groupmod --append --users test nine-p-host<br>localhost:~#<br>localhost:~# mount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /m<br>nt/9p-host<br>localhost:~#<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124365,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vdb3 on / type ext4 (rw,relatime)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201340k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>tracefs on /sys/kernel/debug/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)<br>/dev/vdb1 on /boot type ext4 (rw,relatime)<br>tmpfs on /tmp type tmpfs (rw,nosuid,nodev,relatime,inode64)<br>/dev/vdc on /mnt/repo type ext4 (ro,relatime)<br>host on /mnt/9p-host type 9p (rw,relatime,sync,dirsync,access=client,msize=512000,trans=virtio)<br>localhost:~#<br>localhost:~# pwd<br>/root<br>localhost:~#<br>localhost:~# id<br>uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel),11(floppy),20(dialout),26(tape),27(video)<br>localhost:~#<br>localhost:~# su - test<br>Password:<br>localhost:~$ pwd<br>/home/test<br>localhost:~$<br>localhost:~$ id<br>uid=1000(test) gid=1000(test) groups=1000(test),10(wheel),18(audio),27(video),28(netdev),9997(nine-p-host)<br>localhost:~$<br>localhost:~$ echo $SHELL<br>/bin/bash<br>localhost:~$<br>localhost:~$ touch /mnt/9p-termux/from-guest-os-to-termux.txt<br>touch: cannot touch '/mnt/9p-termux/from-guest-os-to-termux.txt': No such file or directory<br>localhost:~$ touch /mnt/9p-host/from-guest-os-to-host.txt<br>localhost:~$<br>localhost:~$ ls -laR /mnt/9p-host<br>/mnt/9p-host:<br>total 2823904<br>drwxrwx--- 2 root nine-p-host       3488 Apr 12 11:53 .<br>drwxr-xr-x 5 root root              4096 Apr 12 11:46 ..<br>-rw-rw---- 1 root nine-p-host          0 Apr 12 11:53 from-guest-os-to-host.txt<br>-rw-rw---- 1 root nine-p-host  209715200 Apr 12 09:02 test-disk1-200mb.ext<br>-rw-rw---- 1 root nine-p-host 2679111680 Apr 12 11:51 vmtest2.raw<br>localhost:~$<br>localhost:~$ netstat -rn<br>Kernel IP routing table<br>Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface<br>0.0.0.0         10.0.2.2        0.0.0.0         UG        0 0          0 eth0<br>10.0.2.0        0.0.0.0         255.255.255.0   U         0 0          0 eth0<br>localhost:~$<br>localhost:~$ lftp anonymous@10.0.2.2 --port 12345<br>Password:<br>lftp anonymous@10.0.2.2:~> dir<br>dr-x------   0 anonymous anonymous            0 Dec 31  1969 /fs<br>dr-x------   0 anonymous anonymous            0 Dec 31  1969 /superuser<br>dr-x------   0 anonymous anonymous            0 Dec 31  1969 /saf<br>dr-x------   0 anonymous anonymous            0 Dec 31  1969 /rosaf<br>lftp anonymous@10.0.2.2:/> cd /saf<br>cd ok, cwd=/saf<br>lftp anonymous@10.0.2.2:/saf> dir<br>-rw-------   0 anonymous anonymous    209715200 Apr 12 05:02 test-disk1-200mb.ext<br>-rw-------   0 anonymous anonymous   2679111680 Apr 12 07:57 vmtest2.raw<br>-rw-------   0 anonymous anonymous            0 Apr 12 07:53 from-guest-os-to-host.txt<br>lftp anonymous@10.0.2.2:/saf> quit<br>localhost:~$<br>localhost:~$<br>localhost:~$ exit<br>logout<br><br><br>localhost:~# export SUDO_EDITOR=nano<br><br>localhost:~# export EDITOR=nano<br><br>localhost:~# grep wheel /etc/sudoers<br>## Uncomment to allow members of group wheel to execute any command<br>%wheel ALL=(ALL:ALL) ALL<br># %wheel ALL=(ALL:ALL) NOPASSWD: ALL<br>localhost:~#                                                                           mkdir -p /var/www/localhost/htdocs /var/log/lighttpd /var/lib/lighttpdr/lib/lighttpd<br>localhost:~#<br>localchown  -R lighttpd:lighttpd /var/log/lighttpd /var/lib/lighttpd /var/www/localhost/htdocst/htdocs<br>localhost:~#<br>localhost:~#<br>localhost:~# ls -al  /var/www/localhost/htdocs<br>total 12<br>drwxr-xr-x 2 lighttpd lighttpd 4096 Apr 12 10:13 .<br>drwxr-xr-x 4 root     root     4096 Apr 12 10:13 ..<br>-rw-r--r-- 1 lighttpd lighttpd   45 Mar  7 19:33 index.html<br>localhost:~#<br>localhost:~#<br>localhost:~# touch /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# chown root:lighttpd /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# ls -l /etc/lighttpd/webdav-htpasswd-passwd<br>-rw-r--r-- 1 root lighttpd 0 Apr 12 12:05 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# stat /etc/lighttpd/webdav-htpasswd-passwd<br>  File: /etc/lighttpd/webdav-htpasswd-passwd<br>  Size: 0               Blocks: 0          IO Block: 4096   regular empty file<br>Device: 253,19  Inode: 56354       Links: 1<br>Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (  105/lighttpd)<br>Access: 2023-04-12 12:05:35.170000000 +0000<br>Modify: 2023-04-12 12:05:35.170000000 +0000<br>Change: 2023-04-12 12:05:47.210000000 +0000<br> Birth: -<br>localhost:~#<br>localhost:~# chmod 640 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# ls -l /etc/lighttpd/webdav-htpasswd-passwd<br>-rw-r----- 1 root lighttpd 0 Apr 12 12:05 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# stat /etc/lighttpd/webdav-htpasswd-passwd<br>  File: /etc/lighttpd/webdav-htpasswd-passwd<br>  Size: 0               Blocks: 0          IO Block: 4096   regular empty file<br>Device: 253,19  Inode: 56354       Links: 1<br>Access: (0640/-rw-r-----)  Uid: (    0/    root)   Gid: (  105/lighttpd)<br>Access: 2023-04-12 12:05:35.170000000 +0000<br>Modify: 2023-04-12 12:05:35.170000000 +0000<br>Change: 2023-04-12 12:06:55.550000000 +0000<br> Birth: -<br>localhost:~#<br>localhost:~#<br>localhost:~# htpasswd -m /etc/lighttpd/webdav-htpasswd-passwd test1<br>New password:<br>Re-type new password:<br>Adding password for user test1<br>localhost:~#<br>localhost:~# cp -pi /etc/lighttpd/webdav.conf /root/backup<br>cp: cannot stat '/etc/lighttpd/webdav.conf': No such file or directory<br>localhost:~#<br>localhost:~# cat << 'END-OF-WEBDAV-CONF' > /etc/lighttpd/webdav.conf<br>server.port = 15081<br>server.upload-dirs = ( "/tmp" )<br>server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_file")<br>alias.url = ( "/webdav" => "/mnt/disk1" )<br>$HTTP["url"] =~ "^/webdav($|/)" {<br>    webdav.activate = "enable"<br>    webdav.is-readonly = "disable"<br>    webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"<br>    auth.backend = "htpasswd"<br>    auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-passwd"<br>    auth.require  = ("" => ("method" => "basic","realm" => "realm-webdav","require" => "valid-user"))<br>  }<br>END-OF-WEBDAV-CONF<br>localhost:~#<br>localhost:~# cat /etc/lighttpd/webdav.conf<br>server.port = 15081<br>server.upload-dirs = ( "/tmp" )<br>server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_file")<br>alias.url = ( "/webdav" => "/mnt/disk1" )<br>$HTTP["url"] =~ "^/webdav($|/)" {<br>    webdav.activate = "enable"<br>    webdav.is-readonly = "disable"<br>    webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"<br>    auth.backend = "htpasswd"<br>    auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-passwd"<br>    auth.require  = ("" => ("method" => "basic","realm" => "realm-webdav","require" => "valid-user"))<br>  }<br>localhost:~#<br>localhost:~# echo 'include "webdav.conf"' >> /etc/lighttpd/lighttpd.conf<br>localhost:~#<br>localhost:~# lighttpd -tt -f /etc/lighttpd/lighttpd.conf<br>localhost:~#<br>localhost:~# rc-update add lighttpd default<br> * service lighttpd added to runlevel default<br>localhost:~#<br>localhost:~# reboot<br><br><br>[    0.000000] Linux version 5.15.106-0-virt (buildozer@build-3-17-x86_64) (gcc (Alpine 12.2.1_git20220924-r4) 12.2.1 20220924, GNU ld (GNU Binutils) 2.39) #1-Alpine SMP Wed, 05 Apr 2023 10:48:45 +0000<br>[00:00:00.000] [    0.000000] Command line: BOOT_IMAGE=vmlinuz-virt root=UUID=2f076e61-7a3e-43fd-86bf-63dcde993c23 modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4 initrd=initramfs-virt<br>[00:00:00.004] [    0.000000] x86/fpu: x87 FPU will use FXSAVE<br>[00:00:00.005] [    0.000000] signal: max sigframe size: 1440                           [00:00:00.006] [    0.000000] BIOS-provided physical RAM map:<br>[00:00:00.007] [    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable<br>[00:00:00.008] [    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved<br>[00:00:00.010] [    0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved<br>[00:00:00.012] [    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000003ffd6fff] usable<br>[00:00:00.013] [    0.000000] BIOS-e820: [mem 0x000000003ffd7000-0x000000003fffffff] reserved<br>[00:00:00.015] [    0.000000] BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved<br>[00:00:00.016] [    0.000000] BIOS-e820: [mem 0x000000fd00000000-0x000000ffffffffff] reserved<br>[00:00:00.018] [    0.000000] NX (Execute Disable) protection: active                   [00:00:00.019] [    0.000000] SMBIOS 2.8 present.<br>[00:00:00.019] [    0.000000] DMI: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.16.1-0-g3208b098f51a-prebuilt.qemu.org 04/01/2014<br>[00:00:00.022] [    0.000000] tsc: Fast TSC calibration failed<br>[00:00:00.022] [    0.000000] last_pfn = 0x3ffd7 max_arch_pfn = 0x400000000<br>[00:00:00.024] [    0.000000] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT<br>[00:00:00.025] [    0.000000] RAMDISK: [mem 0x3f929000-0x3ffd6fff]<br>[00:00:00.026] [    0.000000] ACPI: Early table checksum verification disabled<br>[00:00:00.027] [    0.000000] ACPI: RSDP 0x00000000000F59F0 000014 (v00 BOCHS )<br>[00:00:00.029] [    0.000000] ACPI: RSDT 0x000000003FFE1BDD 000034 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.031] [    0.000000] ACPI: FACP 0x000000003FFE1A79 000074 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.032] [    0.000000] ACPI: DSDT 0x000000003FFE0040 001A39 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.033] [    0.000000] ACPI: FACS 0x000000003FFE0000 000040<br>[00:00:00.034] [    0.000000] ACPI: APIC 0x000000003FFE1AED 000090 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.036] [    0.000000] ACPI: HPET 0x000000003FFE1B7D 000038 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.037] [    0.000000] ACPI: WAET 0x000000003FFE1BB5 000028 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.039] [    0.000000] ACPI: Reserving FACP table memory at [mem 0x3ffe1a79-0x3ffe1aec]<br>[00:00:00.041] [    0.000000] ACPI: Reserving DSDT table memory at [mem 0x3ffe0040-0x3ffe1a78]<br>[00:00:00.042] [    0.000000] ACPI: Reserving FACS table memory at [mem 0x3ffe0000-0x3ffe003f]<br>[00:00:00.043] [    0.000000] ACPI: Reserving APIC table memory at [mem 0x3ffe1aed-0x3ffe1b7c]<br>[00:00:00.045] [    0.000000] ACPI: Reserving HPET table memory at [mem 0x3ffe1b7d-0x3ffe1bb4]<br>[00:00:00.046] [    0.000000] ACPI: Reserving WAET table memory at [mem 0x3ffe1bb5-0x3ffe1bdc]<br>[00:00:00.047] [    0.000000] Zone ranges:<br>[00:00:00.048] [    0.000000]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]<br>[00:00:00.049] [    0.000000]   DMA32    [mem 0x0000000001000000-0x000000003ffd6fff]<br>[00:00:00.050] [    0.000000]   Normal   empty<br>[00:00:00.051] [    0.000000] Movable zone start for each node<br>[00:00:00.052] [    0.000000] Early memory node ranges<br>[00:00:00.052] [    0.000000]   node   0: [mem 0x0000000000001000-0x000000000009efff]<br>[00:00:00.053] [    0.000000]   node   0: [mem 0x0000000000100000-0x000000003ffd6fff]<br>[00:00:00.054] [    0.000000] Initmem setup node 0 [mem 0x0000000000001000-0x000000003ffd6fff]<br>[00:00:00.054] [    0.000000] On node 0, zone DMA: 1 pages in unavailable ranges<br>[00:00:00.055] [    0.000000] On node 0, zone DMA: 97 pages in unavailable ranges<br>[00:00:00.056] [    0.000000] On node 0, zone DMA32: 41 pages in unavailable ranges<br>[00:00:00.057] [    0.000000] ACPI: PM-Timer IO Port: 0x608<br>[00:00:00.058] [    0.000000] ACPI: LAPIC_NMI (acpi_id[0xff] dfl dfl lint[0x1])<br>[00:00:00.059] [    0.000000] IOAPIC[0]: apic_id 0, version 32, address 0xfec00000, GSI 0-23<br>[00:00:00.061] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)<br>[00:00:00.062] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 5 global_irq 5 high level)<br>[00:00:00.063] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)<br>[00:00:00.065] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 10 global_irq 10 high level)<br>[00:00:00.066] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 11 global_irq 11 high level)<br>[00:00:00.068] [    0.000000] ACPI: Using ACPI (MADT) for SMP configuration information<br>[00:00:00.069] [    0.000000] ACPI: HPET id: 0x8086a201 base: 0xfed00000<br>[00:00:00.070] [    0.000000] smpboot: Allowing 4 CPUs, 0 hotplug CPUs<br>[00:00:00.071] [    0.000000] [mem 0x40000000-0xfffbffff] available for PCI devices<br>[00:00:00.072] [    0.000000] Booting paravirtualized kernel on bare hardware<br>[00:00:00.073] [    0.000000] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[00:00:00.075] [    0.000000] setup_percpu: NR_CPUS:256 nr_cpumask_bits:256 nr_cpu_ids:4 nr_node_ids:1<br>[00:00:00.077] [    0.000000] percpu: Embedded 54 pages/cpu s183896 r8192 d29096 u524288<br>[00:00:00.078] [    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 257751<br>[00:00:00.080] [    0.000000] Kernel command line: BOOT_IMAGE=vmlinuz-virt root=UUID=2f076e61-7a3e-43fd-86bf-63dcde993c23 modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4 initrd=initramfs-virt<br>[00:00:00.083] [    0.000000] Unknown kernel command line parameters "BOOT_IMAGE=vmlinuz-virt modules=sd-mod,usb-storage,ext4", will be passed to user space.<br>[00:00:00.085] [    0.000000] printk: log_buf_len individual max cpu contribution: 4096 bytes<br>[00:00:00.086] [    0.000000] printk: log_buf_len total cpu_extra contributions: 12288 bytes<br>[00:00:00.088] [    0.000000] printk: log_buf_len min size: 16384 bytes<br>[00:00:00.089] [    0.000000] printk: log_buf_len: 32768 bytes<br>[00:00:00.090] [    0.000000] printk: early log buf free: 11200(68%)<br>[00:00:00.092] [    0.000000] Dentry cache hash table entries: 131072 (order: 8, 1048576 bytes, linear)<br>[00:00:00.093] [    0.000000] Inode-cache hash table entries: 65536 (order: 7, 524288 bytes, linear)<br>[00:00:00.095] [    0.000000] mem auto-init: stack:byref(zero), heap alloc:on, heap free:off<br>[00:00:00.097] [    0.000000] Memory: 994632K/1048020K available (10246K kernel code, 1191K rwdata, 3024K rodata, 1824K init, 2032K bss, 53128K reserved, 0K cma-reserved)<br>[00:00:00.100] [    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1<br>[00:00:00.101] [    0.000000] rcu: Hierarchical RCU implementation.<br>[00:00:00.102] [    0.000000] rcu:      RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.<br>[00:00:00.104] [    0.000000]   Tracing variant of Tasks RCU enabled.<br>[00:00:00.105] [    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.<br>[00:00:00.107] [    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4<br>[00:00:00.109] [    0.000000] NR_IRQS: 16640, nr_irqs: 456, preallocated irqs: 16<br>[00:00:00.110] [    0.000000] kfence: initialized - using 2097152 bytes for 255 objects at 0x(____ptrval____)-0x(____ptrval____)<br>[00:00:00.113] [    0.000000] Console: colour VGA+ 80x25<br>[00:00:00.113] [    0.000000] printk: console [tty0] enabled<br>[00:00:00.115] [    0.000000] printk: console [ttyS0] enabled<br>[00:00:00.123] [    0.000000] ACPI: Core revision 20210730<br>[00:00:00.184] [    0.000000] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604467 ns<br>[00:00:00.245] [    0.030000] APIC: Switch to symmetric I/O mode setup<br>[00:00:00.298] [    0.080000] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1<br>[00:00:00.423] [    0.160000] tsc: Unable to calibrate against PIT<br>[00:00:00.425] [    0.160000] tsc: using HPET reference calibration<br>[00:00:00.426] [    0.160000] tsc: Detected 999.989 MHz processor<br>[00:00:00.435] [    0.005683] tsc: Marking TSC unstable due to TSCs unsynchronized<br>[00:00:00.442] [    0.011725] Calibrating delay loop (skipped), value calculated using timer frequency.. 1999.97 BogoMIPS (lpj=9999890)<br>[00:00:00.445] [    0.015941] pid_max: default: 32768 minimum: 301<br>[00:00:00.460] [    0.031322] LSM: Security Framework initializing<br>[00:00:00.480] [    0.051105] landlock: Up and running.<br>[00:00:00.509] [    0.080153] Mount-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[00:00:00.512] [    0.083118] Mountpoint-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[00:00:00.740] [    0.310996] process: using AMD E400 aware idle routine<br>[00:00:00.743] [    0.313954] Last level iTLB entries: 4KB 512, 2MB 255, 4MB 127<br>[00:00:00.744] [    0.315677] Last level dTLB entries: 4KB 512, 2MB 255, 4MB 127, 1GB 0<br>[00:00:00.750] [    0.321265] Spectre V1 : Mitigation: usercopy/swapgs barriers and __user pointer sanitization<br>[00:00:00.754] [    0.325443] Spectre V2 : Mitigation: Retpolines<br>[00:00:00.756] [    0.326876] Spectre V2 : Spectre v2 / SpectreRSB mitigation: Filling RSB on context switch<br>[00:00:00.759] [    0.329818] Spectre V2 : Spectre v2 / SpectreRSB : Filling RSB on VMEXIT<br>[00:00:02.435] [    2.000654] Freeing SMP alternatives memory: 32K<br>[00:00:02.724] [    2.279413] smpboot: CPU0: AMD QEMU Virtual CPU version 2.5+ (family: 0xf, model: 0x6b, stepping: 0x1)<br>[00:00:02.842] [    2.386230] Performance Events: PMU not available due to virtualization, using software events only.<br>[00:00:02.866] [    2.415828] rcu: Hierarchical SRCU implementation.<br>[00:00:02.925] [    2.475264] NMI watchdog: Perf NMI watchdog permanently disabled<br>[00:00:02.973] [    2.522609] smp: Bringing up secondary CPUs ...<br>[00:00:03.009] [    2.559881] x86: Booting SMP configuration:<br>[00:00:03.452] [    2.561471] .... node  #0, CPUs:      #1<br>[00:00:03.455] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:03.456] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:03.995] [    3.092904]  #2<br>[00:00:03.995] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:03.999] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:04.380] [    3.480859]  #3<br>[00:00:04.381] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:04.382] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:04.941] [    4.191354] smp: Brought up 1 node, 4 CPUs<br>[00:00:04.943] [    4.193361] smpboot: Max logical packages: 1<br>[00:00:04.944] [    4.194750] ----------------<br>[00:00:04.945] [    4.195644] | NMI testsuite:<br>[00:00:04.946] [    4.196429] --------------------<br>[00:00:04.958] [    4.197643]   remote IPI:  ok  |<br>[00:00:04.960] [    4.209590]    local IPI:  ok  |<br>[00:00:04.961] [    4.211807] --------------------<br>[00:00:04.962] [    4.212554] Good, all   2 testcases passed! |<br>[00:00:04.963] [    4.213476] ---------------------------------<br>[00:00:04.965] [    4.214924] smpboot: Total of 4 processors activated (2365.45 BogoMIPS)<br>[00:00:05.210] [    4.459976] devtmpfs: initialized<br>[00:00:05.260] [    4.510201] x86/mm: Memory block size: 128MB<br>[00:00:05.342] [    4.592098] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[00:00:05.349] [    4.598888] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)<br>[00:00:05.508] [    4.758791] NET: Registered PF_NETLINK/PF_ROUTE protocol family<br>[00:00:05.548] [    4.798227] audit: initializing netlink subsys (disabled)<br>[00:00:05.599] [    4.839858] audit: type=2000 audit(1681303043.980:1): state=initialized audit_enabled=0 res=1<br>[00:00:05.630] [    4.862034] thermal_sys: Registered thermal governor 'step_wise'<br>[00:00:05.632] [    4.880434] cpuidle: using governor ladder<br>[00:00:05.635] [    4.885175] cpuidle: using governor menu<br>[00:00:05.658] [    4.906555] ACPI: bus type PCI registered<br>[00:00:05.662] [    4.911014] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5<br>[00:00:05.707] [    4.956817] PCI: Using configuration type 1 for base access<br>[00:00:05.736] [    4.986787] mtrr: your CPUs had inconsistent fixed MTRR settings<br>[00:00:05.740] [    4.989779] mtrr: your CPUs had inconsistent variable MTRR settings<br>[00:00:05.741] [    4.991668] mtrr: your CPUs had inconsistent MTRRdefType settings<br>[00:00:05.742] [    4.992808] mtrr: probably your BIOS does not setup all CPUs.<br>[00:00:05.744] [    4.993932] mtrr: corrected configuration.<br>[00:00:05.875] [    5.125381] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.<br>[00:00:05.925] [    5.173951] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages<br>[00:00:06.264] [    5.513744] ACPI: Added _OSI(Module Device)<br>[00:00:06.266] [    5.515355] ACPI: Added _OSI(Processor Device)<br>[00:00:06.269] [    5.518456] ACPI: Added _OSI(3.0 _SCP Extensions)<br>[00:00:06.272] [    5.519565] ACPI: Added _OSI(Processor Aggregator Device)<br>[00:00:06.279] [    5.526103] ACPI: Added _OSI(Linux-Dell-Video)<br>[00:00:06.280] [    5.529590] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)<br>[00:00:06.282] [    5.531100] ACPI: Added _OSI(Linux-HPI-Hybrid-Graphics)<br>[00:00:06.485] [    5.734609] ACPI: 1 ACPI AML tables successfully acquired and loaded<br>[00:00:06.699] [    5.948965] ACPI: Interpreter enabled<br>[00:00:06.711] [    5.961538] ACPI: PM: (supports S0 S3 S5)<br>[00:00:06.713] [    5.963253] ACPI: Using IOAPIC for interrupt routing<br>[00:00:06.721] [    5.972100] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug<br>[00:00:06.745] [    5.995285] ACPI: Enabled 2 GPEs in block 00 to 0F<br>[00:00:07.208] [    6.454053] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-ff])<br>[00:00:07.217] [    6.464431] acpi PNP0A03:00: _OSC: OS supports [ASPM ClockPM Segments MSI HPX-Type3]<br>[00:00:07.226] [    6.474942] acpi PNP0A03:00: fail to add MMCONFIG information, can't access extended PCI configuration space under this bridge.<br>[00:00:07.311] [    6.561034] acpiphp: Slot [3] registered<br>[00:00:07.313] [    6.563775] acpiphp: Slot [4] registered<br>[00:00:07.315] [    6.565830] acpiphp: Slot [5] registered<br>[00:00:07.320] [    6.570317] acpiphp: Slot [6] registered<br>[00:00:07.323] [    6.573503] acpiphp: Slot [7] registered<br>[00:00:07.325] [    6.575596] acpiphp: Slot [8] registered<br>[00:00:07.328] [    6.579078] acpiphp: Slot [9] registered<br>[00:00:07.332] [    6.580852] acpiphp: Slot [10] registered<br>[00:00:07.334] [    6.582645] acpiphp: Slot [11] registered<br>[00:00:07.336] [    6.584706] acpiphp: Slot [12] registered<br>[00:00:07.340] [    6.590161] acpiphp: Slot [13] registered<br>[00:00:07.342] [    6.592970] acpiphp: Slot [14] registered<br>[00:00:07.344] [    6.594959] acpiphp: Slot [15] registered<br>[00:00:07.346] [    6.596611] acpiphp: Slot [16] registered<br>[00:00:07.351] [    6.600785] acpiphp: Slot [17] registered<br>[00:00:07.353] [    6.603831] acpiphp: Slot [18] registered<br>[00:00:07.355] [    6.605754] acpiphp: Slot [19] registered<br>[00:00:07.359] [    6.609759] acpiphp: Slot [20] registered<br>[00:00:07.362] [    6.612987] acpiphp: Slot [21] registered<br>[00:00:07.364] [    6.614934] acpiphp: Slot [22] registered<br>[00:00:07.366] [    6.616850] acpiphp: Slot [23] registered<br>[00:00:07.371] [    6.621167] acpiphp: Slot [24] registered<br>[00:00:07.373] [    6.623210] acpiphp: Slot [25] registered<br>[00:00:07.375] [    6.624957] acpiphp: Slot [26] registered<br>[00:00:07.379] [    6.628609] acpiphp: Slot [27] registered<br>[00:00:07.383] [    6.633716] acpiphp: Slot [28] registered<br>[00:00:07.385] [    6.635891] acpiphp: Slot [29] registered<br>[00:00:07.389] [    6.639702] acpiphp: Slot [30] registered<br>[00:00:07.392] [    6.642596] acpiphp: Slot [31] registered<br>[00:00:07.396] [    6.646392] PCI host bridge to bus 0000:00<br>[00:00:07.401] [    6.650686] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]<br>[00:00:07.403] [    6.653708] pci_bus 0000:00: root bus resource [io  0x0d00-0xffff window]<br>[00:00:07.406] [    6.655755] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]<br>[00:00:07.412] [    6.660031] pci_bus 0000:00: root bus resource [mem 0x40000000-0xfebfffff window]<br>[00:00:07.413] [    6.661718] pci_bus 0000:00: root bus resource [mem 0x100000000-0x17fffffff window]<br>[00:00:07.419] [    6.666540] pci_bus 0000:00: root bus resource [bus 00-ff]<br>[00:00:07.446] [    6.696135] pci 0000:00:00.0: [8086:1237] type 00 class 0x060000<br>[00:00:07.566] [    6.816566] pci 0000:00:01.0: [8086:7000] type 00 class 0x060100<br>[00:00:07.615] [    6.865736] pci 0000:00:01.1: [8086:7010] type 00 class 0x010180<br>[00:00:07.680] [    6.885820] pci 0000:00:01.1: reg 0x20: [io  0xc1e0-0xc1ef]<br>[00:00:07.732] [    6.919413] pci 0000:00:01.1: legacy IDE quirk: reg 0x10: [io  0x01f0-0x01f7]<br>[00:00:07.736] [    6.923042] pci 0000:00:01.1: legacy IDE quirk: reg 0x14: [io  0x03f6]<br>[00:00:07.742] [    6.930452] pci 0000:00:01.1: legacy IDE quirk: reg 0x18: [io  0x0170-0x0177]<br>[00:00:07.746] [    6.934930] pci 0000:00:01.1: legacy IDE quirk: reg 0x1c: [io  0x0376]<br>[00:00:07.795] [    6.984687] pci 0000:00:01.3: [8086:7113] type 00 class 0x068000<br>[00:00:07.806] [    6.994808] pci 0000:00:01.3: quirk: [io  0x0600-0x063f] claimed by PIIX4 ACPI<br>[00:00:07.811] [    7.000722] pci 0000:00:01.3: quirk: [io  0x0700-0x070f] claimed by PIIX4 SMB<br>[00:00:07.836] [    7.025919] pci 0000:00:02.0: [1234:1111] type 00 class 0x030000<br>[00:00:07.865] [    7.049566] pci 0000:00:02.0: reg 0x10: [mem 0xfd000000-0xfdffffff pref]<br>[00:00:07.922] [    7.089487] pci 0000:00:02.0: reg 0x18: [mem 0xfebd0000-0xfebd0fff]<br>[00:00:07.977] [    7.099413] pci 0000:00:02.0: reg 0x30: [mem 0xfebc0000-0xfebcffff pref]<br>[00:00:08.031] [    7.111826] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]<br>[00:00:08.108] [    7.188418] pci 0000:00:03.0: [1af4:1005] type 00 class 0x00ff00<br>[00:00:08.148] [    7.199434] pci 0000:00:03.0: reg 0x10: [io  0xc180-0xc19f]<br>[00:00:08.176] [    7.219413] pci 0000:00:03.0: reg 0x14: [mem 0xfebd1000-0xfebd1fff]<br>[00:00:08.326] [    7.279725] pci 0000:00:03.0: reg 0x20: [mem 0xfe000000-0xfe003fff 64bit pref]<br>[00:00:08.449] [    7.388911] pci 0000:00:04.0: [1af4:1000] type 00 class 0x020000<br>[00:00:08.482] [    7.399413] pci 0000:00:04.0: reg 0x10: [io  0xc1a0-0xc1bf]<br>[00:00:08.520] [    7.419788] pci 0000:00:04.0: reg 0x14: [mem 0xfebd2000-0xfebd2fff]<br>[00:00:08.663] [    7.499867] pci 0000:00:04.0: reg 0x20: [mem 0xfe004000-0xfe007fff 64bit pref]<br>[00:00:08.713] [    7.509413] pci 0000:00:04.0: reg 0x30: [mem 0xfeb80000-0xfebbffff pref]<br>[00:00:08.801] [    7.600364] pci 0000:00:05.0: [1af4:1001] type 00 class 0x010000<br>[00:00:08.824] [    7.618528] pci 0000:00:05.0: reg 0x10: [io  0xc000-0xc07f]<br>[00:00:08.871] [    7.619413] pci 0000:00:05.0: reg 0x14: [mem 0xfebd3000-0xfebd3fff]<br>[00:00:09.004] [    7.669413] pci 0000:00:05.0: reg 0x20: [mem 0xfe008000-0xfe00bfff 64bit pref]<br>[00:00:09.142] [    7.782620] pci 0000:00:06.0: [1af4:1001] type 00 class 0x010000<br>[00:00:09.164] [    7.789413] pci 0000:00:06.0: reg 0x10: [io  0xc080-0xc0ff]<br>[00:00:09.222] [    7.809413] pci 0000:00:06.0: reg 0x14: [mem 0xfebd4000-0xfebd4fff]<br>[00:00:09.351] [    7.849683] pci 0000:00:06.0: reg 0x20: [mem 0xfe00c000-0xfe00ffff 64bit pref]<br>[00:00:09.518] [    7.986702] pci 0000:00:07.0: [1af4:1001] type 00 class 0x010000<br>[00:00:09.551] [    7.999789] pci 0000:00:07.0: reg 0x10: [io  0xc100-0xc17f]<br>[00:00:09.590] [    8.009710] pci 0000:00:07.0: reg 0x14: [mem 0xfebd5000-0xfebd5fff]<br>[00:00:09.715] [    8.079707] pci 0000:00:07.0: reg 0x20: [mem 0xfe010000-0xfe013fff 64bit pref]<br>[00:00:09.836] [    8.176547] pci 0000:00:08.0: [1af4:1009] type 00 class 0x000200<br>[00:00:09.872] [    8.189782] pci 0000:00:08.0: reg 0x10: [io  0xc1c0-0xc1df]<br>[00:00:09.911] [    8.199607] pci 0000:00:08.0: reg 0x14: [mem 0xfebd6000-0xfebd6fff]<br>[00:00:10.045] [    8.249896] pci 0000:00:08.0: reg 0x20: [mem 0xfe014000-0xfe017fff 64bit pref]<br>[00:00:10.224] [    8.414351] ACPI: PCI: Interrupt link LNKA configured for IRQ 10<br>[00:00:10.234] [    8.424759] ACPI: PCI: Interrupt link LNKB configured for IRQ 10<br>[00:00:10.243] [    8.433044] ACPI: PCI: Interrupt link LNKC configured for IRQ 11<br>[00:00:10.250] [    8.440328] ACPI: PCI: Interrupt link LNKD configured for IRQ 11<br>[00:00:10.254] [    8.443864] ACPI: PCI: Interrupt link LNKS configured for IRQ 9<br>[00:00:10.314] [    8.504614] iommu: Default domain type: Translated<br>[00:00:10.316] [    8.506575] iommu: DMA domain TLB invalidation policy: lazy mode<br>[00:00:10.356] [    8.546220] SCSI subsystem initialized<br>[00:00:10.396] [    8.586486] pps_core: LinuxPPS API ver. 1 registered<br>[00:00:10.399] [    8.589090] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it><br>[00:00:10.403] [    8.593583] PTP clock support registered<br>[00:00:10.533] [    8.723131] PCI: Using ACPI for IRQ routing<br>[00:00:10.579] [    8.760434] hpet: 3 channels of 0 reserved for per-cpu timers<br>[00:00:10.606] [    8.794961] clocksource: Switched to clocksource hpet<br>[00:00:11.362] [    9.548539] VFS: Disk quotas dquot_6.6.0<br>[00:00:11.377] [    9.563457] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)<br>[00:00:11.412] [    9.597994] pnp: PnP ACPI init<br>[00:00:11.520] [    9.706112] pnp: PnP ACPI: found 6 devices<br>[00:00:11.960] [   10.146388] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns<br>[00:00:11.970] [   10.156866] NET: Registered PF_INET protocol family<br>[00:00:11.985] [   10.171690] IP idents hash table entries: 16384 (order: 5, 131072 bytes, linear)<br>[00:00:12.055] [   10.239770] tcp_listen_portaddr_hash hash table entries: 512 (order: 1, 8192 bytes, linear)<br>[00:00:12.060] [   10.246613] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)<br>[00:00:12.066] [   10.252206] TCP established hash table entries: 8192 (order: 4, 65536 bytes, linear)<br>[00:00:12.072] [   10.257987] TCP bind hash table entries: 8192 (order: 5, 131072 bytes, linear)<br>[00:00:12.077] [   10.263440] TCP: Hash tables configured (established 8192 bind 8192)<br>[00:00:12.093] [   10.279022] UDP hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[00:00:12.099] [   10.285009] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[00:00:12.121] [   10.307176] NET: Registered PF_UNIX/PF_LOCAL protocol family<br>[00:00:12.129] [   10.315373] NET: Registered PF_XDP protocol family<br>[00:00:12.140] [   10.326610] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]<br>[00:00:12.142] [   10.328107] pci_bus 0000:00: resource 5 [io  0x0d00-0xffff window]<br>[00:00:12.143] [   10.329234] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]<br>[00:00:12.146] [   10.332370] pci_bus 0000:00: resource 7 [mem 0x40000000-0xfebfffff window]<br>[00:00:12.147] [   10.334035] pci_bus 0000:00: resource 8 [mem 0x100000000-0x17fffffff window]<br>[00:00:12.160] [   10.346568] pci 0000:00:01.0: PIIX3: Enabling Passive Release<br>[00:00:12.163] [   10.349212] pci 0000:00:00.0: Limiting direct PCI/PCI transfers<br>[00:00:12.166] [   10.352982] pci 0000:00:01.0: Activating ISA DMA hang workarounds<br>[00:00:12.169] [   10.355326] PCI: CLS 0 bytes, default 64<br>[00:00:12.300] [   10.486371] Unpacking initramfs...<br>[00:00:12.335] [   10.521128] Initialise system trusted keyrings<br>[00:00:12.428] [   10.614654] workingset: timestamp_bits=46 max_order=18 bucket_order=0<br>[00:00:12.631] [   10.817673] zbud: loaded<br>[00:00:12.691] [   10.877438] Key type asymmetric registered<br>[00:00:12.693] [   10.879545] Asymmetric key parser 'x509' registered<br>[00:00:12.710] [   10.896353] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)<br>[00:00:12.738] [   10.924160] io scheduler mq-deadline registered<br>[00:00:12.740] [   10.926715] io scheduler kyber registered<br>[00:00:12.756] [   10.942695] io scheduler bfq registered<br>[00:00:12.902] [   11.088375] ERST DBG: ERST support is disabled.<br>[00:00:17.421] [   15.606862] Freeing initrd memory: 6840K<br>[00:00:17.758] [   15.944567] ACPI: \_SB_.LNKC: Enabled at IRQ 11<br>[00:00:20.221] [   18.407060] ACPI: \_SB_.LNKD: Enabled at IRQ 10<br>[00:00:22.636] [   20.822153] ACPI: \_SB_.LNKA: Enabled at IRQ 10<br>[00:00:25.060] [   23.246508] ACPI: \_SB_.LNKB: Enabled at IRQ 11<br>[00:00:29.931] [   28.109401] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled<br>[00:00:29.968] [   28.154333] 00:04: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A<br>[00:00:30.184] [   28.359656] VMware PVSCSI driver - version 1.0.7.0-k<br>[00:00:30.362] [   28.548240] scsi host0: ata_piix<br>[00:00:30.432] [   28.618575] scsi host1: ata_piix<br>[00:00:30.459] [   28.644780] ata1: PATA max MWDMA2 cmd 0x1f0 ctl 0x3f6 bmdma 0xc1e0 irq 14<br>[00:00:30.461] [   28.647600] ata2: PATA max MWDMA2 cmd 0x170 ctl 0x376 bmdma 0xc1e8 irq 15<br>[00:00:30.525] [   28.711803] i8042: PNP: PS/2 Controller [PNP0303:KBD,PNP0f13:MOU] at 0x60,0x64 irq 1,12<br>[00:00:30.619] [   28.805320] serio: i8042 KBD port at 0x60,0x64 irq 1<br>[00:00:30.623] [   28.809190] serio: i8042 AUX port at 0x60,0x64 irq 12<br>[00:00:30.633] [   28.819101] rtc_cmos 00:05: RTC can wake from S4<br>[00:00:30.807] [   28.881017] hpet: Lost 5 RTC interrupts<br>[00:00:31.203] [   29.386455] ata2.00: ATAPI: QEMU DVD-ROM, 2.5+, max UDMA/100<br>[00:00:31.675] [   29.828287] rtc_cmos 00:05: registered as rtc0<br>[00:00:31.719] [   29.901739] rtc_cmos 00:05: setting system clock to 2023-04-12T12:37:51 UTC (1681303071)<br>[00:00:31.830] [   30.016061] rtc_cmos 00:05: alarms up to one day, y3k, 242 bytes nvram, hpet irqs<br>[00:00:32.001] [   30.187629] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input0<br>[00:00:32.158] [   30.344559] gre: GRE over IPv4 demultiplexor driver<br>[00:00:32.262] [   30.448607] scsi 1:0:0:0: CD-ROM            QEMU     QEMU DVD-ROM     2.5+ PQ: 0 ANSI: 5<br>[00:00:32.275] [   30.457721] Key type dns_resolver registered<br>[00:00:32.301] [   30.487202] IPI shorthand broadcast: enabled<br>[00:00:32.487] [   30.673323] registered taskstats version 1<br>[00:00:32.491] [   30.677141] Loading compiled-in X.509 certificates<br>[00:00:33.702] [   31.888091] Loaded X.509 cert 'Build time autogenerated kernel key: 90200cc09a919577283b2cb6eca2ff9ac9891c1d'<br>[00:00:33.752] [   31.938130] zswap: loaded using pool lzo/zbud<br>[00:00:33.868] [   32.054520] Key type .fscrypt registered<br>[00:00:33.869] [   32.056001] Key type fscrypt-provisioning registered<br>[00:00:33.960] [   32.146150] Unstable clock detected, switching default tracing clock to "global"<br>[00:00:33.961] [   32.146150] If you want to keep using the local clock, then add:<br>[00:00:33.962] [   32.146150]   "trace_clock=local"<br>[00:00:33.964] [   32.146150] on the kernel command line<br>[00:00:34.227] [   32.413628] Freeing unused kernel image (initmem) memory: 1824K<br>[00:00:34.246] [   32.432736] Write protecting the kernel read-only data: 16384k<br>[00:00:34.297] [   32.482833] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[00:00:34.313] [   32.499316] Freeing unused kernel image (rodata/data gap) memory: 1072K<br>[00:00:34.321] [   32.508008] rodata_test: all tests were successful<br>[00:00:34.327] [   32.513414] Run /init as init process<br>[00:00:35.888] [   34.074400] Alpine Init 3.7.0-r1<br>[00:00:35.915] Alpine Init 3.7.0-r1<br>[00:00:35.949] [   34.135189] Loading boot drivers...<br>[00:00:35.953]  * Loading boot drivers: [   35.431824] ACPI: bus type USB registered<br>[00:00:37.258] [   35.444668] usbcore: registered new interface driver usbfs<br>[00:00:37.262] [   35.449017] usbcore: registered new interface driver hub<br>[00:00:37.283] [   35.469290] usbcore: registered new device driver usb<br>[00:00:37.469] [   35.655595] usbcore: registered new interface driver usb-storage<br>[00:00:40.259] [   38.445370] loop: module loaded<br>[00:00:42.809] [   40.995845] Loading boot drivers: ok.<br>[00:00:42.815] ok.<br>[00:00:43.001] [   41.187057] Mounting root...<br>[00:00:43.014]  * Mounting root: [   48.549016] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[00:00:50.367] [   48.553945] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[00:00:52.107] [   50.293118] virtio_blk virtio2: [vda] 100352 512-byte logical blocks (51.4 MB/49.0 MiB)<br>[00:00:52.218] [   50.404677]  vda: vda1 vda2<br>[00:00:52.309] [   50.494679] virtio_blk virtio3: [vdb] 5232640 512-byte logical blocks (2.68 GB/2.50 GiB)<br>[00:00:52.343] [   50.529156]  vdb: vdb1 vdb2 vdb3<br>[00:00:52.418] [   50.604796] virtio_blk virtio4: [vdc] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[00:01:25.191] [   83.353920] EXT4-fs (vdb3): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[00:01:25.259] [   83.445530] Mounting root: ok.<br>[00:01:25.287] ok.<br>[00:01:27.725]<br>[00:01:27.814]    OpenRC 0.45.2 is starting up Linux 5.15.106-0-virt (x86_64)<br>[00:01:27.815]<br>[00:01:28.624]  * /proc is already mounted<br>[00:01:29.092]  * Mounting /run ... * /run/openrc: creating directory<br>[00:01:29.675]  * /run/lock: creating directory<br>[00:01:29.676]  * /run/lock: correcting owner<br>[00:01:50.596]  * Caching service dependencies ... [ ok ]<br>[00:01:53.163]  * Remounting devtmpfs on /dev ... [ ok ]<br>[00:01:54.262]  * Mounting /dev/mqueue ... [ ok ]<br>[00:01:58.497]  * Mounting security filesystem ... [ ok ]<br>[00:01:58.819]  * Mounting debug filesystem ... [ ok ]<br>[00:01:59.150]  * Mounting persistent storage (pstore) filesystem ... [ ok ]<br>[00:02:00.830]  * Starting busybox mdev ... [ ok ]<br>[00:02:01.049]  * Scanning hardware for mdev ... [ ok ]<br>[00:02:23.605]  * Loading hardware drivers ... [ ok ]<br>[00:03:19.705]  * Loading modules ... [ ok ]<br>[00:03:26.644]  * Setting system clock using the hardware clock [UTC] ... [ ok ]<br>[00:03:30.032]  * Checking local filesystems  .../dev/vdb3: clean, 56362/144288 files, 422590/577024 blocks<br>[00:03:31.183] /dev/vdb1: clean, 27/38456 files, 33615/153600 blocks<br>[00:03:31.329]  [ ok ]<br>[00:03:33.132]  * Remounting root filesystem read/write ... [ ok ]<br>[00:03:33.654]  * Remounting filesystems ... [ ok ]<br>[00:03:36.104]  * Activating swap devices ... [ ok ]<br>[00:03:38.343]  * Mounting local filesystems ... [ ok ]<br>[00:03:43.492]  * Configuring kernel parameters ... [ ok ]<br>[00:03:47.321]  * Creating user login records ... [ ok ]<br>[00:03:50.304]  * Setting hostname ... [ ok ]<br>[00:03:52.192]  * Starting networking ... *   lo ... [ ok ]<br>[00:03:54.975]  *   eth0 ...udhcpc: started, v1.35.0<br>[00:03:56.833] udhcpc: broadcasting discover<br>[00:03:57.071] udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>[00:03:57.174] udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br>[00:03:59.004]  [ ok ]<br>[00:04:00.795]  * Seeding random number generator ... * Seeding 256 bits and crediting<br>[00:04:01.004]  * Saving 256 bits of creditable seed for next boot<br>[00:04:01.095]  [ ok ]<br>[00:04:02.854]  * Starting busybox syslog ... [ ok ]<br>[00:04:10.647]  * Starting busybox acpid ... [ ok ]<br>[00:04:12.974]  * Starting busybox crond ... [ ok ]<br>[00:04:19.074]  * Starting sshd ... [ ok ]<br>[00:04:26.396]  * Starting lighttpd ... [ ok ]<br>[00:04:31.286]<br>[00:04:31.286] Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br>[00:04:31.288]<br>localhost login:<br>[00:06:55.724] Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br>[00:06:55.725]<br>localhost login:<br>[00:07:01.806] Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br>[00:07:01.808]<br>localhost login:<br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login:<br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~#<br>localhost:~# pwd<br>/root<br>localhost:~#<br>localmount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /mnt/9p-host/9p-host<br>localhost:~#<br>localhost:~#<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124365,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vdb3 on / type ext4 (rw,relatime)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201340k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>tracefs on /sys/kernel/debug/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)<br>/dev/vdb1 on /boot type ext4 (rw,relatime)<br>tmpfs on /tmp type tmpfs (rw,nosuid,nodev,relatime,inode64)<br>host on /mnt/9p-host type 9p (rw,relatime,sync,dirsync,access=client,msize=512000,trans=virtio)<br>localhost:~#<br>localhost:~# df -ahT<br>Filesystem     Type        Size  Used Avail Use% Mounted on<br>sysfs          sysfs          0     0     0    - /sys<br>devtmpfs       devtmpfs     10M     0   10M   0% /dev<br>proc           proc           0     0     0    - /proc<br>devpts         devpts         0     0     0    - /dev/pts<br>shm            tmpfs       492M     0  492M   0% /dev/shm<br>/dev/vdb3      ext4        2.1G  1.6G  475M  77% /<br>tmpfs          tmpfs       197M  128K  197M   1% /run<br>mqueue         mqueue         0     0     0    - /dev/mqueue<br>securityfs     securityfs     0     0     0    - /sys/kernel/security<br>debugfs        debugfs        0     0     0    - /sys/kernel/debug<br>pstore         pstore         0     0     0    - /sys/fs/pstore<br>tracefs        tracefs        0     0     0    - /sys/kernel/debug/tracing<br>/dev/vdb1      ext4        136M   18M  107M  15% /boot<br>tmpfs          tmpfs       492M     0  492M   0% /tmp<br>host           9p          9.6G  9.0G  659M  94% /mnt/9p-host<br>localhost:~#<br>localhost:~# exit<br>logout<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~# poweroff<br>localhost:~#<br>[ 6161.624754] reboot: Power down<br>~ $<br></pre></td>
</tr>
</table>

<p><br></p>

<a id="termux-session-for-termux-command-line"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#termux-command-line">Termux-Command-Line</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ export SOCKET_FILENAME=socket.RkS6jHIE5Q<br>~ $<br>~ $ echo $SOCKET_FILENAME<br>socket.RkS6jHIE5Q<br>~ $<br>~ $ export DIRECTORY_9p_HOST_mktemp=/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>~ $<br>~ $ echo $DIRECTORY_9p_HOST_mktemp<br>/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>~ $<br>~ $ cd $HOME<br>~ $<br>~ $ echo 'info usernet' | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info usernet<br>Hub -1 (net0):<br>  Protocol[State]    FD  Source Address  Port   Dest. Address  Port RecvQ SendQ<br>  TCP[HOST_FORWARD]  15               * 15022       10.0.2.15    22     0     0<br>  TCP[HOST_FORWARD]  14               * 15081       10.0.2.15 15081     0     0<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block123): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block357): /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/vmtest2.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block515): /storage/2240-5293/Android/data/com.termux/files/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br>(qemu) ~ $<br>~ $<br>~ $ echo "drive_add 0 if=none,file=$DIRECTORY_9p_HOST_mktemp/test-disk1-200mb.ext,format=raw,id=disk1" | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>-diskdrive_add 0 if=none,file=/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/test-disk1-200mb.ext,format=raw,id=disk1<br>OK<br>(qemu) ~ $<br>~ $<br>~ $ echo 'device_add virtio-blk-pci,drive=disk1,id=virt1' | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) device_add virtio-blk-pci,drive=disk1,id=virt1<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block123): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block357): /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/vmtest2.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block515): /storage/2240-5293/Android/data/com.termux/files/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk1 (#block719): /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/test-disk1-200mb.ext (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu) ~ $<br>~ $<br>~ $ echo 'info block'  | nc -UN $SOCKET_FILENAME<br>QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info block<br>drive1 (#block123): /storage/emulated/0/Download/alpine-virt-3.17.3-x86_64.iso (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk1/virtio-backend<br>    Cache mode:       writeback<br><br>drive2 (#block357): /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/vmtest2.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block515): /storage/2240-5293/Android/data/com.termux/files/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk1 (#block719): /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi/test-disk1-200mb.ext (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu) ~ $<br>~ $<br>~ $ ssh test@127.0.0.1 -p 15022<br>The authenticity of host '[127.0.0.1]:15022 ([127.0.0.1]:15022)' can't be established.<br>ED25519 key fingerprint is SHA256:2QTm3mvsRq4LD6aMcGFtgvMt7UkOvUqby8J6jf25Fv8.<br>This key is not known by any other names.<br>Are you sure you want to continue connecting (yes/no/[fingerprint])? yes<br>Warning: Permanently added '[127.0.0.1]:15022' (ED25519) to the list of known hosts.<br>test@127.0.0.1's password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~$<br>localhost:~$ blkid<br>/dev/vdb1: UUID="b2eb3d69-02e2-49c2-8310-1d4b57f3b06a" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="6046661c-01"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660" PTUUID="77b851c3" PTTYPE="dos" PARTUUID="77b851c3-01"<br>/dev/vdb2: UUID="65da52b4-34b0-4e59-b8bf-cde21e825ca4" TYPE="swap" PARTUUID="6046661c-02"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vdb3: UUID="2f076e61-7a3e-43fd-86bf-63dcde993c23" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="6046661c-03"<br>/dev/vdd: LABEL="disk1-200mb" UUID="29564dd2-6701-4c01-bd5c-e653af0a44e3" BLOCK_SIZE="1024" TYPE="ext4"<br>localhost:~$<br>localhost:~$<br>localhost:~$ lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0  2.5G  0 disk<br>├─vdb1 253:17   0  150M  0 part /boot<br>├─vdb2 253:18   0  150M  0 part [SWAP]<br>└─vdb3 253:19   0  2.2G  0 part /<br>vdc    253:32   0   50G  1 disk<br>vdd    253:48   0  200M  0 disk<br>localhost:~$<br>localhost:~$ blkid|grep disk1-200mb<br>/dev/vdd: LABEL="disk1-200mb" UUID="29564dd2-6701-4c01-bd5c-e653af0a44e3" BLOCK_SIZE="1024" TYPE="ext4"<br>localhost:~$<br>localhost:~$ grep -i virt /var/log/messages | tail -10<br>localhost:~$<br>localhost:~$ dmesg|grep -i virt|tail -5<br>dmesg: read kernel buffer failed: Operation not permitted<br>localhost:~$<br>localhost:~$<br>localhost:~$ sudo dmesg|grep -i virt|tail -5<br><br>We trust you have received the usual lecture from the local System<br>Administrator. It usually boils down to these three things:<br><br>    #1) Respect the privacy of others.<br>    #2) Think before you type.<br>    #3) With great power comes great responsibility.<br><br>[sudo] password for test:<br>[   50.494679] virtio_blk virtio3: [vdb] 5232640 512-byte logical blocks (2.68 GB/2.50 GiB)<br>[   50.604796] virtio_blk virtio4: [vdc] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[  168.796384] kvm: Nested Virtualization enabled<br>[ 1111.255257] virtio-pci 0000:00:09.0: enabling device (0000 -> 0003)<br>[ 1116.397754] virtio_blk virtio6: [vdd] 409600 512-byte logical blocks (210 MB/200 MiB)<br>localhost:~$<br>localhost:~$<br>localhost:~$ sudo mount LABEL=disk1-200mb /mnt/disk1<br>localhost:~$<br>localhost:~$<br>localhost:~$ sudo chmod a+rwx,o+t /mnt/disk1<br>localhost:~$<br>localhost:~$ stat /mnt/disk1|grep 'rwx'<br>Access: (1777/drwxrwxrwt)  Uid: (    0/    root)   Gid: (    0/    root)<br>localhost:~$<br>localhost:~$ stat /tmp|grep 'rwx'<br>Access: (1777/drwxrwxrwt)  Uid: (    0/    root)   Gid: (    0/    root)<br>localhost:~$<br>localhost:~$ ls -alR /mnt/disk1<br>/mnt/disk1:<br>total 17<br>drwxrwxrwt 3 root root  1024 Apr 12 09:02 .<br>drwxr-xr-x 5 root root  4096 Apr 12 11:46 ..<br>drwx------ 2 root root 12288 Apr 12 09:02 lost+found<br>ls: cannot open directory '/mnt/disk1/lost+found': Permission denied<br>localhost:~$<br>localhost:~$ touch /mnt/disk1/file1-made-on-server<br>localhost:~$ touch /mnt/disk1/file2-made-on-server<br>localhost:~$<br>localhost:~$ pwd<br>/home/test<br>localhost:~$<br>localhost:~$ sudo mkdir /mnt/disk2<br>localhost:~$<br>localhost:~$ date<br>Wed Apr 12 13:06:47 UTC 2023<br>localhost:~$<br>localhost:~$ cryptsetup benchmark<br># Tests are approximate using memory only (no storage IO).<br>PBKDF2-sha1         4299 iterations per second for 256-bit key<br>PBKDF2-sha256       9186 iterations per second for 256-bit key<br>PBKDF2-sha512       7343 iterations per second for 256-bit key<br>PBKDF2-ripemd160    5429 iterations per second for 256-bit key<br>PBKDF2-whirlpool    4335 iterations per second for 256-bit key<br>argon2i       4 iterations, 65536 memory, 4 parallel threads (CPUs) for 256-bit key (requested 2000 ms time)<br>argon2id      4 iterations, 65536 memory, 4 parallel threads (CPUs) for 256-bit key (requested 2000 ms time)<br>#     Algorithm |       Key |      Encryption |      Decryption<br>        aes-cbc        128b         0.6 MiB/s         4.1 MiB/s<br>date    serpent-cbc        128b         0.5 MiB/s         4.1 MiB/s<br>    twofish-cbc        128b         0.6 MiB/s         2.7 MiB/s<br>        aes-cbc        256b         3.1 MiB/s         3.0 MiB/s<br><br>    serpent-cbc        256b         3.3 MiB/s         4.3 MiB/s<br>    twofish-cbc        256b         3.9 MiB/s         3.0 MiB/s<br>        aes-xts        256b         1.1 MiB/s         4.4 MiB/s<br>    serpent-xts        256b         1.2 MiB/s         4.5 MiB/s<br>    twofish-xts        256b         1.4 MiB/s         2.8 MiB/s<br>        aes-xts        512b         3.7 MiB/s         3.2 MiB/s<br>    serpent-xts        512b         4.6 MiB/s         4.6 MiB/s<br>    twofish-xts        512b         3.0 MiB/s         2.8 MiB/s<br>localhost:~$ date<br>Wed Apr 12 13:10:10 UTC 2023<br>localhost:~$<br>localhost:~$ fallocate -l 30M /mnt/9p-host/disk2-luks-30mb.img<br>fallocate: fallocate failed: Not supported<br>localhost:~$<br>localhost:~$ dd if=/dev/urandom of=/mnt/9p-host/disk2-luks-30mb.img bs=1M count=30<br>30+0 records in<br>30+0 records out<br>31457280 bytes (31 MB, 30 MiB) copied, 4.805 s, 6.5 MB/s<br>localhost:~$<br>localhost:~$ sudo losetup --show --find /mnt/9p-host/disk2-luks-30mb.img<br>/dev/loop0<br>localhost:~$<br>localhost:~$ sudo cryptsetup luksFormat --type=luks2 /dev/loop0<br><br>WARNING!<br>========<br>This will overwrite data on /dev/loop0 irrevocably.<br><br>Are you sure? (Type 'yes' in capital letters): YES<br>Enter passphrase for /mnt/9p-host/disk2-luks-30mb.img:<br>Verify passphrase:<br>localhost:~$<br>localhost:~$ sudo cryptsetup luksOpen /dev/loop0 mapped-disk2-luks<br>Enter passphrase for /mnt/9p-host/disk2-luks-30mb.img:<br>localhost:~$<br>localhost:~$ sudo mkfs.ext4 -m 0 -L disk2-luks /dev/mapper/mapped-disk2-luks<br>mke2fs 1.46.6 (1-Feb-2023)<br>Creating filesystem with 14336 1k blocks and 3584 inodes<br>Filesystem UUID: 33651d35-3741-4565-9dbc-b9399b70099b<br>Superblock backups stored on blocks:<br>        8193<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (1024 blocks): done<br>Writing superblocks and filesystem accounting information: done<br><br>localhost:~$<br>localhost:~$ sudo mount /dev/mapper/mapped-disk2-luks /mnt/disk2<br>localhost:~$<br>localhost:~$ sudo chown test:test /mnt/disk2/.<br>localhost:~$<br>localhost:~$ sudo umount /mnt/disk2<br>localhost:~$<br>localhost:~$ sudo cryptsetup luksClose mapped-disk2-luks<br>localhost:~$<br>localhost:~$ sudo losetup --detach /dev/loop0<br>localhost:~$<br>localhost:~$ sudo losetup --show --find /mnt/9p-host/disk2-luks-30mb.img<br>/dev/loop0<br>localhost:~$<br>localhost:~$ sudo cryptsetup luksOpen /dev/loop0 mapped-disk2-luks<br>Enter passphrase for /mnt/9p-host/disk2-luks-30mb.img:<br>localhost:~$<br>localhost:~$ sudo mount /dev/mapper/mapped-disk2-luks /mnt/disk2<br>localhost:~$<br>localhost:~$ ls -laR /mnt/disk2<br>/mnt/disk2:<br>total 17<br>drwxr-xr-x 3 test test  1024 Apr 12 13:26 .<br>drwxr-xr-x 6 root root  4096 Apr 12 13:06 ..<br>drwx------ 2 root root 12288 Apr 12 13:26 lost+found<br>ls: cannot open directory '/mnt/disk2/lost+found': Permission denied<br>localhost:~$<br>localhost:~$ touch /mnt/disk2/file3-from-server<br>localhost:~$<br>localhost:~$ ls -laR /mnt/disk2<br>/mnt/disk2:<br>total 17<br>drwxr-xr-x 3 test test  1024 Apr 12 13:30 .<br>drwxr-xr-x 6 root root  4096 Apr 12 13:06 ..<br>-rw-r--r-- 1 test test     0 Apr 12 13:30 file3-from-server<br>drwx------ 2 root root 12288 Apr 12 13:26 lost+found<br>ls: cannot open directory '/mnt/disk2/lost+found': Permission denied<br>localhost:~$<br>localhost:~$ sudo umount /mnt/disk2<br>localhost:~$<br>localhost:~$ sudo cryptsetup luksClose mapped-disk2-luks<br>localhost:~$<br>localhost:~$ sudo losetup --detach /dev/loop0<br>localhost:~$<br>localhost:~$ df -h<br>Filesystem      Size  Used Avail Use% Mounted on<br>devtmpfs         10M     0   10M   0% /dev<br>shm             492M     0  492M   0% /dev/shm<br>/dev/vdb3       2.1G  1.6G  475M  77% /<br>tmpfs           197M  132K  197M   1% /run<br>/dev/vdb1       136M   18M  107M  15% /boot<br>tmpfs           492M     0  492M   0% /tmp<br>host            9.6G  9.0G  629M  94% /mnt/9p-host<br>/dev/vdd        182M   64K  178M   1% /mnt/disk1<br>localhost:~$<br>localhost:~$ ls -laR /mnt/9p-host<br>/mnt/9p-host:<br>total 2854656<br>drwxrwx--- 2 root nine-p-host       3488 Apr 12 13:10 .<br>drwxr-xr-x 6 root root              4096 Apr 12 13:06 ..<br>-rw-rw---- 1 root nine-p-host   31457280 Apr 12 13:30 disk2-luks-30mb.img<br>-rw-rw---- 1 root nine-p-host          0 Apr 12 11:53 from-guest-os-to-host.txt<br>-rw-rw---- 1 root nine-p-host  209715200 Apr 12 13:05 test-disk1-200mb.ext<br>-rw-rw---- 1 root nine-p-host 2679111680 Apr 12 13:32 vmtest2.raw<br>localhost:~$<br>localhost:~$ mv -iv /mnt/9p-host/disk2-luks-30mb.img /mnt/disk1<br>copied '/mnt/9p-host/disk2-luks-30mb.img' -> '/mnt/disk1/disk2-luks-30mb.img'<br>removed '/mnt/9p-host/disk2-luks-30mb.img'<br>localhost:~$<br>localhost:~$ ls -laR /mnt/9p-host<br>/mnt/9p-host:<br>total 2823904<br>drwxrwx--- 2 root nine-p-host       3488 Apr 12 13:32 .<br>drwxr-xr-x 6 root root              4096 Apr 12 13:06 ..<br>-rw-rw---- 1 root nine-p-host          0 Apr 12 11:53 from-guest-os-to-host.txt<br>-rw-rw---- 1 root nine-p-host  209715200 Apr 12 13:32 test-disk1-200mb.ext<br>-rw-rw---- 1 root nine-p-host 2679111680 Apr 12 13:32 vmtest2.raw<br>localhost:~$<br>localhost:~$ ls -laR /mnt/disk1<br>/mnt/disk1:<br>total 30737<br>drwxrwxrwt 3 root root            1024 Apr 12 13:32 .<br>drwxr-xr-x 6 root root            4096 Apr 12 13:06 ..<br>-rw-rw---- 1 test nine-p-host 31457280 Apr 12 13:30 disk2-luks-30mb.img<br>-rw-r--r-- 1 test test               0 Apr 12 13:05 file1-made-on-server<br>-rw-r--r-- 1 test test               0 Apr 12 13:05 file2-made-on-server<br>drwx------ 2 root root           12288 Apr 12 09:02 lost+found<br>ls: cannot open directory '/mnt/disk1/lost+found': Permission denied<br>localhost:~$<br>localhost:~$ logout<br>Connection to 127.0.0.1 closed.<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ env<br>SHELL=/data/data/com.termux/files/usr/bin/bash<br>COLORTERM=truecolor<br>HISTCONTROL=ignoreboth<br>PREFIX=/data/data/com.termux/files/usr<br>JAVA_HOME=/data/data/com.termux/files/usr/opt/openjdk<br>TERMUX_IS_DEBUGGABLE_BUILD=1<br>TERMUX_MAIN_PACKAGE_FORMAT=debian<br>PWD=/data/data/com.termux/files/home<br>SOCKET_FILENAME=socket.RkS6jHIE5Q<br>TERMUX_VERSION=0.118.0<br>EXTERNAL_STORAGE=/sdcard<br>LD_PRELOAD=/data/data/com.termux/files/usr/lib/libtermux-exec.so<br>TERMUX_API_VERSION=0.50.1<br>HOME=/data/data/com.termux/files/home<br>LANG=en_US.UTF-8<br>ANDROID_RUNTIME_ROOT=/apex/com.android.runtime<br>TERMUX_APK_RELEASE=GITHUB<br>DEX2OATBOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/QPerformance.jar:/system/framework/UxPerformance.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/knoxsdk.jar:/system/framework/knoxanalyticssdk.jar:/system/framework/smartbondingservice.jar:/system/framework/securetimersdk.jar:/system/framework/drutils.jar:/system/framework/android.test.base.jar:/system/framework/tcmiface.jar:/system/framework/telephony-ext.jar<br>TMPDIR=/data/data/com.termux/files/usr/tmp<br>DIRECTORY_9p_HOST_mktemp=/storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>ANDROID_DATA=/data<br>TERM=xterm-256color<br>SHLVL=1<br>ANDROID_ROOT=/system<br>BOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/QPerformance.jar:/system/framework/UxPerformance.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/knoxsdk.jar:/system/framework/knoxanalyticssdk.jar:/system/framework/smartbondingservice.jar:/system/framework/securetimersdk.jar:/system/framework/drutils.jar:/system/framework/android.test.base.jar:/system/framework/tcmiface.jar:/system/framework/telephony-ext.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar<br>ANDROID_TZDATA_ROOT=/apex/com.android.tzdata<br>TERMUX_APP_PID=5253<br>PATH=/data/data/com.termux/files/usr/bin<br>OLDPWD=/data/data/com.termux/files/home<br>_=/data/data/com.termux/files/usr/bin/env<br>~ $<br>~ $ whereis termux-info<br>termux-info: /data/data/com.termux/files/usr/bin/termux-info<br>~ $<br>~ $<br>~ $ cadaver http://127.0.0.1:15081/webdav<br>Authentication required for realm-webdav on server `127.0.0.1':<br>Username: test1<br>Password:<br>dav:/webdav/> ls<br>Listing collection `/webdav/': succeeded.<br>Coll:   lost+found                         12288  Apr 12 05:02<br>        disk2-luks-30mb.img             31457280  Apr 12 09:30<br>        file1-made-on-server                   0  Apr 12 09:05<br>        file2-made-on-server                   0  Apr 12 09:05<br>dav:/webdav/><br>dav:/webdav/> lls<br>lls: unknown program ‘lls’<br>Try 'lls --help' for more information.<br>dav:/webdav/><br>dav:/webdav/> lls --help<br>Usage: lls --coreutils-prog=PROGRAM_NAME [PARAMETERS]...<br>Execute the PROGRAM_NAME built-in program with the given PARAMETERS.<br><br>      --help        display this help and exit<br>      --version     output version information and exit<br><br>Built-in programs:<br> [ b2sum base32 base64 basename basenc cat chcon chgrp chmod chown chroot cksum comm cp csplit cut date dd dir dircolors dirname du echo env expand expr factor false fmt fold ginstall groups head id join kill link ln logname ls md5sum mkdir mkfifo mknod mktemp mv nice nl nohup nproc numfmt od paste pathchk pr printenv printf ptx pwd readlink realpath rm rmdir runcon seq sha1sum sha224sum sha256sum sha384sum sha512sum shred shuf sleep sort split stat stdbuf stty sum sync tac tail tee test timeout touch tr true truncate tsort tty uname unexpand uniq unlink vdir wc whoami yes<br><br>Use: 'lls --coreutils-prog=PROGRAM_NAME --help' for individual program help.<br><br>GNU coreutils online help: <https://www.gnu.org/software/coreutils/><br>Report any translation bugs to <https://translationproject.org/team/><br>Full documentation <https://www.gnu.org/software/coreutils/coreutils><br>or available locally via: info '(coreutils) Multi-call invocation'<br>dav:/webdav/><br>dav:/webdav/> lls --coreutils-prog=ls<br>backup  socket.RkS6jHIE5Q  storage<br>dav:/webdav/><br>dav:/webdav/> lls --coreutils-prog=ls -l<br>total 7<br>drwx------ 2 u0_a188 u0_a188 3488 Apr 10 12:31 backup<br>srwx------ 1 u0_a188 u0_a188    0 Apr 12 05:41 socket.RkS6jHIE5Q<br>drwx------ 2 u0_a188 u0_a188 3488 Apr  3 16:32 storage<br>dav:/webdav/><br>dav:/webdav/> lcd /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>dav:/webdav/> lpwd<br>Local directory: /storage/emulated/0/Download/host-guest-os.bOv9BQWrgi<br>dav:/webdav/><br>dav:/webdav/> lls --coreutils-prog=ls -l<br>total 2823896<br>-rw-rw---- 1 root everybody          0 Apr 12 07:53 from-guest-os-to-host.txt<br>-rw-rw---- 1 root everybody  209715200 Apr 12 09:33 test-disk1-200mb.ext<br>-rw-rw---- 1 root everybody 2679111680 Apr 12 10:06 vmtest2.raw<br>dav:/webdav/><br>dav:/webdav/> ls<br>Listing collection `/webdav/': succeeded.<br>Coll:   lost+found                         12288  Apr 12 05:02<br>        disk2-luks-30mb.img             31457280  Apr 12 09:30<br>        file1-made-on-server                   0  Apr 12 09:05<br>        file2-made-on-server                   0  Apr 12 09:05<br>dav:/webdav/><br>dav:/webdav/> get file1-from-server<br>Downloading `/webdav/file1-from-server' to file1-from-server:<br>Progress: [=============================>] 100.0% of 341 bytes failed:<br>404 Not Found<br>dav:/webdav/><br>dav:/webdav/> get file1-made-on-server<br>Downloading `/webdav/file1-made-on-server' to file1-made-on-server: [.] succeeded.<br>dav:/webdav/><br>dav:/webdav/> lls --coreutils-prog=ls -l<br>total 2823896<br>-rw-rw---- 1 root everybody          0 Apr 12 10:10 file1-from-server<br>-rw-rw---- 1 root everybody          0 Apr 12 10:11 file1-made-on-server<br>-rw-rw---- 1 root everybody          0 Apr 12 07:53 from-guest-os-to-host.txt<br>-rw-rw---- 1 root everybody  209715200 Apr 12 09:33 test-disk1-200mb.ext<br>-rw-rw---- 1 root everybody 2679111680 Apr 12 10:12 vmtest2.raw<br>dav:/webdav/><br>dav:/webdav/> put /data/data/com.termux/files/usr/bin/termux-info<br>Uploading /data/data/com.termux/files/usr/bin/termux-info to `/webdav/termux-info':<br>Progress: [=============================>] 100.0% of 3270 bytes succeeded.<br>dav:/webdav/><br>dav:/webdav/> ls<br>Listing collection `/webdav/': succeeded.<br>Coll:   lost+found                         12288  Apr 12 05:02<br>        disk2-luks-30mb.img             31457280  Apr 12 09:30<br>        file1-made-on-server                   0  Apr 12 09:05<br>        file2-made-on-server                   0  Apr 12 09:05<br>        termux-info                         3270  Apr 12 10:12<br>dav:/webdav/><br>dav:/webdav/> quit<br>Connection to `127.0.0.1' closed.<br>~ $<br>~ $ cd $HOME<br>~ $<br>~ $ ssh test@127.0.0.1 -p 15022<br>test@127.0.0.1's password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~$<br>localhost:~$ sudo umount /mnt/disk1<br>[sudo] password for test:<br>localhost:~$<br>localhost:~$ exit<br>logout<br>Connection to 127.0.0.1 closed.<br>~ $<br>~ $<br></pre></td>
</tr>
</table>

---

<p><br></p>

### Reference Links


1. "Configuring LUKS: Linux Unified Key Setup": https://www.redhat.com/sysadmin/disk-encryption-luks
2. "Frequently Asked Questions Cryptsetup/LUKS": https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions
2. "Encrypted Archive with Cryptsetup": https://dashohoxha.gitlab.io/cryptsetup-encrypted-archive/ , https://github.com/dashohoxha ([dashohoxha](https://github.com/dashohoxha)), https://gitlab.com/dashohoxha
2. "Basic Guide To Encrypting Linux Partitions With LUKS": https://linuxconfig.org/basic-guide-to-encrypting-linux-partitions-with-luks , https://linuxconfig.org/how-to-use-a-file-as-a-luks-device-key , https://linuxconfig.org/how-to-use-luks-with-a-detached-header
2. "How To Linux Hard Disk Encryption With LUKS [ cryptsetup encrypt command ]": https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/
2. "How to encrypt a single Linux filesystem": https://www.redhat.com/sysadmin/encrypt-single-filesystem (LUKS)
2. "Create an encrypted file vault on Linux": https://opensource.com/article/21/4/linux-encryption (LUKS)
2. "Encrypted filesystems, loop devices, cryptsetup": http://jeromebelleman.gitlab.io/posts/filesystems/cryptsetup/ (LUKS)
2. "luks encryption with loopback file": https://gist.github.com/dbehnke/ad19ca8f1ccf80aebca5 , ([@dbehnke](https://github.com/dbehnke))
2. "An introduction to Linux filesystems": https://opensource.com/life/16/10/introduction-linux-filesystems (Linux "mount" command)
2. "mount Command in Linux | Explained": https://itslinuxfoss.com/mount-command-linux/
2. "How to Mount and Unmount Filesystems in Linux": https://www.baeldung.com/linux/mount-unmount-filesystems (Linux "fdisk" command)
2. "How to Mount and Unmount File Systems in Linux": https://linuxize.com/post/how-to-mount-and-unmount-file-systems-in-linux/  (Linux "fdisk" command)
2. "Managing partitions in Linux with fdisk": https://www.redhat.com/sysadmin/partitions-fdisk
2. "Creating and managing partitions in Linux with parted": https://www.redhat.com/sysadmin/partitions-parted
2. "Linux mount Command with Examples": https://phoenixnap.com/kb/linux-mount-command
2. "An introduction to the Linux /etc/fstab file": https://www.redhat.com/sysadmin/etc-fstab
2. "Chapter 24. Mounting file systems": https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/managing_file_systems/index
2. "Linux: Mount Disk Partition Using LABEL": https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/
2. "Linux commands: du and the options you should be using": https://www.redhat.com/sysadmin/du-command-options
2. "Hard links and soft links in Linux explained": https://www.redhat.com/sysadmin/linking-linux-explained
2. "Linux permissions: SUID, SGID, and sticky bit": https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
2. "How to audit permissions with the find command": https://www.redhat.com/sysadmin/audit-permissions-find
2. "Getting started with socat, a multipurpose relay tool for Linux": https://www.redhat.com/sysadmin/getting-started-socat
2. "Basic troubleshooting with telnet and netcat": https://www.redhat.com/sysadmin/telnet-netcat-troubleshooting (Linux "nc" command)
2. Linux "mktemp" command: https://www.gnu.org/software/coreutils/manual/coreutils.html
2. "How to use grep": https://www.redhat.com/sysadmin/how-to-use-grep
2. "Manipulating text at the command line with grep": https://www.redhat.com/sysadmin/manipulating-text-grep
2. "Manipulating text at the command line with sed": https://www.redhat.com/sysadmin/manipulating-text-sed
2. "Manipulating text with sed and grep": https://www.redhat.com/sysadmin/manipulating-text-sed-grep
2. "How to Kill a Process in Linux? Commands to Terminate": https://phoenixnap.com/kb/how-to-kill-a-process-in-linux
2. kill, ps, "Linux Command Basics: 7 commands for process management": https://www.redhat.com/sysadmin/linux-command-basics-7-commands-process-management
2. "Bash scripting: Moving from backtick operator to $ parentheses": https://www.redhat.com/sysadmin/backtick-operator-vs-parens
2. Linux ext4 filesystem: "Filesystems in the Linux kernel": https://docs.kernel.org/filesystems/index.html , https://docs.kernel.org/filesystems/ext4/index.html ("ext4 Data Structures and Algorithms"), https://www.cyberciti.biz/faq/linux-modify-partition-labels-command-to-change-diskname/ ("Linux Change Disk Label Name on EXT2 / EXT3 / EXT4 File Systems"), https://www.redhat.com/sysadmin/disk-space ("Linux sysadmins want to know: Where did my disk space go?")
2. "What sysadmins need to know about using Bash": https://www.redhat.com/sysadmin/bash-navigation
2. "10 basic Linux commands you need to know": https://www.redhat.com/sysadmin/basic-linux-commands
2. "8 fundamental Linux file-management commands for new users": https://www.redhat.com/sysadmin/linux-file-management-commands
2. "8 essential Linux file navigation commands for new users": https://www.redhat.com/sysadmin/Linux-file-navigation-commands
2. "Basic Linux commands and tools every sysadmin should know": https://clockhash.com/blog/basic-linux-commands-and-tools-every-sysadmin-should-know
2. bash: https://www.gnu.org/software/bash/manual/bash.html ("Bash Reference Manual"), https://www.redhat.com/sysadmin/linux-environment-variables ("Linux environment variable tips and tricks"), https://www.redhat.com/sysadmin/scripting-writing-text-file ("Bash scripting: How to write data to text files"), https://www.redhat.com/sysadmin/pipes-command-line-linux ("Working with pipes on the Linux command line" "here-document (heredoc)" "here-string"), https://linuxhint.com/linux-pipe-command-examples/ ("Linux Pipe Command with Examples"), https://www.redhat.com/sysadmin/linux-shell-redirection-pipelining ("How to manipulate files with shell redirection and pipelines in Linux"), https://www.redhat.com/sysadmin/redirect-shell-command-script-output ("How to redirect shell command output"), https://www.redhat.com/sysadmin/history-command ("How to manage your Linux command history"), https://www.redhat.com/sysadmin/parsing-bash-history ("Parsing Bash history in Linux"), https://tldp.org/LDP/abs/html/ ("Advanced Bash-Scripting Guide" "Here Documents"), https://wiki.bash-hackers.org
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. "The Linux man-pages project": https://www.kernel.org/doc/man-pages/ , https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/book/
2. "How to find out what a Linux command does": https://www.redhat.com/sysadmin/linux-command-documentation
2. Linux 'tree" and "ls" commands: https://www.cyberciti.biz/faq/linux-show-directory-structure-command-line/ ("Linux see directory tree structure using tree command"), https://www.redhat.com/sysadmin/ls-command-options ("Sysadmin tools: 11 ways to use the ls command in Linux"), https://www.redhat.com/sysadmin/Linux-file-navigation-commands ("8 essential Linux file navigation commands for new users")
2. "How to Use the less, more, and most Commands to Read Text Files in Linux": https://www.makeuseof.com/use-less-more-and-most-linux-commands/
2. Linux text editor "nano": https://www.redhat.com/sysadmin/getting-started-nano ("Getting started with Nano")
2. Linux text editors "vi", "vim", "ed": https://www.redhat.com/sysadmin/get-started-vi-editor ("How to get started with the Vi editor"), https://www.redhat.com/sysadmin/introduction-vi-editor ("An introduction to the vi editor"), https://www.redhat.com/sysadmin/beginners-guide-vim ("Linux basics: A beginner's guide to text editing with vim"), https://www.redhat.com/sysadmin/vim-commands ("Vim: Basic and intermediate commands"), https://www.redhat.com/sysadmin/introduction-ed-editor ("How to get started with the ed text editor")
2. Linux web browswer "links": http://links.twibright.com , http://links.twibright.com/download.php ("Documentation"), https://www.tecmint.com/command-line-web-browsers/ ("A Command Line Web Browsing with Lynx and Links Tools")
2. Linux "grep" command: https://www.redhat.com/sysadmin/find-text-files-using-grep ("Find text in files using the Linux grep command")
2. Linux "echo" command: https://phoenixnap.com/kb/echo-command-linux ("Echo Command in Linux (With Examples)"), https://www.tecmint.com/echo-command-in-linux/ ("15 Practical Examples of ‘echo’ command in Linux"), 
2. Linux "find" command: https://www.redhat.com/sysadmin/linux-find-command ("10 ways to use the Linux find command"), : https://www.redhat.com/sysadmin/find-best-friend ("When it comes to Linux system troubleshooting, find is my best friend")
2. Regular expressions (regex): https://www.redhat.com/sysadmin/introducing-regular-expressions ("Introducing regular expressions"), https://www.redhat.com/sysadmin/getting-started-regular-expressions-example ("Getting started with regular expressions: An example"), https://www.redhat.com/sysadmin/regex-grep-data-flow ("Regex and grep: Data flow and building blocks"), https://www.redhat.com/sysadmin/regular-expressions-pulling-it-all-together ("Regular expressions: Pulling it all together"), https://opensource.com/article/18/5/getting-started-regular-expressions ("Getting started with regular expressions")
2. Linux "chmod" command: https://www.redhat.com/sysadmin/linux-file-permissions-xplained ("Linux file permissions explained"), https://www.redhat.com/sysadmin/introduction-chmod ("Linux permissions: An introduction to chmod"), https://www.redhat.com/sysadmin/manage-permissions ("How to manage Linux permissions for users, groups, and others"), https://www.redhat.com/sysadmin/linux-permissions ("What sysadmins need to know about Linux permissions")
2. Linux "bc" command: https://www.gnu.org/software/bc/manual/html_mono/bc.html ("bc" "an arbitrary precision calculator language"), https://linuxconfig.org/bc ("bc command in Linux with examples"), https://web.archive.org/web/20211207113205/docstore.mik.ua/orelly/unix/upt/ch49_03.htm ("Chapter 49 Working with Numbers" "49.3 Gotchas in Base Conversion"), https://www.networkworld.com/article/3681079/converting-numbers-on-linux-among-decimal-hexadecimal-octal-and-binary.html ("Converting numbers on Linux among decimal, hexadecimal, octal, and binary"), https://www.theunixschool.com/2011/05/bc-unix-calculator.html ("bc - Unix calculator"),  https://www.real-world-systems.com/docs/bc.1.html ("bc" "arbitrary precision calculator"), http://www.physics.smu.edu/coan/linux/bc.html ("6. (Very) Brief intro to bc")
2. Linux "apt" command: https://linuxhint.com/debian_sources-list/ ("Understanding and Using Debian sources.list"), https://wiki.debian.org/SourcesList ("Configuring Apt Sources")
2. Web-based Distributed Authoring and Versioning (WebDAV), Linux command "cadaver": http://www.webdav.org , https://docs.vscentrum.be/en/latest/data/cadaver_client_access.html ("Cadaver Client Access"), https://github.com/hpcloud/swift-webdav/blob/master/doc/Cadaver.md ("Using the Cadaver WebDAV Client"). https://help.webpal.net/apis/webdav ("WebPal Resources for Editors, Admins, Collaborators and Coders" "WebDAV Interface")
2. Check the apps: https://www.virustotal.com/gui/home/url ("OPSWAT. MetaDefender Cloud"), https://metadefender.opswat.com ("VirusTotal")
2. darkhttpd: When you need a web server in a hurry.: https://github.com/emikulic/darkhttpd ([@emikulic](https://github.com/emikulic)), https://unix4lyfe.org/darkhttpd/ ("darkhttpd" "When you need a web server in a hurry.")
<p><br></p>

### Additional Installed Software
- Apk Analyzer (Martin Styk, sk.styk.martin.apkanalyzer): https://github.com/MartinStyk/AndroidApkAnalyzer (@MartinStyk), https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer
- Chmod calculator (Bonaventura Novellino, com.chmod.calc.o): https://play.google.com/store/apps/details?id=com.chmod.calc.o
- Device Info HW (Andrey Efremov, ru.andr7e.deviceinfohw): https://play.google.com/store/apps/details?id=ru.andr7e.deviceinfohw
- Files (Marc apps & software, com.marc.files): https://play.google.com/store/apps/details?id=com.marc.files
- Firefox Beta: (mozilla-mobile. org.mozilla.firefox_beta): https://github.com/mozilla-mobile/firefox-android (@mozilla-mobile), https://www.mozilla.org/en-US/firefox/browsers/mobile/
- Hash Droid (Hobby One, com.hobbyone.HashDroid): https://f-droid.org/en/packages/com.hobbyone.HashDroid/ , https://github.com/HobbyOneDroid/HashDroid (@HobbyOneDroid), https://play.google.com/store/apps/details?id=com.hobbyone.HashDroid
- Material Files (Hai Zhang, me.zhanghai.android.files): https://github.com/zhanghai/MaterialFiles (@zhanghai), https://play.google.com/store/apps/details?id=me.zhanghai.android.files
- MiX Image (Hootan Parsa, com.mixplorer.addon.image): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- MiX PDF (Hootan Parsa, com.mixplorer.addon.pdf): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- Primitive FTPd (wolpi, org.primftpd): https://github.com/wolpi/prim-ftpd (@wolpi), https://play.google.com/store/apps/details?id=org.primftpd
- RealCalc Scientific Calculator (Quartic Software, uk.co.nickfines.RealCalc): https://play.google.com/store/apps/details?id=uk.co.nickfines.RealCalc
- Simple HTTP Server (Phlox Development, com.phlox.simpleserver): https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- Termux:GUI (termux, com.termux.gui): https://github.com/termux/termux-gui (@termux), https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- USB Device Info (Alexandros Schillings, aws.apps.usbDeviceEnumerator): https://play.google.com/store/apps/details?id=aws.apps.usbDeviceEnumerator

---
---
---


<a id="NoteAfterNote-4"></a><h3 align="center">NoteAfterNote-4<br>Termux And The ext4 Filesystem, Part 4 Of 5: QEMU, A Guest Operating System, GNU GRUB Bootloader, And fdisk<br>Published: April 14, 2023<br>Link: https://gist.github.com/NoteAfterNote/0ec14839db016b6d3b905d4eda5db263</h3>


<p><br></p>

### Mobile Device Configuration
   - Rooted: No
   - Connected to any network: No
   - Operating system: 

         neofetch --stdout|grep --color=never --ignore-case 'os:'
            OS: Android 11 armv7l 
   - CPU:

         neofetch --stdout|grep --color=never --ignore-case 'cpu:'
            CPU: MT6761V/WAB (4) @ 2.001GHz
   - Display resolution: 1440x720
   - Builtin internal storage: 32 Gigabytes
   - Builtin memory: 3 Gigabytes
   - Adoptable Storage: Enabled
   - Application Binary Interface (ABI): armeabi-v7a, 32-bit
   - Linux shell: bash (Bourne Again SHell)
   - Termux wake lock: Always enable
   - Termux packages installed: qemu-system-x86-64 qemu-utils  manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate
   - "Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required": https://gist.github.com/NoteAfterNote/2558deec94bac7ec9fa58aa5ad5e9d1b , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))

<p><br></p>

Guest Operating System Installation
- Read "Alpine User Handbook": https://docs.alpinelinux.org/user-handbook/0.1a/index.html
- From https://alpinelinux.org download the "Virtual" "x86_64" files: https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso , https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso.sha256
- Alpine Linux Wiki: https://wiki.alpinelinux.org
- "Setting up disks manually": https://wiki.alpinelinux.org/wiki/Setting_up_disks_manually
- "Bootloaders": https://wiki.alpinelinux.org/wiki/Bootloaders
- "GNU GRUB": https://www.gnu.org/software/grub/
- "GNU GRUB Manual 2.06": https://www.gnu.org/software/grub/manual/grub/grub.html
- "Production Web server: Lighttpd": https://wiki.alpinelinux.org/wiki/Production_Web_server:_Lighttpd
- "Lighttpd": https://wiki.alpinelinux.org/wiki/Lighttpd
- Lighttpd: https://redmine.lighttpd.net/projects/lighttpd , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_webdav , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_auth
- "htdigest - manage user files for digest authentication": https://httpd.apache.org/docs/2.4/programs/htdigest.html
- "htpasswd - Manage user files for basic authentication": https://httpd.apache.org/docs/2.4/programs/htpasswd.html
- "Termux And The ext4 Filesystem, Part 3 Of 5: QEMU, A Guest Operating System, LUKS Encryption, lighttpd, WebDAV": https://gist.github.com/NoteAfterNote/cabd411777f2ad5ae57d3d98c576471c , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))
<p><br></p>


Do Know
- ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
- Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
- Reset a Termux terminal session at anytime, very useful when lines are truncated while booting: https://wiki.termux.com/wiki/User_Interface ("create new terminal sessions", "specify a session title", "Resetting the terminal"), see https://user-images.githubusercontent.com/21236430/126444437-7570cdcb-e825-4970-97ff-71f41e426b0f.jpg in https://github.com/termux/termux-app/issues/2184#issuecomment-883939230 ("Feature request: termux transcript #2184" "Gameye98 commented on Jul 21, 2021" )

Introduction To Linux System Administration
- Read "4 System Administration": https://tldp.org/LDP/gs/node6.html
- Read "Chapter 1. Getting Started with Linux": https://www.oreilly.com/library/view/practical-linux-system/9781098109028/ch01.html
- Read "Reboot Linux System Command": https://www.cyberciti.biz/faq/howto-reboot-linux/
- "Linux superuser access, explained": https://www.redhat.com/sysadmin/linux-superuser-access
- "Why Do We Use su – and Not Just su?": https://www.baeldung.com/linux/su-command-options
- "Linux command line basics: sudo": https://www.redhat.com/sysadmin/sudo
- "Exploring the differences between sudo and su commands in Linux": https://www.redhat.com/sysadmin/difference-between-sudo-su
- "Using sudo to delegate permissions in Linux": https://www.redhat.com/sysadmin/using-sudo-delegate
- "Real sysadmins don't sudo": https://www.redhat.com/sysadmin/sysadmins-dont-sudo
- "Linux sysadmin basics: User account management": https://www.redhat.com/sysadmin/linux-user-account-management
- "How to create, delete, and modify groups in Linux": https://www.redhat.com/sysadmin/linux-groups (Linux "id" command)
- "Linux sysadmin basics: User account management with UIDs and GIDs": https://www.redhat.com/sysadmin/user-account-gid-uid
- "Managing local group accounts in Linux": https://www.redhat.com/sysadmin/local-group-accounts
- "How to use a command line random password generator PWGEN on Linux": https://linuxconfig.org/how-to-use-a-command-line-random-password-generator-pwgen-on-linux

<p><br></p>

Network Port Numbers
- "Recommendations on Using Assigned Transport Port Numbers": https://www.rfc-editor.org/rfc/rfc7605.html
- "Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry": https://www.rfc-editor.org/rfc/rfc6335 ("the Dynamic Ports, also known as the Private or Ephemeral Ports, from 49152-65535 (never assigned)")
- Linux "shuf" command": https://www.gnu.org/software/coreutils/manual/html_node/shuf-invocation.html
   ````
   shuf --input-range=49152-65535  --head-count=1  --random-source=/dev/urandom --repeat

   shuf -i 49152-65535  -n 1 --random-source=/dev/urandom -r
   ````

<p><br></p>

4GB - 1 = (4*(1\*1024\*1024\*1024)) - 1 = (2^32) - 1 = 4294967295 bytes
- "Working with File Systems": http://web.archive.org/web/20130423054811/technet.microsoft.com/en-us/library/bb457112.aspx ("4 GB minus 1 byte"), "Working with File Systems": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb457112(v=technet.10)
- "How FAT Works": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776720(v=ws.10)

<p><br></p>

QEMU: https://www.qemu.org , https://github.com/qemu/qemu ([@qemu](https://github.com/qemu)), https://www.qemu.org/docs/master/ , https://wiki.qemu.org , https://github.com/qemu/qemu/tree/master/docs
- "Device Emulation": https://www.qemu.org/docs/master/system/device-emulation.html ("Common Terms" "Device Front End" "Device Back End"), https://qemu.readthedocs.io/en/latest/system/device-emulation.html
- "QEMU User Documentation": https://www.qemu.org/docs/master/system/qemu-manpage.html , https://qemu.readthedocs.io/en/latest/system/qemu-manpage.html
- "QEMU Documentation": https://qemu.readthedocs.io/_/downloads/en/latest/pdf/
- https://github.com/qemu/qemu/blob/master/qemu-options.hx
- "QEMU disk image utility": https://www.qemu.org/docs/master/tools/qemu-img.html ("qemu-img create"), https://qemu.readthedocs.io/en/latest/tools/qemu-img.html 


qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -monitor unix:$SOCKET_FILENAME,server,wait=off -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR
- "Invocation": https://www.qemu.org/docs/master/system/invocation.html , https://qemu.readthedocs.io/en/latest/system/invocation.html
- "Managing device boot order with bootindex properties": https://www.qemu.org/docs/master/system/bootindex.html , https://qemu.readthedocs.io/en/latest/system/bootindex.html
- "Network emulation": https://www.qemu.org/docs/master/system/devices/net.html ("Using the user mode network stack" "-net user" "The QEMU VM behaves as if it was behind a firewall which blocks all incoming connections."), 
- "Documentation/Networking": https://wiki.qemu.org/Documentation/Networking ("hostfwd")
- "Documentation/9psetup": https://wiki.qemu.org/Documentation/9psetup ("-virtfs"), https://wiki.qemu.org/Documentation/9p
https://wiki.qemu.org/Features/VirtIORNG ("virtio-rng-pci")
- "QEMU command-line: behavior of ‘-serial stdio’ vs. ‘-serial mon:stdio’": https://kashyapc.wordpress.com/2016/02/11/qemu-command-line-behavior-of-serial-stdio-vs-serial-monstdio/ ("-serial mon:stdio")


"QEMU Monitor": https://www.qemu.org/docs/master/system/monitor.html , https://qemu.readthedocs.io/en/latest/system/monitor.html
- "Keys in the character backend multiplexer": https://www.qemu.org/docs/master/system/mux-chardev.html ("Ctrl-a h", "Ctrl-a t", "Ctrl-a c", "Ctrl-a x"), https://qemu.readthedocs.io/en/latest/system/mux-chardev.html
- "Introduction": https://www.qemu.org/docs/master/system/introduction.html ("QEMU provides a number of management interfaces including a line based Human Monitor Protocol (HMP) that allows you to dynamically add and remove devices as well as introspect the system state.")
- "Security": https://www.qemu.org/docs/master/system/security.html ("Monitor console (QMP and HMP)", "The general recommendation is that the monitor console should be exposed over a UNIX domain socket backend to the local host only."), https://qemu.readthedocs.io/en/latest/system/security.html
- "QemuDiskHotplug": https://wiki.ubuntu.com/QemuDiskHotplug and
- "QEMU Human Monitor Interface, Example Usage": https://web.archive.org/web/20180104171638/nairobi-embedded.org/qemu_monitor_console.html ("Nographic Mode")

QEMU HMP Monitor Commands
- Hotplugging disks, if a disk is mounted in the operating system, unmount it before a "device_del"

   ````
   info block

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk1.img,format=raw,id=hd1

   device_add virtio-blk-pci,drive=hd1,id=virt1

   ```` 

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/disk2.ext,format=raw,id=drive2 

   device_add virtio-blk-pci,drive=drive2,id=virtual2

   ````

   ```` 
   drive_add 0 if=none,file=/storage/emulated/0/Downloads/50gb.ext,format=raw,id=hd3 

   device_add virtio-blk-pci,drive=hd3,id=virtual3

   ````

   ```` 
   device_del virtual3

   device_del virt1

   device_del virtual2

   ````
- QEMU firewall network ports

   ````
   info usernet

   hostfwd_add ::2049-:2049

   info usernet

   hostfwd_remove ::2049

   info usernet

   ````

- Communicate with QEMU through a socket

   ```` 
   echo 'info block' | nc -UN $SOCKET_FILENAME

   ```` 

<p><br></p>

---

<p><br></p>

<a id=qemu-linux-console></a>
### Termux Session: [QEMU-Linux-Console](#termux-session-for-qemu-linux-console)

````
export NINE_P_DIR=/storage/emulated/0/Download/qemu-test

cd $NINE_P_DIR
sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256
cd $HOME
pwd
export ISO=$NINE_P_DIR/alpine-virt-3.17.3-x86_64.iso

dd if=/dev/urandom of=$NINE_P_DIR/disk3-1gb.img bs=1M count=1024
fdisk $NINE_P_DIR/disk3-1gb.img


export VMDISK=$NINE_P_DIR/vm-template-grub.raw
qemu-img create -f raw -o preallocation=full $VMDISK 6G


#
# For the guest operating system 9p setup: Save the Group ID (GID)
#
export GID_NINE_P_DIR=$(stat $NINE_P_DIR|grep -i gid)
echo $GID_NINE_P_DIR

#
# Bootup may take some time. Watch the "QEMU Linux Console"
#
# "QEMU Monitor" communication is done using "Ctrl-a c"
#
# Still in the Termux home directory
#
pwd

qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR

#
# Install from the ISO: no password, login as 'root'
# 50gb.ext: v3.17/main/x86_64 repository
#           v3.17/community/x86_64 repository
#           v3.17/releases (selected files)
#
blkid
df -h
mkdir /root/repo
mkdir /root/backup
cat /etc/apk/repositories

cp -pi /etc/apk/repositories /root/backup
echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories

#   mount --help  
#   mount the disk read-only
#   mount LABEL=50gb -o ro,remount /root/repo
#   mount LABEL=50gb -o rw,remount /root/repo
mount -r LABEL=50gb /root/repo
mount|egrep repo


apk update
#
# Note for the next installation: Do not install
# "inetutils-ftp"
#
apk add nano inetutils-ftp cfdisk util-linux e2fsprogs e2fsprogs-extra  grub grub-bios


lsblk
blkid
#
# grep -E 'SWAP_SIZE|BOOT_SIZE|ROOT_SIZE' /sbin/setup-disk
#   Sizes are in megabytes
#
# Need space for the "/tmp" partition
#
export BOOTLOADER=grub
export SWAP_SIZE=1024
export BOOT_SIZE=500
export ROOT_SIZE=3644
export EDITOR=nano
export KERNELOPTS="console=tty0 console=ttyS0,115200n8"

env
#
# During setup add a username.
# During setup if a pager is presented, type 'h' and 'q'
#
setup-alpine 
umount /root/repo

#
# Setup the "/tmp" partition
#
# One: /mnt/etc/fstab modified for "/tmp"
mount /dev/vdb3 /mnt
cp -piv /mnt/etc/fstab /root/backup
cat /mnt/etc/fstab
sed -i -e 's/^tmpfs/# tmpfs/' /mnt/etc/fstab
echo 'LABEL=tmp-partition /tmp ext4 defaults 1 2' >> /mnt/etc/fstab
cat /mnt/etc/fstab
umount /mnt

# Two: make the /tmp partition with fdisk
fdisk /dev/vdb

# Three: mkfs.ext4 followed by "poweroff" 
mkfs.ext4 -L tmp-partition /dev/vdb4

# Poweroff the server
poweroff

# Reset the Termux terminal if necessary: "tput reset"
# at the Termux command line or select the Termux session
# reset option.
#
# Booting from the ISO is finished. Remove
#   -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1
#   -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1
#
# and press the Enter/Return key.
#   

qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=1  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR 


# If the lines displayed as while booting are truncated use
# the Termux session reset option as the server continues to boot.
#
# Toggle the timestamps: ctrl-a t
# 

#
# When the server boots up login as root.
# 

cat /etc/os-release
uname -a
mkdir /root/backup
mkdir /mnt/repo

lsblk
blkid
df -ahT
df -ahT|grep tmp

cp -pi /etc/apk/repositories /root/backup
cat /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/main' >> /etc/apk/repositories
echo '/mnt/repo/alpine/v3.17/community' >> /etc/apk/repositories
cat /etc/apk/repositories
mount -r LABEL=50gb /mnt/repo


cat /etc/modules ; cp -pi /etc/modules /root/backup
echo fuse >> /etc/modules ; cat /etc/modules

#
# Install the packages
#
apk update
date

apk add linux-lts linux-virt vim cryptsetup asciinema neofetch xca polkit  screen  rpm cifs-utils device-mapper rng-tools qt5-qtwebglplugin inetutils-telnet perl hdparm fsarchiver progress pv davfs2 libcdio-tools lftp-doc lftp pssh mutt neomutt alpine ncftp sshfs samba apache2 apache2-doc apache2-webdav apache2-ctl apache2-utils alpine-sdk build-base apk-tools alpine-conf busybox libpwquality fakeroot syslinux xorriso mtools dosfstools grub-efi make git sudo lynx links nodejs npm dhcp-server-vanilla ccache ccache-doc udisks2 udisks2-doc libarchive-tools libarchive-doc cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc gcc abuild binutils binutils-doc gcc-doc py3-pip pandoc iproute2 util-linux pciutils usbutils coreutils binutils findutils grep bash bash-doc utmps pass pass-otp darkhttpd vsftpd vsftpd-doc zstd pwgen easy-rsa  markdown expect sshpass keepassxc gzip rpm xz bzip2 gawk bc diffutils psmisc procps shadow util-linux-bash-completion util-linux-login mount umount netcat-openbsd nmap nmap-nping nmap-nselibs nmap-scripts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix gptfdisk sgdisk parted grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosfstools texinfo e2fsprogs e2fsprogs-extra  mkinitfs haveged f2fs-tools jfsutils ntfs-3g ntfs-3g-progs xfsprogs cpio whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils fuse-exfat-doc nfs-utils ncurses sharutils mandoc man-pages mandoc-apropos docs cmd:rsvg-convert iptables ip6tables perl-net-ssleay stress-ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plugins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vifm-zsh-completion  vifm-bash-completion  fish  zsh udisks2-bash-completion ncdu gnome-disk-utility zim chezdav lighttpd lighttpd-doc lighttpd-mod_webdav lighttpd-mod_auth grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsql apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate cadaver

date

cat /boot/grub/grub.cfg


cp -iv /etc/default/grub /root/backup
cp -iv /etc/update-extlinux.conf /root/backup

cat /etc/default/grub

sed -i -e 's/^GRUB_TIMEOUT/# GRUB_TIMEOUT/' /etc/default/grub

sed -i -e 's/^GRUB_DISABLE_SUBMENU/# GRUB_DISABLE_SUBMENU/' /etc/default/grub

sed -i -e 's/^GRUB_CMDLINE_LINUX_DEFAULT/# GRUB_CMDLINE_LINUX_DEFAULT/' /etc/default/grub

echo 'GRUB_TERMINAL="serial console"' >> /etc/default/grub

echo 'GRUB_SERIAL_COMMAND="serial --speed=115200"' >> /etc/default/grub

echo 'GRUB_TIMEOUT=-1' >> /etc/default/grub
echo 'GRUB_DISABLE_SUBMENU=n' >> /etc/default/grub
cat /etc/default/grub

cat /etc/update-extlinux.conf

# nano --linenumbers /etc/update-extlinux.conf

sed -i -e 's/^default=lts/default=virt/' /etc/update-extlinux.conf

cat /etc/update-extlinux.conf|grep -E '^default|^modules'

grep GRUB_CMDLINE_LINUX_DEFAULT /etc/default/grub

sed -i -e 's/default_kernel_opts=quiet/default_kernel_opts="console=tty0 console=ttyS0,115200n8 rootfstype=ext4"/' /etc/update-extlinux.conf


grep -E '^default|^modules' /etc/update-extlinux.conf

#
# Update the settings
#
grub-mkconfig -o /boot/grub/grub.cfg

cat /boot/grub/grub.cfg

#
# Change the shell
#
echo $SHELL
chsh -s /bin/bash root
chsh -s /bin/bash test


mkdir /mnt/9p-host
mkdir /mnt/disk1

export SUDO_EDITOR=nano
export EDITOR=nano

grep wheel /etc/sudoers

## Uncomment the wheel line
# Use the command: "sudoedit /etc/sudoers"
grep wheel /etc/sudoers

#
# Setup lighttpd for WebDAV
#
mkdir -p /var/www/localhost/htdocs /var/log/lighttpd /var/lib/lighttpd

chown  -R lighttpd:lighttpd /var/log/lighttpd /var/lib/lighttpd /var/www/localhost/htdocs

ls -al  /var/www/localhost/htdocs

#
# Create an empty webdav-htpasswd-passwd file
#
touch /etc/lighttpd/webdav-htpasswd-passwd

chown root:lighttpd /etc/lighttpd/webdav-htpasswd-passwd

ls -l /etc/lighttpd/webdav-htpasswd-passwd

stat /etc/lighttpd/webdav-htpasswd-passwd

# 640 (octal) means u=rw,g=r,o-rwx
chmod 640 /etc/lighttpd/webdav-htpasswd-passwd

ls -l /etc/lighttpd/webdav-htpasswd-passwd

stat /etc/lighttpd/webdav-htpasswd-passwd


# Add WebDAV username
htpasswd -m /etc/lighttpd/webdav-htpasswd-passwd test1


cp -pi /etc/lighttpd/webdav.conf /root/backup

#
# Use "here-document" to create /etc/lighttpd/webdav.conf 
#
cat << 'END-OF-WEBDAV-CONF' > /etc/lighttpd/webdav.conf
server.port = 15081
server.upload-dirs = ( "/tmp" )
server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_file")
alias.url = ( "/webdav" => "/mnt/disk1" )
$HTTP["url"] =~ "^/webdav($|/)" {
    webdav.activate = "enable"
    webdav.is-readonly = "disable"
    webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"
    auth.backend = "htpasswd"
    auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-passwd"
    auth.require  = ("" => ("method" => "basic","realm" => "realm-webdav","require" => "valid-user"))                       
  }
END-OF-WEBDAV-CONF

cat /etc/lighttpd/webdav.conf

cp -pi /etc/lighttpd/lighttpd.conf /root/backup

echo 'include "webdav.conf"' >> /etc/lighttpd/lighttpd.conf
#
# Check the /etc/lighttpd/lighttpd.conf configuration file
#   lighttpd -tt -f /etc/lighttpd/webdav.conf

lighttpd -tt -f /etc/lighttpd/lighttpd.conf


# Services automatically started
rc-update add lighttpd default


passwd --delete --expire root
passwd --delete --expire test
ls -al /root
rm -f /etc/ssh/ssh*key
rm -i /root/.lesshst
rm -i /root/.ash_history
rm -ir /root/backup
poweroff

#
# Back at the Termux command line
#
cd $HOME
pwd
env

cp -iv $VMDISK $NINE_P_DIR/vm-linux-grub.raw

export VMDISK=$NINE_P_DIR/vm-linux-grub.raw

#
# Boot from vm-linux-grub.raw
#
# Toggle the console timestamps: ctrl-a t
#
qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=1  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR 

# After the server boots up login as root
#
pwd
echo $SHELL
ls -la

su - test
pwd
echo $SHELL
ls -la
exit

pwd

blkid
df -ahT
mkdir /root/repo
mkdir /root/backup
cat /etc/apk/repositories


mount -r LABEL=50gb /root/repo
mount

#
# NINE_P_DIR=/storage/emulated/0/Download/qemu-test
#
# QEMU 9p: -virtfs local,security_model=none,
#          id=host,mount_tag=host,
#          path=$NINE_P_DIR
#
# For the Linux mount command: "mount_tag=host"
#
# Get GID_NINE_P_DIR
#
groupadd --gid GID_NINE_P_DIR_HERE nine-p-host 
groupmod --append --users test nine-p-host

mount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /mnt/9p-host

mount
df -hT
ls -lRa /mnt/9p-host

su - test
touch /mnt/9p-host/test.txt
ls -lRa /mnt/9p-host
exit


#
# "QEMU Monitor" commands using "Ctrl-a c" (on/off toggle)
#    info usernet
#    info block
#    drive_add 0 if=none,file=/storage/emulated/0/Download/qemu-test/disk3-1gb.img,format=raw,id=disk3
#    device_add virtio-blk-pci,drive=disk3,id=virt1
#    info block


blkid
lsblk

grep -i virt /var/log/messages | tail -10
dmesg | grep -i virt | tail -5

fdisk -l /dev/vdc

mkfs.ext4 -m 0 -L disk3-ext4 /dev/vdc1
mkfs.vfat -F 32 -n DISK3-VFAT /dev/vdc2
mkfs.exfat -n disk3-exfat /dev/vdc3
mkfs.ntfs --quick --label disk3-ntfs /dev/vdc4

lsblk
blkid|grep vdc

#
# Logout
#
exit

#
# "QEMU Monitor" commands using "Ctrl-a c" 
#    system_powerdown
#

pwd

````

<p><br></p>

<a id="termux-session-for-qemu-linux-console"></a>
<table>
<tr>
<th align="left">Termux session for <a href="#qemu-linux-console">QEMU-Linux-Console</a></th>
</tr>
<tr>
<td align="left" valign="top"><pre>Welcome to Termux!<br><br>Community forum: https://termux.com/community<br>Gitter chat:     https://gitter.im/termux/termux<br>IRC channel:     #termux on libera.chat<br><br>Working with packages:<br><br> * Search packages:   pkg search <query><br> * Install a package: pkg install <package><br> * Upgrade packages:  pkg upgrade<br><br>Subscribing to additional repositories:<br><br> * Root:     pkg install root-repo<br> * X11:      pkg install x11-repo<br><br>Report issues at https://termux.com/issues<br><br>~ $ export NINE_P_DIR=/storage/emulated/0/Download/qemu-test<br>~ $<br>~ $ cd $NINE_P_DIR<br>.../Download/qemu-test $<br>.../Download/qemu-test $ sha256sum -c alpine-virt-3.17.3-x86_64.iso.sha256<br>alpine-virt-3.17.3-x86_64.iso: OK<br>.../Download/qemu-test $<br>.../Download/qemu-test $ cd $HOME<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ export ISO=$NINE_P_DIR/alpine-virt-3.17.3-x86_64.iso<br>~ $<br>~ $ dd if=/dev/urandom of=$NINE_P_DIR/disk3-1gb.img bs=1M count=1024<br>1024+0 records in<br>1024+0 records out<br>1073741824 bytes (1.1 GB, 1.0 GiB) copied, 43.5356 s, 24.7 MB/s<br>~ $<br>~ $ fdisk $NINE_P_DIR/disk3-1gb.img<br><br>Welcome to fdisk (util-linux 2.38.1).<br>Changes will remain in memory only, until you decide to write them.<br>Be careful before using the write command.<br><br>Device does not contain a recognized partition table.<br>Created a new DOS disklabel with disk identifier 0x67aee5a3.<br><br>Command (m for help): p<br>Disk /storage/emulated/0/Download/qemu-test/disk3-1gb.img: 1 GiB, 1073741824 bytes, 2097152 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x67aee5a3<br><br>Command (m for help): n<br>Partition type<br>   p   primary (0 primary, 0 extended, 4 free)<br>   e   extended (container for logical partitions)<br>Select (default p):<br><br>Using default response p.<br>Partition number (1-4, default 1):<br>First sector (2048-2097151, default 2048):<br>Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-2097151, default 2097151): +250M<br><br>Created a new partition 1 of type 'Linux' and of size 250 MiB.<br><br>Command (m for help): p<br>Disk /storage/emulated/0/Download/qemu-test/disk3-1gb.img: 1 GiB, 1073741824 bytes, 2097152 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x67aee5a3<br><br>Device                                                Boot Start    End Sectors  Size Id Type<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img1       2048 514047  512000  250M 83 Linu<br><br>Command (m for help): n<br>Partition type<br>   p   primary (1 primary, 0 extended, 3 free)<br>   e   extended (container for logical partitions)<br>Select (default p):<br><br>Using default response p.<br>Partition number (2-4, default 2):<br>First sector (514048-2097151, default 514048):<br>Last sector, +/-sectors or +/-size{K,M,G,T,P} (514048-2097151, default 2097151): +250M<br><br>Created a new partition 2 of type 'Linux' and of size 250 MiB.<br><br>Command (m for help): m<br><br>Help:<br><br>  DOS (MBR)<br>   a   toggle a bootable flag<br>   b   edit nested BSD disklabel<br>   c   toggle the dos compatibility flag<br><br>  Generic<br>   d   delete a partition<br>   F   list free unpartitioned space<br>   l   list known partition types<br>   n   add a new partition<br>   p   print the partition table<br>   t   change a partition type<br>   v   verify the partition table<br>   i   print information about a partition<br><br>  Misc<br>   m   print this menu<br>   u   change display/entry units<br>   x   extra functionality (experts only)<br><br>  Script<br>   I   load disk layout from sfdisk script file<br>   O   dump disk layout to sfdisk script file<br><br>  Save & Exit<br>   w   write table to disk and exit<br>   q   quit without saving changes<br><br>  Create a new label<br>   g   create a new empty GPT partition table<br>   G   create a new empty SGI (IRIX) partition table<br>   o   create a new empty DOS partition table<br>   s   create a new empty Sun partition table<br><br><br>Command (m for help): t<br>Partition number (1,2, default 2):<br>Hex code or alias (type L to list all): L<br><br>00 Empty            27 Hidden NTFS Win  82 Linux swap / So  c1 DRDOS/sec (FAT-<br>01 FAT12            39 Plan 9           83 Linux            c4 DRDOS/sec (FAT-<br>02 XENIX root       3c PartitionMagic   84 OS/2 hidden or   c6 DRDOS/sec (FAT-<br>03 XENIX usr        40 Venix 80286      85 Linux extended   c7 Syrinx <br>04 FAT16 <32M       41 PPC PReP Boot    86 NTFS volume set  da Non-FS data<br>05 Extended         42 SFS              87 NTFS volume set  db CP/M / CTOS / .<br>06 FAT16            4d QNX4.x           88 Linux plaintext  de Dell Utility<br>07 HPFS/NTFS/exFAT  4e QNX4.x 2nd part  8e Linux LVM        df BootIt <br>08 AIX              4f QNX4.x 3rd part  93 Amoeba           e1 DOS access<br>09 AIX bootable     50 OnTrack DM       94 Amoeba BBT       e3 DOS R/O<br>0a OS/2 Boot Manag  51 OnTrack DM6 Aux  9f BSD/OS           e4 SpeedStor<br>0b W95 FAT32        52 CP/M             a0 IBM Thinkpad hi  ea Linux extended<br>0c W95 FAT32 (LBA)  53 OnTrack DM6 Aux  a5 FreeBSD          eb BeOS fs<br>0e W95 FAT16 (LBA)  54 OnTrackDM6       a6 OpenBSD          ee GPT    <br>0f W95 Ext'd (LBA)  55 EZ-Drive         a7 NeXTSTEP         ef EFI (FAT-12/16/<br>10 OPUS             56 Golden Bow       a8 Darwin UFS       f0 Linux/PA-RISC b<br>11 Hidden FAT12     5c Priam Edisk      a9 NetBSD           f1 SpeedStor<br>12 Compaq diagnost  61 SpeedStor        ab Darwin boot      f4 SpeedStor<br>14 Hidden FAT16 <3  63 GNU HURD or Sys  af HFS / HFS+       f2 DOS secondary<br>16 Hidden FAT16     64 Novell Netware   b7 BSDI fs          f8 EBBR protective<br>17 Hidden HPFS/NTF  65 Novell Netware   b8 BSDI swap        fb VMware VMFS<br>18 AST SmartSleep   70 DiskSecure Mult  bb Boot Wizard hid  fc VMware VMKCORE<br>1b Hidden W95 FAT3  75 PC/IX            bc Acronis FAT32 L  fd Linux raid auto<br>1c Hidden W95 FAT3  80 Old Minix        be Solaris boot     fe LANstep<br>1e Hidden W95 FAT1  81 Minix / old Lin  bf Solaris          ff BBT    <br>24 NEC DOS<br><br>Aliases:<br>   linux          - 83<br>   swap           - 82<br>   extended       - 05<br>   uefi           - EF<br>   raid           - FD<br>   lvm            - 8E<br>   linuxex        - 85<br>Hex code or alias (type L to list all): c<br><br>Changed type of partition 'Linux' to 'W95 FAT32 (LBA)'.<br><br>Command (m for help): n<br>Partition type<br>   p   primary (2 primary, 0 extended, 2 free)<br>   e   extended (container for logical partitions)<br>Select (default p):<br><br>Using default response p.<br>Partition number (3,4, default 3):<br>First sector (1026048-2097151, default 1026048):<br>Last sector, +/-sectors or +/-size{K,M,G,T,P} (1026048-2097151, default 2097151): +250M<br><br>Created a new partition 3 of type 'Linux' and of size 250 MiB.<br><br>Command (m for help): t<br>Partition number (1-3, default 3): 7<br>Value out of range.<br>Partition number (1-3, default 3): 3<br>Hex code or alias (type L to list all): 7<br><br>Changed type of partition 'Linux' to 'HPFS/NTFS/exFAT'.<br><br>Command (m for help): p<br>Disk /storage/emulated/0/Download/qemu-test/disk3-1gb.img: 1 GiB, 1073741824 bytes, 2097152 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x67aee5a3<br><br>Device                                                Boot   Start     End Sectors  Size Id Type<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img1         2048  514047  512000  250M 83 Linu<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img2       514048 1026047  512000  250M  c W95<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img3      1026048 1538047  512000  250M  7 HPFS<br><br>Command (m for help): n<br>Partition type<br>   p   primary (3 primary, 0 extended, 1 free)<br>   e   extended (container for logical partitions)<br>Select (default e): p<br><br>Selected partition 4<br>First sector (1538048-2097151, default 1538048):<br>Last sector, +/-sectors or +/-size{K,M,G,T,P} (1538048-2097151, default 2097151):<br><br>Created a new partition 4 of type 'Linux' and of size 273 MiB.<br><br>Command (m for help): t<br>Partition number (1-4, default 4):<br>Hex code or alias (type L to list all): 7<br><br>Changed type of partition 'Linux' to 'HPFS/NTFS/exFAT'.<br><br>Command (m for help): p<br>Disk /storage/emulated/0/Download/qemu-test/disk3-1gb.img: 1 GiB, 1073741824 bytes, 2097152 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x67aee5a3<br><br>Device                                                Boot   Start     End Sectors  Size Id Type<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img1         2048  514047  512000  250M 83 Linu<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img2       514048 1026047  512000  250M  c W95<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img3      1026048 1538047  512000  250M  7 HPFS<br>/storage/emulated/0/Download/qemu-test/disk3-1gb.img4      1538048 2097151  559104  273M  7 HPFS<br><br>Command (m for help): w<br>The partition table has been altered.<br>Syncing disks.<br><br>~ $ export VMDISK=$NINE_P_DIR/vm-template-grub.raw<br>~ $<br>~ $ qemu-img create -f raw -o preallocation=full $VMDISK 6G<br>Formatting '/storage/emulated/0/Download/qemu-test/vm-template-grub.raw', fmt=raw size=6442450944 preallocation=full<br>~ $<br>~ $ export GID_NINE_P_DIR=$(stat $NINE_P_DIR|grep -i gid)<br>~ $<br>~ $ export GID_NINE_P_DIR=$(stat $NINE_P_DIR|grep -i gid)<br>~ $<br>~ $ echo $NINE_P_DIR<br>/storage/emulated/0/Download/qemu-test<br>~ $<br>~ $ echo $GID_NINE_P_DIR<br>Access: (0770/drwxrwx---) Uid: ( 0/ root) Gid: ( 9997/everybody)<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$ISO,media=cdrom,readonly=on,format=raw,id=drive1 -device virtio-blk-pci,drive=drive1,id=virtblk1,bootindex=1  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=2  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR<br><br><br>OpenRC 0.45.2 is starting up Linux 5.15.104-0-virt (x86_64)<br><br> * /proc is already mounted                                            * Mounting /run ... * /run/openrc: creating directory                 * /run/lock: creating directory                                       * /run/lock: correcting owner                                         * Caching service dependencies ... [ ok ]                             * Remounting devtmpfs on /dev ... [ ok ]                              * Mounting /dev/mqueue ... [ ok ]                                     * Mounting modloop  ... * Verifying modloop                           [ ok ]                                                                * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]                                * Mounting persistent storage (pstore) filesystem ... [ ok ]<br> * Starting busybox mdev ... [ ok ]<br> * Scanning hardware for mdev ... [ ok ]<br> * Loading hardware drivers ... [ ok ]<br> * Loading modules ... [ ok ]                                          * Setting system clock using the hardware clock [UTC] ... [ ok ]      * Checking local filesystems  ... [ ok ]                              * Remounting filesystems ... [ ok ]                                   * Mounting local filesystems ... [ ok ]                               * Configuring kernel parameters ... [ ok ]                            * Migrating /var/lock to /run/lock ... [ ok ]                         * Creating user login records ... [ ok ]                              * Cleaning /tmp directory ... [ ok ]                                  * Setting hostname ... [ ok ]<br> * Starting busybox syslog ... [ ok ]<br> * Starting firstboot ... [ ok ]<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.104-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~#<br>localhost:~# blkid<br>/dev/loop/0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" TYPE="ext4"<br>/dev/vda2: TYPE="vfat"<br>/dev/vda1: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/vda: LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660"<br>/dev/loop0: TYPE="squashfs"<br>localhost:~#<br>localhost:~# df -h<br>Filesystem                Size      Used Available Use% Mounted on<br>devtmpfs                 10.0M         0     10.0M   0% /dev<br>shm                     491.6M         0    491.6M   0% /dev/shm<br>/dev/vda                 49.0M     49.0M         0 100% /media/vda<br>tmpfs                   491.6M     10.4M    481.2M   2% /<br>tmpfs                   196.6M     44.0K    196.6M   0% /run<br>/dev/loop0               14.1M     14.1M         0 100% /.modloop<br>localhost:~#<br>localhost:~# mkdir /root/repo<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>localhost:~#<br>localhost:~# cp -pi /etc/apk/repositories /root/backup<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/main' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# echo '/root/repo/alpine/v3.17/community' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>/media/vda/apks<br>/root/repo/alpine/v3.17/main<br>/root/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /root/repo<br>localhost:~#<br>localhost:~# apk update<br>3.17.3 [/media/vda/apks]<br>v3.17.3-51-gb3e182d1e6a [/root/repo/alpine/v3.17/main]<br>v3.17.3-50-ga35f8409359 [/root/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~#<br>localhost:~# apk add nano inetutils-ftp cfdisk util-linux e2fsprogs e2fsprogs-ex<br>tra  grub grub-bios<br>(1/53) Installing libblkid (2.38.1-r1)<br>(2/53) Installing libuuid (2.38.1-r1)<br>(3/53) Installing libfdisk (2.38.1-r1)<br>(4/53) Installing libmount (2.38.1-r1)<br>(5/53) Installing ncurses-terminfo-base (6.3_p20221119-r0)<br>(6/53) Installing ncurses-libs (6.3_p20221119-r0)<br>(7/53) Installing libsmartcols (2.38.1-r1)<br>(8/53) Installing cfdisk (2.38.1-r1)<br>(9/53) Installing libcom_err (1.46.6-r0)<br>(10/53) Installing e2fsprogs-libs (1.46.6-r0)<br>(11/53) Installing e2fsprogs (1.46.6-r0)<br>(12/53) Installing e2fsprogs-extra (1.46.6-r0)<br>(13/53) Installing lddtree (1.26-r3)<br>(14/53) Installing xz-libs (5.2.9-r0)<br>(15/53) Installing zstd-libs (1.5.5-r0)<br>(16/53) Installing kmod (30-r1)<br>(17/53) Installing kmod-openrc (30-r1)<br>(18/53) Installing argon2-libs (20190702-r2)<br>(19/53) Installing device-mapper-libs (2.03.17-r1)<br>(20/53) Installing json-c (0.16-r2)<br>(21/53) Installing cryptsetup-libs (2.5.0-r2)<br>(22/53) Installing kmod-libs (30-r1)<br>(23/53) Installing mkinitfs (3.7.0-r1)<br>Executing mkinitfs-3.7.0-r1.post-install<br>(24/53) Installing grub (2.06-r7)<br>(25/53) Installing grub-bios (2.06-r7)<br>(26/53) Installing readline (8.2.0-r0)<br>(27/53) Installing inetutils-ftp (2.4-r0)<br>(28/53) Installing nano (7.0-r0)<br>(29/53) Installing util-linux (2.38.1-r1)<br>(30/53) Installing util-linux-misc (2.38.1-r1)<br>(31/53) Installing libeconf (0.4.7-r0)<br>(32/53) Installing linux-pam (1.5.2-r1)<br>(33/53) Installing runuser (2.38.1-r1)<br>(34/53) Installing mount (2.38.1-r1)<br>(35/53) Installing losetup (2.38.1-r1)<br>(36/53) Installing hexdump (2.38.1-r1)<br>(37/53) Installing uuidgen (2.38.1-r1)<br>(38/53) Installing blkid (2.38.1-r1)<br>(39/53) Installing sfdisk (2.38.1-r1)<br>(40/53) Installing mcookie (2.38.1-r1)<br>(41/53) Installing agetty (2.38.1-r1)<br>(42/53) Installing agetty-openrc (0.45.2-r7)<br>(43/53) Installing wipefs (2.38.1-r1)<br>(44/53) Installing umount (2.38.1-r1)<br>(45/53) Installing util-linux-openrc (2.38.1-r1)<br>(46/53) Installing flock (2.38.1-r1)<br>(47/53) Installing lsblk (2.38.1-r1)<br>(48/53) Installing libcap-ng (0.8.3-r1)<br>(49/53) Installing setpriv (2.38.1-r1)<br>(50/53) Installing logger (2.38.1-r1)<br>(51/53) Installing partx (2.38.1-r1)<br>(52/53) Installing fstrim (2.38.1-r1)<br>(53/53) Installing findmnt (2.38.1-r1)<br>Executing busybox-1.35.0-r29.trigger<br>OK: 40 MiB in 79 packages<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>loop0    7:0    0   14M  1 loop /.modloop<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0   49M  1 disk /media/vda<br>├─vda1 253:1    0   49M  1 part<br>└─vda2 253:2    0  1.4M  1 part<br>vdb    253:16   0    6G  0 disk<br>vdc    253:32   0   50G  1 disk /root/repo<br>localhost:~#<br>localhost:~# blkid<br>/dev/loop0: TYPE="squashfs"<br>/dev/vdc: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda2: SEC_TYPE="msdos" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="77b851c3-02"<br>/dev/vda1: BLOCK_SIZE="2048" UUID="2022-11-22-03-30-35-00" LABEL="alpine-virt 3.17.3 x86_64" TYPE="iso9660" PTUUID="77b851c3" PTTYPE="dos" PARTUUID="77b851c3-01"<br>localhost:~#<br>localhost:~# export BOOTLOADER=grub<br>localhost:~# export SWAP_SIZE=1024<br>localhost:~# export BOOT_SIZE=500<br>localhost:~# export ROOT_SIZE=3644<br>localhost:~#<br>localhost:~# export EDITOR=nano<br>localhost:~# export KERNELOPTS="console=tty0 console=ttyS0,115200n8"<br>localhost:~#<br>localhost:~# env<br>USER=root<br>SHLVL=1<br>HOME=/root<br>PAGER=less<br>BOOTLOADER=grub<br>LOGNAME=root<br>TERM=vt100<br>ROOT_SIZE=3644<br>BOOT_SIZE=500<br>LC_COLLATE=C<br>PATH=/sbin:/usr/sbin:/bin:/usr/bin:/usr/local/sbin:/usr/local/bin<br>LANG=C.UTF-8<br>SWAP_SIZE=1024<br>KERNELOPTS=console=tty0 console=ttyS0,115200n8<br>SHELL=/bin/ash<br>PWD=/root<br>CHARSET=UTF-8<br>EDITOR=nano<br>localhost:~#<br>localhost:~# setup-alpine<br>Enter system hostname (fully qualified form, e.g. 'foo.example.org') [localhost]<br>Available interfaces are: eth0.<br>Enter '?' for help on bridges, bonding and vlans.<br>Which one do you want to initialize? (or '?' or 'done') [eth0]<br>Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp]<br>Do you want to do any manual network configuration? (y/n) [n]<br>udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br>Changing password for root<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for root changed by root<br>Which timezone are you in? ('?' for list) [UTC]<br> * Seeding random number generator ...<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox acpid ...<br> [ ok ]<br> * Starting busybox crond ...<br> [ ok ]<br>HTTP/FTP proxy URL? (e.g. 'http://proxy:8080', or 'none') [none]<br>Which NTP client to run? ('busybox', 'openntpd', 'chrony' or 'none') [chrony] none<br>wget: bad address 'mirrors.alpinelinux.org'<br>wget: bad address 'mirrors.alpinelinux.org'<br><br>r) Add random from the above list<br>f) Detect and add fastest mirror from above list<br>e) Edit /etc/apk/repositories with text editor<br><br>Enter mirror number (1-0) or URL to add (or r/f/e/done) [1] done<br>Setup a user? (enter a lower-case loginname, or 'no') [no] test<br>Full name for user test [test]<br>Changing password for test<br>New password:<br>Bad password: too short<br>Retype password:<br>passwd: password for test changed by root<br>Enter ssh key or URL for test (or 'none') [none]<br>(1/1) Installing doas (6.8.2-r3)<br>Executing doas-6.8.2-r3.post-install<br>Executing busybox-1.35.0-r29.trigger<br>OK: 40 MiB in 80 packages<br>Which ssh server? ('openssh', 'dropbear' or 'none') [openssh]<br> * service sshd added to runlevel default<br> * Caching service dependencies ...<br> [ ok ]<br>ssh-keygen: generating new host keys: RSA ECDSA ED25519<br> * Starting sshd ...<br> [ ok ]<br>Available disks are:<br>  fd0   (0.0 GB  )<br>  sr0   (1.1 GB QEMU     QEMU DVD-ROM    )<br>  vdb   (6.4 GB 0x1af4 )<br>Which disk(s) would you like to use? (or '?' for help or 'none') [none] vdb<br>The following disk is selected:<br>  vdb   (6.4 GB 0x1af4 )<br>How would you like to use it? ('sys', 'data', 'crypt', 'lvm' or '?' for help) [?] sys<br>WARNING: The following disk(s) will be erased:<br>  vdb   (6.4 GB 0x1af4 )<br>WARNING: Erase the above disk(s) and continue? (y/n) [n] y<br>Creating file systems...<br>Installing system on /dev/vdb3:<br>Installing for i386-pc platform.<br>Installation finished. No error reported.<br>100% ████████████████████████████████████████████==> initramfs: creating /boot/initramfs-virt<br>Generating grub configuration file ...<br>Found linux image: /boot/vmlinuz-virt<br>Found initrd image: /boot/initramfs-virt<br>Warning: os-prober will not be executed to detect other bootable partitions.<br>Systems on them will not be added to the GRUB boot configuration.<br>Check GRUB_DISABLE_OS_PROBER documentation entry.<br>done<br><br>Installation is complete. Please reboot.<br>localhost:~#<br>localhost:~#<br>localhost:~# umount /root/repo<br>localhost:~#<br>localhost:~# mount /dev/vdb3 /mnt<br>localhost:~# cp -piv /mnt/etc/fstab /root/backup<br>'/mnt/etc/fstab' -> '/root/backup/fstab'<br>localhost:~# cat /mnt/etc/fstab<br>UUID=ada017ef-3181-40be-8e14-f45c49e00f3a       /       ext4    rw,relatime 0 1<br>UUID=9adeb32c-979a-47e7-b034-cd800a81e867       /boot   ext4    rw,relatime 0 2<br>UUID=d34884c7-e0f9-4346-ac60-373b204cc274       swap    swap    defaults      0 0<br>/dev/cdrom      /media/cdrom    iso9660 noauto,ro 0 0<br>/dev/usbdisk    /media/usb      vfat    noauto  0 0<br>tmpfs   /tmp    tmpfs   nosuid,nodev    0       0<br>localhost:~#<br>localhost:~# sed -i -e 's/^tmpfs/# tmpfs/' /mnt/etc/fstab<br>localhost:~#<br>localhost:~# echo 'LABEL=tmp-partition /tmp ext4 defaults 1 2' >> /mnt/etc/fstab<br>localhost:~#<br>localhost:~# cat /mnt/etc/fstab<br>UUID=ada017ef-3181-40be-8e14-f45c49e00f3a       /       ext4    rw,relatime 0 1<br>UUID=9adeb32c-979a-47e7-b034-cd800a81e867       /boot   ext4    rw,relatime 0 2<br>UUID=d34884c7-e0f9-4346-ac60-373b204cc274       swap    swap    defaults      0 0<br>/dev/cdrom      /media/cdrom    iso9660 noauto,ro 0 0<br>/dev/usbdisk    /media/usb      vfat    noauto  0 0<br># tmpfs /tmp    tmpfs   nosuid,nodev    0       0<br>LABEL=tmp-partition /tmp ext4 defaults 1 2<br>localhost:~# umount /mnt<br>localhost:~#<br>localhost:~# fdisk /dev/vdb<br><br>Welcome to fdisk (util-linux 2.38.1).<br>Changes will remain in memory only, until you decide to write them.<br>Be careful before using the write command.<br><br><br>Command (m for help): p<br>Disk /dev/vdb: 6 GiB, 6442450944 bytes, 12582912 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x30d6984f<br><br>Device     Boot   Start      End Sectors  Size Id Type<br>/dev/vdb1  *       2048  1026047 1024000  500M 83 Linux<br>/dev/vdb2       1026048  3123199 2097152    1G 82 Linux swap / Solaris<br>/dev/vdb3       3123200 10586111 7462912  3.6G 83 Linux<br><br>Command (m for help): n<br>Partition type<br>   p   primary (3 primary, 0 extended, 1 free)<br>   e   extended (container for logical partitions)<br>Select (default e): p<br><br>Selected partition 4<br>First sector (10586112-12582911, default 10586112):<br>Last sector, +/-sectors or +/-size{K,M,G,T,P} (10586112-12582911, default 12582911):<br><br>Created a new partition 4 of type 'Linux' and of size 975 MiB.<br><br>Command (m for help): p<br>Disk /dev/vdb: 6 GiB, 6442450944 bytes, 12582912 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x30d6984f<br><br>Device     Boot    Start      End Sectors  Size Id Type<br>/dev/vdb1  *        2048  1026047 1024000  500M 83 Linux<br>/dev/vdb2        1026048  3123199 2097152    1G 82 Linux swap / Solaris<br>/dev/vdb3        3123200 10586111 7462912  3.6G 83 Linux<br>/dev/vdb4       10586112 12582911 1996800  975M 83 Linux<br><br>Command (m for help): w<br>The partition table has been altered.<br>Calling ioctl() to re-read partition table.<br>Syncing disks.<br><br>localhost:~#<br>localhost:~# mkfs.ext4 -L tmp-partition /dev/vdb4<br>mke2fs 1.46.6 (1-Feb-2023)<br>Discarding device blocks: done<br>Creating filesystem with 249600 4k blocks and 62464 inodes<br>Filesystem UUID: bc45f4ae-37b9-41fe-a76d-3b3c56187ba5<br>Superblock backups stored on blocks:<br>        32768, 98304, 163840, 229376<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (4096 blocks): done<br>Writing superblocks and filesystem accounting information: done<br><br>localhost:~# poweroff<br>localhost:~# ^[[30;14R * Stopping sshd ... [ ok ]<br> * Saving random number generator seed ... * Seeding 256 bits and crediting<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Stopping busybox crond ... [ ok ]<br> * Stopping busybox syslog ... [ ok ]<br> * Stopping busybox acpid ... [ ok ]<br> * Unmounting loop devices<br> *   Remounting /.modloop read only ... [ ok ]<br> * Unmounting filesystems<br> *   Unmounting /media/vda ... [ ok ]<br> * Setting hardware clock using the system clock [UTC] ... [ ok ]<br> * Stopping busybox mdev ... [ ok ]<br> [ ok ]<br> * Terminating remaining processes ...[ 2423.748288] reboot: Power down<br>~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=1  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR<br><br><br><br>SeaBIOS (version rel-1.16.1-0-g3208b098f51a-prebuilt.qemu.org)<br><br><br>iPXE (http://ipxe.org) 00:04.0 CA00 PCI2.10 PnP PMM+3EFD0FD0+3EF30FD00<br><br>                                                                      <br>Booting from Hard Disk...<br>GRUB loading.<br>Welcome to GRUB!<br><br>[   35.328335] ata2.00: ATAPI: QEMU DVD-ROM, 2.5+, max UDMA/100<br>[   35.360046] rtc_cmos 00:05: alarms up to one day, y3k, 242 bytes nvram, hpet irqs<br>[   35.432965] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input0<br>[   35.479927] gre: GRE over IPv4 demultiplexor driver<br>[   35.558680] Key type dns_resolver registered<br>[   35.581789] IPI shorthand broadcast: enabled<br>[   35.692762] registered taskstats version 1<br>[   35.708835] Loading compiled-in X.509 certificates<br>[   35.773103] scsi 1:0:0:0: CD-ROM            QEMU     QEMU DVD-ROM     2.5+ PQ: 0 ANSI: 5<br>[   37.291875] Loaded X.509 cert 'Build time autogenerated kernel key: 90200cc09a919577283b2cb6eca2ff9ac9891c1d'<br>[   37.332738] zswap: loaded using pool lzo/zbud<br>[   37.410275] Key type .fscrypt registered<br>[   37.412433] Key type fscrypt-provisioning registered<br>[   37.504711] Unstable clock detected, switching default tracing clock to "global"<br>[   37.504711] If you want to keep using the local clock, then add:<br>[   37.504711]   "trace_clock=local"<br>[   37.504711] on the kernel command line<br>[   37.847385] Freeing unused kernel image (initmem) memory: 1824K<br>[   37.867821] Write protecting the kernel read-only data: 16384k<br>[   37.919116] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[   37.938824] Freeing unused kernel image (rodata/data gap) memory: 1072K<br>[   37.948760] rodata_test: all tests were successful<br>[   37.957617] Run /init as init process<br>[   39.870865] Alpine Init 3.7.0-r1<br>Alpine Init 3.7.0-r1<br>[   39.943585] Loading boot drivers...<br> * Loading boot drivers: [   41.376796] ACPI: bus type USB registered<br>[   41.384055] usbcore: registered new interface driver usbfs<br>[   41.400988] usbcore: registered new interface driver hub<br>[   41.405491] usbcore: registered new device driver usb<br>[   41.599704] usbcore: registered new interface driver usb-storage<br>[   44.902105] loop: module loaded<br>[   47.965056] Loading boot drivers: ok.<br>ok.<br>[   48.230211] Mounting root...<br> * Mounting root: [   58.235018] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[   58.241559] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[   64.220685] virtio_blk virtio2: [vda] 12582912 512-byte logical blocks (6.44 GB/6.00 GiB)<br>[   64.402095]  vda: vda1 vda2 vda3 vda4<br>[   64.554445] virtio_blk virtio3: [vdb] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[   99.978772] EXT4-fs (vda3): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[  100.052732] Mounting root: ok.<br>ok.<br><br>   OpenRC 0.45.2 is starting up Linux 5.15.106-0-virt (x86_64)<br><br> * /proc is already mounted<br> * Mounting /run ... * /run/openrc: creating directory<br> * /run/lock: creating directory<br> * /run/lock: correcting owner<br> * Caching service dependencies ... [ ok ]<br> * Remounting devtmpfs on /dev ... [ ok ]<br> * Mounting /dev/mqueue ... [ ok ]<br> * Mounting security filesystem ... [ ok ]<br> * Mounting debug filesystem ... [ ok ]<br> * Mounting persistent storage (pstore) filesystem ... [ ok ]<br> * Starting busybox mdev ... [ ok ]<br> * Scanning hardware for mdev ... [ ok ]<br> * Loading hardware drivers ... [ ok ]<br> * Loading modules ... [ ok ]<br> * Setting system clock using the hardware clock [UTC] ... [ ok ]<br> * Checking local filesystems  .../dev/vda3: clean, 2986/233392 files, 51936/932864 blocks<br>/dev/vda1: clean, 305/128016 files, 64890/512000 blocks<br>tmp-partition: clean, 11/62464 files, 8637/249600 blocks<br> [ ok ]<br> * Remounting root filesystem read/write ... [ ok ]<br> * Remounting filesystems ... [ ok ]<br> * Activating swap devices ... [ ok ]<br> * Mounting local filesystems ... [ ok ]<br> * Configuring kernel parameters ... [ ok ]<br> * Migrating /var/lock to /run/lock ... [ ok ]<br> * Creating user login records ... [ ok ]<br> * Cleaning /tmp directory ... [ ok ]<br> * Setting hostname ... [ ok ]<br> * Starting networking ... *   lo ... [ ok ]<br> *   eth0 ...udhcpc: started, v1.35.0<br>udhcpc: broadcasting discover<br>udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br> [ ok ]<br> * Seeding random number generator ... * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Starting busybox syslog ... [ ok ]<br> * Starting busybox acpid ... [ ok ]<br> * Starting busybox crond ... [ ok ]<br> * Starting sshd ... [ ok ]<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>Password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~#<br>localhost:~# cat /etc/os-release<br>NAME="Alpine Linux"<br>ID=alpine<br>VERSION_ID=3.17.3<br>PRETTY_NAME="Alpine Linux v3.17"<br>HOME_URL="https://alpinelinux.org/"<br>BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"<br>localhost:~#<br>localhost:~# uname -a<br>Linux localhost 5.15.106-0-virt #1-Alpine SMP Wed, 05 Apr 2023 10:48:45 +0000 x86_64 Linux<br>localhost:~#<br>localhost:~# mkdir /root/backup<br>localhost:~# mkdir /mnt/repo<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0    6G  0 disk<br>├─vda1 253:1    0  500M  0 part /boot<br>├─vda2 253:2    0    1G  0 part [SWAP]<br>├─vda3 253:3    0  3.6G  0 part /<br>└─vda4 253:4    0  975M  0 part /tmp<br>vdb    253:16   0   50G  1 disk<br>localhost:~# blkid<br>/dev/vda1: UUID="9adeb32c-979a-47e7-b034-cd800a81e867" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="30d6984f-01"<br>/dev/vda4: LABEL="tmp-partition" UUID="bc45f4ae-37b9-41fe-a76d-3b3c56187ba5" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-04"<br>/dev/vda2: UUID="d34884c7-e0f9-4346-ac60-373b204cc274" TYPE="swap" PARTUUID="30d6984f-02"<br>/dev/vdb: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda3: UUID="ada017ef-3181-40be-8e14-f45c49e00f3a" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-03"<br>localhost:~#<br>localhost:~# df -ahT<br>Filesystem           Type            Size      Used Available Use% Mounted on<br>sysfs                sysfs              0         0         0   0% /sys<br>devtmpfs             devtmpfs       10.0M         0     10.0M   0% /dev<br>proc                 proc               0         0         0   0% /proc<br>devpts               devpts             0         0         0   0% /dev/pts<br>shm                  tmpfs         491.6M         0    491.6M   0% /dev/shm<br>/dev/vda3            ext4            3.4G     67.4M      3.2G   2% /<br>tmpfs                tmpfs         196.6M    108.0K    196.5M   0% /run<br>mqueue               mqueue             0         0         0   0% /dev/mqueue<br>securityfs           securityfs         0         0         0   0% /sys/kernel/security<br>debugfs              debugfs            0         0         0   0% /sys/kernel/debug<br>pstore               pstore             0         0         0   0% /sys/fs/pstore<br>tracefs              tracefs            0         0         0   0% /sys/kernel/debug/tracing<br>/dev/vda1            ext4          458.3M     21.7M    407.6M   5% /boot<br>/dev/vda4            ext4          941.3M     32.0K    876.5M   0% /tmp<br>localhost:~#<br>localhost:~# df -ahT|grep tmp<br>devtmpfs             devtmpfs       10.0M         0     10.0M   0% /dev<br>shm                  tmpfs         491.6M         0    491.6M   0% /dev/shm<br>tmpfs                tmpfs         196.6M    108.0K    196.5M   0% /run<br>/dev/vda4            ext4          941.3M     32.0K    876.5M   0% /tmp<br>localhost:~# cp -pi /etc/apk/repositories /root/backup<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# echo '/mnt/repo/alpine/v3.17/main' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>/mnt/repo/alpine/v3.17/main<br>localhost:~# echo '/mnt/repo/alpine/v3.17/community' >> /etc/apk/repositories<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>/mnt/repo/alpine/v3.17/main<br>/mnt/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /mnt/repo<br>localhost:~#<br>localhost:~# cat /etc/modules ; cp -pi /etc/modules /root/backup<br>af_packet<br>ipv6<br>localhost:~#<br>localhost:~# echo fuse >> /etc/modules ; cat /etc/modules<br>af_packet<br>ipv6<br>fuse<br>localhost:~# apk update<br>v3.17.3-51-gb3e182d1e6a [/mnt/repo/alpine/v3.17/main]<br>v3.17.3-50-ga35f8409359 [/mnt/repo/alpine/v3.17/community]<br>OK: 17818 distinct packages available<br>localhost:~#<br>localhost:~#<br>localhost:~# date<br>Fri Apr 14 09:19:42 UTC 2023<br>rchive-tools libarchive-doc cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc gcc abuild binutils binutils-doc gcc-doc py3-pip pandoc iproute2 util-linux pciutils usbutils coreutils binutils findutils grep bash bash-doc utmps pass pass-otp darkhttpd vsftpd vsftpd-doc zstd pwgen easy-rsa  markdown expect sshpass keepassxc gzip rpm xz bzip2 gawk bc diffutils psmisc procps shadow util-linux-bash-completion util-linux-login mount umount netcat-openbsd nmap nmap-nping nmap-nselibs nmap-scripts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix gptfdisk sgdisk parted grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sfdisk btrfs-progs dosfstools texinfo e2fsprogs e2fsprogs-extra  mkinitfs haveged f2fs-tools jfsutils ntfs-3g ntfs-3g-progs xfsprogs cpio whois wget unzip zip tar curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils fuse-exfat-doc nfs-utils ncurses sharutils mandoc man-pages mandoc-apropos docs cmd:rsvg-convert iptables ip6tables perl-net-ssleay stress-ng dbus dbus-x11 mc nnn nnn-bash-completion nnn-plugins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vifm-zsh-completion  vifm-bash-completion  fish  zsh udisks2-bash-completion ncdu gnome-disk-utility zim chezdav lighttpd lighttpd-doc lighttpd-mod_webdav lighttpd-mod_auth grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsql apr-util-dbd_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate cadaver<br><br>date<br>localhost:~#<br>localhost:~# apk add linux-lts linux-virt vim cryptsetup asciinema neofetch xca<br>polkit  screen  rpm cifs-utils device-mapper rng-tools qt5-qtwebglplugin inetuti<br>ls-telnet perl hdparm fsarchiver progress pv davfs2 libcdio-tools lftp-doc lftp<br>pssh mutt neomutt alpine ncftp sshfs samba apache2 apache2-doc apache2-webdav ap<br>ache2-ctl apache2-utils alpine-sdk build-base apk-tools alpine-conf busybox libp<br>wquality fakeroot syslinux xorriso mtools dosfstools grub-efi make git sudo lynx<br> links nodejs npm dhcp-server-vanilla ccache ccache-doc udisks2 udisks2-doc liba<br>rchive-tools libarchive-doc cmake cmake-doc extra-cmake-modules extra-cmake-modu<br>les-doc gcc abuild binutils binutils-doc gcc-doc py3-pip pandoc iproute2 util-li<br>nux pciutils usbutils coreutils binutils findutils grep bash bash-doc utmps pass<br> pass-otp darkhttpd vsftpd vsftpd-doc zstd pwgen easy-rsa  markdown expect sshpa<br>ss keepassxc gzip rpm xz bzip2 gawk bc diffutils psmisc procps shadow util-linux<br>-bash-completion util-linux-login mount umount netcat-openbsd nmap nmap-nping nm<br>ap-nselibs nmap-scripts net-tools socat rlwrap iputils perl-digest-sha3 dos2unix<br> gptfdisk sgdisk parted grub grub-bios grub-doc efibootmgr cfdisk lvm2 libusb sf<br>disk btrfs-progs dosfstools texinfo e2fsprogs e2fsprogs-extra  mkinitfs haveged<br>f2fs-tools jfsutils ntfs-3g ntfs-3g-progs xfsprogs cpio whois wget unzip zip tar<br> curl p7zip ipcalc sed nano fuse-exfat fuse-exfat-utils fuse-exfat-doc nfs-utils<br> ncurses sharutils mandoc man-pages mandoc-apropos docs cmd:rsvg-convert iptable<br>s ip6tables perl-net-ssleay stress-ng dbus dbus-x11 mc nnn nnn-bash-completion n<br>nn-plugins nnn-zsh-completion nnn-fish-completion  vifm vifm-fish-completion vif<br>m-zsh-completion  vifm-bash-completion  fish  zsh udisks2-bash-completion ncdu g<br>nome-disk-utility zim chezdav lighttpd lighttpd-doc lighttpd-mod_webdav lighttpd<br>-mod_auth grub-bash-completion apr-util-dbd_mysql apr-util-dbd_pgsql apr-util-db<br>d_sqlite3 apr-util-ldap uuidgen ed  gifsicle mlocate cadaver<br>(1/773) Installing fakeroot (1.29-r0)<br>(2/773) Installing libattr (2.5.1-r2)<br>(3/773) Installing attr (2.5.1-r2)<br>(4/773) Installing libacl (2.3.1-r1)<br>(5/773) Installing tar (1.34-r2)<br>(6/773) Installing pkgconf (1.9.4-r0)<br>(7/773) Installing patch (2.7.6-r9)<br>(8/773) Installing libgcc (12.2.1_git20220924-r4)<br>(9/773) Installing libstdc++ (12.2.1_git20220924-r4)<br>(10/773) Installing lzip (1.23-r0)<br>(11/773) Installing ca-certificates (20220614-r4)<br>(12/773) Installing brotli-libs (1.0.9-r9)<br>(13/773) Installing nghttp2-libs (1.51.0-r0)<br>(14/773) Installing libcurl (7.88.1-r1)<br>(15/773) Installing curl (7.88.1-r1)<br>(16/773) Installing abuild (3.10.0-r0)<br>Executing abuild-3.10.0-r0.pre-install<br>(17/773) Installing gdbm (1.23-r0)<br>(18/773) Installing libsasl (2.1.28-r3)<br>(19/773) Installing libldap (2.6.3-r6)<br>(20/773) Installing alpine (2.26-r1)<br>(21/773) Installing binutils (2.39-r2)<br>(22/773) Installing libmagic (5.43-r0)<br>(23/773) Installing file (5.43-r0)<br>(24/773) Installing libgomp (12.2.1_git20220924-r4)<br>(25/773) Installing libatomic (12.2.1_git20220924-r4)<br>(26/773) Installing gmp (6.2.1-r2)<br>(27/773) Installing isl25 (0.25-r0)<br>(28/773) Installing mpfr4 (4.1.0-r0)<br>(29/773) Installing mpc1 (1.2.1-r1)<br>(30/773) Installing gcc (12.2.1_git20220924-r4)<br>(31/773) Installing libstdc++-dev (12.2.1_git20220924-r4)<br>(32/773) Installing musl-dev (1.2.3-r4)<br>(33/773) Installing libc-dev (0.7.2-r3)<br>(34/773) Installing g++ (12.2.1_git20220924-r4)<br>(35/773) Installing make (4.3-r1)<br>(36/773) Installing fortify-headers (1.1-r1)<br>(37/773) Installing build-base (0.5-r3)<br>(38/773) Installing libexpat (2.5.0-r0)<br>(39/773) Installing pcre2 (10.42-r0)<br>(40/773) Installing git (2.38.4-r1)<br>(41/773) Installing alpine-sdk (1.0-r1)<br>(42/773) Installing apr (1.7.2-r0)<br>(43/773) Installing apr-util (1.6.3-r0)<br>(44/773) Installing pcre (8.45-r2)<br>(45/773) Installing apache2 (2.4.56-r0)<br>Executing apache2-2.4.56-r0.pre-install<br>(46/773) Installing less (608-r1)<br>(47/773) Installing gzip (1.12-r0)<br>(48/773) Installing libintl (0.21.1-r1)<br>(49/773) Installing lynx (2.8.9_p1-r8)<br>(50/773) Installing apache2-ctl (2.4.56-r0)<br>(51/773) Installing apache2-doc (2.4.56-r0)<br>(52/773) Installing apache2-utils (2.4.56-r0)<br>(53/773) Installing apache2-webdav (2.4.56-r0)<br>(54/773) Installing mariadb-connector-c (3.3.3-r0)<br>(55/773) Installing apr-util-dbd_mysql (1.6.3-r0)<br>(56/773) Installing libpq (15.2-r0)<br>(57/773) Installing apr-util-dbd_pgsql (1.6.3-r0)<br>(58/773) Installing sqlite-libs (3.40.1-r0)<br>(59/773) Installing apr-util-dbd_sqlite3 (1.6.3-r0)<br>(60/773) Installing apr-util-ldap (1.6.3-r0)<br>(61/773) Installing libbz2 (1.0.8-r4)<br>(62/773) Installing libffi (3.4.4-r0)<br>(63/773) Installing mpdecimal (2.5.1-r1)<br>(64/773) Installing python3 (3.10.11-r0)<br>(65/773) Installing ncurses (6.3_p20221119-r0)<br>(66/773) Installing asciinema (2.2.0-r0)<br>(67/773) Installing bash (5.2.15-r0)<br>Executing bash-5.2.15-r0.post-install<br>(68/773) Installing bash-doc (5.2.15-r0)<br>(69/773) Installing bc (1.07.1-r2)<br>(70/773) Installing binutils-doc (2.39-r2)<br>(71/773) Installing lzo (2.10-r3)<br>(72/773) Installing eudev-libs (3.2.11-r4)<br>(73/773) Installing btrfs-progs (6.0.2-r0)<br>(74/773) Installing bzip2 (1.0.8-r4)<br>(75/773) Installing neon (0.32.4-r0)<br>(76/773) Installing cadaver (0.23.3-r6)<br>(77/773) Installing hiredis (1.0.2-r1)<br>(78/773) Installing ccache (4.7.5-r0)<br>(79/773) Installing ccache-doc (4.7.5-r0)<br>(80/773) Installing dbus-libs (1.14.4-r0)<br>(81/773) Installing avahi-libs (0.8-r6)<br>(82/773) Installing libdaemon (0.14-r3)<br>(83/773) Installing libevent (2.1.12-r5)<br>(84/773) Installing avahi (0.8-r6)<br>Executing avahi-0.8-r6.pre-install<br>(85/773) Installing glib (2.74.6-r0)<br>(86/773) Installing avahi-glib (0.8-r6)<br>(87/773) Installing gsettings-desktop-schemas (43.0-r0)<br>(88/773) Installing nettle (3.8.1-r0)<br>(89/773) Installing p11-kit (0.24.1-r1)<br>(90/773) Installing libtasn1 (4.19.0-r0)<br>(91/773) Installing libunistring (1.1-r0)<br>(92/773) Installing gnutls (3.7.8-r3)<br>(93/773) Installing libproxy (0.4.18-r1)<br>(94/773) Installing glib-networking (2.74.0-r2)<br>(95/773) Installing libidn2 (2.3.4-r0)<br>(96/773) Installing libpsl (0.21.1-r1)<br>(97/773) Installing libsoup3 (3.2.2-r0)<br>(98/773) Installing libxml2 (2.10.3-r1)<br>(99/773) Installing phodav (3.0-r0)<br>(100/773) Installing chezdav (3.0-r0)<br>(101/773) Installing krb5-conf (1.0-r2)<br>(102/773) Installing keyutils-libs (1.6.3-r1)<br>(103/773) Installing libverto (0.3.2-r1)<br>(104/773) Installing krb5-libs (1.20.1-r0)<br>(105/773) Installing talloc (2.3.4-r0)<br>(106/773) Installing libwbclient (4.16.10-r0)<br>(107/773) Installing cifs-utils (7.0-r0)<br>(108/773) Installing lz4-libs (1.9.4-r1)<br>(109/773) Installing libarchive (3.6.1-r2)<br>(110/773) Installing rhash-libs (1.4.3-r1)<br>(111/773) Installing libuv (1.44.2-r0)<br>(112/773) Installing cmake (3.24.4-r0)<br>(113/773) Installing cmake-doc (3.24.4-r0)<br>(114/773) Installing libxau (1.0.10-r0)<br>(115/773) Installing libmd (1.0.4-r0)<br>(116/773) Installing libbsd (0.11.7-r0)<br>(117/773) Installing libxdmcp (1.1.4-r0)<br>(118/773) Installing libxcb (1.15-r0)<br>(119/773) Installing libx11 (1.8.4-r0)<br>(120/773) Installing libxext (1.3.5-r0)<br>(121/773) Installing libxrender (0.9.11-r0)<br>(122/773) Installing libpng (1.6.38-r0)<br>(123/773) Installing freetype (2.12.1-r0)<br>(124/773) Installing fontconfig (2.14.1-r0)<br>(125/773) Installing pixman (0.42.2-r0)<br>(126/773) Installing cairo (1.17.6-r3)<br>(127/773) Installing shared-mime-info (2.2-r2)<br>(128/773) Installing libjpeg-turbo (2.1.4-r0)<br>(129/773) Installing libwebp (1.2.4-r1)<br>(130/773) Installing tiff (4.4.0-r3)<br>(131/773) Installing gdk-pixbuf (2.42.10-r0)<br>(132/773) Installing libxft (2.3.7-r0)<br>(133/773) Installing fribidi (1.0.12-r0)<br>(134/773) Installing graphite2 (1.3.14-r2)<br>(135/773) Installing harfbuzz (5.3.1-r1)<br>(136/773) Installing pango (1.50.13-r0)<br>(137/773) Installing rsvg-convert (2.55.1-r0)<br>(138/773) Installing skalibs (2.12.0.1-r0)<br>(139/773) Installing utmps-libs (0.1.2.0-r1)<br>(140/773) Installing coreutils (9.1-r0)<br>(141/773) Installing cpio (2.13-r3)<br>(142/773) Installing popt (1.19-r0)<br>(143/773) Installing cryptsetup (2.5.0-r2)<br>(144/773) Installing cryptsetup-openrc (2.5.0-r2)<br>(145/773) Installing darkhttpd (1.14-r0)<br>Executing darkhttpd-1.14-r0.pre-install<br>(146/773) Installing darkhttpd-openrc (1.14-r0)<br>(147/773) Installing davfs2 (1.6.1-r0)<br>Executing davfs2-1.6.1-r0.pre-install<br>(148/773) Installing dbus (1.14.4-r0)<br>Executing dbus-1.14.4-r0.pre-install<br>Executing dbus-1.14.4-r0.post-install<br>(149/773) Installing dbus-openrc (1.14.4-r0)<br>(150/773) Installing dbus-x11 (1.14.4-r0)<br>(151/773) Installing libaio (0.3.113-r0)<br>(152/773) Installing device-mapper-event-libs (2.03.17-r1)<br>(153/773) Installing lvm2-libs (2.03.17-r1)<br>(154/773) Installing device-mapper (2.03.17-r1)<br>(155/773) Installing dhcp (4.4.3_p1-r1)<br>Executing dhcp-4.4.3_p1-r1.pre-install<br>(156/773) Installing dhcp-openrc (4.4.3_p1-r1)<br>(157/773) Installing dhcp-server-vanilla (4.4.3_p1-r1)<br>(158/773) Installing diffutils (3.8-r1)<br>(159/773) Installing mandoc (1.14.6-r6)<br>(160/773) Installing mandoc-doc (1.14.6-r6)<br>(161/773) Installing man-pages (6.01-r0)<br>(162/773) Installing docs (0.2-r6)<br>(163/773) Installing btrfs-progs-doc (6.0.2-r0)<br>(164/773) Installing lzo-doc (2.10-r3)<br>(165/773) Installing harfbuzz-doc (5.3.1-r1)<br>(166/773) Installing lynx-doc (2.8.9_p1-r8)<br>(167/773) Installing libwebp-doc (1.2.4-r1)<br>(168/773) Installing less-doc (608-r1)<br>(169/773) Installing busybox-doc (1.35.0-r29)<br>(170/773) Installing alpine-doc (2.26-r1)<br>(171/773) Installing cadaver-doc (0.23.3-r6)<br>(172/773) Installing gdk-pixbuf-doc (2.42.10-r0)<br>(173/773) Installing libjpeg-turbo-doc (2.1.4-r0)<br>(174/773) Installing mpc1-doc (1.2.1-r1)<br>(175/773) Installing davfs2-doc (1.6.1-r0)<br>(176/773) Installing ncurses-doc (6.3_p20221119-r0)<br>(177/773) Installing gmp-doc (6.2.1-r2)<br>(178/773) Installing cifs-utils-doc (7.0-r0)<br>(179/773) Installing libx11-doc (1.8.4-r0)<br>(180/773) Installing attr-doc (2.5.1-r2)<br>(181/773) Installing libffi-doc (3.4.4-r0)<br>(182/773) Installing pango-doc (1.50.13-r0)<br>(183/773) Installing gzip-doc (1.12-r0)<br>(184/773) Installing popt-doc (1.19-r0)<br>(185/773) Installing libxcb-doc (1.15-r0)<br>(186/773) Installing abuild-doc (3.10.0-r0)<br>(187/773) Installing freetype-doc (2.12.1-r0)<br>(188/773) Installing mpdecimal-doc (2.5.1-r1)<br>(189/773) Installing phodav-doc (3.0-r0)<br>(190/773) Installing cairo-doc (1.17.6-r3)<br>(191/773) Installing p11-kit-doc (0.24.1-r1)<br>(192/773) Installing apk-tools-doc (2.12.10-r1)<br>(193/773) Installing gdbm-doc (1.23-r0)<br>(194/773) Installing ca-certificates-doc (20220614-r4)<br>(195/773) Installing libmd-doc (1.0.4-r0)<br>(196/773) Installing libarchive-doc (3.6.1-r2)<br>(197/773) Installing acct-doc (6.6.4-r1)<br>(198/773) Installing gcc-doc (12.2.1_git20220924-r4)<br>(199/773) Installing openssl-doc (3.0.8-r3)<br>(200/773) Installing fribidi-doc (1.0.12-r0)<br>(201/773) Installing pkgconf-doc (1.9.4-r0)<br>(202/773) Installing libxrender-doc (0.9.11-r0)<br>(203/773) Installing libaio-doc (0.3.113-r0)<br>(204/773) Installing openrc-doc (0.45.2-r7)<br>(205/773) Installing bc-doc (1.07.1-r2)<br>(206/773) Installing pcre2-doc (10.42-r0)<br>(207/773) Installing coreutils-doc (9.1-r0)<br>(208/773) Installing libxft-doc (2.3.7-r0)<br>(209/773) Installing dbus-doc (1.14.4-r0)<br>(210/773) Installing talloc-doc (2.3.4-r0)<br>(211/773) Installing tar-doc (1.34-r2)<br>(212/773) Installing libxau-doc (1.0.10-r0)<br>(213/773) Installing avahi-doc (0.8-r6)<br>(214/773) Installing cryptsetup-doc (2.5.0-r2)<br>(215/773) Installing libxml2-doc (2.10.3-r1)<br>(216/773) Installing patch-doc (2.7.6-r9)<br>(217/773) Installing neon-doc (0.32.4-r0)<br>(218/773) Installing mpfr4-doc (4.1.0-r0)<br>(219/773) Installing doas-doc (6.8.2-r3)<br>(220/773) Installing libxdmcp-doc (1.1.4-r0)<br>(221/773) Installing libbsd-doc (0.11.7-r0)<br>(222/773) Installing ifupdown-ng-doc (0.12.1-r1)<br>(223/773) Installing asciinema-doc (2.2.0-r0)<br>(224/773) Installing libpng-doc (1.6.38-r0)<br>(225/773) Installing make-doc (4.3-r1)<br>(226/773) Installing cpio-doc (2.13-r3)<br>(227/773) Installing gnutls-doc (3.7.8-r3)<br>(228/773) Installing tiff-doc (4.4.0-r3)<br>(229/773) Installing diffutils-doc (3.8-r1)<br>(230/773) Installing rsvg-convert-doc (2.55.1-r0)<br>(231/773) Installing fontconfig-doc (2.14.1-r0)<br>(232/773) Installing libpsl-doc (0.21.1-r1)<br>(233/773) Installing git-doc (2.38.4-r1)<br>(234/773) Installing skalibs-doc (2.12.0.1-r0)<br>(235/773) Installing libdaemon-doc (0.14-r3)<br>(236/773) Installing glib-doc (2.74.6-r0)<br>(237/773) Installing shared-mime-info-doc (2.2-r2)<br>(238/773) Installing libidn2-doc (2.3.4-r0)<br>(239/773) Installing lzip-doc (1.23-r0)<br>(240/773) Installing dhcp-doc (4.4.3_p1-r1)<br>(241/773) Installing pcre-doc (8.45-r2)<br>(242/773) Installing libtasn1-doc (4.19.0-r0)<br>(243/773) Installing libxext-doc (1.3.5-r0)<br>(244/773) Installing zlib-doc (1.2.13-r0)<br>(245/773) Installing readline-doc (8.2.0-r0)<br>(246/773) Installing curl-doc (7.88.1-r1)<br>(247/773) Installing python3-doc (3.10.11-r0)<br>(248/773) Installing bzip2-doc (1.0.8-r4)<br>(249/773) Installing file-doc (5.43-r0)<br>(250/773) Installing fakeroot-doc (1.29-r0)<br>(251/773) Installing libunistring-doc (1.1-r0)<br>(252/773) Installing json-c-doc (0.16-r2)<br>(253/773) Installing dos2unix (7.4.3-r1)<br>(254/773) Installing dos2unix-doc (7.4.3-r1)<br>(255/773) Installing dosfstools (4.2-r1)<br>(256/773) Installing dosfstools-doc (4.2-r1)<br>(257/773) Installing e2fsprogs-doc (1.46.6-r0)<br>(258/773) Installing easy-rsa (3.1.1-r0)<br>(259/773) Installing easy-rsa-doc (3.1.1-r0)<br>(260/773) Installing ed (1.18-r2)<br>(261/773) Installing ed-doc (1.18-r2)<br>(262/773) Installing efivar-libs (38-r1)<br>(263/773) Installing efibootmgr (18-r0)<br>(264/773) Installing efibootmgr-doc (18-r0)<br>(265/773) Installing tzdata (2023c-r0)<br>(266/773) Installing tzdata-doc (2023c-r0)<br>(267/773) Installing tcl (8.6.12-r1)<br>(268/773) Installing tcl-doc (8.6.12-r1)<br>(269/773) Installing expect (5.45.4-r3)<br>(270/773) Installing expect-doc (5.45.4-r3)<br>(271/773) Installing extra-cmake-modules (5.100.0-r0)<br>(272/773) Installing extra-cmake-modules-doc (5.100.0-r0)<br>(273/773) Installing f2fs-tools-libs (1.15.0-r0)<br>(274/773) Installing f2fs-tools (1.15.0-r0)<br>(275/773) Installing f2fs-tools-doc (1.15.0-r0)<br>(276/773) Installing findutils (4.9.0-r3)<br>(277/773) Installing findutils-doc (4.9.0-r3)<br>(278/773) Installing libpcre2-32 (10.42-r0)<br>(279/773) Installing fish (3.5.1-r1)<br>Executing fish-3.5.1-r1.post-install<br>(280/773) Installing curl-fish-completion (7.88.1-r1)<br>(281/773) Installing fish-doc (3.5.1-r1)<br>(282/773) Installing libgpg-error (1.46-r1)<br>(283/773) Installing libgpg-error-doc (1.46-r1)<br>(284/773) Installing libgcrypt (1.10.1-r0)<br>(285/773) Installing libgcrypt-doc (1.10.1-r0)<br>(286/773) Installing fsarchiver (0.8.6-r1)<br>(287/773) Installing fsarchiver-doc (0.8.6-r1)<br>(288/773) Installing fuse-common (3.12.0-r0)<br>(289/773) Installing fuse-openrc (3.12.0-r0)<br>(290/773) Installing fuse (2.9.9-r2)<br>(291/773) Installing fuse-doc (2.9.9-r2)<br>(292/773) Installing fuse-exfat (1.3.0-r3)<br>(293/773) Installing fuse-exfat-doc (1.3.0-r3)<br>(294/773) Installing fuse-exfat-utils (1.3.0-r3)<br>(295/773) Installing gawk (5.1.1-r1)<br>(296/773) Installing gawk-doc (5.1.1-r1)<br>(297/773) Installing gifsicle (1.93-r1)<br>(298/773) Installing gifsicle-doc (1.93-r1)<br>(299/773) Installing gptfdisk (1.0.9-r2)<br>(300/773) Installing gptfdisk-doc (1.0.9-r2)<br>(301/773) Installing parted (3.5-r0)<br>(302/773) Installing parted-doc (3.5-r0)<br>(303/773) Installing libatasmart (0.19-r2)<br>(304/773) Installing libatasmart-doc (0.19-r2)<br>(305/773) Installing libbytesize (2.7-r1)<br>(306/773) Installing libbytesize-doc (2.7-r1)<br>(307/773) Installing dmraid (1.0.0_rc16-r1)<br>(308/773) Installing dmraid-doc (1.0.0_rc16-r1)<br>(309/773) Installing ndctl-libs (74-r0)<br>(310/773) Installing nspr (4.35-r0)<br>(311/773) Installing nss (3.85-r1)<br>(312/773) Installing libassuan (2.5.5-r1)<br>(313/773) Installing libassuan-doc (2.5.5-r1)<br>(314/773) Installing pinentry (1.2.1-r0)<br>Executing pinentry-1.2.1-r0.post-install<br>(315/773) Installing pinentry-doc (1.2.1-r0)<br>(316/773) Installing gnupg-gpgconf (2.2.40-r0)<br>(317/773) Installing gpg (2.2.40-r0)<br>(318/773) Installing npth (1.6-r2)<br>(319/773) Installing gpg-agent (2.2.40-r0)<br>(320/773) Installing libksba (1.6.3-r0)<br>(321/773) Installing libksba-doc (1.6.3-r0)<br>(322/773) Installing gpgsm (2.2.40-r0)<br>(323/773) Installing gpgme (1.18.0-r0)<br>(324/773) Installing gpgme-doc (1.18.0-r0)<br>(325/773) Installing volume_key (0.3.12-r3)<br>(326/773) Installing volume_key-doc (0.3.12-r3)<br>(327/773) Installing yaml (0.2.5-r0)<br>(328/773) Installing libblockdev (2.28-r0)<br>(329/773) Installing libgudev (237-r1)<br>(330/773) Installing polkit-libs (122-r0)<br>(331/773) Installing udisks2-libs (2.9.4-r1)<br>(332/773) Installing udisks2 (2.9.4-r1)<br>(333/773) Installing udisks2-doc (2.9.4-r1)<br>(334/773) Installing libatk-1.0 (2.46.0-r0)<br>(335/773) Installing sound-theme-freedesktop (0.8-r0)<br>(336/773) Installing libltdl (2.4.7-r1)<br>(337/773) Installing libogg (1.3.5-r2)<br>(338/773) Installing libogg-doc (1.3.5-r2)<br>(339/773) Installing libvorbis (1.3.7-r0)<br>(340/773) Installing libvorbis-doc (1.3.7-r0)<br>(341/773) Installing libcanberra (0.30-r9)<br>(342/773) Installing libcanberra-doc (0.30-r9)<br>(343/773) Installing hicolor-icon-theme (0.17-r2)<br>(344/773) Installing gtk-update-icon-cache (3.24.36-r0)<br>(345/773) Installing libxcomposite (0.4.5-r1)<br>(346/773) Installing libxcomposite-doc (0.4.5-r1)<br>(347/773) Installing libxfixes (6.0.0-r0)<br>(348/773) Installing libxfixes-doc (6.0.0-r0)<br>(349/773) Installing libxcursor (1.2.1-r1)<br>(350/773) Installing libxcursor-doc (1.2.1-r1)<br>(351/773) Installing libxdamage (1.1.5-r1)<br>(352/773) Installing libxi (1.8-r0)<br>(353/773) Installing libxi-doc (1.8-r0)<br>(354/773) Installing libxinerama (1.1.5-r0)<br>(355/773) Installing libxinerama-doc (1.1.5-r0)<br>(356/773) Installing libxrandr (1.5.3-r0)<br>(357/773) Installing libxrandr-doc (1.5.3-r0)<br>(358/773) Installing libxtst (1.2.4-r0)<br>(359/773) Installing libxtst-doc (1.2.4-r0)<br>(360/773) Installing at-spi2-core (2.46.0-r0)<br>(361/773) Installing at-spi2-core-doc (2.46.0-r0)<br>(362/773) Installing libatk-bridge-2.0 (2.46.0-r0)<br>(363/773) Installing cairo-gobject (1.17.6-r3)<br>(364/773) Installing cups-libs (2.4.2-r1)<br>(365/773) Installing libepoxy (1.5.10-r0)<br>(366/773) Installing wayland-libs-client (1.21.0-r1)<br>(367/773) Installing wayland-libs-cursor (1.21.0-r1)<br>(368/773) Installing wayland-libs-egl (1.21.0-r1)<br>(369/773) Installing xkeyboard-config (2.37-r0)<br>(370/773) Installing xkeyboard-config-doc (2.37-r0)<br>(371/773) Installing libxkbcommon (1.4.1-r0)<br>(372/773) Installing xkbcli-doc (1.4.1-r0)<br>(373/773) Installing gtk+3.0 (3.24.36-r0)<br>Executing gtk+3.0-3.24.36-r0.post-install<br>(374/773) Installing gtk+3.0-doc (3.24.36-r0)<br>(375/773) Installing libcanberra-gtk3 (0.30-r9)<br>(376/773) Installing libdvdcss (1.4.3-r0)<br>(377/773) Installing libdvdcss-doc (1.4.3-r0)<br>(378/773) Installing libdvdread (6.1.3-r0)<br>(379/773) Installing libdvdread-doc (6.1.3-r0)<br>(380/773) Installing libelogind (246.10-r5)<br>(381/773) Installing libhandy1 (1.8.2-r0)<br>(382/773) Installing libnotify (0.8.1-r1)<br>(383/773) Installing cracklib-words (2.9.8-r0)<br>(384/773) Installing cracklib (2.9.8-r0)<br>(385/773) Installing linux-pam-doc (1.5.2-r1)<br>(386/773) Installing libpwquality (1.4.4-r3)<br>(387/773) Installing libpwquality-doc (1.4.4-r3)<br>(388/773) Installing libsecret (0.20.5-r0)<br>(389/773) Installing libsecret-doc (0.20.5-r0)<br>(390/773) Installing gnome-disk-utility (43.0-r0)<br>(391/773) Installing gnome-disk-utility-doc (43.0-r0)<br>(392/773) Installing grep (3.8-r1)<br>(393/773) Installing grep-doc (3.8-r1)<br>(394/773) Installing kmod-doc (30-r1)<br>(395/773) Installing mkinitfs-doc (3.7.0-r1)<br>(396/773) Installing grub-doc (2.06-r7)<br>(397/773) Installing grub-bash-completion (2.06-r7)<br>(398/773) Installing grub-efi (2.06-r7)<br>(399/773) Installing haveged (1.9.18-r0)<br>(400/773) Installing haveged-openrc (1.9.18-r0)<br>(401/773) Installing haveged-doc (1.9.18-r0)<br>(402/773) Installing hdparm (9.65-r0)<br>(403/773) Installing hdparm-doc (9.65-r0)<br>(404/773) Installing inetutils-ftp-doc (2.4-r0)<br>(405/773) Installing inetutils-telnet (2.4-r0)<br>(406/773) Installing inetutils-telnet-doc (2.4-r0)<br>ERROR: inetutils-telnet-doc-2.4-r0: trying to overwrite usr/share/info/inetutils.info owned by inetutils-ftp-doc-2.4-r0.<br>(407/773) Installing libmnl (1.0.5-r0)<br>(408/773) Installing libnftnl (1.2.4-r0)<br>(409/773) Installing iptables (1.8.8-r2)<br>(410/773) Installing iptables-doc (1.8.8-r2)<br>(411/773) Installing iptables-openrc (1.8.8-r2)<br>(412/773) Installing ip6tables (1.8.8-r2)<br>(413/773) Installing ip6tables-openrc (1.8.8-r2)<br>(414/773) Installing libmaxminddb-libs (1.7.1-r0)<br>(415/773) Installing libmaxminddb (1.7.1-r0)<br>(416/773) Installing libmaxminddb-doc (1.7.1-r0)<br>(417/773) Installing ipcalc (1.0.1-r1)<br>(418/773) Installing ipcalc-doc (1.0.1-r1)<br>(419/773) Installing musl-fts (1.2.7-r3)<br>(420/773) Installing libelf (0.187-r2)<br>(421/773) Installing iproute2-minimal (6.0.0-r1)<br>(422/773) Installing ifupdown-ng-iproute2 (0.12.1-r1)<br>(423/773) Installing iproute2-tc (6.0.0-r1)<br>(424/773) Installing iproute2-ss (6.0.0-r1)<br>(425/773) Installing iproute2 (6.0.0-r1)<br>Executing iproute2-6.0.0-r1.post-install<br>(426/773) Installing iproute2-doc (6.0.0-r1)<br>(427/773) Installing iputils (20211215-r0)<br>(428/773) Installing jfsutils (1.1.15-r4)<br>(429/773) Installing jfsutils-doc (1.1.15-r4)<br>(430/773) Installing icu-data-full (72.1-r1)<br>(431/773) Installing icu-libs (72.1-r1)<br>(432/773) Installing libpcre2-16 (10.42-r0)<br>(433/773) Installing qt5-qtbase (5.15.6_git20221010-r0)<br>(434/773) Installing qt5-qtbase-doc (5.15.6_git20221010-r0)<br>(435/773) Installing libice (1.0.10-r1)<br>(436/773) Installing libice-doc (1.0.10-r1)<br>(437/773) Installing libsm (1.2.3-r1)<br>(438/773) Installing libsm-doc (1.2.3-r1)<br>(439/773) Installing libxt (1.2.1-r0)<br>(440/773) Installing libxt-doc (1.2.1-r0)<br>(441/773) Installing libxmu (1.1.4-r0)<br>(442/773) Installing libxmu-doc (1.1.4-r0)<br>(443/773) Installing xset (1.2.4-r1)<br>(444/773) Installing xset-doc (1.2.4-r1)<br>(445/773) Installing xprop (1.2.5-r1)<br>(446/773) Installing xprop-doc (1.2.5-r1)<br>(447/773) Installing xdg-utils (1.1.3-r4)<br>(448/773) Installing xdg-utils-doc (1.1.3-r4)<br>(449/773) Installing mesa (22.2.5-r1)<br>(450/773) Installing hwdata-pci (0.364-r0)<br>(451/773) Installing libpciaccess (0.17-r0)<br>(452/773) Installing libpciaccess-doc (0.17-r0)<br>(453/773) Installing libdrm (2.4.114-r0)<br>(454/773) Installing wayland-libs-server (1.21.0-r1)<br>(455/773) Installing libxxf86vm (1.1.5-r0)<br>(456/773) Installing libxxf86vm-doc (1.1.5-r0)<br>(457/773) Installing mesa-glapi (22.2.5-r1)<br>(458/773) Installing libxshmfence (1.3.1-r0)<br>(459/773) Installing mesa-gl (22.2.5-r1)<br>(460/773) Installing qt5-qtdeclarative (5.15.6_git20220908-r0)<br>(461/773) Installing qt5-qtwayland (5.15.6_git20220927-r1)<br>(462/773) Installing mesa-gbm (22.2.5-r1)<br>(463/773) Installing mesa-egl (22.2.5-r1)<br>(464/773) Installing libevdev (1.13.0-r0)<br>(465/773) Installing libevdev-doc (1.13.0-r0)<br>(466/773) Installing mtdev (1.1.6-r1)<br>(467/773) Installing libinput-libs (1.22.1-r0)<br>(468/773) Installing xcb-util-wm (0.4.2-r0)<br>(469/773) Installing xcb-util (0.4.0-r3)<br>(470/773) Installing xcb-util-image (0.4.1-r0)<br>(471/773) Installing xcb-util-keysyms (0.4.1-r0)<br>(472/773) Installing xcb-util-renderutil (0.3.10-r0)<br>(473/773) Installing libxkbcommon-x11 (1.4.1-r0)<br>(474/773) Installing qt5-qtbase-x11 (5.15.6_git20221010-r0)<br>(475/773) Installing qt5-qtsvg (5.15.6_git20220908-r0)<br>(476/773) Installing qt5-qtx11extras (5.15.6_git20220816-r0)<br>(477/773) Installing botan-libs (2.19.3-r0)<br>(478/773) Installing minizip (1.2.13-r0)<br>(479/773) Installing pcsc-lite-libs (1.9.9-r0)<br>(480/773) Installing libqrencode (4.1.1-r1)<br>(481/773) Installing libqrencode-doc (4.1.1-r1)<br>(482/773) Installing libusb (1.0.26-r0)<br>(483/773) Installing keepassxc (2.7.4-r0)<br>(484/773) Installing keepassxc-doc (2.7.4-r0)<br>(485/773) Installing lftp (4.9.2-r4)<br>(486/773) Installing lftp-doc (4.9.2-r4)<br>(487/773) Installing libarchive-tools (3.6.1-r2)<br>(488/773) Installing libcddb (1.3.2-r4)<br>(489/773) Installing libcdio (2.1.0-r1)<br>(490/773) Installing libcdio-doc (2.1.0-r1)<br>(491/773) Installing libcdio-tools (2.1.0-r1)<br>(492/773) Installing libdbi (0.9.0-r2)<br>(493/773) Installing libdbi-doc (0.9.0-r2)<br>(494/773) Installing lua5.4-libs (5.4.4-r6)<br>(495/773) Installing lighttpd (1.4.67-r0)<br>Executing lighttpd-1.4.67-r0.pre-install<br>(496/773) Installing lighttpd-doc (1.4.67-r0)<br>(497/773) Installing lighttpd-openrc (1.4.67-r0)<br>(498/773) Installing lighttpd-mod_auth (1.4.67-r0)<br>(499/773) Installing lighttpd-mod_webdav (1.4.67-r0)<br>(500/773) Installing links (2.28-r0)<br>(501/773) Installing links-doc (2.28-r0)<br>(502/773) Installing linux-lts (5.15.106-r0)<br>(503/773) Installing linux-lts-doc (5.15.106-r0)<br>(504/773) Installing lvm2 (2.03.17-r1)<br>(505/773) Installing lvm2-openrc (2.03.17-r1)<br>(506/773) Installing lvm2-doc (2.03.17-r1)<br>(507/773) Installing mandoc-apropos (1.14.6-r6)<br>(508/773) Installing perl (5.36.0-r0)<br>(509/773) Installing perl-doc (5.36.0-r0)<br>(510/773) Installing perl-error (0.17029-r1)<br>(511/773) Installing perl-error-doc (0.17029-r1)<br>(512/773) Installing perl-git (2.38.4-r1)<br>(513/773) Installing git-perl (2.38.4-r1)<br>(514/773) Installing markdown (1.0.1-r3)<br>(515/773) Installing markdown-doc (1.0.1-r3)<br>(516/773) Installing gpm-libs (1.20.7-r2)<br>(517/773) Installing slang (2.3.3-r0)<br>(518/773) Installing slang-doc (2.3.3-r0)<br>(519/773) Installing libssh2 (1.10.0-r3)<br>(520/773) Installing libssh2-doc (1.10.0-r3)<br>(521/773) Installing mc (4.8.28-r0)<br>(522/773) Installing mc-doc (4.8.28-r0)<br>(523/773) Installing mlocate (0.26-r8)<br>Executing mlocate-0.26-r8.pre-install<br>(524/773) Installing mlocate-doc (0.26-r8)<br>(525/773) Installing mtools (4.0.42-r0)<br>(526/773) Installing mtools-doc (4.0.42-r0)<br>(527/773) Installing libidn (1.41-r0)<br>(528/773) Installing libidn-doc (1.41-r0)<br>(529/773) Installing libgsasl (2.2.0-r0)<br>(530/773) Installing libgsasl-doc (2.2.0-r0)<br>(531/773) Installing mutt (2.2.9-r0)<br>(532/773) Installing mutt-doc (2.2.9-r0)<br>(533/773) Installing nano-doc (7.0-r0)<br>(534/773) Installing ncdu (1.17-r1)<br>(535/773) Installing ncdu-doc (1.17-r1)<br>(536/773) Installing ncftp (3.2.6-r5)<br>(537/773) Installing ncftp-doc (3.2.6-r5)<br>(538/773) Installing neofetch (7.1.0-r1)<br>(539/773) Installing neofetch-doc (7.1.0-r1)<br>(540/773) Installing gpg-wks-server (2.2.40-r0)<br>(541/773) Installing gpgv (2.2.40-r0)<br>(542/773) Installing gnupg-dirmngr (2.2.40-r0)<br>(543/773) Installing gnupg-utils (2.2.40-r0)<br>(544/773) Installing gnupg-wks-client (2.2.40-r0)<br>(545/773) Installing gnupg (2.2.40-r0)<br>(546/773) Installing gnupg-doc (2.2.40-r0)<br>(547/773) Installing gmime (3.2.13-r0)<br>(548/773) Installing gmime-doc (3.2.13-r0)<br>(549/773) Installing libxapian (1.4.21-r0)<br>(550/773) Installing notmuch-libs (0.37-r1)<br>(551/773) Installing neomutt (20220429-r2)<br>(552/773) Installing neomutt-doc (20220429-r2)<br>(553/773) Installing mii-tool (2.10-r0)<br>(554/773) Installing net-tools (2.10-r0)<br>(555/773) Installing net-tools-doc (2.10-r0)<br>(556/773) Installing netcat-openbsd (1.130-r4)<br>(557/773) Installing netcat-openbsd-doc (1.130-r4)<br>(558/773) Installing libtirpc-conf (1.3.3-r0)<br>(559/773) Installing libtirpc (1.3.3-r0)<br>(560/773) Installing libtirpc-doc (1.3.3-r0)<br>(561/773) Installing rpcbind (1.2.6-r1)<br>Executing rpcbind-1.2.6-r1.pre-install<br>(562/773) Installing rpcbind-doc (1.2.6-r1)<br>(563/773) Installing rpcbind-openrc (1.2.6-r1)<br>(564/773) Installing libnfsidmap (2.6.2-r0)<br>(565/773) Installing nfs-utils (2.6.2-r0)<br>(566/773) Installing nfs-utils-doc (2.6.2-r0)<br>(567/773) Installing nfs-utils-openrc (2.6.2-r0)<br>(568/773) Installing lua5.3-libs (5.3.6-r4)<br>(569/773) Installing libpcap (1.10.1-r1)<br>(570/773) Installing libpcap-doc (1.10.1-r1)<br>(571/773) Installing nmap (7.93-r0)<br>(572/773) Installing nmap-doc (7.93-r0)<br>(573/773) Installing nmap-nping (7.93-r0)<br>(574/773) Installing nmap-nselibs (7.93-r0)<br>(575/773) Installing nmap-scripts (7.93-r0)<br>(576/773) Installing nnn (4.6-r0)<br>(577/773) Installing nnn-doc (4.6-r0)<br>(578/773) Installing nnn-fish-completion (4.6-r0)<br>(579/773) Installing nnn-bash-completion (4.6-r0)<br>(580/773) Installing nnn-plugins (4.6-r0)<br>Executing nnn-plugins-4.6-r0.post-install<br>* To use nnn plugins you have to install them into your HOME, run: nnn-getplugs.<br>(581/773) Installing nnn-zsh-completion (4.6-r0)<br>(582/773) Installing c-ares (1.18.1-r1)<br>(583/773) Installing c-ares-doc (1.18.1-r1)<br>(584/773) Installing nodejs (18.14.2-r0)<br>(585/773) Installing nodejs-doc (18.14.2-r0)<br>(586/773) Installing npm (9.1.2-r0)<br>(587/773) Installing npm-doc (9.1.2-r0)<br>(588/773) Installing ntfs-3g-libs (2022.10.3-r0)<br>(589/773) Installing ntfs-3g (2022.10.3-r0)<br>(590/773) Installing ntfs-3g-doc (2022.10.3-r0)<br>(591/773) Installing ntfs-3g-progs (2022.10.3-r0)<br>(592/773) Installing libedit-doc (20221030.3.1-r0)<br>(593/773) Installing openssh-doc (9.1_p1-r2)<br>(594/773) Installing p7zip (17.04-r3)<br>(595/773) Installing p7zip-doc (17.04-r3)<br>(596/773) Installing pandoc (2.19.2-r0)<br>(597/773) Installing pandoc-doc (2.19.2-r0)<br>(598/773) Installing tree (2.0.4-r0)<br>(599/773) Installing tree-doc (2.0.4-r0)<br>(600/773) Installing pass (1.7.4-r1)<br>(601/773) Installing pass-doc (1.7.4-r1)<br>(602/773) Installing pass-fish-completion (1.7.4-r1)<br>(603/773) Installing oath-toolkit-liboath (2.6.7-r2)<br>(604/773) Installing oath-toolkit-oathtool (2.6.7-r2)<br>(605/773) Installing pass-otp (1.2.0-r0)<br>(606/773) Installing pass-otp-doc (1.2.0-r0)<br>(607/773) Installing pciutils-libs (3.9.0-r0)<br>(608/773) Installing pciutils (3.9.0-r0)<br>(609/773) Installing pciutils-doc (3.9.0-r0)<br>(610/773) Installing perl-digest-sha3 (1.05-r0)<br>(611/773) Installing perl-digest-sha3-doc (1.05-r0)<br>(612/773) Installing perl-net-ssleay (1.92-r2)<br>(613/773) Installing perl-net-ssleay-doc (1.92-r2)<br>(614/773) Installing polkit-common (122-r0)<br>Executing polkit-common-122-r0.pre-install<br>(615/773) Installing duktape (2.7.0-r0)<br>(616/773) Installing polkit (122-r0)<br>(617/773) Installing polkit-openrc (122-r0)<br>(618/773) Installing polkit-doc (122-r0)<br>(619/773) Installing libproc (3.3.17-r2)<br>(620/773) Installing procps (3.3.17-r2)<br>(621/773) Installing procps-doc (3.3.17-r2)<br>(622/773) Installing progress (0.16-r0)<br>(623/773) Installing progress-doc (0.16-r0)<br>(624/773) Installing psmisc (23.5-r0)<br>(625/773) Installing psmisc-doc (23.5-r0)<br>(626/773) Installing pssh (2.3.4-r2)<br>(627/773) Installing pssh-doc (2.3.4-r2)<br>(628/773) Installing pv (1.6.20-r1)<br>(629/773) Installing pv-doc (1.6.20-r1)<br>(630/773) Installing pwgen (2.08-r2)<br>(631/773) Installing pwgen-doc (2.08-r2)<br>(632/773) Installing py3-six (1.16.0-r3)<br>(633/773) Installing py3-retrying (1.3.3-r3)<br>(634/773) Installing py3-parsing (3.0.9-r0)<br>(635/773) Installing py3-packaging (21.3-r2)<br>(636/773) Installing py3-setuptools (65.6.0-r0)<br>(637/773) Installing py3-pip (22.3.1-r1)<br>(638/773) Installing py3-pip-doc (22.3.1-r1)<br>(639/773) Installing qt5-qtwebsockets (5.15.6_git20220907-r0)<br>(640/773) Installing qt5-qtwebglplugin (5.15.6_git20220816-r0)<br>(641/773) Installing qt5-qtwebglplugin-doc (5.15.6_git20220816-r0)<br>(642/773) Installing rlwrap (0.46.1-r0)<br>(643/773) Installing rlwrap-doc (0.46.1-r0)<br>(644/773) Installing jitterentropy-library (3.3.1-r0)<br>(645/773) Installing jitterentropy-library-doc (3.3.1-r0)<br>(646/773) Installing rng-tools (6.15-r1)<br>(647/773) Installing rng-tools-openrc (6.15-r1)<br>(648/773) Installing rng-tools-doc (6.15-r1)<br>(649/773) Installing rpm (4.18.0-r1)<br>(650/773) Installing rpm-doc (4.18.0-r1)<br>(651/773) Installing samba-common (4.16.10-r0)<br>(652/773) Installing tevent (0.13.0-r0)<br>(653/773) Installing samba-util-libs (4.16.10-r0)<br>(654/773) Installing jansson (2.14-r0)<br>(655/773) Installing lmdb (0.9.29-r2)<br>(656/773) Installing lmdb-doc (0.9.29-r2)<br>(657/773) Installing tdb-libs (1.4.6-r0)<br>(658/773) Installing ldb (2.5.3-r0)<br>(659/773) Installing ldb-doc (2.5.3-r0)<br>(660/773) Installing samba-libs (4.16.10-r0)<br>(661/773) Installing samba-common-server-libs (4.16.10-r0)<br>(662/773) Installing samba-client-libs (4.16.10-r0)<br>(663/773) Installing liburing (2.3-r0)<br>(664/773) Installing liburing-doc (2.3-r0)<br>(665/773) Installing samba-server (4.16.10-r0)<br>(666/773) Installing samba-server-openrc (4.16.10-r0)<br>(667/773) Installing libsmbclient (4.16.10-r0)<br>(668/773) Installing samba-client (4.16.10-r0)<br>(669/773) Installing samba-common-tools (4.16.10-r0)<br>(670/773) Installing samba (4.16.10-r0)<br>(671/773) Installing samba-doc (4.16.10-r0)<br>(672/773) Installing libutempter (1.2.1-r5)<br>(673/773) Installing libutempter-doc (1.2.1-r5)<br>(674/773) Installing screen (4.9.0-r0)<br>(675/773) Installing screen-doc (4.9.0-r0)<br>(676/773) Installing sed (4.9-r0)<br>(677/773) Installing sed-doc (4.9-r0)<br>(678/773) Installing sgdisk (1.0.9-r2)<br>(679/773) Installing shadow (4.13-r0)<br>(680/773) Installing shadow-doc (4.13-r0)<br>(681/773) Installing xz (5.2.9-r0)<br>(682/773) Installing xz-doc (5.2.9-r0)<br>(683/773) Installing sharutils (4.15.2-r2)<br>(684/773) Installing sharutils-doc (4.15.2-r2)<br>(685/773) Installing socat (1.7.4.4-r0)<br>(686/773) Installing socat-doc (1.7.4.4-r0)<br>(687/773) Installing fuse3-libs (3.12.0-r0)<br>(688/773) Installing fuse3 (3.12.0-r0)<br>(689/773) Installing fuse3-doc (3.12.0-r0)<br>(690/773) Installing sshfs (3.7.3-r0)<br>(691/773) Installing sshfs-doc (3.7.3-r0)<br>(692/773) Installing sshpass (1.09-r1)<br>(693/773) Installing sshpass-doc (1.09-r1)<br>(694/773) Installing judy (1.0.5-r1)<br>(695/773) Installing judy-doc (1.0.5-r1)<br>(696/773) Installing liblksctp (1.0.19-r1)<br>(697/773) Installing stress-ng (0.14.00-r0)<br>(698/773) Installing stress-ng-doc (0.14.00-r0)<br>(699/773) Installing sudo (1.9.12_p2-r1)<br>(700/773) Installing sudo-doc (1.9.12_p2-r1)<br>(701/773) Installing syslinux (6.04_pre1-r11)<br>(702/773) Installing syslinux-doc (6.04_pre1-r11)<br>(703/773) Installing texinfo (7.0.1-r0)<br>(704/773) Installing texinfo-doc (7.0.1-r0)<br>(705/773) Installing udisks2-bash-completion (2.9.4-r1)<br>(706/773) Installing unzip (6.0-r13)<br>(707/773) Installing unzip-doc (6.0-r13)<br>(708/773) Installing hwdata-usb (0.364-r0)<br>(709/773) Installing usbutils (015-r0)<br>(710/773) Installing usbutils-doc (015-r0)<br>(711/773) Installing libeconf-doc (0.4.7-r0)<br>(712/773) Installing util-linux-doc (2.38.1-r1)<br>(713/773) Installing libcap-ng-doc (0.8.3-r1)<br>(714/773) Installing util-linux-bash-completion (2.38.1-r1)<br>(715/773) Installing util-linux-login (2.38.1-r1)<br>(716/773) Installing util-linux-login-doc (2.38.1-r1)<br>(717/773) Installing s6-ipcserver (2.11.1.2-r0)<br>(718/773) Installing utmps (0.1.2.0-r1)<br>Executing utmps-0.1.2.0-r1.pre-install<br>(719/773) Installing utmps-doc (0.1.2.0-r1)<br>(720/773) Installing utmps-openrc (0.1.2.0-r1)<br>(721/773) Installing vifm (0.12.1-r1)<br>(722/773) Installing vifm-doc (0.12.1-r1)<br>(723/773) Installing vifm-fish-completion (0.12.1-r1)<br>(724/773) Installing vifm-bash-completion (0.12.1-r1)<br>(725/773) Installing vifm-zsh-completion (0.12.1-r1)<br>(726/773) Installing xxd (9.0.0999-r0)<br>(727/773) Installing vim (9.0.0999-r0)<br>(728/773) Installing vim-doc (9.0.0999-r0)<br>(729/773) Installing vsftpd (3.0.5-r2)<br>Executing vsftpd-3.0.5-r2.pre-install<br>(730/773) Installing vsftpd-doc (3.0.5-r2)<br>(731/773) Installing vsftpd-openrc (3.0.5-r2)<br>(732/773) Installing wget (1.21.3-r2)<br>(733/773) Installing wget-doc (1.21.3-r2)<br>(734/773) Installing whois (5.5.14-r0)<br>(735/773) Installing whois-doc (5.5.14-r0)<br>(736/773) Installing qt5-qtbase-sqlite (5.15.6_git20221010-r0)<br>(737/773) Installing llvm15-libs (15.0.7-r0)<br>(738/773) Installing clang15-libclang (15.0.7-r0)<br>(739/773) Installing qt5-qttools (5.15.6_git20220907-r1)<br>(740/773) Installing xca (2.4.0-r2)<br>(741/773) Installing xca-doc (2.4.0-r2)<br>(742/773) Installing inih (56-r0)<br>(743/773) Installing userspace-rcu (0.13.2-r0)<br>(744/773) Installing userspace-rcu-doc (0.13.2-r0)<br>(745/773) Installing xfsprogs (6.0.0-r0)<br>(746/773) Installing xfsprogs-doc (6.0.0-r0)<br>(747/773) Installing libburn (1.5.4-r2)<br>(748/773) Installing libburn-doc (1.5.4-r2)<br>(749/773) Installing libisofs (1.5.4-r2)<br>(750/773) Installing libisoburn (1.5.4-r2)<br>(751/773) Installing libisoburn-doc (1.5.4-r2)<br>(752/773) Installing xorriso (1.5.4-r2)<br>(753/773) Installing gobject-introspection (1.74.0-r1)<br>(754/773) Installing gobject-introspection-doc (1.74.0-r1)<br>(755/773) Installing py3-gobject3 (3.42.2-r0)<br>(756/773) Installing py3-xdg (0.28-r0)<br>(757/773) Installing zim (0.75.1-r0)<br>(758/773) Installing zim-doc (0.75.1-r0)<br>(759/773) Installing zip (3.0-r10)<br>(760/773) Installing zip-doc (3.0-r10)<br>(761/773) Installing zsh (5.9-r0)<br>Executing zsh-5.9-r0.post-install<br>(762/773) Installing gcc-zsh-completion (5.9-r0)<br>(763/773) Installing pass-zsh-completion (1.7.4-r1)<br>(764/773) Installing apk-tools-zsh-completion (2.12.10-r1)<br>(765/773) Installing openrc-zsh-completion (0.45.2-r7)<br>(766/773) Installing zsh-pcre (5.9-r0)<br>(767/773) Installing py3-pip-zsh-completion (22.3.1-r1)<br>(768/773) Installing git-zsh-completion (5.9-r0)<br>(769/773) Installing zsh-doc (5.9-r0)<br>(770/773) Installing lynx-zsh-completion (5.9-r0)<br>(771/773) Installing curl-zsh-completion (7.88.1-r1)<br>(772/773) Installing zstd (1.5.5-r0)<br>(773/773) Installing zstd-doc (1.5.5-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing ca-certificates-20220614-r4.trigger<br>Executing glib-2.74.6-r0.trigger<br>Executing shared-mime-info-2.2-r2.trigger<br>Executing gdk-pixbuf-2.42.10-r0.trigger<br>Executing dbus-1.14.4-r0.trigger<br>Executing gtk-update-icon-cache-3.24.36-r0.trigger<br>Executing cracklib-2.9.8-r0.trigger<br>Executing kmod-30-r1.trigger<br>Executing mkinitfs-3.7.0-r1.trigger<br>==> initramfs: creating /boot/initramfs-lts<br>Executing grub-2.06-r7.trigger<br>Generating grub configuration file ...<br>sort: fflush failed: 'standard output': Broken pipe<br>sort: write error<br>Found linux image: /boot/vmlinuz-virt<br>Found initrd image: /boot/initramfs-virt<br>fgrep: warning: fgrep is obsolescent; using grep -F<br>Found linux image: /boot/vmlinuz-lts<br>Found initrd image: /boot/initramfs-lts<br>fgrep: warning: fgrep is obsolescent; using grep -F<br>Warning: os-prober will not be executed to detect other bootable partitions.<br>Systems on them will not be added to the GRUB boot configuration.<br>Check GRUB_DISABLE_OS_PROBER documentation entry.<br>done<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>Executing syslinux-6.04_pre1-r11.trigger<br>WARNING: Root device is not specified in /etc/update-extlinux.conf.<br>/boot is device /dev/vda1<br>extlinux: no previous syslinux boot sector found<br>1 error; 1701 MiB in 865 packages<br>localhost:~#<br>localhost:~# date<br>Fri Apr 14 10:36:27 UTC 2023<br>localhost:~#<br>localhost:~# apk del inetutils-telnet inetutils-ftp<br>(1/4) Purging inetutils-ftp-doc (2.4-r0)<br>(2/4) Purging inetutils-ftp (2.4-r0)<br>(3/4) Purging inetutils-telnet-doc (2.4-r0)<br>(4/4) Purging inetutils-telnet (2.4-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br>OK: 1700 MiB in 861 packages<br>localhost:~#<br>localhost:~# apk add inetutils-telnet<br>(1/2) Installing inetutils-telnet (2.4-r0)<br>(2/2) Installing inetutils-telnet-doc (2.4-r0)<br>Executing busybox-1.35.0-r29.trigger<br>Executing mandoc-apropos-1.14.6-r6.trigger<br><br>OK: 1701 MiB in 863 packages<br>localhost:~#<br>localhost:~# cat /boot/grub/grub.cfg<br>#<br># DO NOT EDIT THIS FILE<br>#<br># It is automatically generated by grub-mkconfig using templates<br># from /etc/grub.d and settings from /etc/default/grub<br>#<br><br>### BEGIN /etc/grub.d/00_header ###<br>if [ -s $prefix/grubenv ]; then<br>  load_env<br>fi<br>if [ "${next_entry}" ] ; then<br>   set default="${next_entry}"<br>   set next_entry=<br>   save_env next_entry<br>   set boot_once=true<br>else<br>   set default="0"<br>fi<br><br>if [ x"${feature_menuentry_id}" = xy ]; then<br>  menuentry_id_option="--id"<br>else<br>  menuentry_id_option=""<br>fi<br><br>export menuentry_id_option<br><br>if [ "${prev_saved_entry}" ]; then<br>  set saved_entry="${prev_saved_entry}"<br>  save_env saved_entry<br>  set prev_saved_entry=<br>  save_env prev_saved_entry<br>  set boot_once=true<br>fi<br><br>function savedefault {<br>  if [ -z "${boot_once}" ]; then<br>    saved_entry="${chosen}"<br>    save_env saved_entry<br>  fi<br>}<br><br>function load_video {<br>  if [ x$feature_all_video_module = xy ]; then<br>    insmod all_video<br>  else<br>    insmod efi_gop<br>    insmod efi_uga<br>    insmod ieee1275_fb<br>    insmod vbe<br>    insmod vga<br>    insmod video_bochs<br>    insmod video_cirrus<br>  fi<br>}<br><br>if [ x$feature_default_font_path = xy ] ; then<br>   font=unicode<br>else<br>insmod part_msdos<br>insmod ext2<br>search --no-floppy --fs-uuid --set=root ada017ef-3181-40be-8e14-f45c49e00f3a<br>    font="/usr/share/grub/unicode.pf2"<br>fi<br><br>if loadfont $font ; then<br>  set gfxmode=auto<br>  load_video<br>  insmod gfxterm<br>fi<br>terminal_output gfxterm<br>if [ x$feature_timeout_style = xy ] ; then<br>  set timeout_style=menu<br>  set timeout=2<br># Fallback normal timeout code in case the timeout_style feature is<br># unavailable.<br>else<br>  set timeout=2<br>fi<br>### END /etc/grub.d/00_header ###<br><br>### BEGIN /etc/grub.d/10_linux ###<br>menuentry 'Alpine Linux v3.17, with Linux virt' --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-virt-advanced-ada017ef-3181-40be-8e14-f45c49e00f3a' {<br>        load_video<br>        insmod gzio<br>        insmod part_msdos<br>        insmod ext2<br>        search --no-floppy --fs-uuid --set=root 9adeb32c-979a-47e7-b034-cd800a81e867<br>        echo    'Loading Linux virt ...'<br>        linux   /vmlinuz-virt root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro  modules=sd-mod,usb-storage,ext4 quiet modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>        echo    'Loading initial ramdisk ...'<br>        initrd  /initramfs-virt<br>}<br>menuentry 'Alpine Linux v3.17, with Linux lts' --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-lts-advanced-ada017ef-3181-40be-8e14-f45c49e00f3a' {<br>        load_video<br>        insmod gzio<br>        insmod part_msdos<br>        insmod ext2<br>        search --no-floppy --fs-uuid --set=root 9adeb32c-979a-47e7-b034-cd800a81e867<br>        echo    'Loading Linux lts ...'<br>        linux   /vmlinuz-lts root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro  modules=sd-mod,usb-storage,ext4 quiet modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>        echo    'Loading initial ramdisk ...'<br>        initrd  /initramfs-lts<br>}<br><br>### END /etc/grub.d/10_linux ###<br><br>### BEGIN /etc/grub.d/20_linux_xen ###<br><br>### END /etc/grub.d/20_linux_xen ###<br><br>### BEGIN /etc/grub.d/30_os-prober ###<br>### END /etc/grub.d/30_os-prober ###<br><br>### BEGIN /etc/grub.d/30_uefi-firmware ###<br>### END /etc/grub.d/30_uefi-firmware ###<br><br>### BEGIN /etc/grub.d/40_custom ###<br># This file provides an easy way to add custom menu entries.  Simply type the<br># menu entries you want to add after this comment.  Be careful not to change<br># the 'exec tail' line above.<br>### END /etc/grub.d/40_custom ###<br><br>### BEGIN /etc/grub.d/41_custom ###<br>if [ -f  ${config_directory}/custom.cfg ]; then<br>  source ${config_directory}/custom.cfg<br>elif [ -z "${config_directory}" -a -f  $prefix/custom.cfg ]; then<br>  source $prefix/custom.cfg<br>fi<br>### END /etc/grub.d/41_custom ###<br>localhost:~#<br>localhost:~#<br>localhost:~#<br>localhost:~# cp -iv /etc/default/grub /root/backup<br>'/etc/default/grub' -> '/root/backup/grub'<br>localhost:~#<br>localhost:~# cp -iv /etc/update-extlinux.conf /root/backup<br>'/etc/update-extlinux.conf' -> '/root/backup/update-extlinux.conf'<br>localhost:~#<br>localhost:~# cat /etc/default/grub<br>GRUB_TIMEOUT=2<br>GRUB_DISABLE_SUBMENU=y<br>GRUB_DISABLE_RECOVERY=true<br>GRUB_CMDLINE_LINUX_DEFAULT="modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4"<br>localhost:~#<br>localhost:~#<br>localhost:~# sed -i -e 's/^GRUB_TIMEOUT/# GRUB_TIMEOUT/' /etc/default/grub<br>localhost:~#<br>localhost:~# sed -i -e 's/^GRUB_DISABLE_SUBMENU/# GRUB_DISABLE_SUBMENU/' /etc/de<br>fault/grub<br>localhost:~#<br>localhost:~# sed -i -e 's/^GRUB_CMDLINE_LINUX_DEFAULT/# GRUB_CMDLINE_LINUX_DEFAULT/' /etc/default/grub<br>localhost:~#<br>localhost:~# echo 'GRUB_TERMINAL="serial console"' >> /etc/default/grub<br>localhost:~#<br>localhost:~# echo 'GRUB_SERIAL_COMMAND="serial --speed=115200"' >> /etc/default/<br>grub<br>localhost:~# echo 'GRUB_TIMEOUT=-1' >> /etc/default/grub<br>localhost:~#<br>localhost:~# echo 'GRUB_DISABLE_SUBMENU=n' >> /etc/default/grub<br>localhost:~# cat /etc/default/grub<br># GRUB_TIMEOUT=2<br># GRUB_DISABLE_SUBMENU=y<br>GRUB_DISABLE_RECOVERY=true<br># GRUB_CMDLINE_LINUX_DEFAULT="modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4"<br>GRUB_TERMINAL="serial console"<br>GRUB_SERIAL_COMMAND="serial --speed=115200"<br>GRUB_TIMEOUT=-1<br>GRUB_DISABLE_SUBMENU=n<br>localhost:~#<br>localhost:~# cat /etc/update-extlinux.conf<br># configuration for extlinux config builder<br><br># overwrite<br># Overwrite current /boot/extlinux.conf. If this is not '1' we will only<br># write to /boot/extlinux.conf.new<br>overwrite=1<br><br># vesa_menu<br># use fancy vesa menu (vesamenu.c32) menus, won't work with serial<br>vesa_menu=0<br><br># default_kernel_opts<br># default kernel options<br>default_kernel_opts=quiet<br><br># modules<br># modules which should be loaded before pivot_root<br>modules=sd-mod,usb-storage,ext4<br><br># root<br># root device - if not specified, will be guessed using<br># blkid -o export /dev/root<br>root=<br><br># verbose<br># if set to non-zero, update-extlinux will be a lot more verbose.<br>verbose=0<br><br># hidden<br># if set to non-zero, the boot menu will be hidden by default.<br>hidden=1<br><br># timeout<br># number of seconds to wait before booting default<br>timeout=1<br><br># default<br># default kernel to boot<br>default=lts<br><br># serial_port<br># serial port number - if not specified, serial console will be disabled<br>serial_port=<br><br># serial_baud<br># the baudrate for the serial port. Will use 115200 if unset<br>serial_baud=115200<br><br># xen_opts<br># options to hand to xen hypervisor, useful ones are:<br>#    dom0_mem=384M (give domain-0 environment 384M ram)<br>xen_opts=dom0_mem=384M<br><br># if you copy /usr/share/syslinux/reboot.c32 to /boot/, a menu entry<br># will be auto-generated for it<br><br># if you copy hdt.c32, libgpl.c32, and libmenu.c32 from /usr/share/syslinux/<br># to /boot/, a menu entry will be auto-generated for HDT<br><br># if you download and install /boot/memtest, then if HDT is present it<br># will use it, else a separate menu entry will be auto-generated for<br># memtest<br><br># optional password<br># you can generate a SHA512 password using: mkpasswd<br>#<br># if you assign a password, you should make this file world-unreadable<br>#<br># if a password is assigned, the menu entries can't be edited at boot<br># time, and HDT if present is password-protected<br>#<br># you can also include "MENU PASSWD" in any custom entries you have in<br># /etc/update-extlinux.d/<br>password=''<br>localhost:~#<br>localhost:~# sed -i -e 's/^default=lts/default=virt/' /etc/update-extlinux.conf<br>localhost:~#<br>localhost:~# cat /etc/update-extlinux.conf|grep -E '^default|^modules'<br>default_kernel_opts=quiet<br>modules=sd-mod,usb-storage,ext4<br>default=virt<br>localhost:~#<br>localhost:~# grep GRUB_CMDLINE_LINUX_DEFAULT /etc/default/grub<br># GRUB_CMDLINE_LINUX_DEFAULT="modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4"<br>localhost:~#<br>localhost:~#<br>localhost:~# sed -i -e 's/default_kernel_opts=quiet/default_kernel_opts="console=tty0 console=ttyS0,115200n8 rootfstype=ext4"/' /etc/update-extlinux.conf                                                              localhost:~#<br>localhost:~# grep -E '^default|^modules' /etc/update-extlinux.conf<br>default_kernel_opts="console=tty0 console=ttyS0,115200n8 rootfstype=ext4"<br>modules=sd-mod,usb-storage,ext4<br>default=virt<br>localhost:~#<br>localhost:~# grub-mkconfig -o /boot/grub/grub.cfg<br>Generating grub configuration file ...<br>Found linux image: /boot/vmlinuz-virt<br>Found initrd image: /boot/initramfs-virt<br>fgrep: warning: fgrep is obsolescent; using grep -F<br>Found linux image: /boot/vmlinuz-lts<br>Found initrd image: /boot/initramfs-lts<br>fgrep: warning: fgrep is obsolescent; using grep -F<br>Warning: os-prober will not be executed to detect other bootable partitions.<br>Systems on them will not be added to the GRUB boot configuration.<br>Check GRUB_DISABLE_OS_PROBER documentation entry.<br>done<br>localhost:~#<br>localhost:~# cat /boot/grub/grub.cfg<br>#<br># DO NOT EDIT THIS FILE<br>#                                                                     <br># It is automatically generated by grub-mkconfig using templates<br># from /etc/grub.d and settings from /etc/default/grub                <br>#<br>### BEGIN /etc/grub.d/00_header ###<br>if [ -s $prefix/grubenv ]; then                                         <br>load_env<br>fi                                                                    <br>if [ "${next_entry}" ] ; then                                            <br>set default="${next_entry}"<br>   set next_entry=                                                       <br>   save_env next_entry                                                   <br>   set boot_once=true<br>else                                                                     <br>set default="0"<br>fi                                                                    <br>if [ x"${feature_menuentry_id}" = xy ]; then<br>  menuentry_id_option="--id"<br>else<br>  menuentry_id_option=""                                              <br>  fi<br>export menuentry_id_option<br>if [ "${prev_saved_entry}" ]; then<br>  set saved_entry="${prev_saved_entry}"                                 <br>  save_env saved_entry                                                  <br>  set prev_saved_entry=<br>  save_env prev_saved_entry                                             <br>  set boot_once=true<br>fi<br>function savedefault {<br>  if [ -z "${boot_once}" ]; then<br>    saved_entry="${chosen}"                                               <br>    save_env saved_entry<br>  fi                                                                  <br>  }<br><br>function load_video {                                                   <br>if [ x$feature_all_video_module = xy ]; then<br>    insmod all_video<br>  else<br>    insmod efi_gop<br>    insmod efi_uga<br>    insmod ieee1275_fb                                                    <br>    insmod vbe<br>    insmod vga<br>    insmod video_bochs<br>    insmod video_cirrus<br>  fi<br>}<br><br>serial --speed=115200                                                 <br>terminal_input serial console<br>terminal_output serial console<br>if [ x$feature_timeout_style = xy ] ; then<br>  set timeout_style=menu<br>  set timeout=-1                                                      <br>  # Fallback normal timeout code in case the timeout_style feature is<br># unavailable.                                                        <br>else<br>  set timeout=-1<br>fi<br>### END /etc/grub.d/00_header ###                                     <br>### BEGIN /etc/grub.d/10_linux ###                                    <br>menuentry 'Alpine Linux v3.17' --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-ada017ef-3181-40be-8e14-f45c49e00f3a' {                                                                     load_video<br>        insmod gzio                                                           <br>        insmod part_msdos<br>        insmod ext2<br>        search --no-floppy --fs-uuid --set=root 9adeb32c-979a-47e7-b034-cd800a81e867<br>        echo    'Loading Linux virt ...'                                      <br>        linux   /vmlinuz-virt root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro  modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>        echo    'Loading initial ramdisk ...'<br>        initrd  /initramfs-virt<br>}<br>submenu 'Advanced options for Alpine Linux v3.17' $menuentry_id_option 'gnulinux-advanced-ada017ef-3181-40be-8e14-f45c49e00f3a' {<br>        menuentry 'Alpine Linux v3.17, with Linux virt' --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-virt-advanced-ada017ef-3181-40be-8e14-f45c49e00f3a' {<br>                load_video                                                            <br>                insmod gzio<br>                insmod part_msdos                                                     <br>                insmod ext2<br>                search --no-floppy --fs-uuid --set=root 9adeb32c-979a-47e7-b034-cd800a81e867                                                                echo    'Loading Linux virt ...'<br>                linux   /vmlinuz-virt root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro  modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>                echo    'Loading initial ramdisk ...'<br>                initrd  /initramfs-virt<br>        }<br>        menuentry 'Alpine Linux v3.17, with Linux lts' --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-lts-advanced-ada017ef-3181-40be-8e14-f45c49e00f3a' {<br>                load_video<br>                insmod gzio<br>                insmod part_msdos<br>                insmod ext2                                                           <br>                search --no-floppy --fs-uuid --set=root 9adeb32c-979a-47e7-b034-cd800a81e867<br>                echo    'Loading Linux lts ...'<br>                linux   /vmlinuz-lts root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro  modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4                                                      <br>                echo    'Loading initial ramdisk ...'<br>                initrd  /initramfs-lts<br>        }<br>}                                                                     <br>### END /etc/grub.d/10_linux ###<br><br>### BEGIN /etc/grub.d/20_linux_xen ###<br><br>### END /etc/grub.d/20_linux_xen ###                                  <br>### BEGIN /etc/grub.d/30_os-prober ###<br>### END /etc/grub.d/30_os-prober ###<br><br>### BEGIN /etc/grub.d/30_uefi-firmware ###<br>### END /etc/grub.d/30_uefi-firmware ###<br><br>### BEGIN /etc/grub.d/40_custom ###                                   <br># This file provides an easy way to add custom menu entries.  Simply type the                                                               # menu entries you want to add after this comment.  Be careful not to change<br># the 'exec tail' line above.<br>### END /etc/grub.d/40_custom ###<br><br>### BEGIN /etc/grub.d/41_custom ###<br>if [ -f  ${config_directory}/custom.cfg ]; then<br>  source ${config_directory}/custom.cfg<br>elif [ -z "${config_directory}" -a -f  $prefix/custom.cfg ]; then       <br>source $prefix/custom.cfg<br>fi<br>### END /etc/grub.d/41_custom ###<br>localhost:~#<br>localhost:~#                                                          <br>localhost:~# echo $SHELL<br>/bin/ash<br>localhost:~#<br>localhost:~# chsh -s /bin/bash root                                   <br>Password:<br>localhost:~#                                                          <br>localhost:~# chsh -s /bin/bash test<br>Password:<br>localhost:~#<br>localhost:~# mkdir /mnt/9p-host<br>localhost:~#<br>localhost:~# mkdir /mnt/disk1<br>localhost:~#<br>localhost:~# export SUDO_EDITOR=nano<br>localhost:~#<br>localhost:~# export EDITOR=nano<br>localhost:~#<br>localhost:~# grep wheel /etc/sudoers<br>## Uncomment to allow members of group wheel to execute any command<br># %wheel ALL=(ALL:ALL) ALL<br># %wheel ALL=(ALL:ALL) NOPASSWD: ALL<br>localhost:~#<br>localhost:~# grep wheel /etc/sudoers<br>## Uncomment to allow members of group wheel to execute any command<br>%wheel ALL=(ALL:ALL) ALL<br># %wheel ALL=(ALL:ALL) NOPASSWD: ALL<br>localhost:~#<br>localhost:~#<br>localhost:~# mkdir -p /var/www/localhost/htdocs /var/log/lighttpd /var<br>/lib/lighttpd<br>localhost:~#<br>localhost:~# chown  -R lighttpd:lighttpd /var/log/lighttpd /var/lib/li<br>ghttpd /var/www/localhost/htdocs<br>localhost:~#<br>localhost:~# ls -al  /var/www/localhost/htdocs<br>total 12<br>drwxr-xr-x 2 lighttpd lighttpd 4096 Apr 14 09:39 .<br>drwxr-xr-x 4 root     root     4096 Apr 14 09:39 ..<br>-rw-r--r-- 1 lighttpd lighttpd   45 Mar  7 19:33 index.html<br>localhost:~#<br>localhost:~# touch /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# chown root:lighttpd /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# ls -l /etc/lighttpd/webdav-htpasswd-passwd<br>-rw-r--r-- 1 root lighttpd 0 Apr 14 09:55 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# stat /etc/lighttpd/webdav-htpasswd-passwd<br>  File: /etc/lighttpd/webdav-htpasswd-passwd<br>  Size: 0               Blocks: 0          IO Block: 4096   regular empty file<br>Device: 253,3   Inode: 52583       Links: 1<br>Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (  105/lighttpd)<br>Access: 2023-04-14 09:55:13.810000000 +0000<br>Modify: 2023-04-14 09:55:13.810000000 +0000<br>Change: 2023-04-14 09:55:27.960000000 +0000<br> Birth: -<br>localhost:~#<br>localhost:~# chmod 640 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# ls -l /etc/lighttpd/webdav-htpasswd-passwd<br>-rw-r----- 1 root lighttpd 0 Apr 14 09:55 /etc/lighttpd/webdav-htpasswd-passwd<br>localhost:~#<br>localhost:~# stat /etc/lighttpd/webdav-htpasswd-passwd<br>  File: /etc/lighttpd/webdav-htpasswd-passwd<br>  Size: 0               Blocks: 0          IO Block: 4096   regular empty file<br>Device: 253,3   Inode: 52583       Links: 1<br>Access: (0640/-rw-r-----)  Uid: (    0/    root)   Gid: (  105/lighttpd)<br>Access: 2023-04-14 09:55:13.810000000 +0000<br>Modify: 2023-04-14 09:55:13.810000000 +0000<br>Change: 2023-04-14 09:56:14.200000000 +0000<br> Birth: -<br>localhost:~#<br>localhost:~# htpasswd -m /etc/lighttpd/webdav-htpasswd-passwd test1<br>New password:<br>Re-type new password:<br>Adding password for user test1<br>localhost:~#<br>localhost:~# cp -pi /etc/lighttpd/webdav.conf /root/backup<br>cp: cannot stat '/etc/lighttpd/webdav.conf': No such file or directory<br>localhost:~#<br>localhost:~# cat << 'END-OF-WEBDAV-CONF' > /etc/lighttpd/webdav.conf<br>> server.port = 15081<br>> server.upload-dirs = ( "/tmp" )<br>> server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_fi<br>le")<br>> alias.url = ( "/webdav" => "/mnt/disk1" )<br>> $HTTP["url"] =~ "^/webdav($|/)" {<br>>     webdav.activate = "enable"<br>>     webdav.is-readonly = "disable"<br>>     webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"<br>>     auth.backend = "htpasswd"<br>>     auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-<br>passwd"<br>>     auth.require  = ("" => ("method" => "basic","realm" => "realm-we<br>bdav","require" => "valid-user"))<br>>   }<br>> END-OF-WEBDAV-CONF<br>localhost:~#<br>localhost:~# cat /etc/lighttpd/webdav.conf<br>server.port = 15081<br>server.upload-dirs = ( "/tmp" )<br>server.modules += ("mod_alias","mod_auth","mod_webdav","mod_authn_file")<br>alias.url = ( "/webdav" => "/mnt/disk1" )<br>$HTTP["url"] =~ "^/webdav($|/)" {<br>    webdav.activate = "enable"<br>    webdav.is-readonly = "disable"<br>    webdav.sqlite-db-name = "/var/lib/lighttpd/webdav-lock.db"<br>    auth.backend = "htpasswd"<br>    auth.backend.htpasswd.userfile = "/etc/lighttpd/webdav-htpasswd-passwd"<br>    auth.require  = ("" => ("method" => "basic","realm" => "realm-webdav","require" => "valid-user"))<br>  }<br>localhost:~#<br>localhost:~# cp -pi /etc/lighttpd/lighttpd.conf /root/backup<br>localhost:~#<br>localhost:~#<br>localhost:~# echo 'include "webdav.conf"' >> /etc/lighttpd/lighttpd.conf<br>localhost:~#<br>localhost:~#<br>localhost:~# lighttpd -tt -f /etc/lighttpd/lighttpd.conf<br>localhost:~#<br>localhost:~#<br>localhost:~# rc-update add lighttpd default<br> * service lighttpd added to runlevel default<br>localhost:~#<br>localhost:~# passwd --delete --expire root<br>passwd: password changed.<br>localhost:~#<br>localhost:~# passwd --delete --expire test<br>passwd: password changed.<br>localhost:~#<br>localhost:~# ls -al /root<br>total 24<br>drwx------  3 root root 4096 Apr 14 11:46 .<br>drwxr-xr-x 22 root root 4096 Apr 14 09:10 ..<br>-rw-------  1 root root 6050 Apr 14 11:50 .ash_history<br>-rw-------  1 root root   99 Apr 14 11:46 .bash_history<br>drwxr-xr-x  2 root root 4096 Apr 14 11:19 backup<br>localhost:~#<br>localhost:~# ls -al /home/test<br>total 8<br>drwxr-sr-x 2 test test 4096 Apr 14 11:46 .<br>drwxr-xr-x 3 root root 4096 Apr 14 08:49 ..<br>localhost:~#<br>localhost:~# rm -i /etc/ssh/ssh*key<br>rm: remove regular file '/etc/ssh/ssh_host_ecdsa_key'? y<br>rm: remove regular file '/etc/ssh/ssh_host_ed25519_key'? y<br>rm: remove regular file '/etc/ssh/ssh_host_rsa_key'? y<br>localhost:~#<br>localhost:~# rm -i /root/*history*<br>rm: cannot remove '/root/*history*': No such file or directory<br>localhost:~#<br>localhost:~# rm -i /root/.*history*<br>rm: remove regular file '/root/.ash_history'? y<br>rm: remove regular file '/root/.bash_history'? y<br>localhost:~#<br>localhost:~# rm -ir /root/backup<br>rm: descend into directory '/root/backup'? y<br>rm: remove regular file '/root/backup/modules'? y<br>rm: remove regular file '/root/backup/update-extlinux.conf'? y<br>rm: remove regular file '/root/backup/repositories'? y<br>rm: remove regular file '/root/backup/grub'? y<br>rm: remove regular file '/root/backup/lighttpd.conf'? y<br>rm: remove directory '/root/backup'? y<br>localhost:~# poweroff<br>localhost:~#  * Caching service dependencies ... [ ok ]<br> * Stopping sshd ... [ ok ]<br> * Saving random number generator seed ... * Seeding 256 bits and<br> crediting<br> * Saving 256 bits of creditable seed for next boot<br> [ ok ]<br> * Stopping busybox crond ... [ ok ]<br> * Stopping busybox syslog ... [ ok ]<br> * Stopping busybox acpid ... [ ok ]<br> * Unmounting loop devices<br> * Unmounting filesystems<br> *   Unmounting /mnt/repo ... [ ok ]<br> *   Unmounting /tmp ... [ ok ]<br> *   Unmounting /boot ... [ ok ]<br> * Deactivating swap devices ... [ ok ]<br> * Setting hardware clock using the system clock [UTC] ... [ ok ]<br> * Stopping busybox mdev ... [ ok ]<br> * Terminating remaining processes ...[10426.117825] reboot: Power down<br>~ $ cd $HOME<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br>~ $ env<br>SHELL=/data/data/com.termux/files/usr/bin/bash<br>COLORTERM=truecolor<br>HISTCONTROL=ignoreboth<br>VMDISK=/storage/emulated/0/Download/qemu-test/vm-template-grub.raw<br>PREFIX=/data/data/com.termux/files/usr<br>JAVA_HOME=/data/data/com.termux/files/usr/opt/openjdk<br>TERMUX_IS_DEBUGGABLE_BUILD=1<br>TERMUX_MAIN_PACKAGE_FORMAT=debian<br>PWD=/data/data/com.termux/files/home<br>NINE_P_DIR=/storage/emulated/0/Download/qemu-test<br>TERMUX_VERSION=0.118.0<br>EXTERNAL_STORAGE=/sdcard<br>LD_PRELOAD=/data/data/com.termux/files/usr/lib/libtermux-exec.so<br>TERMUX_API_VERSION=0.50.1<br>HOME=/data/data/com.termux/files/home<br>LANG=en_US.UTF-8<br>TERMUX_APK_RELEASE=GITHUB<br>DEX2OATBOOTCLASSPATH=/apex/com.android.art/javalib/core-oj.jar:/apex/com.android.art/javalib/core-libart.jar:/apex/com.android.art/javalib/core-icu4j.jar:/apex/com.android.art/javalib/okhttp.jar:/apex/com.android.art/javalib/bouncycastle.jar:/apex/com.android.art/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/framework-atb-backward-compatibility.jar:/system/framework/mediatek-telephony-base.jar:/system/framework/mediatek-telephony-common.jar:/system/framework/mediatek-common.jar:/system/framework/mediatek-framework.jar:/system/framework/mediatek-ims-common.jar:/system/framework/mediatek-ims-base.jar:/system/framework/mediatek-telecom-common.jar:/system/framework/OPCommonTelephony.jar<br>TMPDIR=/data/data/com.termux/files/usr/tmp<br>ANDROID_DATA=/data<br>TERM=xterm-256color<br>ANDROID_I18N_ROOT=/apex/com.android.i18n<br>SHLVL=1<br>ANDROID_ROOT=/system<br>BOOTCLASSPATH=/apex/com.android.art/javalib/core-oj.jar:/apex/com.android.art/javalib/core-libart.jar:/apex/com.android.art/javalib/core-icu4j.jar:/apex/com.android.art/javalib/okhttp.jar:/apex/com.android.art/javalib/bouncycastle.jar:/apex/com.android.art/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/framework-atb-backward-compatibility.jar:/system/framework/mediatek-telephony-base.jar:/system/framework/mediatek-telephony-common.jar:/system/framework/mediatek-common.jar:/system/framework/mediatek-framework.jar:/system/framework/mediatek-ims-common.jar:/system/framework/mediatek-ims-base.jar:/system/framework/mediatek-telecom-common.jar:/system/framework/OPCommonTelephony.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar:/apex/com.android.mediaprovider/javalib/framework-mediaprovider.jar:/apex/com.android.os.statsd/javalib/framework-statsd.jar:/apex/com.android.permission/javalib/framework-permission.jar:/apex/com.android.sdkext/javalib/framework-sdkextensions.jar:/apex/com.android.wifi/javalib/framework-wifi.jar:/apex/com.android.tethering/javalib/framework-tethering.jar<br>ANDROID_TZDATA_ROOT=/apex/com.android.tzdata<br>ISO=/storage/emulated/0/Download/qemu-test/alpine-virt-3.17.3-x86_64.iso<br>TERMUX_APP_PID=3606<br>PATH=/data/data/com.termux/files/usr/bin<br>ANDROID_ART_ROOT=/apex/com.android.art<br>GID_NINE_P_DIR=Access: (0770/drwxrwx---)  Uid: (    0/    root)   Gid: ( 9997/everybody)<br>OLDPWD=/data/data/com.termux/files/home<br>_=/data/data/com.termux/files/usr/bin/env<br>~ $<br>~ $ cp -iv $VMDISK $NINE_P_DIR/vm-linux-grub.raw<br>'/storage/emulated/0/Download/qemu-test/vm-template-grub.raw' -> '/storage/emulated/0/Download/qemu-test/vm-linux-grub.raw'<br>~ $<br>~ $ export VMDISK=$NINE_P_DIR/vm-linux-grub.raw<br>~ $<br>~ $<br>~ $ qemu-system-x86_64  -m 1024M  -machine pc  -smp 4  -nographic  -device virtio-rng-pci  -serial mon:stdio  -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=tcp::15022-:22,hostfwd=::15081-:15081  -drive if=none,file=$VMDISK,format=raw,id=drive2 -device virtio-blk-pci,drive=drive2,id=virtblk2,bootindex=1  -drive if=none,file=/storage/emulated/0/Download/50gb.ext,format=raw,id=drive3,readonly=on -device virtio-blk-pci,drive=drive3,id=virtblk3  -virtfs local,security_model=none,id=host,mount_tag=host,path=$NINE_P_DIR<br><br><br>Loading Linux virt ...Loadi<br>.           ial ramdisk ..<br>.oading initial ramdisk ...Loading init<br>[    0.000000] Linux version 5.15.106-0-virt (buildozer@build-3-17-x86_64) (gcc (Alpine 12.2.1_git20220924-r4) 12.2.1 20220924, GNU ld (GNU Binutils) 2.39) #1-Alpine SMP Wed, 05 Apr 2023 10:48:45 +0000<br>[00:00:00.000] [    0.000000] Command line: BOOT_IMAGE=/vmlinuz-virt root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>[00:00:00.005] [    0.000000] x86/fpu: x87 FPU will use FXSAVE<br>[00:00:00.007] [    0.000000] signal: max sigframe size: 1440<br>[00:00:00.008] [    0.000000] BIOS-provided physical RAM map:<br>[00:00:00.009] [    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable<br>[00:00:00.010] [    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved                                               [00:00:00.012] [    0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved                                               [00:00:00.013] [    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000003ffd9fff] usable                                                 [00:00:00.015] [    0.000000] BIOS-e820: [mem 0x000000003ffda000-0x000000003fffffff] reserved                                               [00:00:00.017] [    0.000000] BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved                                               [00:00:00.019] [    0.000000] BIOS-e820: [mem 0x000000fd00000000-0x000000ffffffffff] reserved                                               [00:00:00.021] [    0.000000] NX (Execute Disable) protection: active [00:00:00.022] [    0.000000] SMBIOS 2.8 present.                     [00:00:00.023] [    0.000000] DMI: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.16.1-0-g3208b098f51a-prebuilt.qemu.org 04/01/2014<br>[00:00:00.026] [    0.000000] tsc: Fast TSC calibration failed<br>[00:00:00.027] [    0.000000] last_pfn = 0x3ffda max_arch_pfn = 0x400000000<br>[00:00:00.029] [    0.000000] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT<br>[00:00:00.031] [    0.000000] RAMDISK: [mem 0x37293000-0x37940fff]<br>[00:00:00.032] [    0.000000] ACPI: Early table checksum verification disabled<br>[00:00:00.034] [    0.000000] ACPI: RSDP 0x00000000000F5A00 000014 (v00 BOCHS )<br>[00:00:00.035] [    0.000000] ACPI: RSDT 0x000000003FFE1BDD 000034 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.038] [    0.000000] ACPI: FACP 0x000000003FFE1A79 000074 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.040] [    0.000000] ACPI: DSDT 0x000000003FFE0040 001A39 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.042] [    0.000000] ACPI: FACS 0x000000003FFE0000 000040<br>[00:00:00.043] [    0.000000] ACPI: APIC 0x000000003FFE1AED 000090 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.045] [    0.000000] ACPI: HPET 0x000000003FFE1B7D 000038 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.048] [    0.000000] ACPI: WAET 0x000000003FFE1BB5 000028 (v01 BOCHS  BXPC     00000001 BXPC 00000001)<br>[00:00:00.051] [    0.000000] ACPI: Reserving FACP table memory at [mem 0x3ffe1a79-0x3ffe1aec]<br>[00:00:00.052] [    0.000000] ACPI: Reserving DSDT table memory at [mem 0x3ffe0040-0x3ffe1a78]<br>[00:00:00.054] [    0.000000] ACPI: Reserving FACS table memory at [mem 0x3ffe0000-0x3ffe003f]<br>[00:00:00.056] [    0.000000] ACPI: Reserving APIC table memory at [mem 0x3ffe1aed-0x3ffe1b7c]<br>[00:00:00.058] [    0.000000] ACPI: Reserving HPET table memory at [mem 0x3ffe1b7d-0x3ffe1bb4]<br>[00:00:00.060] [    0.000000] ACPI: Reserving WAET table memory at [mem 0x3ffe1bb5-0x3ffe1bdc]<br>[00:00:00.063] [    0.000000] Zone ranges:<br>[00:00:00.064] [    0.000000]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]<br>[00:00:00.065] [    0.000000]   DMA32    [mem 0x0000000001000000-0x000000003ffd9fff]<br>[00:00:00.066] [    0.000000]   Normal   empty<br>[00:00:00.067] [    0.000000] Movable zone start for each node<br>[00:00:00.068] [    0.000000] Early memory node ranges<br>[00:00:00.069] [    0.000000]   node   0: [mem 0x0000000000001000-0x000000000009efff]<br>[00:00:00.071] [    0.000000]   node   0: [mem 0x0000000000100000-0x000000003ffd9fff]<br>[00:00:00.072] [    0.000000] Initmem setup node 0 [mem 0x0000000000001000-0x000000003ffd9fff]<br>[00:00:00.074] [    0.000000] On node 0, zone DMA: 1 pages in unavailable ranges<br>[00:00:00.076] [    0.000000] On node 0, zone DMA: 97 pages in unavailable ranges<br>[00:00:00.077] [    0.000000] On node 0, zone DMA32: 38 pages in unavailable ranges<br>[00:00:00.079] [    0.000000] ACPI: PM-Timer IO Port: 0x608<br>[00:00:00.080] [    0.000000] ACPI: LAPIC_NMI (acpi_id[0xff] dfl dfl lint[0x1])<br>[00:00:00.082] [    0.000000] IOAPIC[0]: apic_id 0, version 32, address 0xfec00000, GSI 0-23<br>[00:00:00.083] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)<br>[00:00:00.084] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 5 global_irq 5 high level)<br>[00:00:00.086] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)<br>[00:00:00.087] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 10 global_irq 10 high level)<br>[00:00:00.089] [    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 11 global_irq 11 high level)<br>[00:00:00.091] [    0.000000] ACPI: Using ACPI (MADT) for SMP configuration information<br>[00:00:00.092] [    0.000000] ACPI: HPET id: 0x8086a201 base: 0xfed00000<br>[00:00:00.094] [    0.000000] smpboot: Allowing 4 CPUs, 0 hotplug CPUs<br>[00:00:00.095] [    0.000000] [mem 0x40000000-0xfffbffff] available for PCI devices<br>[00:00:00.097] [    0.000000] Booting paravirtualized kernel on bare hardware<br>[00:00:00.098] [    0.000000] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[00:00:00.100] [    0.000000] setup_percpu: NR_CPUS:256 nr_cpumask_bits:256 nr_cpu_ids:4 nr_node_ids:1<br>[00:00:00.102] [    0.000000] percpu: Embedded 54 pages/cpu s183896 r8192 d29096 u524288<br>[00:00:00.104] [    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 257754<br>[00:00:00.106] [    0.000000] Kernel command line: BOOT_IMAGE=/vmlinuz-virt root=UUID=ada017ef-3181-40be-8e14-f45c49e00f3a ro modules=sd-mod,usb-storage,ext4 console=tty0 console=ttyS0,115200n8 rootfstype=ext4<br>[00:00:00.110] [    0.000000] Unknown kernel command line parameters "BOOT_IMAGE=/vmlinuz-virt modules=sd-mod,usb-storage,ext4", will be passed to user space.<br>[00:00:00.112] [    0.000000] printk: log_buf_len individual max cpu contribution: 4096 bytes<br>[00:00:00.114] [    0.000000] printk: log_buf_len total cpu_extra contributions: 12288 bytes<br>[00:00:00.115] [    0.000000] printk: log_buf_len min size: 16384 bytes<br>[00:00:00.115] [    0.000000] printk: log_buf_len: 32768 bytes<br>[00:00:00.116] [    0.000000] printk: early log buf free: 11232(68%)<br>[00:00:00.117] [    0.000000] Dentry cache hash table entries: 131072 (order: 8, 1048576 bytes, linear)<br>[00:00:00.119] [    0.000000] Inode-cache hash table entries: 65536 (order: 7, 524288 bytes, linear)<br>[00:00:00.121] [    0.000000] mem auto-init: stack:byref(zero), heap alloc:on, heap free:off<br>[00:00:00.122] [    0.000000] Memory: 994644K/1048032K available (10246K kernel code, 1191K rwdata, 3024K rodata, 1824K init, 2032K bss, 53128K reserved, 0K cma-reserved)<br>[00:00:00.125] [    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1<br>[00:00:00.127] [    0.000000] rcu: Hierarchical RCU implementation.<br>[00:00:00.128] [    0.000000] rcu:      RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.<br>[00:00:00.130] [    0.000000]   Tracing variant of Tasks RCU enabled.<br>[00:00:00.131] [    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.<br>[00:00:00.133] [    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4<br>[00:00:00.134] [    0.000000] NR_IRQS: 16640, nr_irqs: 456, preallocated irqs: 16<br>[00:00:00.136] [    0.000000] kfence: initialized - using 2097152 bytes for 255 objects at 0x(____ptrval____)-0x(____ptrval____)<br>[00:00:00.138] [    0.000000] Console: colour VGA+ 80x25<br>[00:00:00.140] [    0.000000] printk: console [tty0] enabled<br>[00:00:00.141] [    0.000000] printk: console [ttyS0] enabled<br>[00:00:00.152] [    0.000000] ACPI: Core revision 20210730<br>[00:00:00.222] [    0.000000] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604467 ns<br>[00:00:00.299] [    0.040000] APIC: Switch to symmetric I/O mode setup<br>[00:00:00.356] [    0.090000] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1<br>[00:00:00.485] [    0.170000] tsc: Unable to calibrate against PIT<br>[00:00:00.487] [    0.170000] tsc: using HPET reference calibration<br>[00:00:00.490] [    0.180000] tsc: Detected 1000.008 MHz processor<br>[00:00:00.501] [    0.008083] tsc: Marking TSC unstable due to TSCs unsynchronized<br>[00:00:00.510] [    0.023023] Calibrating delay loop (skipped), value calculated using timer frequency.. 2000.01 BogoMIPS (lpj=10000080)<br>[00:00:00.516] [    0.029058] pid_max: default: 32768 minimum: 301<br>[00:00:00.538] [    0.052022] LSM: Security Framework initializing<br>[00:00:00.563] [    0.077182] landlock: Up and running.<br>[00:00:00.603] [    0.116915] Mount-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[00:00:00.608] [    0.120897] Mountpoint-cache hash table entries: 2048 (order: 2, 16384 bytes, linear)<br>[00:00:00.865] [    0.378939] process: using AMD E400 aware idle routine<br>[00:00:00.869] [    0.383237] Last level iTLB entries: 4KB 512, 2MB 255, 4MB 127<br>[00:00:00.872] [    0.385764] Last level dTLB entries: 4KB 512, 2MB 255, 4MB 127, 1GB 0<br>[00:00:00.879] [    0.392543] Spectre V1 : Mitigation: usercopy/swapgs barriers and __user pointer sanitization<br>[00:00:00.883] [    0.397294] Spectre V2 : Mitigation: Retpolines<br>[00:00:00.886] [    0.400205] Spectre V2 : Spectre v2 / SpectreRSB mitigation: Filling RSB on context switch<br>[00:00:00.890] [    0.402244] Spectre V2 : Spectre v2 / SpectreRSB : Filling RSB on VMEXIT<br>[00:00:02.465] [    1.973164] Freeing SMP alternatives memory: 32K<br>[00:00:02.787] [    2.298491] smpboot: CPU0: AMD QEMU Virtual CPU version 2.5+ (family: 0xf, model: 0x6b, stepping: 0x1)<br>[00:00:02.922] [    2.425247] Performance Events: PMU not available due to virtualization, using software events only.<br>[00:00:02.948] [    2.457961] rcu: Hierarchical SRCU implementation.<br>[00:00:03.038] [    2.547180] NMI watchdog: Perf NMI watchdog permanently disabled<br>[00:00:03.085] [    2.594681] smp: Bringing up secondary CPUs ...<br>[00:00:03.134] [    2.643185] x86: Booting SMP configuration:<br>[00:00:03.576] [    2.645708] .... node  #0, CPUs:      #1<br>[00:00:03.580] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:03.581] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:04.130] [    3.195096]  #2<br>[00:00:04.132] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:04.133] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:04.541] [    3.605686]  #3<br>[00:00:04.550] [    0.000000] calibrate_delay_direct() failed to get a good estimate for loops_per_jiffy.<br>[00:00:04.553] [    0.000000] Probably due to long platform interrupts. Consider using "lpj=" boot option.<br>[00:00:04.755] [    3.973824] smp: Brought up 1 node, 4 CPUs<br>[00:00:04.758] [    3.976586] smpboot: Max logical packages: 1<br>[00:00:04.761] [    3.979166] ----------------<br>[00:00:04.764] [    3.982315] | NMI testsuite:<br>[00:00:04.765] [    3.983828] --------------------<br>[00:00:04.780] [    3.985383]   remote IPI:  ok  |<br>[00:00:04.790] [    4.002138]    local IPI:  ok  |<br>[00:00:04.794] [    4.012615] --------------------<br>[00:00:04.797] [    4.015135] Good, all   2 testcases passed! |<br>[00:00:04.800] [    4.017769] ---------------------------------<br>[00:00:04.805] [    4.021676] smpboot: Total of 4 processors activated (2003.17 BogoMIPS)<br>[00:00:05.128] [    4.317633] devtmpfs: initialized<br>[00:00:05.193] [    4.382996] x86/mm: Memory block size: 128MB<br>[00:00:05.303] [    4.492392] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns<br>[00:00:05.310] [    4.499103] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)<br>[00:00:05.531] [    4.719602] NET: Registered PF_NETLINK/PF_ROUTE protocol family<br>[00:00:05.609] [    4.796671] audit: initializing netlink subsys (disabled)<br>[00:00:05.687] [    4.875300] audit: type=2000 audit(1681483119.000:1): state=initialized audit_enabled=0 res=1<br>[00:00:05.774] [    4.935457] thermal_sys: Registered thermal governor 'step_wise'<br>[00:00:05.776] [    4.963113] cpuidle: using governor ladder<br>[00:00:05.844] [    5.022859] cpuidle: using governor menu<br>[00:00:05.880] [    5.058201] ACPI: bus type PCI registered<br>[00:00:05.911] [    5.075803] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5<br>[00:00:06.064] [    5.223263] PCI: Using configuration type 1 for base access<br>[00:00:06.138] [    5.294466] mtrr: your CPUs had inconsistent fixed MTRR settings<br>[00:00:06.149] [    5.302615] mtrr: your CPUs had inconsistent variable MTRR settings<br>[00:00:06.157] [    5.312465] mtrr: your CPUs had inconsistent MTRRdefType settings<br>[00:00:06.162] [    5.315209] mtrr: probably your BIOS does not setup all CPUs.<br>[00:00:06.166] [    5.322348] mtrr: corrected configuration.<br>[00:00:06.394] [    5.552335] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.<br>[00:00:06.453] [    5.612730] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages<br>[00:00:06.913] [    6.063288] ACPI: Added _OSI(Module Device)<br>[00:00:06.916] [    6.065710] ACPI: Added _OSI(Processor Device)<br>[00:00:06.917] [    6.067552] ACPI: Added _OSI(3.0 _SCP Extensions)<br>[00:00:06.919] [    6.069293] ACPI: Added _OSI(Processor Aggregator Device)<br>[00:00:06.925] [    6.083025] ACPI: Added _OSI(Linux-Dell-Video)<br>[00:00:06.927] [    6.084859] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)<br>[00:00:06.929] [    6.086933] ACPI: Added _OSI(Linux-HPI-Hybrid-Graphics)<br>[00:00:07.254] [    6.404033] ACPI: 1 ACPI AML tables successfully acquired and loaded<br>[00:00:07.504] [    6.652563] ACPI: Interpreter enabled<br>[00:00:07.518] [    6.669609] ACPI: PM: (supports S0 S3 S5)<br>[00:00:07.523] [    6.673176] ACPI: Using IOAPIC for interrupt routing<br>[00:00:07.545] [    6.694338] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug<br>[00:00:07.604] [    6.751676] ACPI: Enabled 2 GPEs in block 00 to 0F<br>[00:00:08.935] [    7.971885] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-ff])<br>[00:00:08.979] [    8.040249] acpi PNP0A03:00: _OSC: OS supports [ASPM ClockPM Segments MSI HPX-Type3]<br>[00:00:09.006] [    8.072387] acpi PNP0A03:00: fail to add MMCONFIG information, can't access extended PCI configuration space under this bridge.<br>[00:00:09.147] [    8.217806] acpiphp: Slot [3] registered<br>[00:00:09.156] [    8.231957] acpiphp: Slot [4] registered<br>[00:00:09.159] [    8.231957] acpiphp: Slot [5] registered<br>[00:00:09.166] [    8.241834] acpiphp: Slot [6] registered<br>[00:00:09.169] [    8.241834] acpiphp: Slot [7] registered<br>[00:00:09.175] [    8.245280] acpiphp: Slot [8] registered<br>[00:00:09.179] [    8.248554] acpiphp: Slot [9] registered<br>[00:00:09.187] [    8.263464] acpiphp: Slot [10] registered<br>[00:00:09.191] [    8.266660] acpiphp: Slot [11] registered<br>[00:00:09.200] [    8.277294] acpiphp: Slot [12] registered<br>[00:00:09.205] [    8.277294] acpiphp: Slot [13] registered<br>[00:00:09.209] [    8.279791] acpiphp: Slot [14] registered<br>[00:00:09.217] [    8.294079] acpiphp: Slot [15] registered<br>[00:00:09.224] [    8.301992] acpiphp: Slot [16] registered<br>[00:00:09.228] [    8.301992] acpiphp: Slot [17] registered<br>[00:00:09.235] [    8.305659] acpiphp: Slot [18] registered<br>[00:00:09.242] [    8.310425] acpiphp: Slot [19] registered<br>[00:00:09.248] [    8.321984] acpiphp: Slot [20] registered<br>[00:00:09.253] [    8.331921] acpiphp: Slot [21] registered<br>[00:00:09.257] [    8.331921] acpiphp: Slot [22] registered<br>[00:00:09.261] [    8.331921] acpiphp: Slot [23] registered<br>[00:00:09.268] [    8.341971] acpiphp: Slot [24] registered<br>[00:00:09.274] [    8.344845] acpiphp: Slot [25] registered<br>[00:00:09.279] [    8.349782] acpiphp: Slot [26] registered<br>[00:00:09.284] [    8.360134] acpiphp: Slot [27] registered<br>[00:00:09.288] [    8.360134] acpiphp: Slot [28] registered<br>[00:00:09.293] [    8.371913] acpiphp: Slot [29] registered<br>[00:00:09.296] [    8.371913] acpiphp: Slot [30] registered<br>[00:00:09.300] [    8.371913] acpiphp: Slot [31] registered<br>[00:00:09.308] [    8.386220] PCI host bridge to bus 0000:00<br>[00:00:09.315] [    8.391877] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]<br>[00:00:09.318] [    8.391877] pci_bus 0000:00: root bus resource [io  0x0d00-0xffff window]<br>[00:00:09.323] [    8.392049] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]<br>[00:00:09.326] [    8.396021] pci_bus 0000:00: root bus resource [mem 0x40000000-0xfebfffff window]<br>[00:00:09.329] [    8.398800] pci_bus 0000:00: root bus resource [mem 0x100000000-0x17fffffff window]<br>[00:00:09.337] [    8.412027] pci_bus 0000:00: root bus resource [bus 00-ff]<br>[00:00:09.375] [    8.451912] pci 0000:00:00.0: [8086:1237] type 00 class 0x060000<br>[00:00:09.542] [    8.611897] pci 0000:00:01.0: [8086:7000] type 00 class 0x060100<br>[00:00:09.617] [    8.691929] pci 0000:00:01.1: [8086:7010] type 00 class 0x010180<br>[00:00:09.685] [    8.755522] pci 0000:00:01.1: reg 0x20: [io  0xc160-0xc16f]<br>[00:00:09.706] [    8.782735] pci 0000:00:01.1: legacy IDE quirk: reg 0x10: [io  0x01f0-0x01f7]<br>[00:00:09.709] [    8.786600] pci 0000:00:01.1: legacy IDE quirk: reg 0x14: [io  0x03f6]<br>[00:00:09.715] [    8.792488] pci 0000:00:01.1: legacy IDE quirk: reg 0x18: [io  0x0170-0x0177]<br>[00:00:09.718] [    8.795544] pci 0000:00:01.1: legacy IDE quirk: reg 0x1c: [io  0x0376]<br>[00:00:09.763] [    8.834186] pci 0000:00:01.3: [8086:7113] type 00 class 0x068000<br>[00:00:09.772] [    8.840946] pci 0000:00:01.3: quirk: [io  0x0600-0x063f] claimed by PIIX4 ACPI<br>[00:00:09.775] [    8.850115] pci 0000:00:01.3: quirk: [io  0x0700-0x070f] claimed by PIIX4 SMB<br>[00:00:09.800] [    8.869061] pci 0000:00:02.0: [1234:1111] type 00 class 0x030000<br>[00:00:09.824] [    8.894425] pci 0000:00:02.0: reg 0x10: [mem 0xfd000000-0xfdffffff pref]<br>[00:00:09.859] [    8.936997] pci 0000:00:02.0: reg 0x18: [mem 0xfebd0000-0xfebd0fff]<br>[00:00:09.937] [    9.012059] pci 0000:00:02.0: reg 0x30: [mem 0xfebc0000-0xfebcffff pref]<br>[00:00:09.946] [    9.021835] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]<br>[00:00:10.025] [    9.095929] pci 0000:00:03.0: [1af4:1005] type 00 class 0x00ff00<br>[00:00:10.049] [    9.122086] pci 0000:00:03.0: reg 0x10: [io  0xc100-0xc11f]<br>[00:00:10.085] [    9.152520] pci 0000:00:03.0: reg 0x14: [mem 0xfebd1000-0xfebd1fff]<br>[00:00:10.187] [    9.241967] pci 0000:00:03.0: reg 0x20: [mem 0xfe000000-0xfe003fff 64bit pref]<br>[00:00:10.298] [    9.348460] pci 0000:00:04.0: [1af4:1000] type 00 class 0x020000<br>[00:00:10.322] [    9.373091] pci 0000:00:04.0: reg 0x10: [io  0xc120-0xc13f]<br>[00:00:10.365] [    9.402592] pci 0000:00:04.0: reg 0x14: [mem 0xfebd2000-0xfebd2fff]<br>[00:00:10.457] [    9.492144] pci 0000:00:04.0: reg 0x20: [mem 0xfe004000-0xfe007fff 64bit pref]<br>[00:00:10.493] [    9.523079] pci 0000:00:04.0: reg 0x30: [mem 0xfeb80000-0xfebbffff pref]<br>[00:00:10.596] [    9.629889] pci 0000:00:05.0: [1af4:1001] type 00 class 0x010000<br>[00:00:10.619] [    9.652179] pci 0000:00:05.0: reg 0x10: [io  0xc000-0xc07f]<br>[00:00:10.654] [    9.682071] pci 0000:00:05.0: reg 0x14: [mem 0xfebd3000-0xfebd3fff]<br>[00:00:10.736] [    9.761947] pci 0000:00:05.0: reg 0x20: [mem 0xfe008000-0xfe00bfff 64bit pref]<br>[00:00:10.838] [    9.870022] pci 0000:00:06.0: [1af4:1001] type 00 class 0x010000<br>[00:00:10.863] [    9.892120] pci 0000:00:06.0: reg 0x10: [io  0xc080-0xc0ff]<br>[00:00:10.904] [    9.924126] pci 0000:00:06.0: reg 0x14: [mem 0xfebd4000-0xfebd4fff]<br>[00:00:11.026] [   10.002215] pci 0000:00:06.0: reg 0x20: [mem 0xfe00c000-0xfe00ffff 64bit pref]<br>[00:00:11.162] [   10.120405] pci 0000:00:07.0: [1af4:1009] type 00 class 0x000200<br>[00:00:11.184] [   10.152074] pci 0000:00:07.0: reg 0x10: [io  0xc140-0xc15f]<br>[00:00:11.234] [   10.174296] pci 0000:00:07.0: reg 0x14: [mem 0xfebd5000-0xfebd5fff]<br>[00:00:11.367] [   10.232991] pci 0000:00:07.0: reg 0x20: [mem 0xfe010000-0xfe013fff 64bit pref]<br>[00:00:11.599] [   10.471604] ACPI: PCI: Interrupt link LNKA configured for IRQ 10<br>[00:00:11.617] [   10.491883] ACPI: PCI: Interrupt link LNKB configured for IRQ 10<br>[00:00:11.636] [   10.512123] ACPI: PCI: Interrupt link LNKC configured for IRQ 11<br>[00:00:11.673] [   10.542689] ACPI: PCI: Interrupt link LNKD configured for IRQ 11<br>[00:00:11.707] [   10.576409] ACPI: PCI: Interrupt link LNKS configured for IRQ 9<br>[00:00:11.917] [   10.781887] iommu: Default domain type: Translated<br>[00:00:11.919] [   10.781887] iommu: DMA domain TLB invalidation policy: lazy mode<br>[00:00:12.052] [   10.920256] SCSI subsystem initialized<br>[00:00:12.256] [   11.116290] pps_core: LinuxPPS API ver. 1 registered<br>[00:00:12.258] [   11.118358] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it><br>[00:00:12.265] [   11.124759] PTP clock support registered<br>[00:00:12.494] [   11.353746] PCI: Using ACPI for IRQ routing<br>[00:00:12.605] [   11.454677] hpet: 3 channels of 0 reserved for per-cpu timers<br>[00:00:12.679] [   11.523876] clocksource: Switched to clocksource hpet<br>[00:00:13.586] [   12.430937] VFS: Disk quotas dquot_6.6.0<br>[00:00:13.604] [   12.448397] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)<br>[00:00:13.704] [   12.548851] pnp: PnP ACPI init<br>[00:00:13.882] [   12.727111] pnp: PnP ACPI: found 6 devices<br>[00:00:14.532] [   13.376397] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns<br>[00:00:14.562] [   13.406648] NET: Registered PF_INET protocol family<br>[00:00:14.625] [   13.468935] IP idents hash table entries: 16384 (order: 5, 131072 bytes, linear)<br>[00:00:14.736] [   13.580659] tcp_listen_portaddr_hash hash table entries: 512 (order: 1, 8192 bytes, linear)<br>[00:00:14.743] [   13.588091] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)<br>[00:00:14.748] [   13.592844] TCP established hash table entries: 8192 (order: 4, 65536 bytes, linear)<br>[00:00:14.754] [   13.598462] TCP bind hash table entries: 8192 (order: 5, 131072 bytes, linear)<br>[00:00:14.762] [   13.606702] TCP: Hash tables configured (established 8192 bind 8192)<br>[00:00:14.784] [   13.628277] UDP hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[00:00:14.791] [   13.636004] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes, linear)<br>[00:00:14.823] [   13.668048] NET: Registered PF_UNIX/PF_LOCAL protocol family<br>[00:00:14.833] [   13.677308] NET: Registered PF_XDP protocol family<br>[00:00:14.847] [   13.691364] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]<br>[00:00:14.852] [   13.696455] pci_bus 0000:00: resource 5 [io  0x0d00-0xffff window]<br>[00:00:14.854] [   13.698806] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]<br>[00:00:14.857] [   13.701345] pci_bus 0000:00: resource 7 [mem 0x40000000-0xfebfffff window]<br>[00:00:14.861] [   13.705734] pci_bus 0000:00: resource 8 [mem 0x100000000-0x17fffffff window]<br>[00:00:14.876] [   13.721208] pci 0000:00:01.0: PIIX3: Enabling Passive Release<br>[00:00:14.882] [   13.727213] pci 0000:00:00.0: Limiting direct PCI/PCI transfers<br>[00:00:14.886] [   13.730915] pci 0000:00:01.0: Activating ISA DMA hang workarounds<br>[00:00:14.890] [   13.734841] PCI: CLS 0 bytes, default 64<br>[00:00:15.132] [   13.976576] Initialise system trusted keyrings<br>[00:00:15.193] [   14.037762] Unpacking initramfs...<br>[00:00:15.222] [   14.067153] workingset: timestamp_bits=46 max_order=18 bucket_order=0<br>[00:00:15.486] [   14.331268] zbud: loaded<br>[00:00:15.565] [   14.409554] Key type asymmetric registered<br>[00:00:15.579] [   14.423305] Asymmetric key parser 'x509' registered<br>[00:00:15.589] [   14.434237] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)<br>[00:00:15.662] [   14.506803] io scheduler mq-deadline registered<br>[00:00:15.665] [   14.509818] io scheduler kyber registered<br>[00:00:15.692] [   14.536283] io scheduler bfq registered<br>[00:00:15.871] [   14.715533] ERST DBG: ERST support is disabled.<br>[00:00:20.374] [   19.218725] Freeing initrd memory: 6840K<br>[00:00:21.403] [   20.247727] ACPI: \_SB_.LNKC: Enabled at IRQ 11<br>[00:00:24.302] [   23.146633] ACPI: \_SB_.LNKD: Enabled at IRQ 10<br>[00:00:27.152] [   25.997080] ACPI: \_SB_.LNKA: Enabled at IRQ 10<br>[00:00:29.965] [   28.809384] ACPI: \_SB_.LNKB: Enabled at IRQ 11<br>[00:00:32.883] [   31.728018] Serial: 8250/16550 driver, 4 ports, IRQ sharing enabled<br>[00:00:32.944] [   31.788421] 00:04: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A<br>[00:00:33.243] [   32.087359] VMware PVSCSI driver - version 1.0.7.0-k<br>[00:00:33.493] [   32.337317] scsi host0: ata_piix<br>[00:00:33.586] [   32.430655] scsi host1: ata_piix<br>[00:00:33.631] [   32.461408] ata1: PATA max MWDMA2 cmd 0x1f0 ctl 0x3f6 bmdma 0xc160 irq 14<br>[00:00:33.634] [   32.478886] ata2: PATA max MWDMA2 cmd 0x170 ctl 0x376 bmdma 0xc168 irq 15<br>[00:00:33.704] [   32.548306] i8042: PNP: PS/2 Controller [PNP0303:KBD,PNP0f13:MOU] at 0x60,0x64 irq 1,12<br>[00:00:33.847] [   32.691199] serio: i8042 KBD port at 0x60,0x64 irq 1<br>[00:00:33.855] [   32.700058] serio: i8042 AUX port at 0x60,0x64 irq 12<br>[00:00:33.878] [   32.723165] rtc_cmos 00:05: RTC can wake from S4<br>[00:00:34.019] [   32.863454] rtc_cmos 00:05: registered as rtc0<br>[00:00:34.052] [   32.893227] rtc_cmos 00:05: setting system clock to 2023-04-14T14:39:08 UTC (1681483148)<br>[00:00:34.130] [   32.974336] rtc_cmos 00:05: alarms up to one day, y3k, 242 bytes nvram, hpet irqs<br>[00:00:34.250] [   33.094957] gre: GRE over IPv4 demultiplexor driver<br>[00:00:34.259] [   33.104141] ata2.00: ATAPI: QEMU DVD-ROM, 2.5+, max UDMA/100<br>[00:00:34.274] [   33.118746] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input0<br>[00:00:34.304] [   33.148606] Key type dns_resolver registered<br>[00:00:34.361] [   33.205605] IPI shorthand broadcast: enabled<br>[00:00:34.513] [   33.357667] registered taskstats version 1<br>[00:00:34.531] [   33.375812] Loading compiled-in X.509 certificates<br>[00:00:34.860] [   33.705026] scsi 1:0:0:0: CD-ROM            QEMU     QEMU DVD-ROM     2.5+ PQ: 0 ANSI: 5<br>[00:00:36.143] [   34.988141] Loaded X.509 cert 'Build time autogenerated kernel key: 90200cc09a919577283b2cb6eca2ff9ac9891c1d'<br>[00:00:36.203] [   35.047892] zswap: loaded using pool lzo/zbud<br>[00:00:36.282] [   35.126947] Key type .fscrypt registered<br>[00:00:36.284] [   35.129076] Key type fscrypt-provisioning registered<br>[00:00:36.381] [   35.224978] Unstable clock detected, switching default tracing clock to "global"<br>[00:00:36.382] [   35.224978] If you want to keep using the local clock, then add:<br>[00:00:36.383] [   35.224978]   "trace_clock=local"<br>[00:00:36.384] [   35.224978] on the kernel command line<br>[00:00:36.805] [   35.649490] Freeing unused kernel image (initmem) memory: 1824K<br>[00:00:36.829] [   35.674216] Write protecting the kernel read-only data: 16384k<br>[00:00:36.888] [   35.732521] Freeing unused kernel image (text/rodata gap) memory: 2040K<br>[00:00:36.910] [   35.754688] Freeing unused kernel image (rodata/data gap) memory: 1072K<br>[00:00:36.923] [   35.767439] rodata_test: all tests were successful<br>[00:00:36.935] [   35.779772] Run /init as init process<br>[00:00:38.821] [   37.665714] Alpine Init 3.7.0-r1<br>[00:00:38.850] Alpine Init 3.7.0-r1<br>[00:00:38.946] [   37.790779] Loading boot drivers...<br>[00:00:38.957]  * Loading boot drivers: [   39.244202] ACPI: bus type USB registered<br>[00:00:40.407] [   39.251383] usbcore: registered new interface driver usbfs<br>[00:00:40.437] [   39.281214] usbcore: registered new interface driver hub<br>[00:00:40.496] [   39.340328] usbcore: registered new device driver usb<br>[00:00:40.733] [   39.578248] usbcore: registered new interface driver usb-storage<br>[00:00:43.674] [   42.518994] loop: module loaded<br>[00:00:46.511] [   45.355870] Loading boot drivers: ok.<br>[00:00:46.519] ok.<br>[00:00:48.432] [   47.248900] Mounting root...<br>[00:00:48.481]  * Mounting root: [   57.687745] sr 1:0:0:0: [sr0] scsi3-mmc drive: 4x/4x cd/rw xa/form2 tray<br>[00:00:58.853] [   57.696888] cdrom: Uniform CD-ROM driver Revision: 3.20<br>[00:01:01.961] [   60.805767] virtio_blk virtio2: [vda] 12582912 512-byte logical blocks (6.44 GB/6.00 GiB)<br>[00:01:02.184] [   61.028572]  vda: vda1 vda2 vda3 vda4<br>[00:01:02.335] [   61.178652] virtio_blk virtio3: [vdb] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[00:01:36.090] [   94.931059] EXT4-fs (vda3): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.<br>[00:01:36.153] [   94.997236] Mounting root: ok.<br>[00:01:36.168] ok.<br>[00:01:40.327]<br>[00:01:40.767]    OpenRC 0.45.2 is starting up Linux 5.15.106-0-virt (x86_64)<br>[00:01:40.768]<br>[00:01:42.507]  * /proc is already mounted<br>[00:01:43.190]  * Mounting /run ... * /run/openrc: creating directory<br>[00:01:43.968]  * /run/lock: creating directory<br>[00:01:43.978]  * /run/lock: correcting owner<br>[00:02:06.227]  * Caching service dependencies ... [ ok ]<br>[00:02:08.731]  * Remounting devtmpfs on /dev ... [ ok ]<br>[00:02:09.843]  * Mounting /dev/mqueue ... [ ok ]<br>[00:02:15.243]  * Mounting security filesystem ... [ ok ]<br>[00:02:15.650]  * Mounting debug filesystem ... [ ok ]<br>[00:02:16.086]  * Mounting persistent storage (pstore) filesystem ... [ ok ]<br>[00:02:18.133]  * Starting busybox mdev ... [ ok ]<br>[00:02:18.375]  * Scanning hardware for mdev ... [ ok ]<br>[00:02:42.977]  * Loading hardware drivers ... [ ok ]<br>[00:04:00.654]  * Loading modules ... [ ok ]<br>[00:04:09.430]  * Setting system clock using the hardware clock [UTC] ... [ ok ]<br>[00:04:13.277]  * Checking local filesystems  .../dev/vda3: clean, 69222/233392 files, 465428/932864 blocks<br>[00:04:15.050] /dev/vda1: clean, 317/128016 files, 90307/512000 blocks<br>[00:04:15.523] tmp-partition: clean, 13/62464 files, 8639/249600 blocks<br>[00:04:15.918]  [ ok ]<br>[00:04:18.267]  * Remounting root filesystem read/write ... [ ok ]<br>[00:04:19.028]  * Remounting filesystems ... [ ok ]<br>[00:04:22.349]  * Activating swap devices ... [ ok ]<br>[00:04:25.182]  * Mounting local filesystems ... [ ok ]<br>[00:04:31.323]  * Configuring kernel parameters ... [ ok ]<br>[00:04:36.218]  * Creating user login records ... [ ok ]<br>[00:04:37.185]  * Cleaning /tmp directory ... [ ok ]<br>[00:04:40.507]  * Setting hostname ... [ ok ]<br>[00:04:43.077]  * Starting networking ... *   lo ... [ ok ]<br>[00:04:46.447]  *   eth0 ...udhcpc: started, v1.35.0<br>[00:04:48.727] udhcpc: broadcasting discover<br>[00:04:48.882] udhcpc: broadcasting select for 10.0.2.15, server 10.0.2.2<br>[00:04:49.068] udhcpc: lease of 10.0.2.15 obtained from 10.0.2.2, lease time 86400<br>[00:04:51.236]  [ ok ]<br>[00:04:53.477]  * Seeding random number generator ... * Seeding 256 bits and crediting<br>[00:04:53.704]  * Saving 256 bits of creditable seed for next boot<br>[00:04:53.840]  [ ok ]<br>[00:04:58.480]  * Starting busybox syslog ... [ ok ]<br>[00:05:05.877]  * Starting busybox acpid ... [ ok ]<br>[00:05:08.557]  * Starting busybox crond ... [ ok ]<br>[00:05:13.509] ssh-keygen: generating new host keys: RSA ECDSA ED25519<br>[00:06:22.040]  * Starting sshd ... [ ok ]<br>[00:06:33.208]  * Starting lighttpd ... [ ok ]<br>[00:06:40.018]<br>[00:06:40.168] Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br>[00:06:40.169]<br>localhost login:<br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: root<br>You are required to change your password immediately (administrator enforced).<br>New password:<br>Retype new password:<br>Welcome to Alpine!<br><br>The Alpine Wiki contains a large amount of how-to guides and general<br>information about administrating Alpine systems.<br>See &lt;https://wiki.alpinelinux.org/&gt;.<br><br>You can setup the system with the command: setup-alpine<br><br>You may change this message by editing /etc/motd.<br><br>localhost:~# pwd<br>/root<br>localhost:~#<br>localhost:~# echo $SHELL<br>/bin/bash<br>localhost:~#<br>localhost:~# ls -la<br>total 12<br>drwx------  2 root root 4096 Apr 14 11:57 .<br>drwxr-xr-x 22 root root 4096 Apr 14 09:10 ..<br>-rw-------  1 root root   29 Apr 14 11:58 .ash_history<br>localhost:~#<br>localhost:~# su - test<br>You are required to change your password immediately (administrator enforced).<br>New password:<br>Retype new password:<br>localhost:~$<br>localhost:~$ pwd<br>/home/test<br>localhost:~$<br>localhost:~$ echo $SHELL<br>/bin/bash<br>localhost:~$<br>localhost:~$ ls -la<br>total 12<br>drwxr-sr-x 2 test test 4096 Apr 14 11:59 .<br>drwxr-xr-x 3 root root 4096 Apr 14 08:49 ..<br>-rw------- 1 test test   36 Apr 14 11:59 .bash_history<br>localhost:~$<br>localhost:~$ exit<br>logout<br>localhost:~# pwd<br>/root<br>localhost:~#<br>localhost:~# blkid<br>/dev/vda1: UUID="9adeb32c-979a-47e7-b034-cd800a81e867" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="30d6984f-01"<br>/dev/vda4: LABEL="tmp-partition" UUID="bc45f4ae-37b9-41fe-a76d-3b3c56187ba5" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-04"<br>/dev/vda2: UUID="d34884c7-e0f9-4346-ac60-373b204cc274" TYPE="swap" PARTUUID="30d6984f-02"<br>/dev/vdb: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda3: UUID="ada017ef-3181-40be-8e14-f45c49e00f3a" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-03"<br>localhost:~#<br>localhost:~# df -ahT<br>Filesystem     Type        Size  Used Avail Use% Mounted on<br>sysfs          sysfs          0     0     0    - /sys<br>devtmpfs       devtmpfs     10M     0   10M   0% /dev<br>proc           proc           0     0     0    - /proc<br>devpts         devpts         0     0     0    - /dev/pts<br>shm            tmpfs       492M     0  492M   0% /dev/shm<br>/dev/vda3      ext4        3.5G  1.7G  1.6G  51% /<br>tmpfs          tmpfs       197M  128K  197M   1% /run<br>mqueue         mqueue         0     0     0    - /dev/mqueue<br>securityfs     securityfs     0     0     0    - /sys/kernel/security<br>debugfs        debugfs        0     0     0    - /sys/kernel/debug<br>pstore         pstore         0     0     0    - /sys/fs/pstore<br>tracefs        tracefs        0     0     0    - /sys/kernel/debug/tracing<br>/dev/vda1      ext4        459M   47M  383M  11% /boot<br>/dev/vda4      ext4        942M   32K  877M   1% /tmp<br>localhost:~#<br>localhost:~# mkdir /root/repo<br>localhost:~# mkdir /root/backup<br>localhost:~#<br>localhost:~# cat /etc/apk/repositories<br>#/media/vda/apks<br>#/root/repo/alpine/v3.17/main<br>#/root/repo/alpine/v3.17/community<br>/mnt/repo/alpine/v3.17/main<br>/mnt/repo/alpine/v3.17/community<br>localhost:~#<br>localhost:~# mount -r LABEL=50gb /root/repo<br>localhost:~#<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124367,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vda3 on / type ext4 (rw,relatime)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201344k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>tracefs on /sys/kernel/debug/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)<br>/dev/vda1 on /boot type ext4 (rw,relatime)<br>/dev/vda4 on /tmp type ext4 (rw,relatime)<br>/dev/vdb on /root/repo type ext4 (ro,relatime)<br>localhost:~#<br>localhost:~# groupadd --gid 9997 nine-p-host<br>localhost:~#<br>localhost:~# groupmod --append --users test nine-p-host<br>localhost:~#<br>localhost:~# mount -t 9mount -t 9p -o trans=virtio,version=9p2000.L,msize=1048576 host  /mnt/9p-host<br>localhost:~#<br>localhost:~# mount<br>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)<br>devtmpfs on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=10240k,nr_inodes=124367,mode=755,inode64)<br>proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)<br>devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)<br>shm on /dev/shm type tmpfs (rw,nosuid,nodev,noexec,relatime,inode64)<br>/dev/vda3 on / type ext4 (rw,relatime)<br>tmpfs on /run type tmpfs (rw,nosuid,nodev,size=201344k,nr_inodes=819200,mode=755,inode64)<br>mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)<br>securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)<br>debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)<br>pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)<br>tracefs on /sys/kernel/debug/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)<br>/dev/vda1 on /boot type ext4 (rw,relatime)<br>/dev/vda4 on /tmp type ext4 (rw,relatime)<br>/dev/vdb on /root/repo type ext4 (ro,relatime)<br>host on /mnt/9p-host type 9p (rw,relatime,sync,dirsync,access=client,msize=512000,trans=virtio)<br>localhost:~#<br>localhost:~# df -hT<br>Filesystem     Type      Size  Used Avail Use% Mounted on<br>devtmpfs       devtmpfs   10M     0   10M   0% /dev<br>shm            tmpfs     492M     0  492M   0% /dev/shm<br>/dev/vda3      ext4      3.5G  1.7G  1.6G  51% /<br>tmpfs          tmpfs     197M  128K  197M   1% /run<br>/dev/vda1      ext4      459M   47M  383M  11% /boot<br>/dev/vda4      ext4      942M   32K  877M   1% /tmp<br>/dev/vdb       ext4       49G   45G  4.8G  91% /root/repo<br>host           9p        117G   86G   31G  74% /mnt/9p-host<br>localhost:~#<br>localhost:~# ls -lRa /mnt/9p-host<br>/mnt/9p-host:<br>total 13681708<br>-rw-rw---- 1 root nine-p-host   51380224 Apr  5 00:35 alpine-virt-3.17.3-x86_64.iso<br>-rw-rw---- 1 root nine-p-host         96 Apr  5 00:35 alpine-virt-3.17.3-x86_64.iso.sha256<br>drwxrwx--- 2 root nine-p-host       4096 Apr 14 14:19 backup<br>-rw-rw---- 1 root nine-p-host 1073741824 Apr 14 08:04 disk3-1gb.img<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 15:30 vm-linux-grub.raw<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 13:53 vm-template-grub.raw<br><br>/mnt/9p-host/backup:<br>total 7340048<br>-rw-rw---- 1 root nine-p-host 1073741824 Apr 14 08:04 disk3-1gb.img<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 13:53 vm-template-grub.raw<br>localhost:~#<br>localhost:~#<br>localhost:~# su - test<br>Password:<br>localhost:~$<br>localhost:~$ touch /mnt/9p-host/test.txt<br>localhost:~$ ls -lRa /mnt/9p-host<br>/mnt/9p-host:<br>total 13681712<br>-rw-rw---- 1 root nine-p-host   51380224 Apr  5 00:35 alpine-virt-3.17.3-x86_64.iso<br>-rw-rw---- 1 root nine-p-host         96 Apr  5 00:35 alpine-virt-3.17.3-x86_64.iso.sha256<br>drwxrwx--- 2 root nine-p-host       4096 Apr 14 14:19 backup<br>-rw-rw---- 1 root nine-p-host 1073741824 Apr 14 08:04 disk3-1gb.img<br>-rw-rw---- 1 root nine-p-host          0 Apr 14 15:33 test.txt<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 15:33 vm-linux-grub.raw<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 13:53 vm-template-grub.raw<br><br>/mnt/9p-host/backup:<br>total 7340048<br>-rw-rw---- 1 root nine-p-host 1073741824 Apr 14 08:04 disk3-1gb.img<br>-rw-rw---- 1 root nine-p-host 6442450944 Apr 14 13:53 vm-template-grub.raw<br>localhost:~$<br>localhost:~$ exit<br>logout<br>localhost:~#<br>localhost:~# blkid<br>/dev/vda1: UUID="9adeb32c-979a-47e7-b034-cd800a81e867" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="30d6984f-01"<br>/dev/vda4: LABEL="tmp-partition" UUID="bc45f4ae-37b9-41fe-a76d-3b3c56187ba5" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-04"<br>/dev/vda2: UUID="d34884c7-e0f9-4346-ac60-373b204cc274" TYPE="swap" PARTUUID="30d6984f-02"<br>/dev/vdb: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda3: UUID="ada017ef-3181-40be-8e14-f45c49e00f3a" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-03"<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0    6G  0 disk<br>├─vda1 253:1    0  500M  0 part /boot<br>├─vda2 253:2    0    1G  0 part [SWAP]<br>├─vda3 253:3    0  3.6G  0 part /<br>└─vda4 253:4    0  975M  0 part /tmp<br>vdb    253:16   0   50G  1 disk /root/repo<br>localhost:~#<br>localhost:~# grep -i virt /var/log/messages | tail -10<br>localhost:~#<br>localhost:~# QEMU 7.2.0 monitor - type 'help' for more information<br>(qemu) info usernet<br>Hub -1 (net0):<br>  Protocol[State]    FD  Source Address  Port   Dest. Address  Port RecvQ SendQ<br>  TCP[HOST_FORWARD]  13               * 15022       10.0.2.15    22     0     0<br>  TCP[HOST_FORWARD]  12               * 15081       10.0.2.15 15081     0     0<br>(qemu)<br>(qemu) info block<br>drive2 (#block159): /storage/emulated/0/Download/qemu-test/vm-linux-grub.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block337): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br>(qemu) drive_add 0 if=none,file=/storage/emulated/0/Download/qemu-test/disk3-1gb.img,format=raw,id=disk3<br>OK<br>(qemu)<br>(qemu) device_add virtio-blk-pci,drive=disk3,id=virt1<br>(qemu)<br>(qemu) info block<br>drive2 (#block159): /storage/emulated/0/Download/qemu-test/vm-linux-grub.raw (raw)<br>    Attached to:      /machine/peripheral/virtblk2/virtio-backend<br>    Cache mode:       writeback<br><br>drive3 (#block337): /storage/emulated/0/Download/50gb.ext (raw, read-only)<br>    Attached to:      /machine/peripheral/virtblk3/virtio-backend<br>    Cache mode:       writeback<br><br>ide1-cd0: [not inserted]<br>    Attached to:      /machine/unattached/device[25]<br>    Removable device: not locked, tray closed<br><br>floppy0: [not inserted]<br>    Attached to:      /machine/unattached/device[19]<br>    Removable device: not locked, tray closed<br><br>sd0: [not inserted]<br>    Removable device: not locked, tray closed<br><br>disk3 (#block554): /storage/emulated/0/Download/qemu-test/disk3-1gb.img (raw)<br>    Attached to:      /machine/peripheral/virt1/virtio-backend<br>    Cache mode:       writeback<br>(qemu)<br>(qemu)<br><br>localhost:~#<br>localhost:~# blkid<br>/dev/vda1: UUID="9adeb32c-979a-47e7-b034-cd800a81e867" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="30d6984f-01"<br>/dev/vda4: LABEL="tmp-partition" UUID="bc45f4ae-37b9-41fe-a76d-3b3c56187ba5" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-04"<br>/dev/vda2: UUID="d34884c7-e0f9-4346-ac60-373b204cc274" TYPE="swap" PARTUUID="30d6984f-02"<br>/dev/vdb: LABEL="50gb" UUID="ed64f636-1b13-4695-ad66-82236229d6e4" BLOCK_SIZE="4096" TYPE="ext4"<br>/dev/vda3: UUID="ada017ef-3181-40be-8e14-f45c49e00f3a" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="30d6984f-03"<br>/dev/vdc2: PARTUUID="67aee5a3-02"<br>/dev/vdc3: PARTUUID="67aee5a3-03"<br>/dev/vdc1: PARTUUID="67aee5a3-01"<br>/dev/vdc4: PARTUUID="67aee5a3-04"<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0    6G  0 disk<br>├─vda1 253:1    0  500M  0 part /boot<br>├─vda2 253:2    0    1G  0 part [SWAP]<br>├─vda3 253:3    0  3.6G  0 part /<br>└─vda4 253:4    0  975M  0 part /tmp<br>vdb    253:16   0   50G  1 disk /root/repo<br>vdc    253:32   0    1G  0 disk<br>├─vdc1 253:33   0  250M  0 part<br>├─vdc2 253:34   0  250M  0 part<br>├─vdc3 253:35   0  250M  0 part<br>└─vdc4 253:36   0  273M  0 part<br>localhost:~#<br>localhost:~# grep -i virt /var/log/messages | tail -10<br>localhost:~#<br>localhost:~# dmesg | grep -i virt | tail -5<br>[   60.805767] virtio_blk virtio2: [vda] 12582912 512-byte logical blocks (6.44 GB/6.00 GiB)<br>[   61.178652] virtio_blk virtio3: [vdb] 104857600 512-byte logical blocks (53.7 GB/50.0 GiB)<br>[  198.521301] kvm: Nested Virtualization enabled<br>[ 3705.086115] virtio-pci 0000:00:08.0: enabling device (0000 -> 0003)<br>[ 3710.408520] virtio_blk virtio5: [vdc] 2097152 512-byte logical blocks (1.07 GB/1.00 GiB)<br>localhost:~#<br>localhost:~#<br>localhost:~# fdisk -l /dev/vdc<br>Disk /dev/vdc: 1 GiB, 1073741824 bytes, 2097152 sectors<br>Units: sectors of 1 * 512 = 512 bytes<br>Sector size (logical/physical): 512 bytes / 512 bytes<br>I/O size (minimum/optimal): 512 bytes / 512 bytes<br>Disklabel type: dos<br>Disk identifier: 0x67aee5a3<br><br>Device     Boot   Start     End Sectors  Size Id Type<br>/dev/vdc1          2048  514047  512000  250M 83 Linux<br>/dev/vdc2        514048 1026047  512000  250M  c W95 FAT32 (LBA)<br>/dev/vdc3       1026048 1538047  512000  250M  7 HPFS/NTFS/exFAT<br>/dev/vdc4       1538048 2097151  559104  273M  7 HPFS/NTFS/exFAT<br>localhost:~#<br>localhost:~# mkfs.ext4 -m 0 -L disk3-ext4 /dev/vdc1<br>mke2fs 1.46.6 (1-Feb-2023)<br>Discarding device blocks: done<br>Creating filesystem with 256000 1k blocks and 64000 inodes<br>Filesystem UUID: 56ba4f32-c1d6-4c6f-8391-d227b1f9d84d<br>Superblock backups stored on blocks:<br>        8193, 24577, 40961, 57345, 73729, 204801, 221185<br><br>Allocating group tables: done<br>Writing inode tables: done<br>Creating journal (4096 blocks): done<br>Writing superblocks and filesystem accounting information: done<br><br>localhost:~#<br>localhost:~# mkfs.vfat -F 32 -n DISK3-VFAT /dev/vdc2<br>mkfs.fat 4.2 (2021-01-31)<br>localhost:~#<br>localhost:~# mkfs.exfat -n disk3-exfat /dev/vdc3<br>mkexfatfs 1.3.0<br>Creating... done.<br>Flushing... done.<br>File system created successfully.<br>localhost:~#<br>localhost:~#<br>localhost:~# mkfs.ntfs --quick --label disk3-ntfs /dev/vdc4<br>Cluster size has been automatically set to 4096 bytes.<br>Creating NTFS volume structures.<br>mkntfs completed successfully. Have a nice day.<br>localhost:~#<br>localhost:~# lsblk<br>NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS<br>fd0      2:0    1    0B  0 disk<br>sr0     11:0    1 1024M  0 rom<br>vda    253:0    0    6G  0 disk<br>├─vda1 253:1    0  500M  0 part /boot<br>├─vda2 253:2    0    1G  0 part [SWAP]<br>├─vda3 253:3    0  3.6G  0 part /<br>└─vda4 253:4    0  975M  0 part /tmp<br>vdb    253:16   0   50G  1 disk /root/repo<br>vdc    253:32   0    1G  0 disk<br>├─vdc1 253:33   0  250M  0 part<br>├─vdc2 253:34   0  250M  0 part<br>├─vdc3 253:35   0  250M  0 part<br>└─vdc4 253:36   0  273M  0 part<br>localhost:~#<br>localhost:~# blkid|grep vdc<br>/dev/vdc2: LABEL_FATBOOT="DISK3-VFAT" LABEL="DISK3-VFAT" UUID="53B6-A533" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="67aee5a3-02"<br>/dev/vdc3: LABEL="disk3-exfat" UUID="54A4-2DDB" BLOCK_SIZE="512" TYPE="exfat" PTTYPE="dos" PARTUUID="67aee5a3-03"<br>/dev/vdc1: LABEL="disk3-ext4" UUID="56ba4f32-c1d6-4c6f-8391-d227b1f9d84d" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="67aee5a3-01"<br>/dev/vdc4: LABEL="disk3-ntfs" BLOCK_SIZE="512" UUID="72C64A15152C97BD" TYPE="ntfs" PARTUUID="67aee5a3-04"<br>localhost:~#<br>localhost:~# exit<br>logout<br><br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login:<br>Welcome to Alpine Linux 3.17<br>Kernel 5.15.106-0-virt on an x86_64 (/dev/ttyS0)<br><br>localhost login: (qemu)<br>(qemu) system_powerdown<br>(qemu)<br>[ 4240.583796] reboot: Power down<br>~ $<br>~ $ pwd<br>/data/data/com.termux/files/home<br>~ $<br></pre></td>
</tr>
</table>

---

<p><br></p>

### Reference Links


1. "Configuring LUKS: Linux Unified Key Setup": https://www.redhat.com/sysadmin/disk-encryption-luks
2. "Frequently Asked Questions Cryptsetup/LUKS": https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions
2. "Encrypted Archive with Cryptsetup": https://dashohoxha.gitlab.io/cryptsetup-encrypted-archive/ , https://github.com/dashohoxha ([dashohoxha](https://github.com/dashohoxha)), https://gitlab.com/dashohoxha
2. "Basic Guide To Encrypting Linux Partitions With LUKS": https://linuxconfig.org/basic-guide-to-encrypting-linux-partitions-with-luks , https://linuxconfig.org/how-to-use-a-file-as-a-luks-device-key , https://linuxconfig.org/how-to-use-luks-with-a-detached-header
2. "How To Linux Hard Disk Encryption With LUKS [ cryptsetup encrypt command ]": https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/
2. "How to encrypt a single Linux filesystem": https://www.redhat.com/sysadmin/encrypt-single-filesystem (LUKS)
2. "Create an encrypted file vault on Linux": https://opensource.com/article/21/4/linux-encryption (LUKS)
2. "Encrypted filesystems, loop devices, cryptsetup": http://jeromebelleman.gitlab.io/posts/filesystems/cryptsetup/ (LUKS)
2. "luks encryption with loopback file": https://gist.github.com/dbehnke/ad19ca8f1ccf80aebca5 , ([@dbehnke](https://github.com/dbehnke))
2. "An introduction to Linux filesystems": https://opensource.com/life/16/10/introduction-linux-filesystems (Linux "mount" command)
2. "mount Command in Linux | Explained": https://itslinuxfoss.com/mount-command-linux/
2. "How to Mount and Unmount Filesystems in Linux": https://www.baeldung.com/linux/mount-unmount-filesystems (Linux "fdisk" command)
2. "How to Mount and Unmount File Systems in Linux": https://linuxize.com/post/how-to-mount-and-unmount-file-systems-in-linux/  (Linux "fdisk" command)
2. "Managing partitions in Linux with fdisk": https://www.redhat.com/sysadmin/partitions-fdisk
2. "Creating and managing partitions in Linux with parted": https://www.redhat.com/sysadmin/partitions-parted
2. "Linux mount Command with Examples": https://phoenixnap.com/kb/linux-mount-command
2. "An introduction to the Linux /etc/fstab file": https://www.redhat.com/sysadmin/etc-fstab
2. "Chapter 24. Mounting file systems": https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/managing_file_systems/index
2. "Linux: Mount Disk Partition Using LABEL": https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/
2. "Linux commands: du and the options you should be using": https://www.redhat.com/sysadmin/du-command-options
2. "Hard links and soft links in Linux explained": https://www.redhat.com/sysadmin/linking-linux-explained
2. "Linux permissions: SUID, SGID, and sticky bit": https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
2. "How to audit permissions with the find command": https://www.redhat.com/sysadmin/audit-permissions-find
2. "Getting started with socat, a multipurpose relay tool for Linux": https://www.redhat.com/sysadmin/getting-started-socat
2. "Basic troubleshooting with telnet and netcat": https://www.redhat.com/sysadmin/telnet-netcat-troubleshooting (Linux "nc" command)
2. Linux "mktemp" command: https://www.gnu.org/software/coreutils/manual/coreutils.html
2. "How to use grep": https://www.redhat.com/sysadmin/how-to-use-grep
2. "Manipulating text at the command line with grep": https://www.redhat.com/sysadmin/manipulating-text-grep
2. "Manipulating text at the command line with sed": https://www.redhat.com/sysadmin/manipulating-text-sed
2. "Manipulating text with sed and grep": https://www.redhat.com/sysadmin/manipulating-text-sed-grep
2. "How to Kill a Process in Linux? Commands to Terminate": https://phoenixnap.com/kb/how-to-kill-a-process-in-linux
2. kill, ps, "Linux Command Basics: 7 commands for process management": https://www.redhat.com/sysadmin/linux-command-basics-7-commands-process-management
2. "Bash scripting: Moving from backtick operator to $ parentheses": https://www.redhat.com/sysadmin/backtick-operator-vs-parens
2. Linux ext4 filesystem: "Filesystems in the Linux kernel": https://docs.kernel.org/filesystems/index.html , https://docs.kernel.org/filesystems/ext4/index.html ("ext4 Data Structures and Algorithms"), https://www.cyberciti.biz/faq/linux-modify-partition-labels-command-to-change-diskname/ ("Linux Change Disk Label Name on EXT2 / EXT3 / EXT4 File Systems"), https://www.redhat.com/sysadmin/disk-space ("Linux sysadmins want to know: Where did my disk space go?")
2. "What sysadmins need to know about using Bash": https://www.redhat.com/sysadmin/bash-navigation
2. "10 basic Linux commands you need to know": https://www.redhat.com/sysadmin/basic-linux-commands
2. "8 fundamental Linux file-management commands for new users": https://www.redhat.com/sysadmin/linux-file-management-commands
2. "8 essential Linux file navigation commands for new users": https://www.redhat.com/sysadmin/Linux-file-navigation-commands
2. "Basic Linux commands and tools every sysadmin should know": https://clockhash.com/blog/basic-linux-commands-and-tools-every-sysadmin-should-know
2. bash: https://www.gnu.org/software/bash/manual/bash.html ("Bash Reference Manual"), https://www.redhat.com/sysadmin/linux-environment-variables ("Linux environment variable tips and tricks"), https://www.redhat.com/sysadmin/scripting-writing-text-file ("Bash scripting: How to write data to text files"), https://www.redhat.com/sysadmin/pipes-command-line-linux ("Working with pipes on the Linux command line" "here-document (heredoc)" "here-string"), https://linuxhint.com/linux-pipe-command-examples/ ("Linux Pipe Command with Examples"), https://www.redhat.com/sysadmin/linux-shell-redirection-pipelining ("How to manipulate files with shell redirection and pipelines in Linux"), https://www.redhat.com/sysadmin/redirect-shell-command-script-output ("How to redirect shell command output"), https://www.redhat.com/sysadmin/history-command ("How to manage your Linux command history"), https://www.redhat.com/sysadmin/parsing-bash-history ("Parsing Bash history in Linux"), https://tldp.org/LDP/abs/html/ ("Advanced Bash-Scripting Guide" "Here Documents"), https://wiki.bash-hackers.org
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. "The Linux man-pages project": https://www.kernel.org/doc/man-pages/ , https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/book/
2. "How to find out what a Linux command does": https://www.redhat.com/sysadmin/linux-command-documentation
2. Linux 'tree" and "ls" commands: https://www.cyberciti.biz/faq/linux-show-directory-structure-command-line/ ("Linux see directory tree structure using tree command"), https://www.redhat.com/sysadmin/ls-command-options ("Sysadmin tools: 11 ways to use the ls command in Linux"), https://www.redhat.com/sysadmin/Linux-file-navigation-commands ("8 essential Linux file navigation commands for new users")
2. "How to Use the less, more, and most Commands to Read Text Files in Linux": https://www.makeuseof.com/use-less-more-and-most-linux-commands/
2. Linux text editor "nano": https://www.redhat.com/sysadmin/getting-started-nano ("Getting started with Nano")
2. Linux text editors "vi", "vim", "ed": https://www.redhat.com/sysadmin/get-started-vi-editor ("How to get started with the Vi editor"), https://www.redhat.com/sysadmin/introduction-vi-editor ("An introduction to the vi editor"), https://www.redhat.com/sysadmin/beginners-guide-vim ("Linux basics: A beginner's guide to text editing with vim"), https://www.redhat.com/sysadmin/vim-commands ("Vim: Basic and intermediate commands"), https://www.redhat.com/sysadmin/introduction-ed-editor ("How to get started with the ed text editor")
2. Linux web browswer "links": http://links.twibright.com , http://links.twibright.com/download.php ("Documentation"), https://www.tecmint.com/command-line-web-browsers/ ("A Command Line Web Browsing with Lynx and Links Tools")
2. Linux "grep" command: https://www.redhat.com/sysadmin/find-text-files-using-grep ("Find text in files using the Linux grep command")
2. Linux "echo" command: https://phoenixnap.com/kb/echo-command-linux ("Echo Command in Linux (With Examples)"), https://www.tecmint.com/echo-command-in-linux/ ("15 Practical Examples of ‘echo’ command in Linux"), 
2. Linux "find" command: https://www.redhat.com/sysadmin/linux-find-command ("10 ways to use the Linux find command"), : https://www.redhat.com/sysadmin/find-best-friend ("When it comes to Linux system troubleshooting, find is my best friend")
2. Regular expressions (regex): https://www.redhat.com/sysadmin/introducing-regular-expressions ("Introducing regular expressions"), https://www.redhat.com/sysadmin/getting-started-regular-expressions-example ("Getting started with regular expressions: An example"), https://www.redhat.com/sysadmin/regex-grep-data-flow ("Regex and grep: Data flow and building blocks"), https://www.redhat.com/sysadmin/regular-expressions-pulling-it-all-together ("Regular expressions: Pulling it all together"), https://opensource.com/article/18/5/getting-started-regular-expressions ("Getting started with regular expressions")
2. Linux "chmod" command: https://www.redhat.com/sysadmin/linux-file-permissions-xplained ("Linux file permissions explained"), https://www.redhat.com/sysadmin/introduction-chmod ("Linux permissions: An introduction to chmod"), https://www.redhat.com/sysadmin/manage-permissions ("How to manage Linux permissions for users, groups, and others"), https://www.redhat.com/sysadmin/linux-permissions ("What sysadmins need to know about Linux permissions")
2. Linux "bc" command: https://www.gnu.org/software/bc/manual/html_mono/bc.html ("bc" "an arbitrary precision calculator language"), https://linuxconfig.org/bc ("bc command in Linux with examples"), https://web.archive.org/web/20211207113205/docstore.mik.ua/orelly/unix/upt/ch49_03.htm ("Chapter 49 Working with Numbers" "49.3 Gotchas in Base Conversion"), https://www.networkworld.com/article/3681079/converting-numbers-on-linux-among-decimal-hexadecimal-octal-and-binary.html ("Converting numbers on Linux among decimal, hexadecimal, octal, and binary"), https://www.theunixschool.com/2011/05/bc-unix-calculator.html ("bc - Unix calculator"),  https://www.real-world-systems.com/docs/bc.1.html ("bc" "arbitrary precision calculator"), http://www.physics.smu.edu/coan/linux/bc.html ("6. (Very) Brief intro to bc")
2. Linux "apt" command: https://linuxhint.com/debian_sources-list/ ("Understanding and Using Debian sources.list"), https://wiki.debian.org/SourcesList ("Configuring Apt Sources")
2. Web-based Distributed Authoring and Versioning (WebDAV), Linux command "cadaver": http://www.webdav.org , https://docs.vscentrum.be/en/latest/data/cadaver_client_access.html ("Cadaver Client Access"), https://github.com/hpcloud/swift-webdav/blob/master/doc/Cadaver.md ("Using the Cadaver WebDAV Client"). https://help.webpal.net/apis/webdav ("WebPal Resources for Editors, Admins, Collaborators and Coders" "WebDAV Interface")
2. Check the apps: https://www.virustotal.com/gui/home/url ("OPSWAT. MetaDefender Cloud"), https://metadefender.opswat.com ("VirusTotal")
2. darkhttpd: When you need a web server in a hurry.: https://github.com/emikulic/darkhttpd ([@emikulic](https://github.com/emikulic)), https://unix4lyfe.org/darkhttpd/ ("darkhttpd" "When you need a web server in a hurry.")
<p><br></p>

### Additional Installed Software
- Apk Analyzer (Martin Styk, sk.styk.martin.apkanalyzer): https://github.com/MartinStyk/AndroidApkAnalyzer (@MartinStyk), https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer
- Chmod calculator (Bonaventura Novellino, com.chmod.calc.o): https://play.google.com/store/apps/details?id=com.chmod.calc.o
- Device Info HW (Andrey Efremov, ru.andr7e.deviceinfohw): https://play.google.com/store/apps/details?id=ru.andr7e.deviceinfohw
- Files (Marc apps & software, com.marc.files): https://play.google.com/store/apps/details?id=com.marc.files
- Firefox Beta: (mozilla-mobile. org.mozilla.firefox_beta): https://github.com/mozilla-mobile/firefox-android (@mozilla-mobile), https://www.mozilla.org/en-US/firefox/browsers/mobile/
- Hash Droid (Hobby One, com.hobbyone.HashDroid): https://f-droid.org/en/packages/com.hobbyone.HashDroid/ , https://github.com/HobbyOneDroid/HashDroid (@HobbyOneDroid), https://play.google.com/store/apps/details?id=com.hobbyone.HashDroid
- Material Files (Hai Zhang, me.zhanghai.android.files): https://github.com/zhanghai/MaterialFiles (@zhanghai), https://play.google.com/store/apps/details?id=me.zhanghai.android.files
- MiX Image (Hootan Parsa, com.mixplorer.addon.image): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- MiX PDF (Hootan Parsa, com.mixplorer.addon.pdf): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- Primitive FTPd (wolpi, org.primftpd): https://github.com/wolpi/prim-ftpd (@wolpi), https://play.google.com/store/apps/details?id=org.primftpd
- RealCalc Scientific Calculator (Quartic Software, uk.co.nickfines.RealCalc): https://play.google.com/store/apps/details?id=uk.co.nickfines.RealCalc
- Simple HTTP Server (Phlox Development, com.phlox.simpleserver): https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- Termux:GUI (termux, com.termux.gui): https://github.com/termux/termux-gui (@termux), https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- USB Device Info (Alexandros Schillings, aws.apps.usbDeviceEnumerator): https://play.google.com/store/apps/details?id=aws.apps.usbDeviceEnumerator


---
---
---

<a id="NoteAfterNote-5"></a><h3 align="center">NoteAfterNote-5<br>Termux And The ext4 Filesystem, Part 5 Of 5: Reading And Writing With debugfs, No Root Required<br>Published: April 16, 2023<br>Link: https://gist.github.com/NoteAfterNote/854468164f8513bea764ac1668489f96</h3>


<p><br></p>

### Mobile Device Configuration
   - Rooted: No
   - Connected to any network: No
   - Operating system: 

         neofetch --stdout|grep --color=never --ignore-case 'os:'
            OS: Android 11 armv7l 
   - CPU:

         neofetch --stdout|grep --color=never --ignore-case 'cpu:'
            CPU: MT6761V/WAB (4) @ 2.001GHz
   - Display resolution: 1440x720
   - Builtin internal storage: 32 Gigabytes
   - Builtin memory: 3 Gigabytes
   - Adoptable Storage: Enabled
   - Application Binary Interface (ABI): armeabi-v7a, 32-bit
   - Linux shell: bash (Bourne Again SHell)
   - Termux wake lock: Always enable
   - Termux packages installed: qemu-system-x86-64 qemu-utils  manpages util-linux teseq vim nano wget android-tools libnfs links openssh man termux-api libusb clang ncurses ncurses-utils asciinema gnutls termux-tools bc samba apache2 traceroute net-tools iproute2 inetutils bsd-games netcat-openbsd nmap nmap-ncat rlwrap dosfstools e2fsprogs pass pass-otp openssl-tool gpgv pwgen openjdk-17 paperkey unrar ncftp lftp darkhttpd file sshpass mutt neomutt alpine neofetch cpufetch progress pv gptfdisk fdisk curl dos2unix lynx gifsicle cadaver mlocate
   - "Termux And The ext4 Filesystem, Part 1 Of 5: Reading And Writing, No Root Required": https://gist.github.com/NoteAfterNote/2558deec94bac7ec9fa58aa5ad5e9d1b , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))

<p><br></p>


---

<p><br></p>

### Termux Session

````
Welcome to Termux!

Community forum: https://termux.com/community
Gitter chat:     https://gitter.im/termux/termux
IRC channel:     #termux on libera.chat

Working with packages:

 * Search packages:   pkg search <query>
 * Install a package: pkg install <package>
 * Upgrade packages:  pkg upgrade

Subscribing to additional repositories:

 * Root:     pkg install root-repo
 * X11:      pkg install x11-repo

Report issues at https://termux.com/issues

#
# "NINE_P_DIR=/storage/emulated/0/Download/qemu-test"
# is from "Termux And The ext4 Filesystem, Part 4 Of 5: 
# QEMU, A Guest Operating System, GNU GRUB Bootloader, 
# And fdisk": https://gist.github.com/NoteAfterNote/0ec14839db016b6d3b905d4eda5db263
#
#
~ $ cd $HOME
~ $
~ $ pwd
/data/data/com.termux/files/home
~ $ export NINE_P_DIR=/storage/emulated/0/Download/qemu-test
~ $
~ $ env
SHELL=/data/data/com.termux/files/usr/bin/bash
COLORTERM=truecolor
HISTCONTROL=ignoreboth
PREFIX=/data/data/com.termux/files/usr
JAVA_HOME=/data/data/com.termux/files/usr/opt/openjdk
TERMUX_IS_DEBUGGABLE_BUILD=1
TERMUX_MAIN_PACKAGE_FORMAT=debian
PWD=/data/data/com.termux/files/home
NINE_P_DIR=/storage/emulated/0/Download/qemu-test
TERMUX_VERSION=0.118.0
EXTERNAL_STORAGE=/sdcard
LD_PRELOAD=/data/data/com.termux/files/usr/lib/libtermux-exec.so
TERMUX_API_VERSION=0.50.1
HOME=/data/data/com.termux/files/home
LANG=en_US.UTF-8
TERMUX_APK_RELEASE=GITHUB
DEX2OATBOOTCLASSPATH=/apex/com.android.art/javalib/core-oj.jar:/apex/com.android.art/javalib/core-libart.jar:/apex/com.android.art/javalib/core-icu4j.jar:/apex/com.android.art/javalib/okhttp.jar:/apex/com.android.art/javalib/bouncycastle.jar:/apex/com.android.art/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/framework-atb-backward-compatibility.jar:/system/framework/mediatek-telephony-base.jar:/system/framework/mediatek-telephony-common.jar:/system/framework/mediatek-common.jar:/system/framework/mediatek-framework.jar:/system/framework/mediatek-ims-common.jar:/system/framework/mediatek-ims-base.jar:/system/framework/mediatek-telecom-common.jar:/system/framework/OPCommonTelephony.jar
TMPDIR=/data/data/com.termux/files/usr/tmp
ANDROID_DATA=/data
TERM=xterm-256color
ANDROID_I18N_ROOT=/apex/com.android.i18n
SHLVL=1
ANDROID_ROOT=/system
BOOTCLASSPATH=/apex/com.android.art/javalib/core-oj.jar:/apex/com.android.art/javalib/core-libart.jar:/apex/com.android.art/javalib/core-icu4j.jar:/apex/com.android.art/javalib/okhttp.jar:/apex/com.android.art/javalib/bouncycastle.jar:/apex/com.android.art/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/framework-atb-backward-compatibility.jar:/system/framework/mediatek-telephony-base.jar:/system/framework/mediatek-telephony-common.jar:/system/framework/mediatek-common.jar:/system/framework/mediatek-framework.jar:/system/framework/mediatek-ims-common.jar:/system/framework/mediatek-ims-base.jar:/system/framework/mediatek-telecom-common.jar:/system/framework/OPCommonTelephony.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar:/apex/com.android.mediaprovider/javalib/framework-mediaprovider.jar:/apex/com.android.os.statsd/javalib/framework-statsd.jar:/apex/com.android.permission/javalib/framework-permission.jar:/apex/com.android.sdkext/javalib/framework-sdkextensions.jar:/apex/com.android.wifi/javalib/framework-wifi.jar:/apex/com.android.tethering/javalib/framework-tethering.jar
ANDROID_TZDATA_ROOT=/apex/com.android.tzdata
TERMUX_APP_PID=4244
PATH=/data/data/com.termux/files/usr/bin
ANDROID_ART_ROOT=/apex/com.android.art
OLDPWD=/data/data/com.termux/files/home
_=/data/data/com.termux/files/usr/bin/env
~ $
~ $
~ $
~ $
~ $ cat << EOF > $NINE_P_DIR/file1.txt    # "here-document" 1
echo $NINE_P_DIR
EOF
~ $
~ $ cat $NINE_P_DIR/file1.txt
echo /storage/emulated/0/Download/qemu-test
~ $
~ $ cat << 'EOF' > $NINE_P_DIR/file2.txt    # "here-document" 2
echo $NINE_P_DIR
EOF
~ $
~ $ cat $NINE_P_DIR/file2.txt
echo $NINE_P_DIR
~ $
~ $ rm $NINE_P_DIR/{file1.txt,file2.txt}
~ $
~ $ ls --color=never -l NINE_P_DIR
ls: cannot access 'NINE_P_DIR': No such file or directory
~ $
~ $ ls -l '$NINE_P_DIR'
ls: cannot access '$NINE_P_DIR': No such file or directory
~ $
~ $ ls --color=never -alR $NINE_P_DIR
/storage/emulated/0/Download/qemu-test:
total 13681712
-rw-rw---- 1 root everybody   51380224 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso
-rw-rw---- 1 root everybody         96 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso.sha256
drwxrwx--- 2 root everybody       4096 Apr 14 10:19 backup
-rw-rw---- 1 root everybody 1073741824 Apr 14 11:46 disk3-1gb.img
-rw-rw---- 1 root everybody          0 Apr 14 11:33 test.txt
-rw-rw---- 1 root everybody 6442450944 Apr 15 11:07 vm-linux-grub.raw
-rw-rw---- 1 root everybody 6442450944 Apr 14 09:53 vm-template-grub.raw

/storage/emulated/0/Download/qemu-test/backup:
total 7340048
-rw-rw---- 1 root everybody 1073741824 Apr 14 04:04 disk3-1gb.img
-rw-rw---- 1 root everybody 6442450944 Apr 14 09:53 vm-template-grub.raw
~ $
~ $ ls --color=never -alR "$NINE_P_DIR"
/storage/emulated/0/Download/qemu-test:
total 13681712
-rw-rw---- 1 root everybody   51380224 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso
-rw-rw---- 1 root everybody         96 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso.sha256
drwxrwx--- 2 root everybody       4096 Apr 14 10:19 backup
-rw-rw---- 1 root everybody 1073741824 Apr 14 11:46 disk3-1gb.img
-rw-rw---- 1 root everybody          0 Apr 14 11:33 test.txt
-rw-rw---- 1 root everybody 6442450944 Apr 15 11:07 vm-linux-grub.raw
-rw-rw---- 1 root everybody 6442450944 Apr 14 09:53 vm-template-grub.raw

/storage/emulated/0/Download/qemu-test/backup:
total 7340048
-rw-rw---- 1 root everybody 1073741824 Apr 14 04:04 disk3-1gb.img
-rw-rw---- 1 root everybody 6442450944 Apr 14 09:53 vm-template-grub.raw
~ $
~ $ tree NINE_P_DIR
NINE_P_DIR  [error opening dir]

0 directories, 0 files
~ $
~ $ tree '$NINE_P_DIR'
$NINE_P_DIR  [error opening dir]

0 directories, 0 files
~ $
~ $ tree "$NINE_P_DIR"
/storage/emulated/0/Download/qemu-test
├── alpine-virt-3.17.3-x86_64.iso
├── alpine-virt-3.17.3-x86_64.iso.sha256
├── backup
│   ├── disk3-1gb.img
│   └── vm-template-grub.raw
├── disk3-1gb.img
├── test.txt
├── vm-linux-grub.raw
└── vm-template-grub.raw

2 directories, 8 files
~ $
~ $
~ $
~ $
~ $ date '+%M:%S' ; dd if=/dev/urandom of=$NINE_P_DIR/disk9-10gb bs=1M count=10240 ; date '+%M:%S'
02:31
10240+0 records in
10240+0 records out
10737418240 bytes (11 GB, 10 GiB) copied, 433.438 s, 24.8 MB/s
09:45
~ $
~ $
~ $ date +%M:%S ; shred --zero --iterations=0 $NINE_P_DIR/disk9-10gb.ext ; date +%M:%S
23:15
29:57
~ $
~ $
~ $
~ $
~ $ echo $PREFIX
/data/data/com.termux/files/usr
~ $
~ $ tree -L 1  $PREFIX
/data/data/com.termux/files/usr
├── bin
├── etc
├── games
├── include
├── lib
├── libexec
├── opt
├── share
├── tmp
└── var

11 directories, 0 files
~ $
~ $ date '+%M:%S' ;du -sch $PREFIX ; date '+%M:%S'
38:13
2.3G    /data/data/com.termux/files/usr
2.3G    total
38:20
~ $
~ $
~ $ date '+%M:%S' ; mkfs.ext4 -m 0 -d $PREFIX $NINE_P_DIR/disk9-10gb.ext ; date '+%M:%S'    # man mkfs.ext4
38:45
mke2fs 1.47.0 (5-Feb-2023)
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: e486791e-6f6d-49fe-9f43-d2b43fffaeed
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Copying files into the device: done
Writing superblocks and filesystem accounting information:done 0

41:29
~ $
~ $ ls --color=never -alR "$NINE_P_DIR"
/storage/emulated/0/Download/qemu-test:
total 24167480
-rw-rw---- 1 root everybody    51380224 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso
-rw-rw---- 1 root everybody          96 Apr  4 20:35 alpine-virt-3.17.3-x86_64.iso.sha256
drwxrwx--- 2 root everybody        4096 Apr 14 10:19 backup
-rw-rw---- 1 root everybody  1073741824 Apr 14 11:46 disk3-1gb.img
-rw-rw---- 1 root everybody 10737418240 Apr 16 06:41 disk9-10gb.ext
-rw-rw---- 1 root everybody           0 Apr 14 11:33 test.txt
-rw-rw---- 1 root everybody  6442450944 Apr 15 11:07 vm-linux-grub.raw
-rw-rw---- 1 root everybody  6442450944 Apr 14 09:53 vm-template-grub.raw

/storage/emulated/0/Download/qemu-test/backup:
total 7340048
-rw-rw---- 1 root everybody 1073741824 Apr 14 04:04 disk3-1gb.img
-rw-rw---- 1 root everybody 6442450944 Apr 14 09:53 vm-template-grub.raw
~ $
~ $ dumpe2fs -h  $NINE_P_DIR/disk9-10gb.ext    # man dumpe2fs
dumpe2fs 1.47.0 (5-Feb-2023)
Filesystem volume name:   <none>
Last mounted on:          <not available>
Filesystem UUID:          e486791e-6f6d-49fe-9f43-d2b43fffaeed
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index orphan_file filetype extent 64bit flex_bg metadata_csum_seed sparse_super large_file huge_file dir_nlink extra_isize metadata_csum
Filesystem flags:         unsigned_directory_hash
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              655360
Block count:              2621440
Reserved block count:     0
Overhead clusters:        66747
Free blocks:              2135235
Free inodes:              587687
First block:              0
Block size:               4096
Fragment size:            4096
Group descriptor size:    64
Reserved GDT blocks:      1024
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Sun Apr 16 06:38:45 2023
Last mount time:          n/a
Last write time:          Sun Apr 16 06:41:29 2023
Mount count:              0
Maximum mount count:      -1
Last checked:             Sun Apr 16 06:38:45 2023
Check interval:           0 (<none>)
Lifetime writes:          1880 MB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:               256
Required extra isize:     32
Desired extra isize:      32
Journal inode:            8
Default directory hash:   half_md4
Directory Hash Seed:      1b5d6333-5f0b-4dc1-9935-ea84bb64d585
Journal backup:           inode blocks
Checksum type:            crc32c
Checksum:                 0xcac8fc7e
Checksum seed:            0x2b3b3ec8
Orphan file inode:        12
Journal features:         (none)
Total journal size:       64M
Total journal blocks:     16384
Max transaction length:   16384
Fast commit length:       0
Journal sequence:         0x00000001
Journal start:            0

~ $
~ $ e2label $NINE_P_DIR/disk9-10gb.ext    # man e2label

~ $
~ $ e2label $NINE_P_DIR/disk9-10gb.ext disk9-10gb
~ $
~ $ e2label $NINE_P_DIR/disk9-10gb.ext
disk9-10gb
~ $
~ $ dumpe2fs -h  $NINE_P_DIR/disk9-10gb.ext | grep 'Filesystem volume name:'
dumpe2fs 1.47.0 (5-Feb-2023)
Filesystem volume name:   disk9-10gb
~ $
~ $
~ $
~ $ export DEBUGFS_PAGER=cat   # man debugfs
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/disk9-10gb.ext    # man debugfs
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
     11   40700 (2)      0      0   16384 16-Apr-2023 06:38 lost+found
     13   40700 (2)  10189  10189   24576  9-Apr-2023 02:33 bin
   1293   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 etc
   1545   40700 (2)  10189  10189    4096 13-Oct-2022 19:33 games
   1554   40700 (2)  10189  10189   12288 29-Mar-2023 02:31 include
  15311   40700 (2)  10189  10189   24576 29-Mar-2023 02:31 lib
  27160   40700 (2)  10189  10189    4096 29-Mar-2023 02:31 libexec
  27606   40700 (2)  10189  10189    4096 16-Dec-2022 01:48 opt
  28280   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 share
  66739   40700 (2)  10189  10189    4096 16-Apr-2023 05:54 tmp
  66742   40700 (2)  10189  10189    4096 23-Feb-2023 17:04 var

~ $
~ $ debugfs -R 'dirsearch /bin termux-info' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
Entry found at logical block 4, phys 50989, offset 2488
offset 2488
~ $
~ $ debugfs -R "dump /bin/termux-info $NINE_P_DIR/termux-info.backup" $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
~ $
~ $ whereis termux-info
termux-info: /data/data/com.termux/files/usr/bin/termux-info
~ $
~ $ sha256sum $NINE_P_DIR/termux-info.backup /data/data/com.termux/files/usr/bin/termux-info
b3e748059dcb1bb22784e8f6eb2a16e2f61ffa624850b55c9ae61185b0f3c6ca  /storage/emulated/0/Download/qemu-test/termux-info.backup
b3e748059dcb1bb22784e8f6eb2a16e2f61ffa624850b55c9ae61185b0f3c6ca  /data/data/com.termux/files/usr/bin/termux-info
~ $
~ $ debugfs -R "write $NINE_P_DIR/termux-info.backup termux-info.backup" $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
write: Filesystem opened read/only
~ $
~ $ debugfs -w -R "write $NINE_P_DIR/termux-info.backup termux-info.backup.on.disk9-10gb" $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
Allocated inode: 67674
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
     11   40700 (2)      0      0   16384 16-Apr-2023 06:38 lost+found
     13   40700 (2)  10189  10189   24576  9-Apr-2023 02:33 bin
   1293   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 etc
   1545   40700 (2)  10189  10189    4096 13-Oct-2022 19:33 games
   1554   40700 (2)  10189  10189   12288 29-Mar-2023 02:31 include
  15311   40700 (2)  10189  10189   24576 29-Mar-2023 02:31 lib
  27160   40700 (2)  10189  10189    4096 29-Mar-2023 02:31 libexec
  27606   40700 (2)  10189  10189    4096 16-Dec-2022 01:48 opt
  28280   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 share
  66739   40700 (2)  10189  10189    4096 16-Apr-2023 05:54 tmp
  66742   40700 (2)  10189  10189    4096 23-Feb-2023 17:04 var
  67674  100660 (1)      0      0    3270 16-Apr-2023 06:47 termux-info.backup.on.disk9-10gb

~ $
~ $ debugfs -R 'stat termux-info.backup.on.disk9-10gb' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
Inode: 67674   Type: regular    Mode:  0660   Flags: 0x80000
Generation: 0    Version: 0x00000000:00000000
User:     0   Group:     0   Project:     0   Size: 3270
File ACL: 0
Links: 1   Blockcount: 8
Fragment:  Address: 0    Number: 0    Size: 0
 ctime: 0x643bd245:00000000 -- Sun Apr 16 06:47:33 2023
 atime: 0x643bd245:00000000 -- Sun Apr 16 06:47:33 2023
 mtime: 0x643bd245:00000000 -- Sun Apr 16 06:47:33 2023
crtime: 0x643bd245:00000000 -- Sun Apr 16 06:47:33 2023
Size of extra inode fields: 32
Inode checksum: 0x9085221a
EXTENTS:
(0):433844
~ $
~ $ debugfs -R 'rm /termux-info.backup.on.disk9-10gb' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
rm: Filesystem opened read/only
~ $
~ $ debugfs -w -R 'rm /termux-info.backup.on.disk9-10gb' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)

~ $
~ $ debugfs -R 'stat termux-info.backup.on.disk9-10gb' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
termux-info.backup.on.disk9-10gb: File not found by ext2_lookup
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
     11   40700 (2)      0      0   16384 16-Apr-2023 06:38 lost+found
     13   40700 (2)  10189  10189   24576  9-Apr-2023 02:33 bin
   1293   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 etc
   1545   40700 (2)  10189  10189    4096 13-Oct-2022 19:33 games
   1554   40700 (2)  10189  10189   12288 29-Mar-2023 02:31 include
  15311   40700 (2)  10189  10189   24576 29-Mar-2023 02:31 lib
  27160   40700 (2)  10189  10189    4096 29-Mar-2023 02:31 libexec
  27606   40700 (2)  10189  10189    4096 16-Dec-2022 01:48 opt
  28280   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 share
  66739   40700 (2)  10189  10189    4096 16-Apr-2023 05:54 tmp
  66742   40700 (2)  10189  10189    4096 23-Feb-2023 17:04 var

~ $
~ $
~ $
~ $ ls -l $NINE_P_DIR/../50gb.ext
-rw-rw---- 1 root everybody 53687091200 Apr 16 05:57 /storage/emulated/0/Download/qemu-test/../50gb.ext
~ $
~ $ file $NINE_P_DIR/../50gb.ext
/storage/emulated/0/Download/qemu-test/../50gb.ext: 
Linux rev 1.0 ext4 filesystem data, UUID=ed64f636-1b13-4695-ad66-82236229d6e4, volume name "50gb" (extents) (64bit) (large files) (huge files)
~ $
~ $ stat $NINE_P_DIR/../50gb.ext
  File: /storage/emulated/0/Download/qemu-test/../50gb.ext
  Size: 53687091200     Blocks: 104857624  IO Block: 4096   regular file
Device: 0,84    Inode: 2130464     Links: 1
Access: (0660/-rw-rw----)  Uid: (    0/    root)   Gid: ( 9997/everybody)
Access: 2023-04-08 02:53:18.872059396 -0400
Modify: 2023-04-16 05:57:59.052009372 -0400
Change: 2023-04-16 05:57:59.052009372 -0400
 Birth: -
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/../50gb.ext
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)   1000   1000    4096 27-Mar-2023 01:44 .
      2   40755 (2)   1000   1000    4096 27-Mar-2023 01:44 ..
     11   40700 (2)      0      0   16384 27-Mar-2023 01:28 lost+found
 655361   40775 (2)   1000   1000    4096 12-Jan-2023 19:57 alpine
 2883585   40755 (2)   1000   1000    4096 12-Dec-2022 06:48 termux

~ $
~ $ debugfs -R 'ls -l alpine/v3.17/releases/x86_64' $NINE_P_DIR/../50gb.ext
debugfs 1.47.0 (5-Feb-2023)
 2490369   40755 (2)   1000   1000    4096  4-Apr-2023 20:35 .
 655365   40755 (2)   1000   1000    4096 23-Feb-2023 00:01 ..
 2490371  100644 (1)   1000   1000     833 12-Jan-2023 20:28 alpine-extended-3.17.0-x86_64.iso.asc
 2490370  100644 (1)   1000   1000   811597824 12-Jan-2023 20:28 alpine-extended-3.17.0-x86_64.iso
 2490375  100644 (1)   1000   1000     104 12-Jan-2023 20:28 alpine-extended-3.17.0_rc1-x86_64.iso.sha256
 2490372  100644 (1)   1000   1000     100 12-Jan-2023 20:28 alpine-extended-3.17.0-x86_64.iso.sha256
 2490373  100644 (1)   1000   1000     164 12-Jan-2023 20:28 alpine-extended-3.17.0-x86_64.iso.sha512
 2490374  100644 (1)   1000   1000   714080256 12-Jan-2023 20:28 alpine-extended-3.17.0_rc1-x86_64.iso
 2490376  100644 (1)   1000   1000     168 12-Jan-2023 20:28 alpine-extended-3.17.0_rc1-x86_64.iso.sha512
 2490377  100644 (1)   1000   1000   811597824 12-Jan-2023 20:29 alpine-extended-3.17.0_rc3-x86_64.iso
 2490378  100644 (1)   1000   1000     104 12-Jan-2023 20:29 alpine-extended-3.17.0_rc3-x86_64.iso.sha256
 2490379  100644 (1)   1000   1000     168 12-Jan-2023 20:29 alpine-extended-3.17.0_rc3-x86_64.iso.sha512
 2490380  100644 (1)   1000   1000   811597824 12-Jan-2023 20:29 alpine-extended-3.17.0_rc4-x86_64.iso
 2490381  100644 (1)   1000   1000     104 12-Jan-2023 20:29 alpine-extended-3.17.0_rc4-x86_64.iso.sha256
 2490382  100644 (1)   1000   1000     168 12-Jan-2023 20:29 alpine-extended-3.17.0_rc4-x86_64.iso.sha512
 2490383  100644 (1)   1000   1000   814743552 12-Jan-2023 20:30 alpine-extended-3.17.1-x86_64.iso
 2490384  100644 (1)   1000   1000     833 12-Jan-2023 20:30 alpine-extended-3.17.1-x86_64.iso.asc
 2490385  100644 (1)   1000   1000     100 12-Jan-2023 20:30 alpine-extended-3.17.1-x86_64.iso.sha256
 2490386  100644 (1)   1000   1000     164 12-Jan-2023 20:30 alpine-extended-3.17.1-x86_64.iso.sha512
 2490387  100644 (1)   1000   1000   814743552 13-Feb-2023 06:35 alpine-extended-3.17.2-x86_64.iso
 2490388  100644 (1)   1000   1000     833 13-Feb-2023 06:35 alpine-extended-3.17.2-x86_64.iso.asc
 2490389  100644 (1)   1000   1000     100 13-Feb-2023 06:35 alpine-extended-3.17.2-x86_64.iso.sha256
 2490390  100644 (1)   1000   1000     164 13-Feb-2023 06:35 alpine-extended-3.17.2-x86_64.iso.sha512
 2490391  100644 (1)   1000   1000   51380224 12-Jan-2023 20:31 alpine-virt-3.17.0-x86_64.iso
 2490392  100644 (1)   1000   1000     833 12-Jan-2023 20:31 alpine-virt-3.17.0-x86_64.iso.asc
 2490393  100644 (1)   1000   1000      96 12-Jan-2023 20:31 alpine-virt-3.17.0-x86_64.iso.sha256
 2490394  100644 (1)   1000   1000     160 12-Jan-2023 20:31 alpine-virt-3.17.0-x86_64.iso.sha512
 2490395  100644 (1)   1000   1000   51380224 12-Jan-2023 20:31 alpine-virt-3.17.0_rc1-x86_64.iso
 2490396  100644 (1)   1000   1000     100 12-Jan-2023 20:31 alpine-virt-3.17.0_rc1-x86_64.iso.sha256
 2490397  100644 (1)   1000   1000     164 12-Jan-2023 20:31 alpine-virt-3.17.0_rc1-x86_64.iso.sha512
 2490398  100644 (1)   1000   1000   51380224 12-Jan-2023 20:31 alpine-virt-3.17.0_rc3-x86_64.iso
 2490399  100644 (1)   1000   1000     100 12-Jan-2023 20:31 alpine-virt-3.17.0_rc3-x86_64.iso.sha256
 2490400  100644 (1)   1000   1000     164 12-Jan-2023 20:31 alpine-virt-3.17.0_rc3-x86_64.iso.sha512
 2490401  100644 (1)   1000   1000   51380224 12-Jan-2023 20:31 alpine-virt-3.17.0_rc4-x86_64.iso
 2490402  100644 (1)   1000   1000     100 12-Jan-2023 20:31 alpine-virt-3.17.0_rc4-x86_64.iso.sha256
 2490403  100644 (1)   1000   1000     164 12-Jan-2023 20:31 alpine-virt-3.17.0_rc4-x86_64.iso.sha512
 2490404  100644 (1)   1000   1000   51380224 12-Jan-2023 20:31 alpine-virt-3.17.1-x86_64.iso
 2490405  100644 (1)   1000   1000     833 12-Jan-2023 20:31 alpine-virt-3.17.1-x86_64.iso.asc
 2490406  100644 (1)   1000   1000      96 12-Jan-2023 20:31 alpine-virt-3.17.1-x86_64.iso.sha256
 2490407  100644 (1)   1000   1000     160 12-Jan-2023 20:31 alpine-virt-3.17.1-x86_64.iso.sha512
 2490408  100644 (1)   1000   1000   51380224 13-Feb-2023 06:36 alpine-virt-3.17.2-x86_64.iso
 2490409  100644 (1)   1000   1000     833 13-Feb-2023 06:36 alpine-virt-3.17.2-x86_64.iso.asc
 2490410  100644 (1)   1000   1000      96 13-Feb-2023 06:36 alpine-virt-3.17.2-x86_64.iso.sha256
 2490411  100644 (1)   1000   1000     160 13-Feb-2023 06:36 alpine-virt-3.17.2-x86_64.iso.sha512
 2490412  100644 (1)   1000   1000    3318 12-Jan-2023 20:31 latest-releases.yaml
 2490413  100644 (1)   1000   1000   816840704  4-Apr-2023 20:34 alpine-extended-3.17.3-x86_64.iso
 2490414  100644 (1)   1000   1000     833  4-Apr-2023 20:34 alpine-extended-3.17.3-x86_64.iso.asc
 2490415  100644 (1)   1000   1000     100  4-Apr-2023 20:34 alpine-extended-3.17.3-x86_64.iso.sha256
 2490416  100644 (1)   1000   1000     164  4-Apr-2023 20:34 alpine-extended-3.17.3-x86_64.iso.sha512
 2490417  100644 (1)   1000   1000   51380224  4-Apr-2023 20:35 alpine-virt-3.17.3-x86_64.iso
 2490418  100644 (1)   1000   1000     833  4-Apr-2023 20:35 alpine-virt-3.17.3-x86_64.iso.asc
 2490419  100644 (1)   1000   1000      96  4-Apr-2023 20:35 alpine-virt-3.17.3-x86_64.iso.sha256
 2490420  100644 (1)   1000   1000     160  4-Apr-2023 20:35 alpine-virt-3.17.3-x86_64.iso.sha512

~ $
~ $ debugfs -R "ls -l /termux/packages.termux.dev/apt/termux-main/pool/main/q"  $NINE_P_DIR/../50gb.ext
debugfs 1.47.0 (5-Feb-2023)
 2883648   40755 (2)   1000   1000    4096 10-Dec-2022 05:42 .
 2883599   40755 (2)   1000   1000    4096 10-Dec-2022 05:46 ..
 3015976   40755 (2)   1000   1000    4096  6-Mar-2023 19:31 qalc-static
 3015977   40755 (2)   1000   1000    4096  6-Mar-2023 19:31 qalc
 3015978   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-common
 3015979   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-aarch64-headless
 3015980   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-arm-headless
 3015981   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-i386-headless
 3015982   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-m68k-headless
 3015983   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-ppc-headless
 3015984   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-ppc64-headless
 3015985   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-riscv32-headless
 3015986   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-riscv64-headless
 3015987   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-system-x86-64-headless
 3015988   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-aarch64
 3015989   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-arm
 3015990   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-i386
 3015991   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-m68k
 3015992   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-ppc
 3015993   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-ppc64
 3015994   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-riscv32
 3015995   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-riscv64
 3015996   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-user-x86-64
 3015997   40755 (2)   1000   1000    4096 16-Dec-2022 21:49 qemu-utils
 3015998   40755 (2)   1000   1000    4096  9-Mar-2023 01:03 qhull-static
 3015999   40755 (2)   1000   1000    4096  9-Mar-2023 01:03 qhull
 3016000   40755 (2)   1000   1000    4096 26-Feb-2023 00:12 qpdf-static
 3016001   40755 (2)   1000   1000    4096 26-Feb-2023 00:12 qpdf
 3016002   40755 (2)   1000   1000    4096 11-Jan-2023 14:44 qrsspig
 3016003   40755 (2)   1000   1000    4096  9-Mar-2023 01:03 quick-lint-js
 3016004   40755 (2)   1000   1000    4096 10-Dec-2022 05:42 quickjs
 3016005   40755 (2)   1000   1000    4096 10-Dec-2022 05:42 quilt

~ $
~ $
~ $ mkdir $NINE_P_DIR/{repository-termux,tmp}
~ $
~ $
~ $ date '+%M:%S' ; debugfs -R "rdump /termux/packages.termux.dev/apt/termux-main/pool/main/q $NINE_P_DIR/repository-termux"  $NINE_P_DIR/../50gb.ext ; date '+%M:%S'
52:47
debugfs 1.47.0 (5-Feb-2023)
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-common/qemu-common_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-aarch64-headless/qemu-system-aarch64-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-arm-headless/qemu-system-arm-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-i386-headless/qemu-system-i386-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-m68k-headless/qemu-system-m68k-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-ppc-headless/qemu-system-ppc-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-ppc64-headless/qemu-system-ppc64-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-riscv32-headless/qemu-system-riscv32-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-riscv64-headless/qemu-system-riscv64-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-system-x86-64-headless/qemu-system-x86-64-headless_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-aarch64/qemu-user-aarch64_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-arm/qemu-user-arm_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-i386/qemu-user-i386_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-m68k/qemu-user-m68k_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-ppc/qemu-user-ppc_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-ppc64/qemu-user-ppc64_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-riscv32/qemu-user-riscv32_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-riscv64/qemu-user-riscv64_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-user-x86-64/qemu-user-x86-64_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/qemu-utils/qemu-utils_1:7.2.0_arm.deb
rdump: Operation not permitted while opening /storage/emulated/0/Download/qemu-test/repository-termux/q/quickjs/quickjs_1:20210327-2_arm.deb
52:50
~ $
~ $ tree $NINE_P_DIR/repository-termux
/storage/emulated/0/Download/qemu-test/repository-termux
└── q
    ├── qalc
    │   └── qalc_4.6.0_arm.deb
    ├── qalc-static
    │   └── qalc-static_4.6.0_arm.deb
    ├── qemu-common
    ├── qemu-system-aarch64-headless
    ├── qemu-system-arm-headless
    ├── qemu-system-i386-headless
    ├── qemu-system-m68k-headless
    ├── qemu-system-ppc-headless
    ├── qemu-system-ppc64-headless
    ├── qemu-system-riscv32-headless
    ├── qemu-system-riscv64-headless
    ├── qemu-system-x86-64-headless
    ├── qemu-user-aarch64
    ├── qemu-user-arm
    ├── qemu-user-i386
    ├── qemu-user-m68k
    ├── qemu-user-ppc
    ├── qemu-user-ppc64
    ├── qemu-user-riscv32
    ├── qemu-user-riscv64
    ├── qemu-user-x86-64
    ├── qemu-utils
    ├── qhull
    │   └── qhull_8.1-alpha3-0_arm.deb
    ├── qhull-static
    │   └── qhull-static_8.1-alpha3-0_arm.deb
    ├── qpdf
    │   └── qpdf_11.3.0_arm.deb
    ├── qpdf-static
    │   └── qpdf-static_11.3.0_arm.deb
    ├── qrsspig
    │   └── qrsspig_0.8.0-1_arm.deb
    ├── quick-lint-js
    │   └── quick-lint-js_2.12.0_arm.deb
    ├── quickjs
    └── quilt
        └── quilt_0.67_all.deb

32 directories, 9 files
~ $
~ $
~ $ debugfs -R "dump /termux/packages.termux.dev/apt/termux-main/pool/main/q/quilt/quilt_0.67_all.deb $NINE_P_DIR/tmp/CopyOf-quilt_0.67_all.deb"  $NINE_P_DIR/../50gb.ext
debugfs 1.47.0 (5-Feb-2023)
~ $
~ $ sha256sum $NINE_P_DIR/repository-termux/q/quilt/quilt_0.67_all.deb $NINE_P_DIR/tmp/CopyOf-quilt_0.67_all.deb
d60ad08a175276a99f0e58f794b4042534d5dc8a66125a7752213ebad9bda330  /storage/emulated/0/Download/qemu-test/repository-termux/q/quilt/quilt_0.67_all.deb
d60ad08a175276a99f0e58f794b4042534d5dc8a66125a7752213ebad9bda330  /storage/emulated/0/Download/qemu-test/tmp/CopyOf-quilt_0.67_all.deb
~ $
~ $
~ $ apt info quilt
Package: quilt
Version: 0.67
Maintainer: @termux
Installed-Size: 705 kB
Depends: coreutils, diffstat, gawk, graphviz, perl
Homepage: https://savannah.nongnu.org/projects/quilt
Download-Size: 358 kB
APT-Sources: http://127.0.0.80:50080/termux/packages.termux.dev/apt/termux-main stable/main arm Packages
Description: Allows you to easily manage large numbers of patches

~ $
~ $ dpkg-deb -c $NINE_P_DIR/tmp/CopyOf-quilt_0.67_all.deb
drwxr-xr-x builder/builder   0 2022-11-16 05:39 ./
drwxr-xr-x builder/builder   0 2022-11-16 05:39 ./data/
drwxr-xr-x builder/builder   0 2022-11-16 05:39 ./data/data/
drwxr-xr-x builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/
drwxr-xr-x builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/files/
drwx------ builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/files/usr/
drwx------ builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/
drwx------ builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/
drwx------ builder/builder   0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/quilt/
-rw------- builder/builder 4013 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/quilt/README.MAIL
lrwxrwxrwx builder/builder    0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/quilt/LICENSE -> ../../LICENSES/GPL-2.0.txt
-rw------- builder/builder 20467 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/quilt/README
-rw------- builder/builder 291088 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/doc/quilt/quilt.pdf
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/
-rwx------ builder/builder   2968 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/files
-rwx------ builder/builder   2524 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/add
-rwx------ builder/builder   2721 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/patches
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/
-rwx------ builder/builder   3525 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/remove-trailing-ws
-rw------- builder/builder  22562 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/patchfns
-rwx------ builder/builder  13137 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/dependency-graph
-rwx------ builder/builder   7978 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/backup-files
-rw------- builder/builder   1022 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/utilfns
-rwx------ builder/builder   6401 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/edmail
-rwx------ builder/builder   5415 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/scripts/inspect-wrapper
-rwx------ builder/builder   1220 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/edit
-rwx------ builder/builder   2446 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/new
-rwx------ builder/builder   1015 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/applied
-rwx------ builder/builder   5941 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/pop
-rwx------ builder/builder    974 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/next
-rwx------ builder/builder   2414 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/revert
-rwx------ builder/builder   1042 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/previous
-rwx------ builder/builder   1540 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/snapshot
-rwx------ builder/builder   2746 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/fold
-rwx------ builder/builder  11733 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/setup
-rwx------ builder/builder   3211 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/header
-rwx------ builder/builder   2495 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/delete
-rwx------ builder/builder   8096 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/refresh
-rwx------ builder/builder   3419 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/annotate
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/compat/
lrwxrwxrwx builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/compat/diffstat -> /data/data/com.termux/files/usr/bin/diffstat
-rwx------ builder/builder    114 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/compat/sendmail
lrwxrwxrwx builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/compat/awk -> /data/data/com.termux/files/usr/bin/gawk
-rwx------ builder/builder   2798 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/graph
-rwx------ builder/builder   8696 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/push
-rwx------ builder/builder   2432 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/upgrade
-rwx------ builder/builder    900 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/top
-rwx------ builder/builder  15805 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/mail
-rwx------ builder/builder   1165 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/unapplied
-rwx------ builder/builder   3126 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/grep
-rwx------ builder/builder   5217 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/import
-rwx------ builder/builder   7898 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/diff
-rwx------ builder/builder   2388 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/fork
-rwx------ builder/builder   1776 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/series
-rwx------ builder/builder   2089 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/remove
-rwx------ builder/builder   2021 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/quilt/rename
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/man/
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/man/man1/
-rw------- builder/builder   2686 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/man/man1/guards.1.gz
-rw------- builder/builder  10121 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/man/man1/quilt.1.gz
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/emacs/
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/emacs/site-lisp/
-rw------- builder/builder  19523 2022-11-16 05:39 ./data/data/com.termux/files/usr/share/emacs/site-lisp/quilt.el
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/etc/
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/etc/bash_completion.d/
-rw------- builder/builder   7117 2022-11-16 05:39 ./data/data/com.termux/files/usr/etc/bash_completion.d/quilt
-rw------- builder/builder   1236 2022-11-16 05:39 ./data/data/com.termux/files/usr/etc/quilt.quiltrc
drwx------ builder/builder      0 2022-11-16 05:39 ./data/data/com.termux/files/usr/bin/
-rwx------ builder/builder   3310 2022-11-16 05:39 ./data/data/com.termux/files/usr/bin/quilt
-rwx------ builder/builder   7293 2022-11-16 05:39 ./data/data/com.termux/files/usr/bin/guards
~ $
~ $
~ $ dumpe2fs -h  $NINE_P_DIR/../50gb.ext
dumpe2fs 1.47.0 (5-Feb-2023)
Filesystem volume name:   50gb
Last mounted on:          /mnt/d4
Filesystem UUID:          ed64f636-1b13-4695-ad66-82236229d6e4
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype extent 64bit flex_bg sparse_super large_file huge_file dir_nlink extra_isize metadata_csum
Filesystem flags:         signed_directory_hash
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              3276800
Block count:              13107200
Reserved block count:     0
Overhead clusters:        284552
Free blocks:              1243884
Free inodes:              3252143
First block:              0
Block size:               4096
Fragment size:            4096
Group descriptor size:    64
Reserved GDT blocks:      1024
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Mon Mar 27 01:28:00 2023
Last mount time:          Sat Apr  8 02:40:45 2023
Last write time:          Sun Apr 16 05:57:58 2023
Mount count:              3
Maximum mount count:      -1
Last checked:             Mon Mar 27 01:28:00 2023
Check interval:           0 (<none>)
Lifetime writes:          47 GB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:               256
Required extra isize:     32
Desired extra isize:      32
Journal inode:            8
Default directory hash:   half_md4
Directory Hash Seed:      b6f57ef5-b9a5-429d-bcf4-d08884e23ec9
Journal backup:           inode blocks
Checksum type:            crc32c
Checksum:                 0x46ee1b5e
Journal features:         journal_incompat_revoke journal_64bit journal_checksum_v3
Total journal size:       256M
Total journal blocks:     65536
Max transaction length:   65536
Fast commit length:       0
Journal sequence:         0x00000107
Journal start:            0
Journal checksum type:    crc32c
Journal checksum:         0xcb0b8022

~ $
~ $
~ $ date '+%M:%S' ; fsck.ext4 $NINE_P_DIR/../50gb.ext ; date '+%M:%S'
56:28
e2fsck 1.47.0 (5-Feb-2023)
50gb: clean, 24657/3276800 files, 11863316/13107200 blocks
56:29
~ $
~ $
~ $
~ $
~ $
~ $ cat << 'DEBUGFS_EOF' > $NINE_P_DIR/copy-iso-to-ext4.txt
mkdir ISO
cd ISO
#
lcd /storage/emulated/0/Download/qemu-test
#
pwd
#
write alpine-virt-3.17.3-x86_64.iso  alpine-virt-3.17.3-x86_64.iso
write alpine-virt-3.17.3-x86_64.iso.sha256 alpine-virt-3.17.3-x86_64.iso.sha256
ls
ls -l
DEBUGFS_EOF
~ $
~ $ date '+%M:%S' ; debugfs -w -f $NINE_P_DIR/copy-iso-to-ext4.txt  $NINE_P_DIR/disk9-10gb.ext ; date '+%M:%S'
04:12
debugfs 1.47.0 (5-Feb-2023)
debugfs: mkdir ISO
debugfs: cd ISO
#
debugfs: lcd /storage/emulated/0/Download/qemu-test
#
debugfs: pwd
[pwd]   INODE:  67674  PATH: /ISO
[root]  INODE:      2  PATH: /
#
debugfs: write alpine-virt-3.17.3-x86_64.iso  alpine-virt-3.17.3-x86_64.iso
Allocated inode: 67675
debugfs: write alpine-virt-3.17.3-x86_64.iso.sha256 alpine-virt-3.17.3-x86_64.iso.sha256
Allocated inode: 67676
debugfs: ls
 67674  (12) .    2  (12) ..    67675  (40) alpine-virt-3.17.3-x86_64.iso
 67676  (4020) alpine-virt-3.17.3-x86_64.iso.sha256
debugfs: ls -l
  67674   40755 (2)      0      0    4096 16-Apr-2023 07:04 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
  67675  100660 (1)      0      0   51380224 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso
  67676  100660 (1)      0      0      96 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso.sha256

04:16
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
     11   40700 (2)      0      0   16384 16-Apr-2023 06:38 lost+found
     13   40700 (2)  10189  10189   24576  9-Apr-2023 02:33 bin
   1293   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 etc
   1545   40700 (2)  10189  10189    4096 13-Oct-2022 19:33 games
   1554   40700 (2)  10189  10189   12288 29-Mar-2023 02:31 include
  15311   40700 (2)  10189  10189   24576 29-Mar-2023 02:31 lib
  27160   40700 (2)  10189  10189    4096 29-Mar-2023 02:31 libexec
  27606   40700 (2)  10189  10189    4096 16-Dec-2022 01:48 opt
  28280   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 share
  66739   40700 (2)  10189  10189    4096 16-Apr-2023 05:54 tmp
  66742   40700 (2)  10189  10189    4096 23-Feb-2023 17:04 var
  67674   40755 (2)      0      0    4096 16-Apr-2023 07:04 ISO

~ $
~ $ debugfs -R 'ls -l ISO' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
  67674   40755 (2)      0      0    4096 16-Apr-2023 07:04 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
  67675  100660 (1)      0      0   51380224 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso
  67676  100660 (1)      0      0      96 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso.sha256

~ $
~ $ cat << DEBUGFS_EOF  > $NINE_P_DIR/copy-files-to-ext4.txt
cd ISO
ls -l
#
pwd
cd ..
pwd
mkdir QEMU
lcd $NINE_P_DIR
#
write vm-template-grub.raw QEMU/vm-template-grub.raw
#
write  vm-linux-grub.raw QEMU/vm-linux-grub.raw
#
write $NINE_P_DIR/disk3-1gb.img QEMU/disk3-1gb.img
ls QEMU
cd QEMU
ls -l
DEBUGFS_EOF
~ $
~ $ date '+%M:%S' ; debugfs -w -f $NINE_P_DIR/copy-files-to-ext4.txt  $NINE_P_DIR/disk9-10gb.ext ; date '+%M:%S'
21:39
debugfs 1.47.0 (5-Feb-2023)
debugfs: cd ISO
debugfs: ls -l
  67674   40755 (2)      0      0    4096 16-Apr-2023 07:04 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
  67675  100660 (1)      0      0   51380224 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso
  67676  100660 (1)      0      0      96 16-Apr-2023 07:04 alpine-virt-3.17.3-x86_64.iso.sha256

#
debugfs: pwd
[pwd]   INODE:  67674  PATH: /ISO
[root]  INODE:      2  PATH: /
debugfs: cd ..
debugfs: pwd
[pwd]   INODE:      2  PATH: /
[root]  INODE:      2  PATH: /
debugfs: mkdir QEMU
debugfs: lcd /storage/emulated/0/Download/qemu-test
#
debugfs: write vm-template-grub.raw QEMU/vm-template-grub.raw
Allocated inode: 67678
#
debugfs: write  vm-linux-grub.raw QEMU/vm-linux-grub.raw
Allocated inode: 67679
#
debugfs: write /storage/emulated/0/Download/qemu-test/disk3-1gb.img QEMU/disk3-1gb.img
Allocated inode: 67680
debugfs: ls QEMU
 67677  (12) .    2  (12) ..    67678  (28) vm-template-grub.raw
 67679  (28) vm-linux-grub.raw    67680  (4004) disk3-1gb.img
debugfs: cd QEMU
debugfs: ls -l
  67677   40755 (2)      0      0    4096 16-Apr-2023 07:21 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
  67678  100660 (1)      0      0   6442450944 16-Apr-2023 07:21 vm-template-grub.raw
  67679  100660 (1)      0      0   6442450944 16-Apr-2023 07:26 vm-linux-grub.raw
  67680  100660 (1)      0      0   1073741824 16-Apr-2023 07:30 disk3-1gb.img

32:31
~ $
~ $ debugfs -R 'ls -l' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
     11   40700 (2)      0      0   16384 16-Apr-2023 06:38 lost+found
     13   40700 (2)  10189  10189   24576  9-Apr-2023 02:33 bin
   1293   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 etc
   1545   40700 (2)  10189  10189    4096 13-Oct-2022 19:33 games
   1554   40700 (2)  10189  10189   12288 29-Mar-2023 02:31 include
  15311   40700 (2)  10189  10189   24576 29-Mar-2023 02:31 lib
  27160   40700 (2)  10189  10189    4096 29-Mar-2023 02:31 libexec
  27606   40700 (2)  10189  10189    4096 16-Dec-2022 01:48 opt
  28280   40700 (2)  10189  10189    4096  9-Apr-2023 02:33 share
  66739   40700 (2)  10189  10189    4096 16-Apr-2023 05:54 tmp
  66742   40700 (2)  10189  10189    4096 23-Feb-2023 17:04 var
  67674   40755 (2)      0      0    4096 16-Apr-2023 07:04 ISO
  67677   40755 (2)      0      0    4096 16-Apr-2023 07:21 QEMU

~ $
~ $ debugfs -R 'ls -l QEMU' $NINE_P_DIR/disk9-10gb.ext
debugfs 1.47.0 (5-Feb-2023)
  67677   40755 (2)      0      0    4096 16-Apr-2023 07:21 .
      2   40755 (2)      0      0    4096 16-Apr-2023 06:38 ..
  67678  100660 (1)      0      0   6442450944 16-Apr-2023 07:21 vm-template-grub.raw
  67679  100660 (1)      0      0   6442450944 16-Apr-2023 07:26 vm-linux-grub.raw
  67680  100660 (1)      0      0   1073741824 16-Apr-2023 07:30 disk3-1gb.img

~ $
~ $ date '+%M:%S' ; fsck.ext4 $NINE_P_DIR/disk9-10gb.ext ; date '+%M:%S'
34:25
e2fsck 1.47.0 (5-Feb-2023)
disk9-10gb: clean, 67680/655360 files, 1708299/2621440 blocks
34:25
~ $
~ $
~ $
~ $
~ $ pwd
/data/data/com.termux/files/home
~ $
~ $

````

---

<p><br></p>

### Reference Links


1. "Configuring LUKS: Linux Unified Key Setup": https://www.redhat.com/sysadmin/disk-encryption-luks
2. "Frequently Asked Questions Cryptsetup/LUKS": https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions
2. "Encrypted Archive with Cryptsetup": https://dashohoxha.gitlab.io/cryptsetup-encrypted-archive/ , https://github.com/dashohoxha ([dashohoxha](https://github.com/dashohoxha)), https://gitlab.com/dashohoxha
2. "Basic Guide To Encrypting Linux Partitions With LUKS": https://linuxconfig.org/basic-guide-to-encrypting-linux-partitions-with-luks , https://linuxconfig.org/how-to-use-a-file-as-a-luks-device-key , https://linuxconfig.org/how-to-use-luks-with-a-detached-header
2. "How To Linux Hard Disk Encryption With LUKS [ cryptsetup encrypt command ]": https://www.cyberciti.biz/security/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/
2. "How to encrypt a single Linux filesystem": https://www.redhat.com/sysadmin/encrypt-single-filesystem (LUKS)
2. "Create an encrypted file vault on Linux": https://opensource.com/article/21/4/linux-encryption (LUKS)
2. "Encrypted filesystems, loop devices, cryptsetup": http://jeromebelleman.gitlab.io/posts/filesystems/cryptsetup/ (LUKS)
2. "luks encryption with loopback file": https://gist.github.com/dbehnke/ad19ca8f1ccf80aebca5 , ([@dbehnke](https://github.com/dbehnke))
2. "An introduction to Linux filesystems": https://opensource.com/life/16/10/introduction-linux-filesystems (Linux "mount" command)
2. "mount Command in Linux | Explained": https://itslinuxfoss.com/mount-command-linux/
2. "How to Mount and Unmount Filesystems in Linux": https://www.baeldung.com/linux/mount-unmount-filesystems (Linux "fdisk" command)
2. "How to Mount and Unmount File Systems in Linux": https://linuxize.com/post/how-to-mount-and-unmount-file-systems-in-linux/  (Linux "fdisk" command)
2. "Managing partitions in Linux with fdisk": https://www.redhat.com/sysadmin/partitions-fdisk
2. "Creating and managing partitions in Linux with parted": https://www.redhat.com/sysadmin/partitions-parted
2. "Linux mount Command with Examples": https://phoenixnap.com/kb/linux-mount-command
2. "An introduction to the Linux /etc/fstab file": https://www.redhat.com/sysadmin/etc-fstab
2. "Chapter 24. Mounting file systems": https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/managing_file_systems/index
2. "Linux: Mount Disk Partition Using LABEL": https://www.cyberciti.biz/faq/rhel-centos-debian-fedora-mount-partition-label/
2. "Linux commands: du and the options you should be using": https://www.redhat.com/sysadmin/du-command-options
2. "Hard links and soft links in Linux explained": https://www.redhat.com/sysadmin/linking-linux-explained
2. "Linux permissions: SUID, SGID, and sticky bit": https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
2. "How to audit permissions with the find command": https://www.redhat.com/sysadmin/audit-permissions-find
2. "Getting started with socat, a multipurpose relay tool for Linux": https://www.redhat.com/sysadmin/getting-started-socat
2. "Basic troubleshooting with telnet and netcat": https://www.redhat.com/sysadmin/telnet-netcat-troubleshooting (Linux "nc" command)
2. Linux "mktemp" command: https://www.gnu.org/software/coreutils/manual/coreutils.html
2. "How to use grep": https://www.redhat.com/sysadmin/how-to-use-grep
2. "Manipulating text at the command line with grep": https://www.redhat.com/sysadmin/manipulating-text-grep
2. "Manipulating text at the command line with sed": https://www.redhat.com/sysadmin/manipulating-text-sed
2. "Manipulating text with sed and grep": https://www.redhat.com/sysadmin/manipulating-text-sed-grep
2. "How to Kill a Process in Linux? Commands to Terminate": https://phoenixnap.com/kb/how-to-kill-a-process-in-linux
2. kill, ps, "Linux Command Basics: 7 commands for process management": https://www.redhat.com/sysadmin/linux-command-basics-7-commands-process-management
2. "Bash scripting: Moving from backtick operator to $ parentheses": https://www.redhat.com/sysadmin/backtick-operator-vs-parens
2. Linux ext4 filesystem: "Filesystems in the Linux kernel": https://docs.kernel.org/filesystems/index.html , https://docs.kernel.org/filesystems/ext4/index.html ("ext4 Data Structures and Algorithms"), https://www.cyberciti.biz/faq/linux-modify-partition-labels-command-to-change-diskname/ ("Linux Change Disk Label Name on EXT2 / EXT3 / EXT4 File Systems"), https://www.redhat.com/sysadmin/disk-space ("Linux sysadmins want to know: Where did my disk space go?")
2. "What sysadmins need to know about using Bash": https://www.redhat.com/sysadmin/bash-navigation
2. "10 basic Linux commands you need to know": https://www.redhat.com/sysadmin/basic-linux-commands
2. "8 fundamental Linux file-management commands for new users": https://www.redhat.com/sysadmin/linux-file-management-commands
2. "8 essential Linux file navigation commands for new users": https://www.redhat.com/sysadmin/Linux-file-navigation-commands
2. "Basic Linux commands and tools every sysadmin should know": https://clockhash.com/blog/basic-linux-commands-and-tools-every-sysadmin-should-know
2. bash: https://www.gnu.org/software/bash/manual/bash.html ("Bash Reference Manual"), https://www.redhat.com/sysadmin/linux-environment-variables ("Linux environment variable tips and tricks"), https://www.redhat.com/sysadmin/scripting-writing-text-file ("Bash scripting: How to write data to text files"), https://www.redhat.com/sysadmin/pipes-command-line-linux ("Working with pipes on the Linux command line" "here-document (heredoc)" "here-string"), https://linuxhint.com/linux-pipe-command-examples/ ("Linux Pipe Command with Examples"), https://www.redhat.com/sysadmin/linux-shell-redirection-pipelining ("How to manipulate files with shell redirection and pipelines in Linux"), https://www.redhat.com/sysadmin/redirect-shell-command-script-output ("How to redirect shell command output"), https://www.redhat.com/sysadmin/history-command ("How to manage your Linux command history"), https://www.redhat.com/sysadmin/parsing-bash-history ("Parsing Bash history in Linux"), https://tldp.org/LDP/abs/html/ ("Advanced Bash-Scripting Guide" "Here Documents"), https://wiki.bash-hackers.org
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. "The Linux man-pages project": https://www.kernel.org/doc/man-pages/ , https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/book/
2. "How to find out what a Linux command does": https://www.redhat.com/sysadmin/linux-command-documentation
2. Linux 'tree" and "ls" commands: https://www.cyberciti.biz/faq/linux-show-directory-structure-command-line/ ("Linux see directory tree structure using tree command"), https://www.redhat.com/sysadmin/ls-command-options ("Sysadmin tools: 11 ways to use the ls command in Linux"), https://www.redhat.com/sysadmin/Linux-file-navigation-commands ("8 essential Linux file navigation commands for new users")
2. "How to Use the less, more, and most Commands to Read Text Files in Linux": https://www.makeuseof.com/use-less-more-and-most-linux-commands/
2. Linux text editor "nano": https://www.redhat.com/sysadmin/getting-started-nano ("Getting started with Nano")
2. Linux text editors "vi", "vim", "ed": https://www.redhat.com/sysadmin/get-started-vi-editor ("How to get started with the Vi editor"), https://www.redhat.com/sysadmin/introduction-vi-editor ("An introduction to the vi editor"), https://www.redhat.com/sysadmin/beginners-guide-vim ("Linux basics: A beginner's guide to text editing with vim"), https://www.redhat.com/sysadmin/vim-commands ("Vim: Basic and intermediate commands"), https://www.redhat.com/sysadmin/introduction-ed-editor ("How to get started with the ed text editor")
2. Linux web browswer "links": http://links.twibright.com , http://links.twibright.com/download.php ("Documentation"), https://www.tecmint.com/command-line-web-browsers/ ("A Command Line Web Browsing with Lynx and Links Tools")
2. Linux "grep" command: https://www.redhat.com/sysadmin/find-text-files-using-grep ("Find text in files using the Linux grep command")
2. Linux "echo" command: https://phoenixnap.com/kb/echo-command-linux ("Echo Command in Linux (With Examples)"), https://www.tecmint.com/echo-command-in-linux/ ("15 Practical Examples of ‘echo’ command in Linux"), 
2. Linux "find" command: https://www.redhat.com/sysadmin/linux-find-command ("10 ways to use the Linux find command"), : https://www.redhat.com/sysadmin/find-best-friend ("When it comes to Linux system troubleshooting, find is my best friend")
2. Regular expressions (regex): https://www.redhat.com/sysadmin/introducing-regular-expressions ("Introducing regular expressions"), https://www.redhat.com/sysadmin/getting-started-regular-expressions-example ("Getting started with regular expressions: An example"), https://www.redhat.com/sysadmin/regex-grep-data-flow ("Regex and grep: Data flow and building blocks"), https://www.redhat.com/sysadmin/regular-expressions-pulling-it-all-together ("Regular expressions: Pulling it all together"), https://opensource.com/article/18/5/getting-started-regular-expressions ("Getting started with regular expressions")
2. Linux "chmod" command: https://www.redhat.com/sysadmin/linux-file-permissions-xplained ("Linux file permissions explained"), https://www.redhat.com/sysadmin/introduction-chmod ("Linux permissions: An introduction to chmod"), https://www.redhat.com/sysadmin/manage-permissions ("How to manage Linux permissions for users, groups, and others"), https://www.redhat.com/sysadmin/linux-permissions ("What sysadmins need to know about Linux permissions")
2. Linux "bc" command: https://www.gnu.org/software/bc/manual/html_mono/bc.html ("bc" "an arbitrary precision calculator language"), https://linuxconfig.org/bc ("bc command in Linux with examples"), https://web.archive.org/web/20211207113205/docstore.mik.ua/orelly/unix/upt/ch49_03.htm ("Chapter 49 Working with Numbers" "49.3 Gotchas in Base Conversion"), https://www.networkworld.com/article/3681079/converting-numbers-on-linux-among-decimal-hexadecimal-octal-and-binary.html ("Converting numbers on Linux among decimal, hexadecimal, octal, and binary"), https://www.theunixschool.com/2011/05/bc-unix-calculator.html ("bc - Unix calculator"),  https://www.real-world-systems.com/docs/bc.1.html ("bc" "arbitrary precision calculator"), http://www.physics.smu.edu/coan/linux/bc.html ("6. (Very) Brief intro to bc")
2. Linux "apt" command: https://linuxhint.com/debian_sources-list/ ("Understanding and Using Debian sources.list"), https://wiki.debian.org/SourcesList ("Configuring Apt Sources")
2. Web-based Distributed Authoring and Versioning (WebDAV), Linux command "cadaver": http://www.webdav.org , https://docs.vscentrum.be/en/latest/data/cadaver_client_access.html ("Cadaver Client Access"), https://github.com/hpcloud/swift-webdav/blob/master/doc/Cadaver.md ("Using the Cadaver WebDAV Client"). https://help.webpal.net/apis/webdav ("WebPal Resources for Editors, Admins, Collaborators and Coders" "WebDAV Interface")
2. "Alpine User Handbook": https://docs.alpinelinux.org/user-handbook/0.1a/index.html
2. From https://alpinelinux.org download the "Virtual" "x86_64" files: https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso , https://dl-cdn.alpinelinux.org/alpine/v3.17/releases/x86_64/alpine-virt-3.17.3-x86_64.iso.sha256
2. Alpine Linux Wiki: https://wiki.alpinelinux.org
2. "Setting up disks manually": https://wiki.alpinelinux.org/wiki/Setting_up_disks_manually
2. "Bootloaders": https://wiki.alpinelinux.org/wiki/Bootloaders
2. "GNU GRUB": https://www.gnu.org/software/grub/
2. "GNU GRUB Manual 2.06": https://www.gnu.org/software/grub/manual/grub/grub.html
2. "Production Web server: Lighttpd": https://wiki.alpinelinux.org/wiki/Production_Web_server:_Lighttpd
2. "Lighttpd": https://wiki.alpinelinux.org/wiki/Lighttpd
2. Lighttpd: https://redmine.lighttpd.net/projects/lighttpd , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_webdav , https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_auth
2. "htdigest - manage user files for digest authentication": https://httpd.apache.org/docs/2.4/programs/htdigest.html
2. "htpasswd - Manage user files for basic authentication": https://httpd.apache.org/docs/2.4/programs/htpasswd.html
2. "Termux And The ext4 Filesystem, Part 3 Of 5: QEMU, A Guest Operating System, LUKS Encryption, lighttpd, WebDAV": https://gist.github.com/NoteAfterNote/cabd411777f2ad5ae57d3d98c576471c , https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote))
2. ctrl-c (control-c), ctrl-d (control-d): https://www.oreilly.com/library/view/learning-the-unix/1565923901/ch01s04.html ("The Unresponsive Terminal"), https://www.networkworld.com/article/3284105/linux-control-sequence-tricks.html ("Linux control sequence tricks"), https://web.cecs.pdx.edu/~rootd/catdoc/guide/TheGuide_38.html ("UNIX Control-Key Commands")
2. Linux commands "tput init", "tput reset", "tput clear": https://www.gnu.org/software/termutils/manual/termutils-2.0/html_mono/tput.html ("Portable Terminal Control From Scripts"), https://tldp.org/LDP/abs/html/terminalccmds.html ("16.7. Terminal Control Commands"), https://www.cyberciti.biz/tips/bash-fix-the-display.html ("BASH Fix Display and Console Garbage and Gibberish on a Linux / Unix / macOS"), https://bash.cyberciti.biz/guide/Fixing_the_display_with_reset ("Fixing the display with reset")
2. Reset a Termux terminal session at anytime, very useful when lines are truncated while booting: https://wiki.termux.com/wiki/User_Interface ("create new terminal sessions", "specify a session title", "Resetting the terminal"), see https://user-images.githubusercontent.com/21236430/126444437-7570cdcb-e825-4970-97ff-71f41e426b0f.jpg in https://github.com/termux/termux-app/issues/2184#issuecomment-883939230 ("Feature request: termux transcript #2184" "Gameye98 commented on Jul 21, 2021" )
2. "4 System Administration": https://tldp.org/LDP/gs/node6.html
2. "Chapter 1. Getting Started with Linux": https://www.oreilly.com/library/view/practical-linux-system/9781098109028/ch01.html
2. "Reboot Linux System Command": https://www.cyberciti.biz/faq/howto-reboot-linux/
2. "Linux superuser access, explained": https://www.redhat.com/sysadmin/linux-superuser-access
2. "Why Do We Use su – and Not Just su?": https://www.baeldung.com/linux/su-command-options
2. "Linux command line basics: sudo": https://www.redhat.com/sysadmin/sudo
2. "Exploring the differences between sudo and su commands in Linux": https://www.redhat.com/sysadmin/difference-between-sudo-su
2. "Using sudo to delegate permissions in Linux": https://www.redhat.com/sysadmin/using-sudo-delegate
2. "Real sysadmins don't sudo": https://www.redhat.com/sysadmin/sysadmins-dont-sudo
2. "Linux sysadmin basics: User account management": https://www.redhat.com/sysadmin/linux-user-account-management
2. "How to create, delete, and modify groups in Linux": https://www.redhat.com/sysadmin/linux-groups (Linux "id" command)
2. "Linux sysadmin basics: User account management with UIDs and GIDs": https://www.redhat.com/sysadmin/user-account-gid-uid
2. "Managing local group accounts in Linux": https://www.redhat.com/sysadmin/local-group-accounts
2. "How to use a command line random password generator PWGEN on Linux": https://linuxconfig.org/how-to-use-a-command-line-random-password-generator-pwgen-on-linux
2. "Recommendations on Using Assigned Transport Port Numbers": https://www.rfc-editor.org/rfc/rfc7605.html
2. "Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry": https://www.rfc-editor.org/rfc/rfc6335 ("the Dynamic Ports, also known as the Private or Ephemeral Ports, from 49152-65535 (never assigned)")
2. Linux "shuf" command": https://www.gnu.org/software/coreutils/manual/html_node/shuf-invocation.html
2. "Working with File Systems": http://web.archive.org/web/20130423054811/technet.microsoft.com/en-us/library/bb457112.aspx ("4 GB minus 1 byte"), "Working with File Systems": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb457112(v=technet.10)
2. "How FAT Works": https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc776720(v=ws.10)
2. QEMU: https://www.qemu.org , https://github.com/qemu/qemu ([@qemu](https://github.com/qemu)), https://www.qemu.org/docs/master/ , https://wiki.qemu.org , https://github.com/qemu/qemu/tree/master/docs
2. "Device Emulation": https://www.qemu.org/docs/master/system/device-emulation.html ("Common Terms" "Device Front End" "Device Back End"), https://qemu.readthedocs.io/en/latest/system/device-emulation.html
2. "QEMU User Documentation": https://www.qemu.org/docs/master/system/qemu-manpage.html , https://qemu.readthedocs.io/en/latest/system/qemu-manpage.html
2. "QEMU Documentation": https://qemu.readthedocs.io/_/downloads/en/latest/pdf/
2. https://github.com/qemu/qemu/blob/master/qemu-options.hx
2. "QEMU disk image utility": https://www.qemu.org/docs/master/tools/qemu-img.html ("qemu-img create"), https://qemu.readthedocs.io/en/latest/tools/qemu-img.html 
2. "Managing device boot order with bootindex properties": https://www.qemu.org/docs/master/system/bootindex.html , https://qemu.readthedocs.io/en/latest/system/bootindex.html
2. "Network emulation": https://www.qemu.org/docs/master/system/devices/net.html ("Using the user mode network stack" "-net user" "The QEMU VM behaves as if it was behind a firewall which blocks all incoming connections."), 
2. "Documentation/Networking": https://wiki.qemu.org/Documentation/Networking ("hostfwd")
2. "Documentation/9psetup": https://wiki.qemu.org/Documentation/9psetup ("-virtfs"), https://wiki.qemu.org/Documentation/9p
https://wiki.qemu.org/Features/VirtIORNG ("virtio-rng-pci")
2. "QEMU command-line: behavior of ‘-serial stdio’ vs. ‘-serial mon:stdio’": https://kashyapc.wordpress.com/2016/02/11/qemu-command-line-behavior-of-serial-stdio-vs-serial-monstdio/ ("-serial mon:stdio")
2. "QEMU Monitor": https://www.qemu.org/docs/master/system/monitor.html , https://qemu.readthedocs.io/en/latest/system/monitor.html
2. "Keys in the character backend multiplexer": https://www.qemu.org/docs/master/system/mux-chardev.html ("Ctrl-a h", "Ctrl-a t", "Ctrl-a c", "Ctrl-a x"), https://qemu.readthedocs.io/en/latest/system/mux-chardev.html
2. "Introduction": https://www.qemu.org/docs/master/system/introduction.html ("QEMU provides a number of management interfaces including a line based Human Monitor Protocol (HMP) that allows you to dynamically add and remove devices as well as introspect the system state.")
2. "Security": https://www.qemu.org/docs/master/system/security.html ("Monitor console (QMP and HMP)", "The general recommendation is that the monitor console should be exposed over a UNIX domain socket backend to the local host only."), https://qemu.readthedocs.io/en/latest/system/security.html
2. "QemuDiskHotplug": https://wiki.ubuntu.com/QemuDiskHotplug and
2. "QEMU Human Monitor Interface, Example Usage": https://web.archive.org/web/20180104171638/nairobi-embedded.org/qemu_monitor_console.html ("Nographic Mode")
2. Check the apps: https://www.virustotal.com/gui/home/url ("OPSWAT. MetaDefender Cloud"), https://metadefender.opswat.com ("VirusTotal")
2. darkhttpd: When you need a web server in a hurry.: https://github.com/emikulic/darkhttpd ([@emikulic](https://github.com/emikulic)), https://unix4lyfe.org/darkhttpd/ ("darkhttpd" "When you need a web server in a hurry.")
<p><br></p>

### Additional Installed Software
- Apk Analyzer (Martin Styk, sk.styk.martin.apkanalyzer): https://github.com/MartinStyk/AndroidApkAnalyzer (@MartinStyk), https://play.google.com/store/apps/details?id=sk.styk.martin.apkanalyzer
- Chmod calculator (Bonaventura Novellino, com.chmod.calc.o): https://play.google.com/store/apps/details?id=com.chmod.calc.o
- Device Info HW (Andrey Efremov, ru.andr7e.deviceinfohw): https://play.google.com/store/apps/details?id=ru.andr7e.deviceinfohw
- Files (Marc apps & software, com.marc.files): https://play.google.com/store/apps/details?id=com.marc.files
- Firefox Beta: (mozilla-mobile. org.mozilla.firefox_beta): https://github.com/mozilla-mobile/firefox-android (@mozilla-mobile), https://www.mozilla.org/en-US/firefox/browsers/mobile/
- Hash Droid (Hobby One, com.hobbyone.HashDroid): https://f-droid.org/en/packages/com.hobbyone.HashDroid/ , https://github.com/HobbyOneDroid/HashDroid (@HobbyOneDroid), https://play.google.com/store/apps/details?id=com.hobbyone.HashDroid
- Material Files (Hai Zhang, me.zhanghai.android.files): https://github.com/zhanghai/MaterialFiles (@zhanghai), https://play.google.com/store/apps/details?id=me.zhanghai.android.files
- MiX Image (Hootan Parsa, com.mixplorer.addon.image): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- MiX PDF (Hootan Parsa, com.mixplorer.addon.pdf): https://forum.xda-developers.com/t/app-2-2-mixplorer-v6-x-released-fully-featured-file-manager.1523691/ ("Downloads")
- Primitive FTPd (wolpi, org.primftpd): https://github.com/wolpi/prim-ftpd (@wolpi), https://play.google.com/store/apps/details?id=org.primftpd
- RealCalc Scientific Calculator (Quartic Software, uk.co.nickfines.RealCalc): https://play.google.com/store/apps/details?id=uk.co.nickfines.RealCalc
- Simple HTTP Server (Phlox Development, com.phlox.simpleserver): https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- Termux:GUI (termux, com.termux.gui): https://github.com/termux/termux-gui (@termux), https://play.google.com/store/apps/details?id=com.phlox.simpleserver
- USB Device Info (Alexandros Schillings, aws.apps.usbDeviceEnumerator): https://play.google.com/store/apps/details?id=aws.apps.usbDeviceEnumerator


---
---
---

<a id="NoteAfterNote-6"></a><h3 align="center">NoteAfterNote-6<br>Experimental: FTP, Termux, QEMU<br>Published: April 18, 2023<br>Link: https://gist.github.com/NoteAfterNote/1ead8e2b91f10cefd8b4cbcb41cb7f5a

<p><br></p>

### Configuring vsftpd

- QEMU Guest Operating System: vsftpd.conf
````
   seccomp_sandbox=NO
   pasv_enable=YES
   pasv_min_port=10000
   pasv_max_port=10005
````

- QEMU firewall
````
   QEMU HMP Monitor Commands
   
   hostfwd_add ::10021-:21
   hostfwd_add ::10001-:10001
   hostfwd_add ::10002-:10002
   hostfwd_add ::10003-:10003
   hostfwd_add ::10004-:10004
   hostfwd_add ::10004-:10005

   
   QEMU command line
   
   -device virtio-net-pci,netdev=net0 -netdev user,id=net0,ipv6=off,hostfwd=::10021-:21,hostfwd=::10001-:10001,hostfwd=::10002-:10002,hostfwd=::10003-:10003,hostfwd=::10004-:10004,hostfwd=::10005-:10005
````

<p><br></p>


### Client: ftp

````
   # Needs testing: Connecting from the guest operating system
      ftp --passive 10.0.2.2 12345
         anonymous
         guest
         epsv4
         binary
 
   # Needs testing: From Termux to vsftpd
      ftp --passive 127.0.0.1 10021
         anonymous
         guest
         epsv4
         binary
 ````

<p><br></p>

### Client: lftp

````
   # Connecting from the guest operating system worked
   # without additional configuration or commands.

    lftp -p 10021 10.0.2.2
````


<p><br></p>

### Reference Links

1. vsftpd: https://security.appspot.com/vsftpd.html , https://security.appspot.com/vsftpd/Changelog.txt ("seccomp_sandbox")
2. GNU Inetutils: https://www.gnu.org/software/inetutils/manual/inetutils.html ("ftp: FTP client")
2. LFTP: https://lftp.yar.ru , https://github.com/lavv17/lftp ([@lavv17](https://github.com/lavv17/lftp))
2. "Termux And The ext4 Filesystem, Part 2 Of 5: QEMU, A Guest Operating System, And darkhttpd", NoteAfterNote-2, April 7, 2023: https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote)), https://gist.github.com/NoteAfterNote/f5bd5e127d0768cb4eac53fb7729d29f
2. "The ext4 Filesystem, Part 3 Of 5: QEMU, A Guest Operating System, LUKS Encryption, lighttpd, WebDAV", NoteAfterNote-3, April 12, 2023: QEMU, A Guest Operating System, GNU GRUB Bootloader, And fdisk", NoteAfterNote-4, April 14, 2023, https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote)), https://gist.github.com/NoteAfterNote/cabd411777f2ad5ae57d3d98c576471c
2. "Termux And The ext4 Filesystem, Part 4 Of 5: QEMU, A Guest Operating System, GNU GRUB Bootloader, And fdisk", NoteAfterNote-4, April 14, 2023, https://github.com/NoteAfterNote ([@NoteAfterNote](https://github.com/NoteAfterNote)), https://gist.github.com/NoteAfterNote/0ec14839db016b6d3b905d4eda5db263

---
---
---
