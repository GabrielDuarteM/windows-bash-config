# Windows 10 bash config

1. enable `Windows Subsystem for Linux (Beta)`
2. inside bash, run:
* `sudo apt-get install -y zsh`
* `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
* edit `~/.zshrc`
* change `ZSH_THEME` to `agnoster`
* add the following to the end of the file:
```
# Removes username@computer from prompt
DEFAULT_USER=$USER
```
* exit `~/.zshrc` and edit `~/.bashrc`
* add the following lines
 ```
# Launch Zsh
if [ -t 1 ]; then
exec zsh
fi
 ```
3. open powershell
4. clone `https://github.com/powerline/fonts.git --depth=1`
5. `cd fonts/`
6. run .\install.ps1 (if you get an error about `about_Execution_Policies`, open powershell as admin and run `Set-ExecutionPolicy Unrestricted` ([more info on that](https://docs.microsoft.com/pt-br/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core)))
7. open `regedit`		
8. go to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Console\TrueTypeFont`		
9. add a new registry with the key `Meslo LG L DZ for Powerline` ([more info on that](https://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-enable-more-fonts-for-the-windows-command-prompt/))		
10. reboot the computer		
11. open bash and go to properties > fonts > change the font to `Meslo LG L DZ for Powerline`


# Cmder config to work with zsh
1. open the settings
2. change the main console font to `Meslo LG L DZ for Powerline`
3. change size to 18
4. change unicode ranges to `Pseudographics: 2013-25C4;`
5. go to `Startup > Tasks` and add a new task `{bash::bash for windows}` with value `%windir%\system32\bash.exe -cur_console:p1`
6. set the `{bash::bash for windows}` as default shell
7. go to `Integration`
8. set `command` to `/single -run {bash::bash for windows}`
9. set `Icon file` to `<PATH/TO/CMDER>\vendor\conemu-maximus5\ConEmu64.exe,0`
10. click register
11. go to `Main > Appearance`
12. uncheck `Enhance progressbars and scrollbars` under the `Appearance` group
13. save settings

# VSCode config to work with zsh
1. add the following lines to `settings.json`
```
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe",
"terminal.integrated.lineHeight": 1.6,
"terminal.integrated.fontFamily": "Meslo LG L DZ for Powerline",  
```

# Warnings
* Always use a linux environment to edit linux files, don't ever edit linux files from windows. If you do so, linux will stop recognizing the file. Edit windows files inside linux is allowed.
* If you ever edit by accident a linux file inside windows, run the following commands:
1. copy the contents of the edited file using windows, and paste to any other file
2. deleted the file in windows
3. touched the file in linux `touch <PATH/TO/EDITED/FILE.txt>`
4. `sudo vim <PATH/TO/EDITED/FILE.txt>`
5. `:set paste`
6. `i`
7. paste contents of old file into new file.
8. press ESC and then `:wq`

# Troubleshooting
#### `command not found: ^M` error
edit `~/.gitconfig` and remove the following lines:
```
[core]
    autocrlf = true
```
