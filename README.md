# CLI Pulse — Homebrew tap

```bash
brew tap cli-pulse/tap
brew trust cli-pulse/tap
brew install --cask cli-pulse
```

The `brew trust` step is not optional and not us being unusual — Homebrew 6
refuses to load casks from any third-party tap until you say you trust it.
Without it the install stops with *"Refusing to load cask … from untrusted
tap"*. It is a one-time confirmation that you have looked at where this
software comes from, which is a reasonable thing for Homebrew to ask.

CLI Pulse is a macOS menu bar app that tracks usage, quota, and cost across your
AI coding tools.

## What this installs

The **Developer ID** build — signed, notarized, and unsandboxed. That last part
matters: the App Store build runs in the App Sandbox and needs an explicit
folder-access grant before it can read `~/.codex` or `~/.claude`, which is the
single most common reason a new install shows no data. The brew build reads
those directly and has no such step.

Requires macOS 13 (Ventura) or later, Apple silicon.

## Updates

`auto_updates true` is set, so `brew upgrade` leaves this alone — the app
updates itself through its own signed updater. Running both would have them
racing each other over the same bundle.

To move off the self-updater and let brew drive instead, uninstall and
reinstall pinned:

```bash
brew uninstall --cask cli-pulse
brew install --cask cli-pulse
```

## Uninstalling

```bash
brew uninstall --cask cli-pulse        # removes the app, keeps your data
brew uninstall --zap --cask cli-pulse  # also removes preferences and local scan state
```

`--zap` is the destructive one: it clears the app-group container holding your
pairing state and folder-access bookmarks.

## Where the releases come from

DMGs are published to
[`cli-pulse-distrib`](https://github.com/JasonYeYuhe/cli-pulse-distrib/releases)
and every cask bump carries that DMG's SHA-256.
