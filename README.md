# Text Corrector

A small Windows tool that fixes typos with a local language model. Select some text in any
program, press a hotkey, and a moment later the corrected text replaces the selection.
Everything runs on your own computer through [Ollama](https://ollama.com), so your text is
never sent to an online service.

<!-- Add screenshots and GIFs here once they are in docs/images, for example:
![The Home page](docs/images/home.png)
![Correcting text in a browser](docs/images/demo.gif)
-->

## Download and use

Get the latest zip from the [Releases page](../../releases), extract it, double-click
`TextCorrector.exe` and download a model. Windows only. See "The ready-to-use zip" below.

## How it works

1. You press a hotkey.
2. The tool copies your selection, sends it to a local Ollama model and asks for a corrected
   version (typos, spelling, casing and punctuation; wording and meaning stay the same).
3. The answer is checked, pasted over your selection, and your previous clipboard text is put back.

Long texts are corrected paragraph by paragraph, so small models keep track and a part the model
keeps getting wrong is left as it was (the activity log says so) instead of losing the whole text.
If the model's answer does not look like a plain correction (for example extra commentary or
changed line breaks), nothing is pasted for that part and the program tells you why.

## Two ways to get it

- **The ready-to-use zip** (for other people): extract it, run `TextCorrector.exe`, download a
  model. No Python, no Ollama installation and no virtual environment are needed. See
  "The ready-to-use zip" below.
- **From the source** (for development): the rest of this readme. It uses your own Ollama.

## Project folder structure

```
Text-Corrector\                  <- the project folder
    env\                         <- the virtual environment
    text_corrector\               <- the program (all its .py files; the folder name matters)
    packaging\                   <- build.bat, build_release.py, uninstall.bat, ... (for the zip)
    requirements.txt, README.md, run.bat, run_console.bat
```

`python packaging\build_release.py --check` checks that everything is in the right place.

## Requirements (running from the source)

