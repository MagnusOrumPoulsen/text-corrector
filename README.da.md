# Text Corrector

[English](README.md) | **Dansk**

**[Hent den nyeste version af Text Corrector](../../releases/latest)** (vælg `TextCorrector-<version>.zip` under "Assets")

Et Windows-værktøj, der er nemt at installere og bruge: markér noget tekst, tryk på en
genvejstast, og stavefejlene bliver rettet af en sprogmodel, der kører på din egen computer.
Alt kører lokalt, med [Ollama](https://ollama.com) som motor. Når du først har hentet en
sprogmodel fra Ollama, virker programmet uden internet.

**Privatliv:** din tekst forlader aldrig din pc. Programmet bruger kun internettet, når du henter en
model.

![Text Corrector i brug](docs/images/showcase.gif)

## Hent og brug

1. Hent `TextCorrector-1.0.0.zip` (eller den nyeste version) fra [den nyeste udgivelse](../../releases/latest) (se under "Assets").
2. Pak den ud, dobbeltklik på `TextCorrector.exe`, og hent en model.

Du behøver ikke installere Python eller Ollama, og der skal ikke sættes noget virtuelt miljø op.
Se [Den færdige zip-fil](#den-færdige-zip-fil) for detaljer.

**Krav:** Windows 10 eller 11 (64-bit). Cirka 1,5 GB at hente, nogle få GB diskplads, når den er
pakket ud, og derefter 3 til 10 GB for hver sprogmodel, du henter (du kan hente flere). Du skal også
have nok ledig hukommelse (RAM eller grafikkortets hukommelse) til den model, du vælger; fanen
Modeller viser cirka, hvor meget hver model kræver. Der er både små og større modeller at vælge
imellem. Et grafikkort er ikke nødvendigt, men gør rettelserne hurtigere.

## Sådan virker det

1. Du markerer noget tekst og trykker på en genvejstast.
2. Værktøjet kopierer din markering, sender den til en lokal Ollama-model og beder om en rettet
   udgave (stavefejl, slåfejl, store og små bogstaver og tegnsætning; ordvalg og betydning forbliver
   de samme).
3. Svaret bliver tjekket og, afhængigt af genvejstasten, enten indsat over din markering eller lagt i
   udklipsholderen, klar til at blive indsat med Ctrl+V.

Lange tekster rettes afsnit for afsnit, så små modeller kan følge med, og en del, som modellen bliver
ved med at lave fejl i, bliver ladt uændret (aktivitetsloggen siger det) i stedet for at hele teksten
går tabt. Hvis modellens svar ikke ligner en almindelig rettelse (fx ekstra kommentarer eller ændrede
linjeskift), indsættes der intet for den del, og programmet fortæller hvorfor.

## Skærmbilleder

![Fanen Status](docs/images/main.png)
![Fanen Modeller](docs/images/models.png)
![Fanen Indstillinger](docs/images/Settings.png)

## Detaljer om programmet

Vinduet har fire faner:

- **Seneste rettelse** (fanen, vinduet åbner på): hurtig hjælp til genvejstasterne (**Skjul hurtig
  hjælp** folder den sammen, når du kender dem), og teksten før (til venstre) og efter (til højre)
  den seneste rettelse, så store som vinduet tillader, med en rullebjælke i hvert felt, når teksten er
  længere. Før-feltet udfyldes, i det øjeblik du trykker på genvejstasten, og Efter-feltet viser
  "Retter...", indtil resultatet er klar. Forskellene farves (se nedenfor); afkrydsningsfeltet
  **Fremhæv ændringer** under farveforklaringen slår farverne til og fra.
- **Status:** modelpanelet og en liste over, hvad programmet har gjort. Modelpanelet viser, om
  modellen er indlæst i hukommelsen, hvor meget hukommelse den bruger (eller cirka kræver), og hvornår
  den fjernes fra hukommelsen efter en periode uden brug (indstillingen "Hold modellen indlæst i").
  **Indlæs model nu** indlæser den på forhånd, så den næste rettelse ikke skal vente på den.
  Programmet indlæser selv modellen, når der er brug for den.
- **Modeller:** de modeller, du kan bruge. Hent så mange, du vil (én ad gangen; programmet er låst
  med et statusvindue, indtil hentningen er færdig), vælg hvilken der skal bruges med **Brug denne
  model**, og **Fjern** dem, du ikke har brug for. Hver model viser sin downloadstørrelse, cirka hvor
  meget hukommelse den kræver, sin udgivelsesdato og et **Mere info**-link til sin side. Mindre
  modeller er hurtigere og kræver mindre hukommelse; større modeller er som regel mere præcise.
  **Brugerdefineret model** lader dig hente en hvilken som helst model fra Ollama-biblioteket ved
  navn. **Sproget** i din tekst og de **avancerede indstillinger** (se nedenfor) indstilles også her,
  under listen.
- **Indstillinger:** én kontrol for hver indstilling, med en beskrivelse. Hver ændring træder i kraft
  og gemmes, så snart du laver den.

Nederst på hver fane står kreditlinjen (til venstre) og versionsnummeret (til højre).

Vinduet kan vises på engelsk eller dansk (**Programmets sprog** øverst på fanen Indstillinger).
"Samme som Windows", som er standard, bruger dansk på en dansk Windows og ellers engelsk.

Ikonet i systembakken er der fra start (medmindre du slår det fra under Indstillinger). Når du
minimerer vinduet, forsvinder det ned i systembakken (ved siden af uret); klik på ikonet, eller vælg
Åbn i dets menu, for at hente det frem igen. Vælg Afslut i menuen, eller luk vinduet, for at stoppe
programmet. På Windows 11 kan et nyt ikon være gemt under den lille pil ved siden af uret, indtil du
trækker det ud. Hvis systembakken ikke kan bruges, siger aktivitetsloggen hvorfor, og vinduet
minimeres til proceslinjen som normalt. Baggrundsfarven på ikonet i systembakken, på vinduets ikon og
på ikonet på proceslinjen viser status: grøn er klar, gullig er klar, men modellen er ikke indlæst,
rød er en fejl, og blå er indlæser eller arbejder. Slå **Minimér til systembakken** fra under
Indstillinger for i stedet at minimere til proceslinjen; så vises der intet ikon i systembakken.

Slå **Opdateringer fra systembakken** til under Indstillinger for at se korte beskeder i hjørnet over
systembakken, mens vinduet er skjult: "Retter...", "Indsat!", "Rettet tekst i udklipsholderen",
"Intet at rette", "Fejl under rettelse", "Indlæser model...", "Model indlæst" og "Model fjernet fra
hukommelsen". Hver besked forsvinder efter cirka et sekund. Beskederne tager aldrig tastaturfokus, så
indsætningen bliver ikke forstyrret.

Ved start indlæser programmet modellen og spiller en kort, stigende lyd, når det er klar. Status
øverst er kun grøn ("Klar"), når modellen også er indlæst i hukommelsen. Den bliver gul, når kun
programmet er klar og modellen ikke er indlæst, fx når den har været ubrugt i længere tid end
"Hold modellen indlæst i". Modellen indlæses så igen, når du bruger den, hvilket tager et øjeblik
ved den første rettelse.

| Genvejstast (standard) | Handling |
| --- | --- |
| Ctrl+Alt+Shift+2 | **Ret og indsæt:** retter den markerede tekst og indsætter resultatet over den |
| Ctrl+Alt+Shift+1 | **Ret til udklipsholder:** retter den markerede tekst, men indsætter den ikke med det samme: den rettede tekst venter i udklipsholderen, indtil du trykker på Ctrl+V. Praktisk til lange tekster, så du ikke behøver vente på resultatet |
| Ctrl+Alt+Shift+3 | **Indlæs/fjern model:** indlæser modellen i hukommelsen, når den ikke er indlæst (så næste rettelse går hurtigt), og fjerner den igen for at frigøre hukommelsen, når den er indlæst |
| Ctrl+Alt+Shift+4 | **Vis/skjul vindue:** minimerer vinduet (til systembakken eller proceslinjen) eller henter det frem igen, på fanen Seneste rettelse (slå **Start på fanen "Seneste rettelse"** fra under Indstillinger for at blive på den fane, der var åben) |

Alle fire genvejstaster kan ændres under Indstillinger. Windows reserverer en genvejstast til dette
program, mens det kører, så programmet i forgrunden aldrig modtager den. Det betyder noget, fordi
mange programmer bruger taster som F10 til deres egen menu. Standardtasterne kan alle trykkes med
venstre hånd, og de er valgt, fordi almindelige programmer ikke bruger dem. Hvis et andet program allerede bruger en
kombination, siger programmet det, og du kan vælge en anden. Hvis du skal bruge standardtasterne til
noget andet, så vælg andre genvejstaster under Indstillinger.

Efter en rettelse farver **Før**- og **Efter**-felterne på fanen Seneste rettelse forskellene:
ændrede ord gule, fjernede ord røde, tilføjede ord grønne, tegnsætning blå og flyttede ord grå. Fjern
fluebenet i **Fremhæv ændringer** under farverne for at slå det fra.

En gang imellem giver en model et svar, der ikke kan bruges, fx fordi den udelader ("glemmer") ord.
Programmet opdager det (det afviser også svar, der har mistet flere ord) og retter så den del af
teksten én sætning ad gangen (op til hvert punktum, spørgsmålstegn eller udråbstegn), fordi korte
stykker sjældent går galt. Modellen ser mindre sammenhæng på den måde, men du får et resultat. En
sætning, der stadig fejler, bliver ladt uændret, og aktivitetsloggen siger det. Det afviste svar vises
med gråt under Efter-feltet på fanen Seneste rettelse, så du kan se, hvad modellen svarede.

**Kopiér diagnostik** på fanen Status kopierer en rapport om programmet og dets seneste fejl (den
indeholder ingen rettet tekst), praktisk ved fejlfinding.

## Programmets indstillinger

Fanen Modeller indeholder også **Sproget** i din tekst ("Registrer automatisk" som standard, hvor
modellen selv finder ud af sproget; vælger du et sprog, bruger Text Corrector sin egen prompt og sit
eget eksempel til det) og de avancerede indstillinger (se nedenfor). Fanen Indstillinger indeholder
resten:

| Indstilling | Hvad den gør |
| --- | --- |
| Programmets sprog | Vinduets sprog: Samme som Windows (standard), English eller Dansk. Text Corrector genstarter for at skifte sprog |
| Genvejstaster | De fire tastekombinationer. Klik på en knap, og tryk på den nye kombination, eller tryk Esc for at beholde den gamle |
| Hold modellen indlæst i | Hvor længe modellen bliver i hukommelsen efter sidste brug, i timer og minutter. **For altid** holder den indlæst, indtil programmet lukkes |
| Tidsgrænse | Hvor længe der ventes på modellen, før der gives op |
| Systembakke | Minimér til systembakken (standard) eller til proceslinjen |
| Opdateringer | **Opdateringer fra systembakken**: korte beskeder over systembakken, som forsvinder efter cirka et sekund (slået fra som standard) |
| Start med Windows | Starter programmet i systembakken, når du logger på, uden at indlæse modellen, så der ikke bruges hukommelse, før du retter noget. Kun i det installerede program |
| Vinduets størrelse | **Nulstil vinduets størrelse** går tilbage til den automatiske størrelse fra næste start |
| Processor | **Prøv GPU** (standard) lægger så meget af modellen på grafikkortet (NVIDIA, AMD eller Intel), som der er plads til, også for modeller, hvis egne indstillinger siger noget andet; **CPU** bruger kun processoren. Prøv CPU, hvis programmet går ned eller opfører sig mærkeligt på en pc. Modelpanelet på fanen Status viser, om den indlæste model kører på GPU'en, CPU'en eller begge, og advarer, når Prøv GPU endte på CPU'en. Det skyldes som regel, at modellen ikke kan være i grafikkortets hukommelse |
| Lyde | Korte lyde, når programmet er klar, og når en rettelse starter, bliver færdig, ikke finder noget at rette eller mislykkes. Hver har sin egen lyd |
| Lydstyrke | Lydstyrken for alle lyde samlet, fra 0 (lydløs) til 100 (højest) |

### Avancerede indstillinger (fanen Modeller)

Nederst på fanen Modeller åbner **Brug avancerede indstillinger** for indstillinger til test, fx for
at få din egen model til at fungere bedre. Når den ikke er slået til, er afsnittet foldet sammen, og
Text Corrector bruger sin egen systemprompt og sit eget eksempel til dit sprog og tjekker hvert svar.

- **Systemprompt**: teksten, modellen læser før din tekst. Feltet viser prompten for det valgte
  sprog, og hvert sprog har sin egen version: skift sproget, og feltet viser det sprogs prompt. Din
  tekst erstatter Text Correctors prompt helt. **Indsæt Text Correctors standard-systemprompt for det
  valgte sprog** (eller at tømme feltet) går tilbage til standarden. Standarden er på engelsk med en
  oplysning om dit sprog; dansk har sin egen danske prompt.
- **Eksempler**: før din tekst får modellen vist ét eksempel på en rettelse (en tekst med fejl og
  dens rettelse), hvilket hjælper små modeller med at svare i den rigtige form. Når det er slået til,
  vises eksemplet for det valgte sprog i et **Før**- og et **Efter**-felt (højst 300 tegn hver), som
  du kan ændre; hvert sprog har sit eget, og **Gendan standardeksempler** henter Text Correctors
  tilbage. Når det er slået fra, sendes der intet eksempel.
- **Tillad alle svar fra modellen**: kun til test. Alt, hvad modellen svarer, bliver indsat, også svar,
  som tjekkene normalt ville afvise (udeladte ord, ekstra tekst, ændrede linjeskift eller svar, der
  ikke er i den ønskede JSON-form). Slået fra som standard.

Indstillingen for temperatur er skjult, fordi et rettelsesværktøj bør give den ene mest sandsynlige
rettelse (temperatur 0). Den kan hentes frem igen ved at sætte `TEMPERATURE_ADJUST = True` øverst i
`text_corrector/settings.py`.

## Den færdige zip-fil

Det er versionen til andre mennesker. Alt, hvad den har brug for, ligger i dens egen mappe.

1. Pak zip-filen ud i en mappe, du kan skrive i, fx `C:\Users\DitNavn\TextCorrector`. Kør ikke
   programmet inde fra zip-filen.
2. Dobbeltklik på `TextCorrector.exe`. Windows advarer måske om en ukendt udgiver første gang ("Flere
   oplysninger" og derefter "Kør alligevel"), fordi programmet ikke er signeret.
3. Første gang er der ingen model endnu, så programmet åbner på fanen Modeller. Tryk på Hent ud for
   en af dem (nogle få gigabyte, én gang). Fremskridtet vises, og modellen tages i brug, så snart den
   er klar. Senere kan du hente andre der og skifte mellem dem.
4. Vil du fjerne det hele, så luk programmet (ikonet i systembakken, Afslut) og slet mappen, eller
   dobbeltklik på `uninstall.bat` i den. Der er ikke ændret andet på pc'en.

### Den indbyggede motor

Zip-filen indeholder sin egen kopi af Ollamas selvstændige tjeneste, omdøbt til
`Text-Corrector-Engine.exe`. Programmet starter den i baggrunden, når det åbner, og stopper den,
når det lukker. `Text-Corrector-Engine.exe` kommer ikke i konflikt med en Ollama-tjeneste, som du
måske selv har installeret: den bruger en ledig lokal port og gemmer sine modeller, indstillinger og
midlertidige filer i programmets mappe (`models` og `data`). Dens log er `data\logs\ollama.log`.

Grafikkort: NVIDIA-kort bruges via CUDA, og AMD- og Intel-kort (også dem, der er bygget ind i
processoren) via Vulkan, med de almindelige grafikdrivere. Når der ikke kan bruges et grafikkort,
klarer processoren arbejdet, hvilket er langsommere. Modelpanelet på fanen Status viser, hvor meget af
modellen der ligger på grafikkortet, og hvor meget der ligger i systemets RAM.

Vil du bruge din egen Ollama i stedet for den indbyggede, så slet eller omdøb mappen `ollama` ved
siden af programmet, og angiv din Ollama-adresse i indstillingsfilen.

## Fejlfinding

- **"Modellens svar udelod N ord"**: modellen droppede en del af teksten, hvilket en korrekturlæser
  ikke bør gøre, så svaret blev ikke brugt. Programmet prøvede så teksten sætning for sætning. Hvis
  det bliver ved med at ske med én model, så prøv en anden på fanen Modeller: små modeller gør det
  oftere.
- **"Modellen svarede ikke i det forventede format"**: modellen svarede med noget andet end det
  JSON-svar, programmet beder om. Prøv igen, eller vælg en anden model på fanen Modeller. Modeller,
  der kan "tænke" (som Gemma 4), bliver bedt om at lade være, og programmet accepterer også et svar
  pakket ind i en kodeblok.
- **"Den indbyggede motor svarer ikke"**: luk Text Corrector, og start programmet igen. Hvis det
  bliver ved med at ske, så tryk på **Kopiér diagnostik** på fanen Status, og se
  `data\logs\ollama.log`.
- **"Den indbyggede motor kunne ikke starte"**: læs `data\logs\ollama.log` i programmets mappe.
  Antivirusprogrammer blokerer nogle gange motoren (`ollama\Text-Corrector-Engine.exe`); tillad den,
  eller tilføj programmets mappe som en undtagelse. Hvis loggen nævner grafikkortet eller driveren, så
  sæt "Processor" til "CPU" under Indstillinger.
- **En model kører på CPU'en, selvom Prøv GPU er valgt**: modellen er måske for stor til
  grafikkortets hukommelse; en mindre model (eller en med en mindre downloadstørrelse) kan være der.
  Nogle modeller i Ollama-biblioteket har også deres egen indstilling, der holder dem væk fra
  grafikkortet; Text Corrector tilsidesætter den, når Prøv GPU er valgt.
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

## Kendte begrænsninger

- Kun tekst i udklipsholderen bliver gendannet bagefter, når du bruger ret og indsæt (Ctrl+Alt+Shift+2). Et
  billede eller en fil, du havde kopieret, går tabt. Ret til udklipsholder (Ctrl+Alt+Shift+1) overskriver
  altid udklipsholderen.
- Andre sprog end engelsk er eksperimentelle.
- Programmet er ikke kodesigneret, så Windows kan vise en advarsel første gang. Nogle
  antivirusprogrammer markerer også programmer, der er lavet med PyInstaller.

## Kildekode

Kildekoden til hver version ligger ved dens udgivelse som `TextCorrector-<version>-source.zip`.
[SOURCE_README.md](SOURCE_README.md) (på engelsk) forklarer, hvordan du kører den, og hvordan du
selv bygger den færdige zip-fil.

## Tak til

Projektet er inspireret af to tidligere værktøjer, og tak går til deres forfattere:

- [ai-typing-assistant](https://github.com/patrickloeber/ai-typing-assistant) af Patrick Loeber
  (MIT-licens)
- [Typing-Assist](https://github.com/x404xx/Typing-Assist) af x404xx

Denne version er siden blevet skrevet om med sin egen kode og udvidet med indstillinger, tjek af
teksten, lyde og et grafisk vindue.

## Licens

Kildekoden er udgivet under [MIT-licensen](LICENSE). Den indbyggede motor er
[Ollama](https://github.com/ollama/ollama) (MIT), og de sprogmodeller, du henter, er selvstændige
værker med deres egne licenser (se hver models side). De biblioteker, programmet bruger, står i
`packaging\THIRD_PARTY_NOTICES.txt`.

## Feedback

Fejlrapporter og idéer er velkomne som GitHub-issues. Når du rapporterer et problem, så tryk på
**Kopiér diagnostik** på fanen Status, og indsæt resultatet i dit issue.
