# Mako changelog

## Mako 1.4.0: semantic versioning + launcher-managed install
<!-- mako v1.4.0 -->

Mako now installs and updates through the ShinraSuite launcher.

- Versioning moves from whole numbers to semantic versioning; this release is **1.4.0**.
- When Mako is installed under Program Files (`C:\Program Files\ShinraCC\Apps\Mako`, managed by the launcher), its data â€” settings, the encrypted Mako-Mem vault, downloaded models and logs â€” lives in `%LocalAppData%\ShinraCC\Mako`. Run it portably and it still keeps everything in a `Mako-Data` folder beside the exe, exactly as before; an existing portable kit is migrated automatically on first run, and the DPAPI vault keeps decrypting for the same Windows user.
- When the launcher manages Mako, updates are delivered by the launcher (no in-place self-update under Program Files).

Signed with the Shinra CC certificate.


## Mako Update 12: Context menu, GPU choice and models by URL

**Context size is now a menu, and it knows the model's limits.**

- Settings offers 2,048 / 4,096 / 8,192 / 16,384 / 32,768 tokens (64k and 128k too when the model allows), each labelled with the memory that window costs for the active model. *Custom...* swaps in a text box: type any size with at least four digits. A value above the model's trained window, or one that needs more memory than this PC has, is refused with a note and the menu comes back unchanged. Enter or clicking away commits, Escape cancels.
- Hover the setting for the full explanation of what context size does and how it differs on the CPU (RAM, slow to read a full window) and the GPU (video memory, can push the model off the card, fast to read).
- Mako now reads each model file's trained context window from its header. Sizes above it are greyed out, and the server is never started above it, so Gemma 2 (8k) and Phi-4 (16k) cannot be pushed into repetition by a big setting.

**Pick which GPU.** A PC with two or more dedicated cards gets a *GPU to use* menu in Settings. The model is loaded onto that card only, instead of the runtime spreading it across all of them, and the Library colours follow the chosen card's memory.

**Any model by URL.** The bottom of Library > Models takes a direct link to a `.gguf` file (a Hugging Face "resolve" link, for example). Mako checks the file exists, downloads it into `models\custom`, and then rates it for this PC like every other model. Gated models, web pages and non-GGUF links are refused with a clear message.


## Mako Update 11: Model fit colours and chat compaction

**Models tell you what they are for and how they will run on this PC.**

- Catalog names now read `Model #B (what it is for)`, for example *Qwen2.5 1.5B Instruct (Fast General Chat and Summarizations)*, *Meta Llama 3.1 8B Instruct (Reliable Long-Form Writing)*, *Qwen2.5 Coder 7B Instruct (Code-Specialized Model)*. Each description says when to pick it, with examples (a tabletop RPG session, a novel chapter, a Python or Bash script, a math proof, a long contract).
- Every model row carries colour-coded chips: download size, quantization, licence (green permissive, amber community terms, orange research-only) and hardware fit. Hover a chip for the numbers.
- Hardware fit is a six-step scale from bright green (runs perfectly with the current settings) through amber and orange to crimson (will crawl), plus grey for a model this PC cannot hold at all. It is computed from this PC's RAM, a measured memory speed, the GPU and its VRAM, the Hardware Acceleration switch and the context size, so changing Settings recolours the list. Labels: *Fits on the GPU*, *Runs on CPU*, *Runs on CPU (GPU Capable)*, *Runs on CPU (Does Not Fit on GPU)*, *Cannot run here*.
- The fit is recomputed on every start, so the same portable folder plugged into a weaker PC shows the truth for that PC. A downloaded model that cannot run there is greyed out in the picker with a tooltip explaining why, is not offered for download, and if it was the active model Mako loads the best model it can run instead and says so in the status line.

**Chat compaction.**

- When a chat slows down (the reply takes three times longer to start than it used to, writes at half the speed, no longer fits the context window, or passes 40 messages), a banner above the input offers *Compact chat*. Compacting folds the older messages into a short structured summary and keeps the last six verbatim; the folded messages stay in the chat file and nothing is deleted. The model then re-reads far less on every turn.
- Settings has a new *Chats* section: pick any chat and *Compact this chat*, or *Compact all chats*.


## Mako Update 10: Tools fixes

Mako Update 10: Tools fixes.

- IT-Tools loads again. Both tool suites are now served by a small built-in loopback server instead of the browser's virtual-host mapping, which failed with ERR_ACCESS_DENIED on some PCs.
- Fully offline: every request a tool page makes to any other host (scripts, fonts, analytics, links) is refused locally and logged. Nothing leaves the machine.
- The Convert tab lists every action the Shinra Conversion Tool offers (35 across Image, Document, Video, Animated, Audio and ISO) at all times. Actions whose vendors are not downloaded yet are marked in red and explain what to fetch; downloading the vendors from Library > Tools lights them up without a restart.
- Tooltips are readable: dark background, light text.

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

