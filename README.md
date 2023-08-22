# openwith
Superfast, hackable and reliable alternative to xdg-open. Assign your favorites applications to file types.

## Use
`$(openwith <file>) <file>` : the file will be opened with the default application.
- It works on multiples files: `$(openwith <file1> <file1> <...>) <file1> <file2> <...>`
- It can check mimetype if the extension of the file doesn't match any application: `$(openwith -m <file>) <file>`<br>
  **! Warning:** checking the mime type is MUCH slower the just checking the extension.
  My tests: ~1.5 sec for 200 files instead of < 0.050 sec by the extension.

#### Openwith can also be usefull in scripting:
`openwith -a <file>` : list all the possible applications you defined for a file type
It is recommanded to combine the -a flag with -o flag for multiples files.

## Config format
The principle of openwith is to check the file type by the file extension instead of the file type, to be faster and more customizable than xdg-open.
Instead of using the mimeapps.list file to associate a mimetype to a .desktop file executing the application, it associates a file extention to a list of possible applications, the first one being the default one. This list of association is set in a file named by default ~/.config/openwith.conf.

`extension <default app> <secondary apps`<br>
examples: see openwith.conf

But you can ALSO associate apps to mimetype, in the section `[mime]` of the config. All the following associations will be used only with the `-m` flag if the file extension doesn't match any one in the config, or if the file extension is not found. 

## Install
Copy openwith to /usr/local/bin.<br>
Copy openwith to ~/.config/openwith.conf (to change its location/name, just edit /usr/local/bin/openwith).
