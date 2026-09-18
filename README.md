# Hawcx Agent Manager

Downloads for the Hawcx Agent Manager desktop app. This repository holds
releases only. The source code is maintained privately by Hawcx.

## Download

Latest release: <https://github.com/hawcx/hawcx_agent_manager/releases/latest>

| Platform | File | Notes |
| --- | --- | --- |
| macOS (Apple silicon and Intel) | `HawcxManager-<version>-macos-universal.pkg` | Signed and notarized installer. `HawcxManager-<version>-macos-universal-app.tar.gz` is the bare `.app` for MDM tooling that prefers one. |
| Windows 10/11 x64 | `HawcxManager-<version>-windows-x64.msi` | For managed deployment (Intune and similar). `HawcxManager-<version>-windows-x64-setup.exe` is the interactive installer. Windows builds are not yet code-signed, so SmartScreen warns on first run. |
| Linux x86_64 | `HawcxManager-<version>-linux-amd64.deb` | Debian and Ubuntu. `HawcxManager-<version>-linux-x86_64.AppImage` is the portable build. |

Direct download URLs follow a fixed pattern, suitable for scripts and MDM
fetches:

```
https://github.com/hawcx/hawcx_agent_manager/releases/download/v<version>/<file>
```

## Configuration

The installer does not carry tenant configuration. Your Hawcx deployment
runbook delivers a `manager.env` alongside the app; the app does not connect to
anything until that file is in place.

## Support

Contact Hawcx through your existing support channel. Issues on this repository
are not monitored.
