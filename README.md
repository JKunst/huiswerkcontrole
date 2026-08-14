# Huiswerkcontrole

Bijhouden of leerlingen hun huiswerk gemaakt hebben. Gebouwd voor de telefoon:
tegels per klas, daarna een raster met bevroren namenkolom en bevroren kopregel.

- Tik 1x = groen (gemaakt), 2x = rood (niet gemaakt), 3x = grijs (terug naar niet gecontroleerd).
- Elke kolom is één opdracht. De controledatum wordt automatisch vastgelegd bij de
  eerste registratie in die kolom, en is achteraf aan te passen via Bewerken.
- Vier tabbladen (Periode 1 t/m 4) per klas. Binnen een periode groepeer je opdrachten
  per hoofdstuk; opdrachtnummers hoeven alleen binnen één hoofdstuk uniek te zijn, dus
  `1-80` in H1 en nogmaals `1-80` in H2 kan gewoon naast elkaar.
- Opdrachten toevoegen accepteert een reeks (`1-80`), losse nummers, of een mix
  (`1-10, 15, 20abc`). Al bestaande nummers in dat hoofdstuk worden overgeslagen.
- Staan er meerdere hoofdstukken in een periode, dan verschijnen filterchips onder de
  tabbladen: per hoofdstuk of alles tegelijk. Bij "Alles" staat het hoofdstuk klein
  onder het opdrachtnummer.
- Percentage gemaakt = groen / (groen + rood). Niet-gecontroleerde vakjes tellen niet mee,
  dus het percentage zakt niet doordat je nog niet aan iemand toegekomen bent. Per leerling
  staat het in de bevroren naamkolom, het klasgemiddelde in de balk boven het raster.
  Beide volgen het geopende tabblad en de hoofdstukfilter; staat er een hoofdstukfilter aan,
  dan toont de balk ook het percentage over de hele periode. Iemand zonder registraties
  krijgt een streepje in plaats van 0%.
- Opdrachten verwijderen: tik in Bewerken op een kolomkop voor de knop Verwijderen
  (één opdracht), of gebruik de leegmaak-knop om het geselecteerde hoofdstuk — of de
  hele periode als je op Alles staat — in één keer te wissen.
- Bestaande databases worden automatisch gemigreerd: bestaande opdrachten krijgen
  periode 1 en een leeg hoofdstuk.

## Lokaal draaien

    python -m venv venv && source venv/bin/activate
    pip install -r requirements.txt
    python app.py

Open http://localhost:5000

## Online zetten

Werkt op elke host die een Python-webservice draait (Render, Railway, Fly.io, een VPS).
Startcommando: `gunicorn app:app`

Stel deze omgevingsvariabelen in:

| Variabele    | Doel                                                        |
|--------------|-------------------------------------------------------------|
| `SECRET_KEY` | Willekeurige string voor de sessiecookie. Verplicht online.  |
| `APP_PIN`    | Pincode voor toegang. Leeg = geen login.                     |
| `DB_PATH`    | Pad naar de SQLite-database, bijv. `/data/huiswerk.db`.      |

Let op: koppel `DB_PATH` aan een persistent volume. Zonder volume wist de host
de database bij elke nieuwe deploy.

## Beheer

Knop **Bewerken** in een klas geeft toegang tot: leerlingen toevoegen of wissen,
opdrachtnummer en controledatum aanpassen, CSV-export en de klas verwijderen.
