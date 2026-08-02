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
3. **Workspace Isolation (CRITICAL)**: Build outputs must be compressed inside the Docker container directly to prevent local files (like package-specific `README.md` and `LICENSE`) from being overwritten by upstream files on the runner host.
4. **Metadata Updates**: Updates `pkgver` and `sha256sums_x86_64` inside `PKGBUILD`, and uses an `archlinux:latest` container to print a clean `.SRCINFO`.
5. **Release Assets**: Uploads the precompiled `tar.gz` to local GitHub Releases under tag `v<version>`.
6. **AUR Submission**: Clones `ssh://aur@aur.archlinux.org/zago-bin.git` using SSH credentials, updates metadata files, and pushes to the AUR.

## Upstream Contributions Workflow

To facilitate contributing back to the upstream repository (e.g., updating documentation or fixing upstream bugs), a local workspace is maintained:

1. **Local Directory**: Cloned upstream fork is located in the `./upstream` directory (ignored by `.gitignore`).
2. **Remotes Configuration**:
   - `origin`: Points to your fork (`https://github.com/cawa0505/zago.git`) for staging PR branches.
   - `upstream`: Points directly to the official repository (`https://github.com/zonble/zago.git`) to pull latest updates.
3. **PR Process**: All upstream contributions should be developed in `./upstream`, pushed to `origin`, and submitted as PRs to `upstream` via `gh pr create` from the `./upstream` working directory.

## Security, Isolation & Documentation Boundaries

1. **Ignored Files Guard**: Do not remove `AUR_SETUP.md` or other local setup/deployment guidelines from `.gitignore`. These files are private credentials-handling notes and MUST NOT be tracked by Git.
2. **Documentation Cleanliness**: Public-facing documentation (such as `README.md`) must never link to, refer to, or mention gitignored setup files (`AUR_SETUP.md`) or local environment paths.


