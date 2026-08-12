# Tiedostonkäsittely Pythonissa

Muuttujiin tallennettu tieto säilyy vain ohjelman suorituksen ajan, mutta usein on tarve tallentaa tietoa myös pysyvästi, jolloin se on käytössä myös ohjelman tulevilla suorituskerroilla.

Pysyvään tallentamiseen käytetään tyypillisesti tietokantoja, (käsitellään tulevilla opintojaksoilla) tai suoraan tiedostoon kirjoittamista, josta se voidaan lukea myöhemmin.

Tällaisia tietoja voivat olla esimerkiksi:

- pelin tallennukset
- käyttäjätiedot
- asetukset
- lokitiedot
- mittausdata
- ym.

Tallennettava/luettavat tiedosto voi olla pelkkää tekstiä tai jossain binääriformaatissa (kuvat, pdf, doc, jne.).

## Tekstitiedostoon tallentaminen ja lukeminen

Python tarjoaa yksinkertaiset sisäänrakennetut työkalut tiedostojen käsittelyyn. Tiedostoon kirjoittaminen tapahtuu seuraavasti:

```python
with open("save.txt", "w") as tiedosto:
    tiedosto.write("Pelaaja pääsi tasolle 2.")
```

Yllä olevassa esimerkissä `open`-funktiolla avataan tiedosto nimeltä `save.txt` kirjoitustilassa (`open`-funktion toinen parametri `"w"`). Jos tiedostoa ei ole vielä olemassa, se luodaan. `with`-lause varmistaa, että tiedosto suljetaan automaattisesti, vaikka kirjoittamisessa tapahtuisikin virhe. `write`-metodilla kirjoitetaan tekstiä tiedostoon.

`w`-parametria käytettäessä ohjelma ylikirjoittaa tiedostossa olleen aiemman sisällön. Jos tiedostoon halutaan lisätä sisältöä, voidaan käyttää `a`-parametria (_append_):

```python
with open("save.txt", "a") as tiedosto:
    tiedosto.write("Pelaaja pääsi tasolle 3.")
```

Huomaa, että toisin kuin konsoliin tulostettaessa (`print()`), `write`-metodi ei lisää rivinvaihtomerkkiä automaattisesti. Tiedoston sisältö on siis tämän jälkeen:

```txt
Pelaaja pääsi tasolle 2.Pelaaja pääsi tasolle 3.
```

Tarvittaessa rivinvaihdon voi lisätä merkkijonoon `\n`-merkillä (_newline_):

```python
with open("save.txt", "w") as tiedosto:
    tiedosto.write("Pelaaja pääsi tasolle 4.\n")
    tiedosto.write("Pelaaja pääsi tasolle 5.\n")
```

Vastaavasti saman tiedoston lukeminen tapahtuu seuraavasti:

```python
with open("save.txt", "r") as tiedosto:
    data = tiedosto.read()
    print(data)
```

`r`-parametri tarkoittaa lukutilaa. `read`-metodilla luetaan koko tiedoston sisältö ja tallennetaan se muuttujaan `data`, joka tulostetaan konsoliin.

Muita tapoja lukea tiedostoa ovat esimerkiksi `readline`-metodi, joka lukee tiedoston rivi kerrallaan, ja `readlines`-metodi, joka lukee kaikki rivit ja tallentaa ne listana.

## Tiedon serialisointi

Serialisointi tarkoittaa tiedon muuttamista tallennettavaan muotoon.

