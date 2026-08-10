# PowerShell Cross-Platform

A personal PowerShell 7+ profile designed to behave consistently across Windows, macOS, and Linux.

This project collects profile configuration, shell helpers, editor preferences, native command completions, and optional maintenance tasks into one cross-platform setup. It is intended for daily interactive terminal use while keeping startup resilient when optional tools are missing.

## What It Includes

- Cross-platform PowerShell profile for PowerShell Core 7.2+
- Windows registry drive mounting for `HKU`, `HKCR`, and `HKCC`
- Optional module maintenance for common shell tooling
- Optional PowerShell update helper with package manager support
- PSReadLine color, history, prediction, and key binding configuration
- Native completions for tools such as `git`, `npm`, `deno`, `dotnet`, and `winget`
- Dynamic editor selection using the first available editor
- Convenience aliases and helper functions for profile editing, reloads, Git identity, and directory listing

## Supported Platforms

- Windows
- macOS
- Linux

PowerShell 7.2 or newer is required.

## Optional Tools

The profile works without these tools, but it enables extra features when they are available:

- `PSReadLine`
- `Terminal-Icons`
- `oh-my-posh`
- `git`
- `dotnet`
- `winget`, `choco`, or `scoop` on Windows
- `brew` on macOS
- `apt`, `dnf`, `pacman`, or `zypper` on Linux

## Setup

Copy or link the profile script to your PowerShell profile path:

```powershell
$PROFILE
```

Then reload your profile:

```powershell
. $PROFILE
```

You can also use the included helper after the profile is loaded:

```powershell
reload
```

## Maintenance Behavior

Automatic package updates are disabled by default:

```powershell
$Script:EnableAutoPackageUpdate = $false
```

The profile can check for module and PowerShell updates during interactive sessions, but it avoids running those checks in non-interactive shells. Update checks are gated so they do not run every time a new shell opens.

To manually check for and install a PowerShell update:

```powershell
Update-PowerShell -Force
```

## Useful Commands

| Command | Purpose |
| --- | --- |
| `ep` | Open the current PowerShell profile in your preferred editor |
| `reload` | Reload the current profile |
| `GWhoami` | Show configured Git author name and email |
| `open` | Open a file or folder with the platform default application |
| `ll` | Detailed directory listing |
| `la` | Name-only directory listing |
| `lh` | Wide directory listing |
| `lv` | List-format directory listing |
| `gcom "message"` | Run `git add .` and commit with the message |
| `lazyg "message"` | Run `git add .`, commit, and push |

## Notes

This profile is optimized for interactive use. Optional integrations are guarded so missing modules or commands should not prevent a shell from opening.
