# Mako changelog

## Mako Update 9: chat works out of the box

Mako Update 9: chat works out of the box.

- The Qwen2.5 1.5B chat model now ships inside Mako.exe alongside the CPU runtime and the BGE embedding model. A bare Mako.exe chats with no network at all; all three are written into Mako-Data on any start where they are missing.
- Phi-3.5 mini (2.3 GB, the better default) is above GitHub's release size cap, so on a kit without it Mako fetches it in the background on first run and switches to it when it lands. A Settings switch turns that off; the Library row can cancel it.
- The exe is about 1.2 GB as a result, so this update and later ones are larger downloads.

## Mako Update 8: every model in the picker

Mako Update 8: every model in the picker.

- The model dropdown now lists every .gguf in the kit, including the bundled BGE Small embedding model. BGE is shown greyed with a note that it ranks knowledge and memory rather than chatting, so it cannot be picked by mistake.

## Mako Update 7: finds your models wherever they are

Mako Update 7: finds your models wherever they ended up.

- The model picker now lists every .gguf under Mako-Data\models: in a tier folder, in a folder of its own, or dropped straight into models.
- A kit arranged by hand, with bin, models, knowledge, tools or Logs still sitting beside Mako.exe, is folded into Mako-Data on start instead of being ignored.
- The Library's Models tab names the folder Mako scans when no chat model is found.

## Mako Update 6: Library accuracy and clearer errors

Mako Update 6: Library accuracy and clearer errors.

- The bundled BGE Small embedding model now shows as Installed in the Library instead of offering a download.
- The empty model picker says what to do: "No chat model yet. Library opens the downloads."
- If Mako ever hits an unexpected error, the dialog now names the exception and where it came from, so it can be fixed from a screenshot. Full details are in Mako-Data\logs (Settings > Export logs).

## Mako Update 5: clean exit and a better update prompt

Mako Update 5 fixes the error dialog on exit and tidies the update flow.

- Fixed: "The CancellationTokenSource has been disposed" appearing when Mako closed or restarted after an update. Services were being shut down twice on the way out.
- The sidebar button now reads "Update Ready: Mako Update N" and fits; the full title is its tooltip.
- The update prompt is a proper dialog: title, the first lines of the release notes, a link to the full notes on GitHub, and Install and restart / Not now.

## Mako Update 4: runtime and embedding model built in

Mako Update 4 makes a bare Mako.exe self-sufficient for chat.

- The CPU model runtime (llamafile 0.10.6) and the BGE Small embedding model now ship inside Mako.exe. On any start where they are missing from Mako-Data, Mako writes them back, hash-checked. No download is needed for either; the only thing to fetch is a chat model.
- The exe grows to about 126 MB as a result. Updates are still a single file.

## Mako Update 3: one Mako-Data folder

Mako Update 3 puts everything in one place.

- Next to Mako.exe there is now a single Mako-Data folder holding the whole kit: data (settings, conversations, Mako-Mem), logs, bin, models, knowledge and tools. Nothing else is created beside the exe.
- Kits from Update 1 and 2 (folders beside the exe) are moved into this shape automatically on the first start; your settings, conversations and memory come along.
- The Logs folder is now Mako-Data\logs; the app's own files sit in Mako-Data\data.

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

