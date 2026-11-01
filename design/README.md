# Momentum – ny design

Två teman med samma layout:

- **Terrakotta** – ljust läge (standard)
- **Natt** – mörkt läge (följer systemet eller väljs i Inställningar → Tema)

Mockups per sida finns i `terrakotta/` och `natt/` (`hem`, `handel`, `modell`, `bolag`, `bolagssida`, `marknad`, `radgivare`, `notiser`, `installningar`).
Filerna är Design Component-HTML: markup och stilar går att läsa direkt, interaktionen ligger i `<script type="text/x-dc">` längst ner.
Alla siffror är demodata från `demo-api/`.

## Navigation

Bottenmeny med fem flikar: **Hem · Modell · Bolag · Marknad · Rådgivare**.
Nås från dessa: **Handel** (från "Följ modellen"), **Bolagssida** (från bolagsrader), **Notiser** och **Inställningar** (ikoner uppe till höger på Hem).
Historik är en flik inne i Modell (Översikt · Historik · Simulera). Veckobrevet ligger under Rådgivaren.

## Färgtokens

| Token | Terrakotta | Natt | Används till |
|---|---|---|---|
| `bg` | `#fbf6f1` | `#121014` | Sidbakgrund, inputfält |
| `surface` | `#ffffff` | `#1c191e` | Kort |
| `soft` | `#f3e8e1` | `#26222a` | Spår för valknappar, små rutor i kort |
| `border` | `#e9dcd3` | `#2c272f` | Kortkant |
| `divider` | `#f0e6df` | `#2c272f` | Linjer mellan rader |
| `text` | `#2e1f1a` | `#f2ece8` | Brödtext, rubriker, länkar |
| `muted` | `#6f6560` | `#a79ea3` | Hjälptext, etiketter |
| `subtle` | `#9a8f89` | `#6e6570` | Jämförelselinjer i grafer |
| `primary` | `#b0573d` + vit text | `#f08a6c` + text `#121014` | Knappar, reglage på, aktiv flik, notisbricka, logga, "Du"-linjen |
| `up` | `#4a705f` (fylld, vit text) | `#5fd09a` (fylld, mörk text) | Köp, plus, gröna staplar |
| `up-text` | `#4a705f` | `#5fd09a` | Positiva siffror |
| `up-soft` | `#e6efe9` | `#1d3226` | Ljus bakgrund för positiv status |
| `down` | `#8a3128` (fylld, vit text) | `#ff8a7a` (fylld, mörk text) | Sälj, minus, röda staplar |
| `down-text` | `#8a3128` | `#ff8a7a` | Negativa siffror |
| `down-soft` | `#f6e0dc` | `#3a2226` | Ljus bakgrund för negativ status |
| `warn` | `#8a6420` (fylld) / `#7d5a1e` (text) | `#f0c36c` | MINSKA, rapport, varning |
| `warn-soft` | `#f6ecd9` | `#3a3020` | |

**Skalor**

- Rutkarta "Dina innehav" (vit/ljus text): upp `#547866 → #4a705f → #3a5e4e` (Natt `#2a3d30 → #2f5a3e → #2f6a45`), ned `#8a3128` (Natt `#5a2a2a`, text `#ffb3a8`). Mörkare = större rörelse.
- Börsrutor på Marknad: upp `#4a705f`; ned 0–1 % `#a8453a`, 1–2 % `#8a3128`, >2 % `#6b2620` (Natt `#25402f`; `#3a2a2c`, `#4f2b2b`, `#6a2c2a`).
- VIX-skala: lugnt `#7d9b89`, nervöst `#c9a86a`, panik `#8a3128` (Natt `#2a4a38`, `#4a4026`, `#5a2a2a`).
- Kategorifärger (modellens bolagsstapel, topp 6): `#8c6f5a #5f7f99 #c9a253 #7d6a9a #4f8a9a #a87a95`, övriga = `subtle`, kassa = `border`.

**Färgregler**

- Grönt betyder bara upp/köp, rött bara ned/sälj, gult bara varning.
- `primary` betyder "app/åtgärd", aldrig en signal.
- All text på fyllda ytor ska klara 4,5:1 i kontrast (kontrollerat för alla par ovan).

## Typografi

- Rubriker och stora siffror: **Space Grotesk 600**. Sidrubrik 28 px, sektionsrubrik 17–18 px, stora tal 44–52 px.
- Brödtext och kontroller: **Inter** 400–700, bas 15 px, hjälptext 12–13 px.
- Alla siffror: `font-variant-numeric: tabular-nums`.
- Smalt hårt mellanslag (U+202F) före `%` och `kr` så att tal aldrig bryts.

## Mått

- Sidmarginal `14px 16px`, avstånd mellan sektioner 16 px.
- Kort: radie 24 px, padding 18 px, 1 px kant + mjuk skugga. Små nyckeltalsrutor: radie 18 px, ingen skugga.
- Alla valknappar och kontroller minst **44 px** höga.

## Komponenter

