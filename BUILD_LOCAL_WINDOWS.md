# Build Pausetta locally on Windows (without GitHub Actions)

## Requirements

- Windows 10/11 x64
- Node.js **24.16.0 or newer**
- pnpm **11.9.0** (the version pinned by `package.json`)
- Rust stable toolchain (`rustup`)
- Visual Studio Build Tools 2022 with **Desktop development with C++**
- Microsoft Edge WebView2 Runtime (normally already installed on Windows)

## Install the tools

1. Install Node.js 24.16+ from https://nodejs.org/
2. Enable/install pnpm:
   ```powershell
   corepack enable
   corepack prepare pnpm@11.9.0 --activate
   ```
3. Install Rust from https://rustup.rs/
4. Install Visual Studio Build Tools 2022 and select **Desktop development with C++**.

Restart PowerShell after installing these tools.

## Build the app

Open PowerShell in the extracted `Pausetta-main` project folder (the folder containing `package.json`) and run:

```powershell
pnpm install --frozen-lockfile
pnpm tauri build
```

This builds the complete Tauri desktop application locally. GitHub Actions is not required.

## Build output

The Windows installers/bundles are normally written under:

```text
src-tauri\target\release\bundle\
```

Look inside `msi` and/or `nsis` for the generated installer, depending on the bundle targets configured by Tauri.

## Development build

To run the app without creating an installer:

```powershell
pnpm tauri dev
```

## Notes

- The first build downloads and compiles Rust dependencies and can take several minutes.
- If `pnpm install --frozen-lockfile` reports a lockfile mismatch, stop and report the error rather than deleting the lockfile.
- The project requires Node.js >=24.16.0; Node 22 will not satisfy its declared engine requirement.
