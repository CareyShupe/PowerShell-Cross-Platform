# PowerShellCrossPlatform

A single PowerShell profile that runs cleanly on **both Windows and Linux (Lubuntu)** — no branching config files, no "works on my machine." One profile, detected and adapted at runtime.

Most PowerShell profiles on GitHub are Windows-only and quietly break the moment you try to reuse them on Linux (registry drives that don't exist, `Out-GridView` that isn't installed, hardcoded `C:\` paths). This one was built specifically to avoid that — every platform-specific piece is detected and swapped out automatically.

## Features

- **True cross-platform support** — runtime detection via `$IsWindows` / `$IsMacOS` / `$IsLinux`, with platform-aware fallbacks for things that don't exist everywhere (e.g. registry drive mounting, admin/role checks, network connectivity checks)
- **Custom PSReadLine key bindings** — including `Get-KeyBindingReport` (aliased `keys`), a utility that diffs your live key bindings against PSReadLine's defaults so you can see exactly what's been customized
- **Cross-platform history picker** — a from-scratch fallback for the classic F7 history popup, using `Out-ConsoleGridView` where available and a console menu where it isn't (since `Out-GridView` is Windows-only)
- **Conditional Vi mode** — automatically enables PSReadLine's Vi edit mode when `nvim`/`vim` is detected as your editor, otherwise stays in the default mode
- **oh-my-posh prompt integration** — with a cross-platform `Join-Path` fix for theme paths
- **Smarter Tab completion** — upgraded to `MenuComplete`
- **Color-coded, CI-safe output** — custom `$PSStyle.Formatting` colors for Error/Warning/Verbose/Debug that automatically fall back to plain text when output is redirected or running in CI/logs
- **Self-updating** — `Update-PowerShell` function with cross-platform package manager logic (winget on Windows, distro-aware package managers on Linux via `/etc/os-release`), plus `-Force` / `-Verbose` / `-WhatIf` support
- **WSL-aware `Open-Item`** — detects and handles WSL paths correctly
- **Opt-in verbose/debug switch** — `$Script:EnableVerboseDebugOutput` to flip on detailed output without touching the profile itself

## Requirements

- PowerShell 7+ (a PowerShell 5.1-compatible variant is also included for Windows-only legacy use)
- [oh-my-posh](https://ohmyposh.dev/) (optional, for the prompt theme)
- `PSReadLine` (bundled with modern PowerShell)

## Installation

1. Clone the repo:

   ```powershell
   git clone https://github.com/CareyShupe/PowerShellCrossPlatform.git
   ```

2. Review the profile script and adjust any user-specific paths or preferences.
3. Symlink or copy it to your PowerShell profile location:

   ```powershell
   # Find your profile path
   $PROFILE
   ```

4. Restart your PowerShell session.

> Tip: if you use this profile across multiple machines, consider symlinking it from a synced folder (OneDrive, Syncthing, etc.) rather than copying it, so updates propagate automatically.

## Why this exists

This started as a review and rewrite of a Windows-only PowerShell profile — identifying every place it silently assumed Windows (registry drives, admin checks, hardcoded paths, package manager calls) and replacing each one with a cross-platform equivalent. What's here is the result of that rewrite plus ongoing refinement: real bugs found and fixed while actually using the profile day to day on both Windows and Lubuntu.

## License

MIT — see [LICENSE](LICENSE) for details.

## Contributing

Issues and PRs welcome, especially if you hit a platform-specific edge case this doesn't handle yet.
