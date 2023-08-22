# openwith
Superfast, hackable and reliable alternative to xdg-open. Assign your favorites applications to file types.

It follows the Unix philosphy: "doing one thing and doing it well". It associates file extensions or mime types with a list of applications (commands, bin files), the first one of the list being the default one. The list of associations is set in one file, easy to understand, read and edit.

## Use
`$(openwith <file>) <file>` : the file will be opened with the default application.
- It works on multiples files: `$(openwith <file1> <file1> <...>) <file1> <file2> <...>`
- It can check mimetype if the extension of the file doesn't match any application: `$(openwith -m <file>) <file>`<br>
  **! Warning:** checking the mime type is MUCH slower the just checking the extension.
  My tests: ~1.5 sec for 200 files instead of < 0.050 sec by the extension.

#### Openwith can also be usefull in scripting:
`openwith -a <file>` : list all the possible applications you defined for a file type
It is recommanded to combine the -a flag with -o flag for multiples files.

#### Run complex commands?
In the config file, the application names cannot contains spaces (there are supposed to be commands). It is not possible to run commands with flags, for example to run `kitty -e ranger`. To use this kind of complex syntax, just create a script in /usr/local/bin, running the complex command, and run this script instead with openwith.

## Config format
The principle of openwith is to check the file type by the file extension instead of the file type, to be faster and more customizable than xdg-open.
Instead of using the mimeapps.list file to associate a mimetype to a .desktop file executing the application, it associates a file extention to a list of possible applications, the first one being the default one. This list of association is set in a file named by default ~/.config/openwith.conf.

`extension <default app> <secondary apps`<br>
examples: see openwith.conf

But you can ALSO associate apps to mimetype, in the section `[mime]` of the config. All the following associations will be used only with the `-m` flag if the file extension doesn't match any one in the config, or if the file extension is not found. 

NOTES:<br>
You can associate applications to open directories with the `directory` type.<br>
You can define applications by default if the file extension if not found, neither the mime type when `-m` is used, by setting the `unknown` type.<br>
cf. openwith.conf for an example...

## Flags
`-m` : if the file extension is missing or not found in openwith.conf, openwith will check the mime type of the file using the command `file -Lb --mime-type <file>`.
       This process if much slower than checking the file extension, that's why is recommanded to add as much as possible of extension types in openwith.conf to avoid the need of checking the mime type.<br>
`-a` : print the all list of applications associated with a file extension/mime type.<br>
`-o` : print the output on one line only (but associated with `-a`, it will be one line per file).
`-n` : if the file extension if not found (and neither the mime type if `-m` is used), openwith open the file with the application associated with the type `unknown` in openwith.conf. This flag overwrites this behavior and print `null` instead. It is designed to be use in scripting.<br>
`-d` : debug.<br>
`-h/--help` : help.

## Install
Copy openwith to /usr/local/bin.<br>
Copy openwith to ~/.config/openwith.conf (to change its location/name, just edit /usr/local/bin/openwith).
