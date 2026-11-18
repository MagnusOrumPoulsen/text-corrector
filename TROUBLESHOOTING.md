# Text Corrector: troubleshooting / fejlfinding

[English](#english) | [Dansk](#dansk)

When asking for help, press **Copy diagnostics** on the Status tab and paste the result into a
[GitHub issue](../../issues). / Når du beder om hjælp, så tryk på **Kopiér diagnostik** på fanen
Status, og indsæt resultatet i et [GitHub-issue](../../issues).

## English

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
- **The first start takes a long time ("Running first-time setup...")**: the first time, the built-in
  engine sets itself up and looks for graphics cards, which can take several minutes on a slow PC. Wait
  until it is done; downloads are locked meanwhile and unlock by themselves.
- **A hotkey does nothing in one program**: some programs react to the key combination themselves (for
  example Notepad when Alt is pressed first). Press the keys in another order, change the hotkeys in the
  settings, or type or paste the text into the Before box on the Last correction tab and press Correct.
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

## Dansk

- **"Modellens svar udelod N ord"**: modellen droppede en del af teksten, hvilket en korrekturlæser
  ikke bør gøre, så svaret blev ikke brugt. Programmet prøvede så teksten sætning for sætning. Hvis
  det bliver ved med at ske med én model, så prøv en anden på fanen Modeller: små modeller gør det
  oftere.
- **"Modellen svarede ikke i det forventede format"**: modellen svarede med noget andet end det
  JSON-svar, programmet beder om. Prøv igen, eller vælg en anden model på fanen Modeller. Modeller,
  der kan "tænke" (som Gemma 4), bliver bedt om at lade være, og programmet accepterer også et svar
  pakket ind i en kodeblok.
- **"Baggrundsprocessen svarer ikke"**: luk Text Corrector, og start programmet igen. Hvis det
  bliver ved med at ske, så tryk på **Kopiér diagnostik** på fanen Status, og se
  `data\logs\ollama.log`.
- **"Baggrundsprocessen kunne ikke starte"**: læs `data\logs\ollama.log` i programmets mappe.
  Antivirusprogrammer blokerer nogle gange baggrundsprocessen (`ollama\Text-Corrector-Engine.exe`); tillad den,
  eller tilføj programmets mappe som en undtagelse. Hvis loggen nævner grafikkortet eller driveren, så
  sæt "Processor" til "CPU" under Indstillinger.
- **En model kører på CPU'en, selvom Prøv GPU er valgt**: modellen er måske for stor til
  grafikkortets hukommelse; en mindre model (eller en med en mindre downloadstørrelse) kan være der.
  Nogle modeller i Ollama-biblioteket har også deres egen indstilling, der holder dem væk fra
  grafikkortet; Text Corrector tilsidesætter den, når Prøv GPU er valgt.
- **Første start tager lang tid ("Kører førstegangsopsætning...")**: første gang sætter baggrundsprocessen
  sig selv op og leder efter grafikkort, hvilket kan tage flere minutter på en langsom pc. Vent, til den er
  færdig; hentning af modeller er låst imens og låses op af sig selv.
- **En genvejstast gør ikke noget i ét program**: nogle programmer reagerer selv på tastekombinationen (for
  eksempel Notesblok, hvis du trykker på Alt først). Tryk tasterne i en anden rækkefølge, skift genvejstasterne
  under Indstillinger, eller skriv eller indsæt teksten i feltet Før på fanen Seneste rettelse, og tryk på Ret.
- **"Der var ingen markeret tekst, eller programmet kopierede den ikke"**: programmet i forgrunden
  kopierede ikke markeringen. Nogle programmer skal bruge lidt længere tid til at kopiere og indsætte.
  Hvis det kun sker i ét program, så prøv en anden genvejstast under Indstillinger.
- **En genvejstast "kan ikke bruges"**: et andet program har allerede taget den tastekombination.
  Vælg en anden under Indstillinger.
- **Kan ikke se ikonet i systembakken**: på Windows 11 kan det være under den lille pil ved siden af
  uret. Aktivitetsloggen på fanen Status siger, hvis ikonet ikke kunne startes.
- **Der sker ikke noget, når programmet starter**: kig efter ikonet i systembakken. Hvis programmet
  stoppede med en fejl, siger en meddelelsesboks det, og detaljerne gemmes i `data\error.log`.
- **"Kunne ikke få forbindelse til Ollama"** (når programmet køres fra kildekoden): start Ollama, og
  prøv igen.
- **HTTP 404 fra Ollama**: modellen er ikke installeret. Kør `ollama pull <modelnavn>`.
- **For at se, hvad modellen svarede**: sæt `CORRECTOR_DEBUG=1`, før du starter (i `cmd`:
  `set CORRECTOR_DEBUG=1`), og brug konsolversionen. Det rå svar vises efter hver forespørgsel.