Tietokoneen muistissa oleva data ei aina ole suoraan tallennettavissa tiedostoon. Esimerkiksi Pythonin listat, sanakirjat tai muut oliot täytyy usein muuntaa tekstimuotoon ennen tallentamista. JSON (JavaScript Object Notation) on yleinen ja helppokäyttöinen formaatti, joka sopii hyvin Pythonin tietorakenteiden serialisointiin. Pythonin [json](https://docs.python.org/3/library/json.html)-kirjasto tarjoaa funktiot tietorakenteiden muuntamiseen JSON-muotoon ja takaisin. JSONia käytetään aktiivisesti ja siihen perehdytään tarkemmin seuraavalla opintojaksolla web-ohjelmoinnin yhteydessä.

```python
import json

tallennus_data = {
    "pelaaja": "Matti",
    "taso": 5,
    "varusteet": ["miekka", "kilpi", "haarniska"]
}
with open("save.json", "w") as tiedosto:
    json.dump(tallennus_data, tiedosto)
with open("save.json", "r") as tiedosto:
    data_luettu = json.load(tiedosto)
print(f"Pelaaja: {data_luettu['pelaaja']}, taso: {data_luettu['taso']}, varusteet: {data_luettu['varusteet']}")
```

Yllä olevassa esimerkissä luodaan Pythonin sanakirja `data`, joka sisältää pelaajan nimen, tason ja varusteet. `json.dump`-funktiolla kirjoitetaan tämä sanakirja JSON-muodossa tiedostoon `save.json`. Tiedoston lukeminen tapahtuu `json.load`-funktiolla, joka muuntaa JSON-tiedoston sisällön takaisin Pythonin tietorakenteeksi.

Tekstimuodon lisäksi tietoa voidaan tallentaa myös binäärimuodossa, joka on usein tehokkaampaa ja nopeampaa, mutta vaatii erityisiä työkaluja lukemiseen ja kirjoittamiseen. [Pickle](https://docs.python.org/3/library/pickle.html)-kirjasto on yksi tapa serialisoida Python-objekteja binäärimuotoon, mutta tällä kurssilla keskitymme tekstimuotoiseen serialisointiin, joka on helpommin myös ihmisen luettavissa ja ymmärrettävissä.

## Tiedoston poistaminen

Tiedoston voi poistaa Pythonin `os`-kirjaston `remove`-funktiolla:

```python
import os
if os.path.exists("save.txt"):
    os.remove("save.txt")
else:
    print("Tiedostoa ei löydy.")
```

Yllä olevassa esimerkissä `if`-lauseella varmistetaan, että tiedosto on olemassa ennen sen poistamista, jotta vältetään virhetilanne.

## Virheiden käsittely

Tiedostojen käsittelyyn voi liittyä myös muita erilaisia virhetilanteita, kuten luku- ja kirjoitusvirheet, tai oikeuksien puute. Erilaisten virheiden käsittelyyn voidaan käyttää `try-except`-rakennetta:

```python
try:
    with open("save.txt", "r") as tiedosto:
        data = tiedosto.read()
except FileNotFoundError:
    print("Tiedostoa ei löydy.")
except IOError:
    print("Tiedoston käsittelyssä tapahtui virhe.")
```

Yllä olevassa esimerkissä `try`-lohkon sisällä yritetään avata ja lukea tiedosto. Jos tiedostoa ei löydy, `FileNotFoundError`-poikkeus käsitellään ja tulostetaan viesti. Jos tapahtuu jokin muu I/O-virhe, se käsitellään `IOError`-poikkeuksella.

Virheenkäsittelyä voidaan hyödyntää myös muissa tapauksissa, joissa ohjelman suorituksen aikana tapahtuu mahdollisia virhetilanteita, vaikka koodi olisikin oikein kirjoitettu. Esimerkiksi käyttäjältä syötetty tieto, joka ei ole odotetussa muodossa, voi aiheuttaa virheen, joka voidaan käsitellä `try-except`-rakenteella:

```python
try:
    pelaajan_ika = int(input("Anna pelaajan ikä: "))
except ValueError:
    print("Virhe: syötetty arvo ei ole kokonaisluku.")
print("Ohjelman suoritus jatkuu.")
```

`try`-koodilohkossa olevaa koodia siis ajetaan niin kauan, kunnes tapahtuu virhe. Virheen tapahtuessa koodin suoritus hyppää heti oikeaan `except`-lohkoon. Jos virhettä ei tapahdu, `except`-lohko(t) sivuutetaan ja ohjelman suoritus jatkuu normaalisti sen jälkeen.

Jotta pelaajan ikä saadaan luettu onnistuneesti ennen ohjelman jatkamista, voidaan käyttää `while`-silmukkaa, joka toistuu niin kauan, kunnes ikä on saatu luettua onnistuneesti:

```python
while True:
    try:
        pelaajan_ika = int(input("Anna pelaajan ikä: "))
        break  # ikä luettu onnistuneesti, poistutaan silmukasta
    except ValueError:
        print("Virhe: syötetty arvo ei ole kokonaisluku. Yritä uudestaan.")
print(f"Pelaajan ikä on {pelaajan_ika}.")
```

Tilanteissa, joissa ohjelman suoritus voi mahdollisesti kaatua johonkin varsinaisesta koodista riippumattomaan ajonaikaiseen virheeseen, on tärkeää käyttää virheenkäsittelyä. Muuten ohjelma kaatuu ja sen suoritus loppuu kokonaan siihen.

---

<!-- add mermaid support for gh pages -->
<script type="module">
    Array.from(document.getElementsByClassName("language-mermaid")).forEach(element => {
      element.classList.add("mermaid");
    });
    import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs';
    mermaid.initialize({ startOnLoad: true });
</script>
