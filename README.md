# SysMedic releases

Signed update bundles for SysMedic **caddy** drives (installed rescue systems). This repository holds no source
history: each [release](../../releases) contains

| File | What it is |
|---|---|
| `sysmedic-bundle.tar.gz` | What a caddy installs: SysMedic's scripts, tests, AI instructions and permissions, package lists, docs |
| `manifest.json` | Version, source commit, SHA-256 and size of the bundle, and the change list |
| `manifest.json.sig` | OpenSSH signature of the manifest (namespace `sysmedic-release`) |

A caddy checks here (`sysmedic-update check`, at boot and every 2 hours when online) and installs only when the
signature verifies against the public key it already holds (`/etc/sysmedic/release-signers`) and the bundle
matches the signed checksum. The signing key never leaves the build machine.

Verify a release yourself:

```
ssh-keygen -Y verify -f release-signers -I sysmedic-release -n sysmedic-release -s manifest.json.sig < manifest.json
sha256sum sysmedic-bundle.tar.gz    # compare with "sha256" in manifest.json
```

This is an update channel for existing SysMedic drives, not a build kit: the OpenCode program, Ollama, the AI
models and the build tooling are not included.
