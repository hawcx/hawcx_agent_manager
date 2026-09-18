# Hawcx Agent Manager

Downloads for the Hawcx Agent Manager desktop app.

## Download

All links below point at the **[latest release](https://github.com/hawcx/hawcx_agent_manager/releases/latest)**.
Older versions are on the [releases page](https://github.com/hawcx/hawcx_agent_manager/releases).

| Platform | Download | Notes |
| --- | --- | --- |
| macOS (Apple silicon and Intel) | [Latest `.pkg`](https://github.com/hawcx/hawcx_agent_manager/releases/latest) | Signed and notarized installer. The `-macos-universal-app.tar.gz` asset is the bare `.app` for MDM tooling that prefers one. |
| Windows 11 x64 | [Latest `.msi`](https://github.com/hawcx/hawcx_agent_manager/releases/latest) | For managed deployment (Intune and similar). The `-windows-x64-setup.exe` asset is the interactive installer. Windows builds are not yet code-signed, so SmartScreen warns on first run. |
| Linux x86_64 | [Latest `.deb`](https://github.com/hawcx/hawcx_agent_manager/releases/latest) | Debian and Ubuntu. The `-linux-x86_64.AppImage` asset is the portable build. |

Asset names follow `HawcxManager-<version>-<platform>.<ext>`, for example
`HawcxManager-0.4.49-macos-universal.pkg`.

### Direct URLs for scripts and MDM

Latest release, by asset name:

```
https://github.com/hawcx/hawcx_agent_manager/releases/latest/download/<file>
```

A specific version:

```
https://github.com/hawcx/hawcx_agent_manager/releases/download/v<version>/<file>
```

## Configuration

The installer does not carry tenant configuration. Your Hawcx deployment
runbook delivers a `manager.env` alongside the app, which the app reads at
startup to find your tenant's services.

## Support

Contact Hawcx through your existing support channel. Issues on this repository
are not monitored.
