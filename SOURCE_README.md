# Text Corrector: building from the source

This is for people who want to run Text Corrector from its source code, or build the
ready-to-use zip themselves. If you just want to use the program, download the ready-to-use zip
from the Releases page instead (see [README.md](README.md)).

## What you need

- Windows 10 or 11 (64-bit).
- Python 3.11 or newer from [python.org](https://www.python.org/downloads/windows/). In the
  installer, tick **Add python.exe to PATH**. The installer also adds the `py` command, which the
  steps below use.
- An internet connection: the build downloads Ollama's Windows release (about 1.5 GB, kept in
  `build\cache` afterwards) and the Python packages.
- About 10 GB of free disk space for the build (more for the models you download later).

## 1. Set up the folder (once)

1. Extract `TextCorrector-<version>-source.zip`, for example to `C:\Text-Corrector`.
2. Open a Command Prompt in that folder: open the folder in File Explorer, click in the address
   bar, type `cmd` and press Enter.
3. Create a virtual environment (a private Python folder for this project, called `env`) and
   install the packages the program needs:

   ```
   py -m venv env
   env\Scripts\activate
   py -m pip install -r requirements.txt
   ```

The folder then looks like this:

```
Text-Corrector\
    env\                  the virtual environment (made in step 3)
    text_corrector\       the program itself
    packaging\            the build scripts (build.bat) and the files that go into the zip
    requirements.txt      the Python packages, with the exact versions used for this release
    run.bat               runs the program from the source
    run_console.bat       runs the console version (shows messages, handy when debugging)
    README.md, README.da.md, SOURCE_README.md, LICENSE
```

## 2. Build the ready-to-use zip

In the project folder, double-click `packaging\build.bat` (or run it in the Command Prompt).
It asks **Full build? (y/n)**: answer **y** the first time.

When it is done:

- `dist\TextCorrector\` is the finished program. You can run `TextCorrector.exe` from there to test it.
- `release\TextCorrector-<version>.zip` is the zip to share.
- `release\TextCorrector-<version>-source.zip` is a zip of the source, like the one you started from.

Answer **n** on later builds: the models and settings in `dist\TextCorrector` are then kept,
so you need not download the models again to test a new build.

The build uses the Ollama version this release was tested with. `packaging\BUILDING.txt` lists
the options, for example `packaging\build.bat --ollama-version latest` to use the newest Ollama.

## 3. Run from the source (optional)

`run.bat` starts the program directly from the source files, without building. It then uses
your own Ollama installation (install it from [ollama.com](https://ollama.com) and start it),
because the built-in engine only comes with the built program. To use the built-in engine of a
build instead, set `CORRECTOR_OLLAMA_DIR` to the `dist\TextCorrector\ollama` folder before
starting:

```
set CORRECTOR_OLLAMA_DIR=%CD%\dist\TextCorrector\ollama
env\Scripts\pythonw.exe -m text_corrector
```

When running from the source, the settings are kept in `%APPDATA%\TextCorrector\config.toml`
(the built program keeps them in its own `data` folder).

## Translations

The window's texts are written in English in the code. The Danish texts are in
`text_corrector\translations_da.py`. After changing a text in the code, run

```
py -m text_corrector.i18n_check
```

to see which texts have no Danish translation (they are shown in English until they get one).

## License

MIT, see [LICENSE](LICENSE). The built-in engine is [Ollama](https://github.com/ollama/ollama)
(MIT); the libraries are listed in `packaging\THIRD_PARTY_NOTICES.txt`.
