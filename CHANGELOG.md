# Mako changelog

## Mako Update 2: converter vendors in the Library

Mako Update 2 completes the "just the exe" story: every part of the kit can now be downloaded from inside the app.

- Library > Tools gains "Converter vendors": FFmpeg 9.0.2, ImageMagick 7.1.2-30, VTracer 0.6.4, Real-ESRGAN 0.2.0 (with the lavapipe software Vulkan driver) and poppler 26.02.0 in one 212 MB download, verified by SHA-256 and unpacked into tools\convert. The Convert tab tells you when they are missing.
- Each vendor keeps its license file; THIRD-PARTY.md in tools\convert lists versions, licenses and upstream sources.
- Library downloads now show unpack progress for zipped components.

## Mako Update 1: first release

First public release of Mako, the portable offline AI desktop app.

- Local chat over llamafile (CPU by default, optional GPU acceleration).
- Just the exe is enough: Mako creates its folders next to itself and downloads the runtime, models and tools from the Library.
- Library: model catalog downloads and offline Kiwix knowledge packs with cited passages.
- Mako-Mem: encrypted memory that learns durable facts from your conversations.
- Tools: CyberChef, IT-Tools and the Convert tab (images, video, GIF, audio, PDF, ISO).
- Encrypted per-component logs with export from Settings.
- In-app updates from this repository: hash- and signature-checked before install.

