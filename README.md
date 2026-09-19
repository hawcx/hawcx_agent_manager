<p align="center">
  <a href="https://www.hawcx.com/"><img src="assets/hawcx-mark.png" width="160" alt="Hawcx"></a>
</p>

<h1 align="center">Hawcx Agent Manager</h1>

<p align="center">
  The desktop app that enrolls an employee's machine, and the AI agents running on it, with your Hawcx deployment.<br>
  IT installs it through Intune or Jamf. Your deployment runbook supplies the configuration.
</p>

<p align="center">
  <a href="https://github.com/hawcx/hawcx_agent_manager/releases/latest"><img alt="Latest release" src="https://img.shields.io/github/v/release/hawcx/hawcx_agent_manager?display_name=tag&label=latest&color=0563e5"></a>
  <a href="https://github.com/hawcx/hawcx_agent_manager/releases/latest"><img alt="Release date" src="https://img.shields.io/github/release-date/hawcx/hawcx_agent_manager?label=released&color=55657A"></a>
  <a href="https://github.com/hawcx/hawcx_agent_manager/releases"><img alt="Downloads" src="https://img.shields.io/github/downloads/hawcx/hawcx_agent_manager/total?label=downloads&color=55657A"></a>
</p>

<p align="center">
  <a href="https://hawcx.github.io/hawcx_agent_manager/"><img alt="Open the downloads page" src="https://img.shields.io/badge/Downloads%20page-hawcx.github.io-0563e5?style=for-the-badge"></a>
</p>

The [downloads page](https://hawcx.github.io/hawcx_agent_manager/) detects your platform, shows the current version and its signing status, and carries the full deployment notes. Everything below is the short version.

## Downloads

| Platform | Package | Signing | Get it |
| --- | --- | --- | --- |
| macOS, Apple silicon and Intel | `HawcxManager-<version>-macos-universal.pkg` | Developer ID signed, notarized by Apple | [Latest release](https://github.com/hawcx/hawcx_agent_manager/releases/latest) |
| Windows 11, x64 | `HawcxManager-<version>-windows-x64.msi` for MDM, `-setup.exe` for interactive installs | Not code-signed yet, SmartScreen warns | [Latest release](https://github.com/hawcx/hawcx_agent_manager/releases/latest) |
| Linux, x86_64 | `HawcxManager-<version>-linux-amd64.deb`, or the `.AppImage` | Unsigned, published for evaluation | [Latest release](https://github.com/hawcx/hawcx_agent_manager/releases/latest) |

Stable URLs for scripts and MDM, by file name:

```
https://github.com/hawcx/hawcx_agent_manager/releases/latest/download/<file>
https://github.com/hawcx/hawcx_agent_manager/releases/download/v<version>/<file>
```

Not every release ships every platform. The [releases list](https://github.com/hawcx/hawcx_agent_manager/releases) shows which files each version has; the downloads page picks the newest release that has yours.

## Install

<details>
<summary><strong>macOS</strong></summary>

Installs `/Applications/Hawcx Manager.app`, a system service, and a local service account named `_hawcxauth`. Administrator rights are required.

```sh
sudo installer -pkg HawcxManager-<version>-macos-universal.pkg -target /
```

With Jamf, upload the package as-is and scope it with a policy that also places `/etc/hawcx/manager.env`.

Dragging the app to the Trash does not uninstall it. Use the uninstaller, which stays on the machine outside the app bundle:

```sh
sudo /opt/hawcx/bin/hawcx-uninstall.sh --dry-run   # show the plan, change nothing
sudo /opt/hawcx/bin/hawcx-uninstall.sh             # remove, keep the enrolled identity
sudo /opt/hawcx/bin/hawcx-uninstall.sh --purge     # remove and destroy the enrolled identity
```
</details>

<details>
<summary><strong>Windows</strong></summary>

Per-machine install. Requires Windows 11 and the WebView2 runtime that ships with it.

```bat
msiexec /i HawcxManager-<version>-windows-x64.msi /qn /norestart
msiexec /x HawcxManager-<version>-windows-x64.msi /qn /norestart   :: uninstall
```

The interactive installer accepts `/S` for a silent install. With Intune, add the MSI as a line-of-business app and place `C:\ProgramData\Hawcx\manager.env` with a separate policy before first launch.

Windows builds are not code-signed yet. Deploy the MSI through your MDM from the URLs above rather than by forwarding the file.
</details>

<details>
<summary><strong>Linux</strong></summary>

```sh
sudo apt install ./HawcxManager-<version>-linux-amd64.deb
# or
chmod +x HawcxManager-<version>-linux-x86_64.AppImage && ./HawcxManager-<version>-linux-x86_64.AppImage
```

Linux builds are published for evaluation. Talk to Hawcx before rolling them out to a fleet.
</details>

## Configure

The installer carries no tenant settings. Your Hawcx deployment runbook produces one plain-text file, `manager.env`, and your MDM places it:

| Platform | Path |
| --- | --- |
| macOS and Linux | `/etc/hawcx/manager.env` (root-owned, world-readable) |
| Windows | `C:\ProgramData\Hawcx\manager.env` |

It holds endpoints and identifiers only. The app is a public OAuth client and needs no secret, so nothing in the file is one. The app reads it at startup.

## Verify

```sh
pkgutil --check-signature HawcxManager-<version>-macos-universal.pkg
spctl --assess --type install -vv HawcxManager-<version>-macos-universal.pkg
```

Both should name a Developer ID Installer certificate belonging to Hawcx and report the package as notarized. Windows and Linux builds carry no signature yet; download them only from this repository over HTTPS and keep the URL in your deployment record.

## Support

Contact Hawcx through your existing support channel. Issues on this repository are not monitored.
