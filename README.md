# Text Corrector

A Windows tool that fixes the typos in any text you highlight, with a language model running on
your own PC. / Et Windows-værktøj, der retter stavefejl i den tekst, du markerer, med en sprogmodel,
der kører på din egen pc.

[**Download the latest version / Hent den nyeste version**](../../releases/latest)

!\[Text Corrector in action](docs/images/showcase.gif)

Choose your language below / Vælg dit sprog nedenfor:

<!-- ENGLISH START: edit the English text here, between these two markers -->

<details>
<summary><b>English: click here to read in English</b></summary>

A simple-to-install-and-use Windows tool: highlight some text, press a hotkey, and it fixes the
typos using a language model running on your own computer, with [Ollama](https://ollama.com) as
the engine. After a one-time download of a language model, it works offline.

**Privacy:** your text never leaves your PC. The only time the program uses the internet is when
you download a model.

## Download and use

1. Get the newest `TextCorrector-<version>.zip` from the [latest release](../../releases/latest)
(look under "Assets").
2. Extract it, double-click `TextCorrector.exe`, and download a model in the Models tab (the
medium model, gemma4:e2b, is a good start).
3. Highlight some text in any program and press **Ctrl+Alt+Shift+2** to correct it in place, or
**Ctrl+Alt+Shift+1** to get the corrected text on the clipboard instead.

No Python, no separate Ollama installation and nothing to set up. Everything stays in the
program's own folder: to remove it, delete the folder (or run `uninstall.bat`).

**Requirements:** Windows 10 or 11 (64-bit), about 1.5 GB to download, and 3 to 10 GB of disk
space per language model. A graphics card (NVIDIA, AMD or Intel) is optional but makes the
corrections faster.

## Features

* **Works in any program.** The corrected text replaces your selection, or waits on the clipboard
until you paste it.
* **Works fully minimized.** Hotkeys for everything (correct, load or unload the model, show or hide
the window), short tray updates ("Correcting...", "Pasted!"), a sound for each step, and a tray
icon whose color shows the status.
* **See what changed.** The text before and after the last correction side by side, with the
changes highlighted.
* **Safe corrections.** Every answer is checked before it is pasted. A part the model gets wrong is
retried sentence by sentence or left as it was; your text is never lost.
* **Your choice of model.** Small, medium and large models to download, any other model from the
Ollama library, and a clear view of whether it runs on the graphics card or the processor.
* **Autodetects and works in most languages (Tested in Danish and English).**
* **Advanced settings** for testing your own system prompt and example correction.

Everything else is explained in the program itself.

## Screenshots

!\[The Last correction tab](docs/images/main.png)
!\[The Settings tab](docs/images/Settings.png)

## Known limitations

* Correct and paste restores only text on the clipboard afterwards; an image or file you had copied
is lost. Correct to clipboard always overwrites the clipboard.
* Languages other than English are experimental.
* The program is not code-signed, so Windows can show a warning the first time ("More info", then
"Run anyway"). Some antivirus programs also flag programs made with PyInstaller.

Problems? See [TROUBLESHOOTING.md](TROUBLESHOOTING.md). Bug reports and ideas are welcome as
[GitHub issues](../../issues); press **Copy diagnostics** on the Status tab and paste the result
into the issue.

## Source code

The source code of each version is attached to its release as `TextCorrector-<version>-source.zip`.
[SOURCE\_README.md](SOURCE_README.md) explains how to run it and how to build the program yourself.

## Credits and license

Inspired by [ai-typing-assistant](https://github.com/patrickloeber/ai-typing-assistant) by Patrick
Loeber (MIT license) and [Typing-Assist](https://github.com/x404xx/Typing-Assist) by x404xx; this
version has since been rewritten with its own code.

The source code is released under the [MIT License](LICENSE). The built-in engine is
[Ollama](https://github.com/ollama/ollama) (MIT), and the language models you download have their
own licenses (see each model's page). The libraries the program uses are listed in
[THIRD\_PARTY\_NOTICES.txt](THIRD_PARTY_NOTICES.txt).

</details>
<!-- ENGLISH END -->

<!-- DANISH START: made from README.da.md by packaging\\update\_readme.py; edit README.da.md, not this part -->

<details>
<summary><b>Dansk: klik her for at læse på dansk</b></summary>

Et Windows-værktøj, der er nemt at installere og bruge: markér noget tekst, tryk på en
genvejstast, og stavefejlene bliver rettet af en sprogmodel, der kører på din egen computer, med
[Ollama](https://ollama.com) som motor. Når du først har hentet en sprogmodel, virker programmet
uden internet.

**Privatliv:** din tekst forlader aldrig din pc. Programmet bruger kun internettet, når du henter en
model.



## Hent og brug

1. Hent den nyeste `TextCorrector-<version>.zip` fra [den nyeste udgivelse](../../releases/latest)
(se under "Assets").
2. Pak den ud, dobbeltklik på `TextCorrector.exe`, og hent en model på fanen Modeller (den
mellemstore model, gemma4:e2b, er et godt sted at starte).
3. Markér noget tekst i et vilkårligt program, og tryk på **Ctrl+Alt+Shift+2** for at rette den på
stedet, eller på **Ctrl+Alt+Shift+1** for i stedet at få den rettede tekst i udklipsholderen.

Ingen Python, ingen separat Ollama-installation og intet at sætte op. Alt ligger i programmets egen
mappe: vil du fjerne det, så slet mappen (eller kør `uninstall.bat`).

**Krav:** Windows 10 eller 11 (64-bit), cirka 1,5 GB at hente og 3 til 10 GB diskplads pr.
sprogmodel. Et grafikkort (NVIDIA, AMD eller Intel) er ikke nødvendigt, men gør rettelserne hurtigere.

## Funktioner

* **Virker i alle programmer.** Den rettede tekst erstatter din markering eller venter i
udklipsholderen, indtil du indsætter den.
* **Virker helt minimeret.** Genvejstaster til det hele (ret, indlæs eller fjern modellen, vis eller
skjul vinduet), korte opdateringer fra systembakken ("Retter...", "Indsat!"), en lyd for hvert trin
og et ikon i systembakken, hvis farve viser status.
* **Se, hvad der blev ændret.** Teksten før og efter den seneste rettelse side om side, med
ændringerne fremhævet.
* **Sikre rettelser.** Hvert svar bliver tjekket, før det indsættes. En del, som modellen laver fejl
i, prøves igen sætning for sætning eller lades uændret; din tekst går aldrig tabt.
* **Du vælger modellen.** Små, mellemstore og store modeller at hente, enhver anden model fra
Ollama-biblioteket og et klart overblik over, om den kører på grafikkortet eller processoren.
* **Autodetekterer og virker med de fleste sprog (Tested med dansk engelsk).**
* **Avancerede indstillinger** til at teste din egen systemprompt og dit eget eksempel.

Resten er forklaret i selve programmet.

## Skærmbilleder

!\[Fanen Seneste rettelse](docs/images/main.png)
!\[Fanen Indstillinger](docs/images/Settings.png)

## Kendte begrænsninger

* Ret og indsæt gendanner kun tekst i udklipsholderen bagefter; et billede eller en fil, du havde
kopieret, går tabt. Ret til udklipsholder overskriver altid udklipsholderen.
* Andre sprog end engelsk er eksperimentelle.
* Programmet er ikke kodesigneret, så Windows kan vise en advarsel første gang ("Flere
oplysninger" og derefter "Kør alligevel"). Nogle antivirusprogrammer markerer også programmer, der
er lavet med PyInstaller.

Problemer? Se [TROUBLESHOOTING.md](TROUBLESHOOTING.md#dansk). Fejlrapporter og idéer er velkomne som
[GitHub-issues](../../issues); tryk på **Kopiér diagnostik** på fanen Status, og indsæt resultatet i
dit issue.

## Kildekode

Kildekoden til hver version ligger ved dens udgivelse som `TextCorrector-<version>-source.zip`.
[SOURCE\_README.md](SOURCE_README.md) (på engelsk) forklarer, hvordan du kører den, og hvordan du
selv bygger programmet.

## Tak og licens

Inspireret af [ai-typing-assistant](https://github.com/patrickloeber/ai-typing-assistant) af Patrick
Loeber (MIT-licens) og [Typing-Assist](https://github.com/x404xx/Typing-Assist) af x404xx; denne
version er siden blevet skrevet om med sin egen kode.

Kildekoden er udgivet under [MIT-licensen](LICENSE). Den indbyggede motor er
[Ollama](https://github.com/ollama/ollama) (MIT), og de sprogmodeller, du henter, har deres egne
licenser (se hver models side). De biblioteker, programmet bruger, står i
[THIRD\_PARTY\_NOTICES.txt](THIRD_PARTY_NOTICES.txt).

</details>

<!-- DANISH END -->

