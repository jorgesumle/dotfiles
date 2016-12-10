# Table of Contents

<!-- vim-markdown-toc GFM -->
* [Development Environment on Windows](#development-environment-on-windows)
    * [Change Computer Name](#change-computer-name)
    * [Set Time](#set-time)
    * [Install Applications](#install-applications)
    * [Download Applications](#download-applications)
    * [Configure](#configure)
        * [Map Keys](#map-keys)
        * [Track Pad](#track-pad)
        * [Mouse Properties](#mouse-properties)
    * [Dotfiles](#dotfiles)
        * [Git](#git)
        * [Vim](#vim)
            * [Link to Vim Configuration](#link-to-vim-configuration)
            * [Install Vim-Plug](#install-vim-plug)
            * [Install Plugins](#install-plugins)
            * [Diff](#diff)
        * [AutoHotKey](#autohotkey)
        * [Install AutoJump](#install-autojump)
    * [Color Codes](#color-codes)
* [Outdated Content](#outdated-content)
    * [Overview of my dotfiles](#overview-of-my-dotfiles)
    * [Git](#git-1)
    * [Vim](#vim-1)
        * [Auto Close](#auto-close)
        * [Vim Markdown](#vim-markdown)
        * [Fuzzy File Finder](#fuzzy-file-finder)
    * [Bash](#bash)

<!-- vim-markdown-toc -->

# Development Environment on Windows

After installing a fresh copy of Windows 10, do following steps.

## Change Computer Name 

Open *Advanced System Settings* using `rundll32.exe shell32.dll,Control_RunDLL sysdm.cpl,,1`.

1. Click on *Change* button
1. Rename

## Set Time

Open time and date settings using `control timedate.cpl`.

1. Set time zone
1. Use 24 hour time format

## Install Applications

1. Install [SyncTazor](https://github.com/canton7/SyncTrayzor)
	1. Sync with other computers
1. Install [1Password](https://1password.com/downloads/)
1. Install [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/)
    1. Enable Firefox sync
    1. Login to RescueTime plugin
    1. Configure Pray Times plugin
1. Install [RescueTime](https://www.rescuetime.com/get_rescuetime)
1. Install [SharpKeys](https://sharpkeys.codeplex.com/)
1. Install [Git for Windows](https://git-for-windows.github.io/)
1. Setup [Qt](https://download.qt.io/archive/qt/)
	1. Install [Latest Qt Creator](https://www.qt.io/download-open-source/#section-9)
    1. Install [Qt `5.5.1` for Windows 32bit (VS 2013)](https://download.qt.io/archive/qt/5.5/5.5.1/)
1. Install Visual Studio 2013
1. Install [Win32 OpenSSL `1.0.1` Light](https://slproweb.com/products/Win32OpenSSL.html) into Windows System folders
1. Install [AutoHotKey](https://autohotkey.com/)
1. Install [7-Zip](http://www.7-zip.org/download.html)
1. Install [Slack](https://slack.com/downloads)
1. Install Chocolatey Packages
	1. Install [Chocolatey](https://chocolatey.org/install)
    1. Install [Ag - The Silver Searcher](https://github.com/ggreer/the_silver_searcher/wiki/Windows)
1. Install [Python2 and Python3](https://www.python.org/downloads/windows/)
1. Install [Ruby](https://rubyinstaller.org/)
1. [Visual Studio Code](https://code.visualstudio.com/)
	1. Install [Visual Studio Code Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)
    1. Download Visual Studio Code settings
1. Install [Inconsolata fonts](https://github.com/google/fonts/tree/master/ofl/inconsolata)
1. Install [Evernote](https://evernote.com/download/get.php?file=Win)

## Download Applications

Create a folder `bin` in `%HOMEPATH%`, using `mkdir %HOMEPATH%\bin` command. This folder is reffered to as `bin`, henceforth.

Download following apps and extract them in `bin` folder, and add their path to `%PATH%` variable.

To edit `%PATH%` variable, open Environment Variables using `rundll32.exe shell32.dll,Control_RunDLL sysdm.cpl,,3`.

1. [Cmder Mini](http://cmder.net/)
1. [Vim](https://tuxproject.de/projects/vim/)
1. [Lua](http://luabinaries.sourceforge.net/)
	1. Navigate and download from `Windows Libraries/Dynamic` folder

You can check path of each command using `where` command. For example,

```
> where gvim
C:\Users\talha\bin\complete-x64\gvim.exe
```

You can use it to test each downloaded program is available from `%PATH%`.

## Configure

### Map Keys

Use SharpKeys to,

1. Map Caps Lock to Ctrl key

### Track Pad
 
To invert the direction of scrolling (natural scrolling on macOS), run following command in PowerShell with adminstrative privileges.

```powershell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Enum\HID\*\*\Device` Parameters FlipFlopWheel -EA 0 | ForEach-Object { Set-ItemProperty $_.PSPath FlipFlopWheel 1 }
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Enum\HID\*\*\Device` Parameters FlipFlopHScroll  -EA 0 | ForEach-Object { Set-ItemProperty $_.PSPath FlipFlopHScroll 1 }

```

See [SuperUser answer](http://superuser.com/a/364353/42415) for details.

Natural direction of scrolling is how you scroll on iPhone, Android and other touch devices. Content scrolls in the direction of your fingers.

### Mouse Properties

Open mouse properties using `control main.cpl`.

1. In *Buttons* tab, turn on *ClickLock*
	1. In *Settings*, set duration to the shortest possible
2. In *Pointer Options* tab, enable *Show Location of Pointer*
3. In *Wheel* tab, change scroll speed to 1

## Dotfiles

Create a `Repos` directory in `%HOMEPATH%`. Clone [dotfiles repository](https://github.com/talha131/dotfiles).

### Git

Start a `cmd` tab with administrative privilege in Cmder. Create symbolic links thusly,

```
mklink %HOME%\.gitconfig %HOME%\Repos\dotfiles\git\gitconfig
mklink %HOME%\.githelper %HOME%\Repos\dotfiles\git\githelper
mklink %HOME%\bin\diff-highlight %HOME%\Repos\dotfiles\bin\diff-highlight
```

### Vim

Open Vim and check you have Python2, Python3, Ruby, and Lua working, using following commands,

```
:echo has('python3')
:echo has('python')
:echo has('ruby')
:echo has('lua')
```

#### Link to Vim Configuration

Start `cmd` with administrative privilege in Cmder. Create symbolic links thusly,

```
mklink %HOME%\.vimrc %HOME%\Repos\dotfiles\vim\vimrc
mklink /d %HOME%\.vim\ %HOME%\Repos\dotfiles\vim\vim\
```

#### Install Vim-Plug

Open Powershell and type these commands

```powershell
md ~\.vim\autoload
$uri = 'https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
(New-Object Net.WebClient).DownloadFile($uri, $ExecutionContext.SessionState.Path.GetUnresolvedProviderPathFromPSPath("~\.vim\autoload\plug.vim"))
```

#### Install Plugins

Open Vim, ignore errors and issue `:PlugInstall!` to install all plugins and themes.

Restart Vim. This time there should be no errors.

#### Diff

It is possible that diff or Gdiff (from Vim Fugitive) will not. Tuxproject Vim does not include a `diff.exe`.

Check output of

```
:!where diff
```

If the result is empty or Gdiff is not working then copy `diff.exe` from Git into Vim program files folder.

In Cmder,

```
cp "C:\Program Files\Git\usr\bin\diff.exe"    %HOME%\bin\complete-x64
```

See this [Github issue](https://github.com/tpope/vim-fugitive/issues/680#issuecomment-134650380) for details.

### AutoHotKey

To auto start the AutoHotKey script everytime windows starts. Start `cmd` with administrative privilege in Cmder. Create symbolic links thusly,

```
mklink "%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup\key-mappings.ahk" %HOME%\Repos\dotfiles\autohotkey\key-mappings.ahk
```

### Install AutoJump

Cmder already has [Clink](https://mridgers.github.io/clink/). If you are not using Cmder then you must install Clink manually.

1. Clone [AutoJump](https://github.com/wting/autojump)
1. Add [patch](https://github.com/wting/autojump/issues/436)
1. Install AutoJump
1. Successful installation will output a path, add this path your `%PATH%`.

## Color Codes

To have [Gruvbox](https://github.com/morhetz/gruvbox) dark theme like background in `cmd` or Git shell, use following color codes:

|   Color Values    | Red | Green | Blue |
|        ---        | --- |  ---  | ---  |
| Screen Background | 44  |  44   |  44  |
|    Screen Text    | 218 |  198  | 144  |

# Outdated Content

I need to review and update following portion of this file.

Overview of my dotfiles
-----------------------

These configuration files do not work out of the box. These are specific to my Mac OSX system.

Following are my not so comprehensive and perhaps out of date notes.

Git
---

1.  [David DeSandro](http://dropshado.ws/post/7844857440/gitconfig-colors) blog entry is a good start point.
2.  [Cheat sheets](http://cheat.errtheblog.com/s/git) has more comprehensive entry.

Vim
---

1.  [Vrome](https://chrome.google.com/webstore/detail/godjoomfiimiddapohpmfklhgmbfffjj) is a Google Chrome extension.

### Auto Close

1.  [SO thread](http://stackoverflow.com/q/883437/177116) has got some good comments.
1.  I decided to use Thiago Alves/Townk's [plugin](https://github.com/Townk/vim-autoclose).
1.  [Townk's plugin tutorial](http://www.vim.org/scripts/script.php?script_id=2009).

### Vim Markdown

1.  [tpope/vim-markdown](https://github.com/tpope/vim-markdown) is mostly used. But it does not conceal text markers in Markdown file.
2.  [xolox/vim-markdown](https://github.com/xolox/vim-markdown) does the concealing. See [this image](https://github.com/tpope/vim-markdown/pull/9#issuecomment-3098050) for example.
3.  But you have to switch to xolox/vim-markdown `conceal` branch to get his code. Use `git checkout -b conceal remotes/origin/conceal` to
    checkout the branch.

### Fuzzy File Finder

1.  I tried [command-t](https://wincent.com/products/command-t/) but I could not make it work. It requires that your copy of Vim should be compiled with the same version of ruby with which you compiled command-t, which effectively means you have to compile Vim yourself.
2.  I took the easier way, use [CtrlP](http://kien.github.com/ctrlp.vim/). It is basically the same as Command-T but written in pure Vimscript. This means it neither requires Ruby support enabled in Vim nor does it require the compilation of some Ruby extension implemented in C.
3.  Other extensions are either not what I wanted, for example, [LustyJuggler](http://www.vim.org/scripts/script.php?script_id%3D2050), or not actively maintained any more like [FuzzyFinder](http://www.vim.org/scripts/script.php?script_id%3D1984) and [fuzzy file finder](https://github.com/jamis/fuzzy_file_finder).

Bash
----

1.  Bash completion depends on bash\_completion package. MacPorts users can do `sudo port install git-core +bash_completion`.
2.  [Git Utilities You Can't Live Without](http://blog.bitfluent.com/post/27983389/git-utilities-you-cant-live-without) blog entry has an entry for Git aware PS1.
