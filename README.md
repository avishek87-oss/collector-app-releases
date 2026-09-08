# HealthMark Collector — release APKs

Signed release builds of the HealthMark Collector Android app, for phlebotomists
working with HealthMark Pathology Laboratory, Raipur.

**This repository holds release assets only. It contains no source code.**

## Why it is public

The app checks for updates by fetching
`https://api.github.com/repos/avishek87-oss/collector-app-releases/releases/latest`
with **no credentials**. A private repository returns 404 to an unauthenticated
caller, and shipping a GitHub token inside the APK to work around that would be
far worse — an APK is trivially unzipped. So the release feed is public while the
application source stays private.

Downloading the APK gains nobody access to anything: the app requires a
collector account that lab staff create and approve, and login is phone + OTP.

## Verifying a download

Every release carries a `checksums.txt`. Before installing a manually downloaded
APK:

```bash
sha256sum -c checksums.txt
```

The app performs this check automatically on any update it downloads itself.

Every release is signed with HealthMark's own release key
(`CN=HealthMark Pathology Laboratory`). Android refuses to install an update
signed by any other key, which is the real protection against a substituted
build — the checksum only guards against a corrupted download.
