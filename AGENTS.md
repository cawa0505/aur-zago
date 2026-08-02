# Repository Work Protocols

This repository maintains the Arch Linux AUR package for `zago-bin`. It automatically tracks upstream updates, builds the precompiled Swift binaries in a clean environment, and publishes them to GitHub Releases and the AUR.

## Packaging Rules

1. **Package Name**: `zago-bin` (tracks precompiled static binaries).
2. **Upstream Source**: https://github.com/zonble/zago
3. **Download Caching**: To prevent local pacman/makepkg cache collisions between updates, downloaded sources in `PKGBUILD` must be version-prefixed (e.g., `$_pkgname-$pkgver-linux-x86_64.tar.gz::https://...`).
4. **Static Linking**: The binary must be compiled with `--static-swift-stdlib` to ensure runtime compatibility on target Arch environments without requiring localized Swift runtimes.

## Automation & Release Pipeline

The automation workflow resides in `.github/workflows/release.yml` and triggers daily or via manual dispatch:

1. **Upstream Checking**: Query GitHub Tags endpoint (not Releases, since upstream publishes tags without release assets) to determine the latest version.
2. **Dockerized Build**: Spawns a clean `swift:6.0` container to compile the upstream source code.
3. **Metadata Updates**: Updates `pkgver` and `sha256sums_x86_64` inside `PKGBUILD`, and uses an `archlinux:latest` container to print a clean `.SRCINFO`.
4. **Release Assets**: Uploads the precompiled `tar.gz` to local GitHub Releases under tag `v<version>`.
5. **AUR Submission**: Clones `ssh://aur@aur.archlinux.org/zago-bin.git` using SSH credentials, updates metadata files, and pushes to the AUR.