- **Valknapp (segment/filter/flik):** spår `soft`, radie 999 px, padding 3 px. Vald = `surface` (Natt `text`-färgad) med skugga, ej vald = `muted` text. Samma utseende överallt (perioder, kr/%, filter, flikar, tema).
- **Etiketter (SÄLJ, KÖP, NY, MINSKA, BEVAKA):** fyllda, versaler 11 px fetstil, radie 8 px, färg enligt färgreglerna.
- **M/R-ikon:** rund 24 px. **M** = i modellen (bakgrund `border`, text `primary`), **R** = rankad men inte i modellen (bakgrund `soft`, text `muted`).
- **Bolagskort (Bolag):** kvadratiskt, `#rang` + M/R uppe, namn, tre upp/ned-staplar (1, 3, 12 mån, gemensam skala, nollinje i `border`), kurs + 1 mån-förändring nederst. Tryck på en stapel visar den periodens % i stället.
- **Upp/ned-staplar:** gemensam skala och nollinje, uppåt = `up`, nedåt = `down`. Används även för avkastning per år.
- **Graflegend:** linjeprov + namn (ingen text som "gul streckad").

## Ord

- "i modellen" / "du äger" – blanda aldrig ihop modellens och användarens innehav.
- "månadsgenomgång" (inte "panel"), "förvaltarens portfölj" (inte "skugga"), "långsiktig trend (200 dagar)" (inte "200 d-snitt"), "Rang 2 av 120".

## Per sida (kort)

- **Hem:** totalvärde, Utveckling (Du/Modellen/All World, period + kr/%), "Följ modellen"-kort → Handel, Dina innehav som rutkarta (filter alla/vinnare/förlorare), Rådgivaren som åtgärdsrader, nyheter.
- **Handel:** en affär i taget med förlopp, "Öppna i Montrose" + "Klar – nästa", översikt, behåll/för små, månadsinsättning.
- **Modell:** flikar Översikt (100 kr → 638 kr, graf mot index, nyckeltal, "Bolag enligt modellen" med stapel, topplista med M/R, senaste affärer) · Historik (år som upp/ned-staplar, innehav en viss dag) · Simulera.
- **Bolag:** sök, filter Topp/Dina/Modell/Förvaltare/Alla, bolagskort i två kolumner.
- **Bolagssida:** pris, Rang av 120 / modellvikt / du äger, kursgraf med legend, flikar Förvaltaren · Rapporter · Ägare · Kursmål.
- **Marknad:** VIX-skala med förvaltarens syn, börsrutor, makro, räntekurva, rubriker med filter, ETF-flöde.
- **Rådgivaren:** status, viktigast nu, flikar Brev · Beslut · Portfölj · Facit.
- **Notiser:** tidslinje, olästa har åtgärdsknapp + "Markera läst".
- **Inställningar:** Montrose-koppling, följ modellen-värden, notisval, tema (Ljust/Mörkt/Auto).

## Kortlayout (A3) – Hem och Modell

Mappen `terrakotta/kort/` innehåller nästa steg för Hem och Modell, inspirerat av hur Avanza bygger sidor: startsidan består av korta, klickbara kort och detaljerna ligger på egna sidor. Det sparar scroll. Övriga sidor länkar till `terrakotta/`.

**Kortmönstret:** vitt kort (`surface`, radie 22 px, padding 16 px), rubrikrad i `muted` med pil till höger, en stor siffra och högst tre rader. Hela kortet är en länk. Överst på Hem och Modell finns en svepbar rad med kort (scroll-snap, 300 px breda).

| Sida | Fil | Innehåll |
|---|---|---|
| Hem | `kort/hem.html` | Svepkort: Utveckling 1 vecka, Totalt värde, Mot modellen · Sparmål · Följ modellen · Dina innehav · Rådgivaren · Börsen i dag · Nyheter |
| Värdeutveckling | `kort/vardeutveckling.html` | Period (1 v, 1 mån, 3 mån), total i kr, bäst/sämst, grupper Aktier · Fonder · Sålda under perioden, Mer |
| Min utveckling | `kort/min-utveckling.html` | %/kr, Jämför (Modellen, OMXS30, All World), period 1 v–Alla, stor graf med y-skala och datum |
| Dina innehav | `kort/innehav.html` | Rutkarta, filter Alla/Vinnare/Förlorare, lista med vikt, antal, värde, resultat, stopplarm |
| Modell | `kort/modell.html` | Svepkort: 100 kr → 638 kr, Avkastning per år · Månadsgenomgång · Bolag enligt modellen · Topplistan · Senaste affärer · Simulera/Historik · Om modellen |
| Bolag enligt modellen | `kort/modell-bolag.html` | Stapel, aktier/kassa/antal, alla 15 med vikt och rang, länk "Jämför med dina innehav" |

**Beräkningar**

- Värdeutveckling per innehav = värde vid periodens slut − värde vid start − nettoköp under perioden. Sålda bolag ingår under "Sålda under perioden". Summan ska stämma med kontots förändring exklusive insättningar (skillnad = courtage).
- Min utveckling i % = tidsviktad avkastning (TWR) från periodens start. I kr = avkastning × värdet vid start.
- Sparmål: målbelopp och antagen avkastning sätts av användaren i Inställningar. Prognosen räknar med månadsinsättningen. Mockupen använder 1 000 000 kr och 8 % per år som platshållare.

**Inte klart än:** detaljsidor för korten 638 kr, Simulera, Historik och Senaste affärer (länkar i dag till `terrakotta/modell.html`). Natt-versioner av kortsidorna saknas – de byggs med samma färgmappning som `natt/`.
