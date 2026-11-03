# Text Corrector

**English** | [Dansk](README.da.md)

A simple-to-install-and-use Windows tool: highlight some text, press a hotkey, and it fixes the typos using a local language model.
Everything runs on your own computer, using [Ollama](https://ollama.com) as the engine. After a 
one-time download of a language model from Ollama, it works offline.

**Privacy:** your text never leaves your PC. The only time the program uses the internet is when
you download a model.

![Text Corrector in action](docs/images/showcase.gif)

## Download and use

1. Get `TextCorrector-1.0.0.zip` (or the newest version) from the [Releases page](../../releases) (look under "Assets").
2. Extract it, double-click `TextCorrector.exe` and download a model.

No Python setup, no separate Ollama installation and no virtual environment is needed.
See [The ready-to-use zip](#the-ready-to-use-zip) for details.

**Requirements:** Windows 10 or 11 (64-bit). About 1.5 GB to download, a few GB of disk space once
extracted, and then 3 to 10 GB for each language model you download (you can download more than one). Also, note that you need enough free
memory (RAM or graphics memory) for the model you choose; the Models tab shows roughly how much
each one needs. Small and larger models are available to choose from. A graphics card is optional but speeds up corrections.

## How it works

1. You highlight some text, press a hotkey.
2. The tool copies your selection, sends it to a local Ollama model and asks for a corrected
   version (typos, spelling, casing and punctuation; wording and meaning stay the same).
3. The answer is checked and, depending on the hotkey, either pasted over your selection, or put on
   the clipboard, ready for you to paste with Ctrl+V.

Long texts are corrected paragraph by paragraph, so small models keep track and a part the model
keeps getting wrong is left as it was (the activity log says so) instead of losing the whole text.
If the model's answer does not look like a plain correction (for example extra commentary or
changed line breaks), nothing is pasted for that part and the program tells you why.

## Screenshots

![The Status tab](docs/images/main.png)
![The Models tab](docs/images/models.png)
![The Settings tab](docs/images/Settings.png)

## Details About the Program

The window has four tabs:

- **Last correction** (the tab the window opens on): quick start help on how to use the hotkeys
  (**Hide quick start help** folds it away once you know them), and the text before
  (left) and after (right) the latest correction, as large as the window allows, with a scroll bar
  inside each box when a text is longer. The Before box is filled the moment you press the hotkey,
  and the After box shows "Correcting..." until the result is ready. What differs is colored (see
  below); the **Highlight changes** box under the color legend turns the colors on and off.
- **Status:** the model panel and a list of what the program has done. The model panel shows whether the model is loaded in memory, how much
  memory it uses (or roughly needs), and when it is unloaded after a period without use (the
  "Keep model loaded for" setting). **Load model now** loads it ahead of time, so the next
  correction does not have to wait for it. The program loads the model by itself when needed.
- **Models:** the models you can use. Download as many as you like (one at a time; the program
  is locked with a progress window until it is done), choose which one to use with **Use this
  model**, and **Remove** the ones you do not need. Each model shows its download size, roughly
  how much memory it needs, its release date and a **More info** link to its page. Smaller models
  are faster and need less memory; larger ones are usually more accurate. **Custom model** lets
  you download any model from the Ollama library by name. The **language** of your text and the
  **advanced settings** (see below) are set here too, below the list.
- **Settings:** one control for every setting, with a description. Every change is applied and
  saved as soon as you make it.

At the bottom of every tab are the credit line (left) and the version number (right).

The window can be shown in English or Danish (**Program language** at the top of the Settings tab).
"Same as Windows", the default, uses Danish on a Danish Windows and English otherwise.

The tray icon is there from the start (unless you turn it off in Settings). When you minimize the
window it disappears into the tray (next to the clock); click the tray icon, or choose Open in its
menu, to bring it back. Choose Quit in the tray menu, or close the window, to stop the program. On Windows 11 a new tray icon may be hidden under the small arrow next to the
clock until you drag it out. If the tray cannot be used, the activity log says why and the window
minimizes to the taskbar as usual. The background color of the tray icon, of the window icon and of
the icon in the taskbar shows the status: green is ready, yellowish is ready but the model is not
loaded, red is an error, and blue is loading or working. In Settings, turn off **Minimize to the
tray** to minimize to the taskbar instead; no tray icon is shown then.

Turn on **Updates from tray** in Settings to see short notes in the corner above the tray while the
window is hidden: "Correcting...", "Pasted!", "Corrected text in clipboard", "Nothing to correct",
"Correction error", "Loading model...", "Model loaded" and "Unloaded model". Each fades away after
about a second. The notes never take the keyboard focus, so pasting is not disturbed.

On start the program loads the model and plays a short rising sound when it is ready. The status
at the top is green ("Ready") only while the model is also loaded in memory. It turns yellow when
only the program is ready and the model is not loaded, for example after it has been idle for
longer than the "Keep model loaded for" time. The model then loads again when you use it, which
takes a moment for the first correction.

| Hotkey (Default) | Action |
| --- | --- |
| Ctrl+Alt+Shift+2 | **Correct and paste:** corrects the selected text and pastes the result over it |
| Ctrl+Alt+Shift+1 | **Correct to clipboard:** corrects the selected text, but does not paste immediately: the corrected text waits on the clipboard until you press Ctrl+V. Handy for long texts, so you need not wait for the result |
| Ctrl+Alt+Shift+3 | **Load/unload model:** loads the model into memory when it is not loaded (so the next correction is fast), and unloads it, to free the memory, when it is loaded |
| Ctrl+Alt+Shift+4 | **Show/hide window:** minimizes the window (to the tray, or the taskbar) or brings it back, on the Last correction tab (turn off **Start at "Last correction" tab** in Settings to keep the tab that was open) |

All four hotkeys can be changed in the settings. Windows reserves a hotkey for this program
while it runs, so the program in front never receives it. This matters because many programs use
keys such as F10 for their own menu. The defaults can all be pressed with the left hand, and were chosen because common programs do not use them. If another program already uses a combination, this program
says so and you can choose another one. If you need the default keys for something else, choose
other hotkeys in the settings.

After a correction, the **Before** and **After** boxes on the Last correction tab color what
differs: changed words yellow, removed words red, added words green, punctuation blue, and words
that moved gray. Untick **Highlight changes** under the colors to turn this off.

Now and then a model gives an answer that cannot be used, for example it leaves out ("forgets") words. The program notices (it also rejects answers that lost
several words) and then corrects that part of the text one sentence at a time (up to each period,
question mark or exclamation mark), because short pieces rarely fail. The model sees less context
that way, but you get a result. A sentence that still fails is left as it was and the activity log
says so. The rejected answer is shown in gray under the After box on the Last correction tab, so you
can see what the model produced.

**Copy diagnostics** on the Status tab copies a report about the program and its
latest errors (it contains no corrected text), handy when troubleshooting.

## Program Settings

The Models tab also holds the **Language** of your text ("Detect automatically" by default, which
lets the model work out the language; choosing a language makes Text Corrector use its own prompt
and example for it) and the advanced settings (see below).
The Settings tab holds the rest:

| Setting | What it does |
| --- | --- |
| Program language | The language of the window: Same as Windows (default), English or Dansk. Text Corrector restarts to change it |
| Hotkeys | The four key combinations. Click a button and press the new combination, or Esc to keep the old one |
| Keep model loaded for | How long the model stays in memory after the last use, as hours and minutes. **Forever** keeps it loaded until the program is closed |
| Request timeout | How long to wait for the model before giving up |
| Tray | Minimize to the tray (default), or to the taskbar |
| Tray updates | **Updates from tray**: short notes above the tray that fade away after about a second (off by default) |
| Start with Windows | Starts the program in the tray when you log in, without loading the model, so no memory is used until you correct something. Installed program only |
| Window size | **Reset window size** goes back to the automatic size from the next start |
| Processor | **Try GPU** (default) puts as much of the model on the graphics card (NVIDIA, AMD or Intel) as fits, also for models whose own settings say otherwise; **CPU** uses just the processor. Try CPU if the program crashes or behaves strangely on a PC. The Model panel on the Status tab shows whether the loaded model runs on the GPU, the CPU or both, and warns when Try GPU ended up on the CPU. This is usually because the model does not fit in the graphics card's memory |
| Sounds | Short sounds when the program is ready, when a correction starts, finishes, finds nothing to fix, or fails. Each has its own sound |
| Sound volume | The volume of all sounds together, from 0 (silent) to 100 (loudest) |

### Advanced settings (Models tab)

At the bottom of the Models tab, **Use advanced settings** opens settings for testing, for example
to get a model of your own to work better. While it is unticked the section is folded away and Text
Corrector uses its own system prompt and example for your language and checks every answer.

- **System prompt**: the text the model reads before your text. The box shows the prompt for the
  selected Language, and each language keeps its own version: change the language and the box
  shows that language's prompt. Your text replaces Text Corrector's prompt completely. **Fill in
  Text Corrector's default system prompt for selected language** (or emptying the box) goes back to
  the default. The default is English with a hint about your language; Danish has its own Danish prompt.
- **Examples**: before your text the model is shown one example correction (a text with typos and
  its correction), which helps small models answer in the right form. Ticked, the example for the
  selected language is shown in a **Before** and an **After** box (at most 300 characters each)
  that you can change; each language has its own, and **Restore default examples** brings back
  Text Corrector's. Unticked, no example is sent.
- **Permit all model outputs**: for testing only. Whatever the model answers is pasted, also
  answers the checks would normally reject (left-out words, extra text, changed line breaks, or
  not in the asked-for JSON form). Off by default.

The temperature setting is hidden, because a corrector should give the single most likely
correction (temperature 0). It can be brought back by setting `TEMPERATURE_ADJUST = True` at the
top of `text_corrector/settings.py`.

## The ready-to-use zip

This is the version for other people. Everything it needs is in its own folder.

1. Extract the zip to a folder you can write to, for example `C:\Users\YourName\TextCorrector`.
   Do not run the program from inside the zip.
2. Double-click `TextCorrector.exe`. Windows may warn about an unknown publisher the first
   time ("More info", then "Run anyway"), because the program is not signed.
3. The first time there is no model yet, so the program opens on the Models tab. Press Download
   next to one (a few gigabytes, once). The progress is shown, and the model is used as soon as
   it is ready. Later you can download others there and switch between them.
4. To remove everything, close the program (tray icon, Quit) and delete the folder, or
   double-click `uninstall.bat` in it. Nothing else on the PC was changed.

### The built-in engine

The zip contains its own copy of Ollama's standalone service, renamed to `Text-Corrector-Engine.exe`. The program starts it in the background when it
opens and stops it when it closes. `Text-Corrector-Engine.exe` does not conflict with an Ollama service you may have installed yourself: it uses
a free local port, and keeps its models, settings and temporary files in the program's folder
(`models` and `data`). Its log is `data\logs\ollama.log`.

Graphics cards: NVIDIA cards are used via CUDA, and AMD and Intel cards (also the ones
built into the processor) via Vulkan, with the normal graphics drivers. When no graphics
card can be used, the CPU does the work, which is slower. The Model panel on the Status
tab shows how much of the model sits on the graphics card or how much in system RAM.

To use your own Ollama instead of the built-in one, delete or rename the `ollama` folder next
to the program, and set your Ollama address in the config file.

## Troubleshooting

- **"The model's answer left out N words"**: the model dropped part of the text, which a proofreader
  should not do, so the answer was not used. The program then tried the text sentence by sentence.
  If it keeps happening with one model, try another one in the Models tab: small models do this more.
- **"The model did not answer in the expected format"**: the model replied with something other
  than the JSON answer the program asks for. Try again, or choose another model in the Models
  tab. Thinking models (such as Gemma 4) are asked not to think, and the program also accepts a
  reply wrapped in a code fence.
- **"The built-in engine is not answering"**: close Text Corrector and start it again. If it keeps
  happening, press **Copy diagnostics** on the Status tab and check `data\logs\ollama.log`.
- **"The built-in engine could not start"**: read `data\logs\ollama.log` in the program's
  folder. Antivirus software sometimes blocks the engine (`ollama\Text-Corrector-Engine.exe`); allow it, or
  add the program's folder as an exception. If the log mentions the graphics card or driver,
  set "Processor" to "CPU" in the settings.
- **A model runs on the CPU although Try GPU is on**: the model may be too large for the graphics
  card's memory; a smaller model (or one with a smaller download size) fits. Some models in the
  Ollama library also come with their own setting that keeps them off the graphics card; Text
  Corrector overrides that while Try GPU is chosen.
- **"No text was selected, or the app did not copy it"**: the program in front did not copy the
  selection. Some programs need a little longer to copy and paste. If it only happens in one
  program, try another hotkey in the settings.
- **A hotkey "cannot be used"**: another program has already taken that key combination.
  Choose a different one in the settings.
- **Cannot see the tray icon**: on Windows 11 it may be under the small arrow next to the clock.
  The activity log on the Status tab says if the tray icon could not be started.
- **Nothing appears when the program starts**: look for the tray icon. If the program stopped
  with an error, a message box says so, and details are saved in `data\error.log`.
- **"Could not reach Ollama"** (running from the source): start Ollama and try again.
- **HTTP 404 from Ollama**: the model is not installed. Run `ollama pull <model name>`.
- **To see what the model answered**: set `CORRECTOR_DEBUG=1` before starting (in `cmd`:
  `set CORRECTOR_DEBUG=1`) and use the console version. The raw reply is shown after every request.
- In the source, the delays the program waits for copy and paste are at the top of `textio.py`.

## Known limitations

- Only text on the clipboard is restored afterwards when using correct and paste (Ctrl+Alt+Shift+2). An image or file you had copied is lost. Correct to clipboard (Ctrl+Alt+Shift+1) always overwrites the clipboard.
- Setting the language model language to other than English is experimental. 
- The program is not code-signed, so Windows can show a warning the first time. Some antivirus programs also flag programs made with PyInstaller.

## Source code

The source code of each version is attached to its release as `TextCorrector-<version>-source.zip`.
[SOURCE_README.md](SOURCE_README.md) explains how to run it and how to build the ready-to-use zip
yourself.

## Credits

This project was inspired by two earlier tools, and thanks go to their authors:

- [ai-typing-assistant](https://github.com/patrickloeber/ai-typing-assistant) by Patrick Loeber
  (MIT license)
- [Typing-Assist](https://github.com/x404xx/Typing-Assist) by x404xx

This version has since been rewritten with its own code, and extended with
settings, text checks, feedback sounds and a graphical window.

## License

The source code is released under the [MIT License](LICENSE). The built-in engine is
[Ollama](https://github.com/ollama/ollama) (MIT), and the language models you download are
separate works with their own licenses (see each model's page). The libraries the program uses
are listed in `packaging\THIRD_PARTY_NOTICES.txt`.

## Feedback

Bug reports and ideas are welcome as GitHub issues. When reporting a problem, press **Copy
diagnostics** on the Status tab and paste the result into the issue.
