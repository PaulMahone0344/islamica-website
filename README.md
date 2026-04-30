# Werkafspraken — Claude Code (Opus / Sonnet)

Generieke README om in **elk project** te zetten. Hij doet 2 dingen:

1. **Spaart tokens** door duidelijk te maken wat goedkoop en wat duur is.
2. **Maakt afspraken duidelijk** tussen jou en Claude.

> Plaats dit bestand als `README.md` in de root van je project.

---

## 1 · Wat ik (Claude) van JOU verwacht

Om snel en goedkoop te kunnen werken:

### Geef precieze scope

| ❌ Vaag (duur) | ✅ Concreet (goedkoop) |
|---------------|------------------------|
| "Maak het mooier" | "Vervang regel 188-193 in HomeScreen.tsx door X" |
| "Verder" | "Doe nu item #18 uit todo.txt" |
| "Wat kan beter?" | "Geef 3 design-tips, geen code" |
| "Fix dit ergens" | "Fix de bug in PlayerContext.tsx waar X gebeurt" |

### Vertel me waar dingen zitten

- Geef het **bestandspad** als je 'm weet
- Geef de **functie- of regelnummer** als je 'm hebt
- Plak een **error-message letterlijk** als die er is

### Eén taak per keer

Maak iets eerst af voor je naar het volgende gaat. Anders blijft de context lang en duur.

### Gebruik `/clear` na een groot stuk werk

Als een feature klaar is en getest → `/clear` en herstart vers. Anders blijven 30+ berichten meegestuurd worden.

### Kies het juiste model

| Wat je wilt | Model |
|-------------|-------|
| Snel typewerk, styling, CRUD, kleine edits | **Sonnet 4.6** |
| Boilerplate, documentatie, repetitief werk | **Sonnet 4.6** |
| Slimme refactor, complexe bug, architectuur | **Opus 4.7** |
| Code review, kritische besluiten | **Opus 4.7** |

Vuistregel: ~80% Sonnet voor uitvoering, ~20% Opus voor de slimme stukken.

### Duidelijke "stop" zeggen

Als je tokens wilt sparen: zeg het. Voorbeelden:
- "Niks implementeren, alleen advies"
- "Stop, tokens zijn op"
- "Alleen lezen, geen edits"

Dan weet ik dat ik geen tools meer mag gebruiken.

---

## 2 · Wat JIJ van mij mag verwachten

### Wel doen

- ✅ Korte, directe antwoorden
- ✅ Eén sentence updates tijdens werk
- ✅ Type-check (`tsc`) draaien na grote wijzigingen
- ✅ Aankondigen vóór ik iets risicovols doe (delete, push, install)
- ✅ Stoppen als jij "stop" zegt
- ✅ Eerlijk zijn over wat ik niet weet of niet kan

### Niet doen

- ❌ Eigen ongevraagde features toevoegen
- ❌ Comments in code zetten zonder duidelijke reden
- ❌ Documentatie-bestanden maken zonder dat je 't vraagt
- ❌ Force-pushen of destructieve git-commando's zonder bevestiging
- ❌ Dependencies installeren zonder te zeggen
- ❌ Tests, lint of build skippen ("--no-verify")
- ❌ Net doen alsof iets werkt zonder het te testen

### Eerlijk zijn

Ik zal duidelijk zeggen:

- "Dit weet ik niet, ik moet eerst kijken"
- "Dit werkt op iPhone maar niet getest op Android"
- "Ik heb dit gewijzigd maar de UI niet gezien — test 't even"
- "Dit is een gok, geen kennis"

---

## 3 · Token-vretende valkuilen

Op volgorde van impact (top = duurste):

### Top 5 dure dingen

1. **Grote files herhaald lezen.** Een 1500-regel screen file = ~10k tokens per Read.
   → Vraag mij eerst `grep -n "X"` te doen, daarna `Read` met `offset` + `limit`.

2. **Grote inline `Edit`-blokken.** Een 250-regel modal in één Edit = veel diff-tokens.
   → Liever: nieuwe component in een nieuw bestand met `Write`.

3. **Lange conversaties zonder `/clear`.** Na 30+ berichten wordt elke nieuwe vraag duurder.
   → Klaar met een feature? `/clear`.

4. **Mijn thinking-blokken bij vage vragen.** Opus denkt veel.
   → Concrete vraag = minder thinking.

5. **"Verder" zonder context.** Ik moet dan zelf scope kiezen → extra thinking + tools.
   → "Doe X" is goedkoper dan "verder".

### Wat juist goedkoop is

- `Bash` met `grep`, `tsc`, `npm install` — kleine output
- `Edit` met kleine `old_string` (3-5 regels)
- Korte tekstantwoorden van mij

---

## 4 · Slash-commands cheatsheet

| Commando | Wat het doet |
|----------|--------------|
| `/cost` | Toon kosten + tokens van huidige sessie |
| `/status` | Accountstatus + plan-info |
| `/clear` | Wis context, start vers |
| `/compact` | Comprimeer conversatie (behoud belangrijke info) |
| `/help` | Help met Claude Code |

---

## 5 · Test-devices

- **iPhone** → Expo Go
- **Samsung** → EAS dev build
- Gebruik `Platform.OS` voor verschillen tussen platforms
- iOS-only bugs → test op iPhone; Android-only → test op Samsung

---

## 6 · Standaard-commands

```bash
# Dev server starten
npx expo start

# Dev server alleen voor iOS of Android
npx expo start --ios
npx expo start --android

# OTA update uitsturen (geen nieuwe build nodig)
eas update --branch production --message "omschrijving"

# Nieuwe build (alleen als native code is gewijzigd — kost geld)
eas build --platform all

# Website deployen naar Cloudflare Pages
wrangler pages deploy . --project-name <projectnaam>

# Type-check
npx tsc --noEmit
```

---

## TL;DR

> **Jij**: precieze scope, één taak per keer, `/clear` na grote stappen, juiste model kiezen.
> **Ik**: kort, eerlijk, niets ongevraagd, stop als jij "stop" zegt.
> **Beiden**: gebruik `grep` + `Read offset/limit` i.p.v. hele files lezen.
