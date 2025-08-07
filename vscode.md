# Visual Studio Code

-------------------------------------------------------------------------------

# Extensions

- [Extensions for Visual Studio Code](https://marketplace.visualstudio.com/vscode)
- [Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
- [Render Line Endings](https://marketplace.visualstudio.com/items?itemName=medo64.render-crlf)
- [Bookmarks](https://marketplace.visualstudio.com/items?itemName=alefragnani.Bookmarks)
- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

-------------------------------------------------------------------------------

## Korean Fixed Width Font

- `Menlo` does not have monospace fonts for Korean characters.
- `D2Coding` supports Korean monospace fonts.
- `D2Coding` can be found at [https://github.com/naver/d2codingfont](https://github.com/naver/d2codingfont).
- `D2Coding` English fonts are narrower than `Menlo` (for proper Korean font width?).
- With `D2Coding` column selection cursors for English-Korean mixed character lines are poorly aligned; difficult column editing.
- `D2Coding` can be applied only to this projects by editing workspace settings.

## Workspace setting example

`.vscode/settings.json`
```.json
{
    "editor.fontFamily": "D2Coding, Menlo, Monaco, 'Courier New', monospace",
}
```

-------------------------------------------------------------------------------

# Cygwin Terminal

Add `terminal` configs for Preference::User Settings (JSON)

`terminal.integrated.profiles.windows` can be populated by choosing **Cygwin** for **Terminal: Select Default Profile** [(link)](https://code.visualstudio.com/docs/terminal/profiles#_unsafe-profile-detection). The Cygwin default arg is `--login` which opens a shell in HOME, so use `-i` for a just interactive shell.

```json
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        },
        "Cygwin": {
            "path": "C:\\cygwin64\\bin\\bash.exe",
            "args": [
                "-i"
            ]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Cygwin",
```

-------------------------------------------------------------------------------

# User Settings (JSON) Example

`Settings.json`
```json
{
    "workbench.colorTheme": "Default Dark+",
    "trailing-spaces.trimOnSave": true,
    "files.insertFinalNewline": true,
    "editor.renderWhitespace": "all",
    "editor.rulers": [ 80, 120 ],
    "editor.fontFamily": "D2Coding, Menlo, Monaco, 'Courier New', monospace",
    "cSpell.enabled": true,
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        },
        "Cygwin": {
            "path": "C:\\cygwin64\\bin\\bash.exe",
            "args": [
                "-i"
            ]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Cygwin",
    "terminal.integrated.copyOnSelection": true,
    "terminal.integrated.cursorBlinking": true,
    "code-eol.highlightExtraWhitespace": true,
    "code-eol.highlightNonDefault": true,
}
```
