# smoothie-rs-git (unofficial, self-hosted PKGBUILD)

Why this exists: the AUR package `smoothie-rs-linux-git` has been broken since
llvm15 got pulled from the AUR (see
[smoothie-rs#79](https://github.com/couleur-tweak-tips/smoothie-rs/issues/79)).
It depends on `vapoursynth-plugin-vsakarin-llvm15-git`, which can't be built
anymore. The actual AUR package hasn't been touched since mid-2025 and AUR
registrations are closed right now, so there's no quick way to adopt or fix
it through the AUR itself.

This PKGBUILD is the same package, pointed at the real upstream repo
(`couleur-tweak-tips/smoothie-rs` instead of a stale fork) with the dead
`vsakarin-llvm15` dependency swapped for `vapoursynth-plugin-vsakarin-git`,
which builds the maintained
[Jaded-Encoding-Thaumaturgy/akarin-vapoursynth-plugin](https://github.com/Jaded-Encoding-Thaumaturgy/akarin-vapoursynth-plugin)
fork against your system's current LLVM instead of the archived llvm15.

## Install

```sh
git clone <this-repo-url>
cd smoothie-rs-git-pkg
makepkg -si
```

`makepkg -si` builds the package and installs it (`-i`), pulling in `-s`
(sync) any missing dependencies via pacman/AUR helper first. If you use an
AUR helper (yay, paru, etc.) that can build from a local PKGBUILD directory,
that works too.

This conflicts with `smoothie-rs-linux-git` / `smoothie-rs-linux` (same
install paths), so uninstall those first if you have them.

## Heads up

I put this together and read through it carefully, but I don't have an Arch
box to actually run `makepkg` against it right now, so it hasn't been
test-built end to end. The structure is a straight adaptation of the
existing AUR package (which does build), just re-pointed at the real
upstream repo and the maintained akarin fork. If something breaks on first
build, it's most likely a dependency version mismatch — open an issue here
or ping in the smoothie-rs repo.

## If AUR registrations reopen

The cleaner long-term fix is still to get this (or a fix to the existing
package) onto the actual AUR so it shows up in normal AUR searches. Once
registration opens back up, either file an orphan request on
`smoothie-rs-linux-git` and adopt it, or push this PKGBUILD as a new AUR
package.
