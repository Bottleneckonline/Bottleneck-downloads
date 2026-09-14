# Bottleneck — downloads

Published builds of [Bottleneck](https://bottleneckonline.com), a Windows tool that measures how
much of a machine's own potential it is actually delivering, and names what is holding it back.

This repository contains **only the released binaries**. The application source is not here and
is not public.

## Getting the application

Take them from the [latest release](https://github.com/Bottleneckonline/Bottleneck-downloads/releases/latest),
or from the [download page](https://bottleneckonline.com/download.html), which shows the size and
SHA-256 of each file alongside the button.

| File | What it is |
| --- | --- |
| `Bottleneck-<version>-Setup.exe` | The normal installer. Adds a Start menu entry. |
| `Bottleneck-<version>.msi` | For deployment by policy across an estate. Silent install supported. |
| `Bottleneck-<version>-Portable.zip` | Unpack and run. Writes nothing outside its own folder. |

The portable zip contains the executable, its `wwwroot` folder, and a file named `portable`.
Keep all three together: the interface is served from `wwwroot`, and the marker file is what
keeps your licence, settings and scan history beside the executable instead of on the machine
you are running it from. That is the whole point of the portable build, and deleting the marker
silently turns it off.

## Checking what you downloaded

These builds are not yet code-signed, so Windows SmartScreen shows an "unknown publisher"
warning the first time you run one. Until a certificate is in place, comparing the hash is how
you confirm you have the file that was published:

```
Get-FileHash .\Bottleneck-1.0.0-Setup.exe -Algorithm SHA256
```

The expected values are on each release and on the download page. They come from the build's own
manifest rather than being typed in by hand, so they cannot drift apart from the files.

## A note for whoever maintains this

This repository has to stay **public**. GitHub serves release assets on a private repository
only to authenticated requests, and the download page fetches them with no credentials at all.
Making this repository private does not produce an error anybody sees — it just turns every
download button on the site into a dead link.