- Windows
- Python 3.11 or newer (older versions also work if you run `pip install tomli`)
- [Ollama](https://ollama.com), running, with a model installed. The default model is
  installed with `ollama pull gemma3:4b`

## Installation

```
python -m venv env
env\Scripts\activate
pip install -r requirements.txt
```

## Running

Double-click `run.bat`. The program opens as a normal window, without a console. Keep `run.bat`
in the project folder, next to the `env` folder and the `text_corrector` folder.

The window has three tabs:

- **Home:** the status, the model panel, the last correction (before and after) and a list of what
  the program has done. The model panel shows whether the model is loaded in memory, how much
  memory it uses (or roughly needs), and when it is unloaded after a period without use (the
  "Keep model loaded for" setting). **Load model now** loads it ahead of time, so the next
  correction does not have to wait for it. The program loads the model by itself when needed.
- **Models:** every model you can use. Download as many as you like (one at a time, the program
  is locked with a progress window until it is done), choose which one to use with **Use this
  model**, and **Remove** the ones you do not need. Each model shows its download size, roughly
  how much memory it needs, its release date and a **More info** link to its page. Smaller models
  are faster and need less memory; larger ones are usually more accurate. **Custom model** lets
  you download any model from the Ollama library by name. The **language** of your text and the
  **extra instructions to the model** are set here too, below the list.
- **Settings:** one control for every setting, with a description. Every change is applied and
  saved as soon as you make it.

At the bottom left of every tab is the credit line; its link is set in `text_corrector\about.py`.

The tray icon is there from the start (unless you turn it off in Settings, see below). When you
minimize the window it disappears into the tray (next to the clock); click the tray icon, or choose
Open in its menu, to bring it back. Choose Quit in the tray menu, press the quit hotkey, or close
the window to stop the program. On Windows 11 a new tray icon may be hidden under the small arrow
next to the clock until you drag it out. If the tray cannot be used (the `pystray` and `pillow`
packages are missing, or Windows refuses), the activity log says why and the window minimizes to
the taskbar as usual. The background color of the tray icon, of the window icon and of the icon in
the taskbar shows the status: green is ready, yellowish is ready but the model is not loaded,
red is an error, and blue is loading or working. In Settings, turn off **Minimize to the tray** to
minimize to the taskbar instead; no tray icon is shown then.

On start the program loads the model and plays a short rising sound when it is ready. The status
at the top is green ("Ready") only while the model is also loaded in memory. It turns yellow when
only the program is ready and the model is not loaded, for example after it has been idle for
longer than the "Keep model loaded for" time. The model then loads again when you use it, which
takes a moment for the first correction.

| Hotkey | Action |
| --- | --- |
| F10 | **Correct and paste:** corrects the selected text and pastes the result over it |
| F9 | **Correct to clipboard:** corrects the selected text too, but does not paste: the corrected text waits on the clipboard until you press Ctrl+V. Handy for long texts, so you need not wait for the result |
| Ctrl+Alt+F12 | Quit |

All three hotkeys can be changed in the settings. Windows reserves a hotkey for this program
while it runs, so the program in front never receives it. This matters because many programs use
keys such as F10 for their own menu. If another program already uses a combination, this program
says so and you can choose another one.

Only one copy of the program runs at a time: starting it again (for example from a taskbar pin)
brings the running window forward. Texts in the window, such as the last correction, can be marked
and copied. **Copy diagnostics** on the Home page copies a report about the program and its
latest errors (it contains no corrected text), handy when asking for help. Before a model
downloads, the program checks that there is enough free disk space.

By default the window opens large enough to show the whole Home page. On a small screen the Home
page gets a scroll bar instead of being cut off. When you close the program it remembers the window
size and uses it next time; **Reset window size** in the Settings tab goes back to the automatic
size. To choose the size new installs start with, set `width` and `height` in the `[window]` section
of `config.toml` (or the defaults of `Window` in `text_corrector/settings.py` before building);
`0` means automatic.

### Console version

The original console version is still available: double-click `run_console.bat`, or run
`python -m text_corrector --console`. Press Ctrl+O in the console window to open a text version of
the settings screen. Press Enter to go back; changes are saved as you make them.

## Settings

The Models tab also holds the **Language** of your text (English by default, "Detect automatically"
lets the model decide; experimental for other languages) and the **Extra instructions to model**
(plain sentences added to what the model is told for every correction, for example "Use British
spelling." Keep it short). The Settings tab holds the rest:

| Setting | What it does |
| --- | --- |
| Hotkeys | The key combinations. Click a button and press the new combination, or Esc to keep the old one |
| Keep model loaded for | How long the model stays in memory after the last use, as hours and minutes. **Forever** keeps it loaded until the program is closed |
| Request timeout | How long to wait for the model before giving up |
| Tray | Minimize to the tray (default), or to the taskbar |
| Start with Windows | Starts the program in the tray when you log in, without loading the model, so no memory is used until you correct something. Installed program only |
| Processor (built-in engine) | Auto uses the graphics card (NVIDIA, AMD or Intel) when it can; CPU only uses just the processor. Try CPU only if the program crashes or behaves strangely on a PC |
| Sounds | Short sounds when the program is ready, when a correction starts, finishes, finds nothing to fix, or fails. Each has its own sound |
| Sound volume | The volume of all sounds together, from 0 (silent) to 100 (loudest) |
| Highlight changes | After a correction, the Before and After boxes color what differs: changed words yellow, removed words red, added words green, punctuation gray, and words that moved blue |

The settings are stored in `%APPDATA%\TextCorrector\config.toml`, created on first start with
explanations next to every setting. Two settings are only in the file: the Ollama `url` (used
with your own Ollama, not with the built-in engine) and the `temperature` (how much the answers
may vary; 0 is the most predictable). You can edit the file by hand too; restart the program for
those changes to apply. If a setting is invalid, the program tells you which one and does not
start. Delete the file to get a fresh copy with the defaults. Set the environment variable
`CORRECTOR_CONFIG` to use a file in another location. Saving from the program rewrites the file
from the program's own template, so comments you added yourself are not kept.

## The ready-to-use zip

This is the version for other people. Everything it needs is in its own folder.

1. Extract the zip to a folder you can write to, for example `C:\Users\YourName\TextCorrector`.
2. Double-click `TextCorrector.exe`. Windows may warn about an unknown publisher the first
   time ("More info", then "Run anyway"), because the program is not signed.
3. The first time there is no model yet, so the program opens on the Models tab. Press Download
   next to one (a few gigabytes, once). The progress is shown, and the model is used as soon as
   it is ready. Later you can download others there and switch between them.
4. To remove everything, close the program (tray icon, Quit) and delete the folder, or
   double-click `uninstall.bat` in it. Nothing else on the PC was changed.

### The built-in engine

The zip contains its own copy of Ollama, which the program starts in the background when it
opens and stops when it closes. It does not install anything in Windows, has no tray icon or
autostart of its own, and does not touch an Ollama you may have installed yourself: it uses a
free local port, and keeps its models, settings and temporary files in the program's folder
(`models` and `data`). Its log is `data\logs\ollama.log`.

Graphics cards: NVIDIA cards are used through CUDA, and AMD and Intel cards (also the ones
built into the processor) through Vulkan, with the normal graphics drivers. When no graphics
card can be used, the processor does the work, which is slower. The Model panel on the Home
page shows how much of the model sits on the graphics card and how much in system RAM.

To use your own Ollama instead of the built-in one, delete or rename the `ollama` folder next
to the program, and set the address in the settings.

### Building the zip

On Windows, in the project folder with the virtual environment in `env`, run
`packaging\build.bat`. It packs the program with PyInstaller, adds Ollama's standalone
Windows zip (about 1.5 GB), the readme, license notices, `uninstall.bat` and the source, and
makes `release\TextCorrector-<date>.zip`. The options and details are in
`packaging\BUILDING.txt`.

## Choosing a model

Small models are fast but make more mistakes, and some are much better than others in languages
other than English. To compare models on your own texts, install the candidates with
`ollama pull` and run:

```
python -m text_corrector.compare gemma4:e4b gemma4:e2b gemma3:4b
```

Each model corrects the same test texts (one Danish and one English text are built in). The
result is scored against the correct version, where 100 means identical, and the time per text is
shown. The score is a rough character-level similarity, so look at the printed texts as well.
The score of the uncorrected text is shown for reference: a model that scores lower than that made
the text worse.

To use your own test texts, make a file such as `cases.toml` and add `--cases cases.toml`:

```toml
[[case]]
name = "My Danish test"
language = "Danish"
text = "text with typos"
expected = "the correct version of the text"
```

The model names above are examples. Check the Ollama library for what is available, and update
Ollama first if a newer model is not recognized.

## Troubleshooting

- **"Could not reach Ollama"**: start Ollama and try again.
- **HTTP 404 from Ollama**: the model is not installed. Run `ollama pull <model name>`.
- **"The model did not answer in the expected format"**: the model replied with something other
  than the JSON answer the program asks for. Try again, or choose another model in the Models
  tab. Thinking models (such as Gemma 4) are asked not to think, and the program also accepts a
  reply wrapped in a code fence. If you use your own Ollama, update it: structured output needs a
  recent version.
- **"No text was selected, or the app did not copy it"**: the program in front did not copy the
  selection. Some programs need a little longer to copy and paste; the delays are at the top of
  `textio.py`. If it only happens in one program, try another hotkey in the settings.
- **A hotkey "cannot be used"**: another program has already taken that key combination.
  Choose a different one in the settings.
- **"The built-in engine could not start"**: read `data\logs\ollama.log` in the program's
  folder. Antivirus software sometimes blocks the engine (`ollama\Text-Corrector-Engine.exe`); allow it, or
  add the program's folder as an exception. If the log mentions the graphics card or driver,
  set "Processor (built-in engine)" to "CPU only" in the settings. The program then tries the
  address from the settings instead, so an Ollama of your own is used if it is running.
- **Cannot see the tray icon**: on Windows 11 it may be under the small arrow next to the clock.
  The activity log on the Home tab says if the tray icon could not be started.
- **Nothing appears when the program starts**: look for the tray icon. If the program stopped
  with an error, a message box says so, and details are saved in
  `%APPDATA%\TextCorrector\error.log`.
- **To see what the model answered**: set `CORRECTOR_DEBUG=1` before starting (in `cmd`:
  `set CORRECTOR_DEBUG=1`) and use the console version. The raw reply is shown after every request.

## Known limitations

- Only text on the clipboard is restored afterwards. An image or file you had copied is lost.
- Settings files from earlier versions keep working: the old "correct line" hotkey setting is now
  the "correct to clipboard" hotkey.
- Language support depends on the model and is experimental.

## Credits

This project was inspired by two earlier tools, and thanks go to their authors:

- [ai-typing-assistant](https://github.com/patrickloeber/ai-typing-assistant) by Patrick Loeber
  (MIT license)
- [Typing-Assist](https://github.com/x404xx/Typing-Assist) by x404xx

This version has since been restructured and rewritten with its own code, and extended with
settings, safety checks, feedback sounds and a window.

## License

The source code is released under the [MIT License](LICENSE). The built-in engine is
[Ollama](https://github.com/ollama/ollama) (MIT), and the language models you download are
separate works with their own licenses (see each model's page). The libraries the program uses
are listed in `packaging\THIRD_PARTY_NOTICES.txt`.

## Contributing

Bug reports and ideas are welcome as GitHub issues. When reporting a problem, press **Copy
diagnostics** on the Home page and paste the result into the issue.
