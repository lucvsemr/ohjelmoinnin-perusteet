---
title: 'Virheiden löytäminen'
nav_order: 1
hidden: false
---

Olemme tähän mennessä harjoitelleet ohjelmointikielen perusteita, kuten muuttujia, ehtoja, silmukoita ja metodeja. Siirrytään seuraavaksi katsomaan ohjelmien ymmärrettävyyteen vaikuttavia tekijöitä ja virheiden löytämistä.

## Ohjelmoija on sokea omalle koodilleen

Ohjelmoija tulee usein sokeaksi omalle koodilleen. Tutustutaan tähän ilmiöön alla olevan videon avulla. Laske kuinka monta kertaa valkopaitaiset pelaajat syöttävät palloa toisilleen. Videolla on ohjeet englanniksi.

[![Link to video: https://www.youtube.com/watch?v=vJG698U2Mvo](https://www.youtube.com/watch?v=vJG698U2Mvo/mqdefault.jpg)](https://www.youtube.com/watch?v=vJG698U2Mvo)

Videolla tapahtuu myös jotain muuta, joka saattaa jäädä huomaamatta. Tätä ilmiötä kutsutaan havaintosokeudeksi, ja se selittyy sillä, että keskittyessämme johonkin tiettyyn tehtävään aivomme suodattavat pois tehtävän kannalta epärelevanttia tietoa. Emme kuitenkaan aina tiedä mikä tieto on itse asiassa olennaista ja mikä ei -- esimerkkinä tästä on opiskelu. Tietyn opiskelutehtävän keskittyminen johonkin tiettyyn osa-alueeseen voi johtaa siihen, että olennainen tieto suodattuu pois.

Onneksi tehtävään keskittyminen vähentää havaintosokeuden esiintymistä. Toisin sanoen harjoittelu kehittää kykyä erottaa olennainen epäolennaisesta.

Yksi tapa miten havaintosokeus ilmenee ohjelmoinnin harjoittelussa on se, että keskittyminen tiettyyn osaan ohjelmaa saattaa johtaa siihen, että huomiota ei kiinnitetä näennäisesti oikealta vaikuttaviin, mutta virheellisiin osiin. Esimerkiksi ohjelman tulostuksen oikeellisuutta tarkastaessaan ohjelmoija saattaa keskittyä tulostuslauseisiin ja erehtyä jättämään huomiotta ohjelman logiikkaan liittyviä asioita.

Samoin ohjelmoija voi keskittyä ohjelman monimutkaisimpaan kohtaan jossa on silmukka, vaikka virhe on jossain aivan muualla. Esimerkkinä tästä on alla oleva ohjelma, joka laskee käyttäjän syöttämien lukujen keskiarvon. Ohjelmassa on virhe, ja virhettä etsiessä silmukka on tyypillisesti ensimmäinen kohde. 

<Note>Muista ALT + SHIFT + F, joka muotoilee koodin automaattisesti.</Note>

```cpp

int values = 0;
int sum = 0;

while (true)
{
  Console.WriteLine("Provide a value, a negative value ends the program");
  int value = Convert.ToInt32(Console.ReadLine());
  if (value < 0)
  {
    break;
  }

  values = values + 1;
  sum = sum + value;
}

if (sum == 0)
{
  Console.WriteLine("The average of the values could not be calculated.");
}
else
{
  Console.WriteLine("Average of values: " + (1.0 * sum / value));
}
```

Kysymys: Huomaatko mikä koodissa on vialla? Vastaus on myös sivun alalaidassa. ÄLÄ HUIJAA, lue koko osa ensin!

Havaintosokeus on jotain mitä emme voi kokonaan eliminoida. Ohjelmoija voi kuitenkin vähentää sen vaikutusta, ja yksi keino on pitää taukoja. Taukojen pitäminen vaatii, että työ aloitetaan ajoissa. Koodikommentit, asioiden nimeäminen oikein ja "debuggaus"-tulosteet ovat myös esimerkkejä asioista jotka auttavat.

## Koodin kommentointi

Kommenteilla on monia tarkoituksia, ja yksi niistä on selittää koodin toimintaa itselleen virheitä etsiessä. Alla on kuvattu melko yksinkertaisen ohjelman suoritus kommenttien avulla.

```cpp
/*
Tulostaa luvut yhdestä kymmeneen.
Jokainen luku tulostetaan omalle rivilleen.
*/

// luomme muuttujan nimeltä value ja annamme sille arvon 10
int value = 10;

// Silmukkaa suoritetaan kunnes
// muuttujan value arvo on pienempi tai yhtäsuuri kuin
// nolla. Suoritus ei lopu _välittömästi_ kun muuttujalle
// annetaan arvoksi nolla, vaan vasta kun silmukan ehto
// vaan vasta kun silmukan ehto tarkistetaan seuraavan kerran.
// Tämä tapahtuu aina silmukan suorituksen jälkeen.
while (value > 0) {
    // tulostamme muuttujan arvon ja uuden rivin
    Console.WriteLine(value);
    // vähennämme muuttujan arvoa yhdellä
    value = value - 1;
}
```

Kommenteilla ei ole vaikutusta ohjelman suoritukseen, eli ohjelma toimii samalla tavalla kommenttien kanssa kuin ilman niitä.

Kommenttien tyyli yllä olevassa esimerkissä on tarkoitettu oppimistarkoituksiin, mutta se on liian yksityiskohtainen oikeaan ohjelmointiin, jossa tavoitteena on, että lähdekoodi on itsessään dokumentoivaa. Tämä tarkoittaa sitä, että ohjelman toiminnallisuus pitäisi olla ilmeistä luokkien, metodien ja muuttujien nimistä.

Esimerkki voidaan myös "kommentoida pois" kapseloimalla koodin sopivasti nimettyyn metodiin. Alla on kaksi esimerkkiä tästä -- toinen metodi on toista monikäyttöisempi. Monikäyttöisempi metodi olettaa kuitenkin, että käyttäjä tietää kumpi parametreista on suurempi ja kumpi pienempi.


```cpp
public static void PrintValuesFromTenToOne()
{
  int value = 10;
  while (value > 0)
  {
    Console.WriteLine(value);
    value = value - 1;
  }
}
```

```cpp
public static void PrintValuesFromLargestToSmallest(int start, int end)
{
  while (start >= end) {
    Console.WriteLine(start);
    start = start - 1;
  }
}
```

## Virheiden etsintä tulostus-debuggauksella (print debugging)

Yksi tarpeellinen taito ohjelmoinnissa on kyky testata ja debugata eli etsiä virheitä. Yksinkertaisin tapa etsiä virheitä on käyttää niin kutsuttua tulostus-debuggausta, joka käytännössä tarkoittaa viestien lisäämistä koodin tiettyihin kohtiin. Nämä viestit käytännössä seuraavat ohjelman suoritusta, ja voivat sisältää myös muuttujien arvoja.

Tarkastellaan jo aiemmin tuttua ohjelmaa, joka laskee käyttäjän antamien positiivisten lukujen keskiarvon.

```cpp

int values = 0;
int sum = 0;

while (true)
{
  Console.WriteLine("Provide a value, a negative value ends the program");
  int value = Convert.ToInt32(Console.ReadLine());
  if (value < 0)
  {
    break;
  }

  values = values + 1;
  sum = sum + value;
}

if (sum == 0)
{
  Console.WriteLine("The average of the values could not be calculated.");
}
else
{
  Console.WriteLine("Average of values: " + (1.0 * sum / value));
}
```

Jos koodissa olisi virhe, tulostus-debuggausta voisi käyttää ohjelman toiminnan selvittämiseen lisäämällä tulostuslauseita oikeisiin paikkoihin. Alla olevassa esimerkissä on yksi mahdollinen tapa lisätä tulostuslauseita.


```cpp

int values = 0;
int sum = 0;

while (true)
{
  Console.WriteLine("-- values-muuttuja: " + values + ", sum-muuttuja: " + sum);

  Console.WriteLine("Provide a value, a negative value ends the program");
  int value = Convert.ToInt32(Console.ReadLine());
  if (value < 0)
  {
    Console.WriteLine("-- arvo oli negatiivinen, lopetetaan silmukka");
    break;
  }

  values = values + 1;
  sum = sum + value;
}

Console.WriteLine("-- silmukka loppui");
Console.WriteLine("-- values-muuttuja: " + values + ", sum-muuttuja: " + sum);

if (sum == 0)
{
  Console.WriteLine("The average of the values could not be calculated.");
}
else
{
  Console.WriteLine("Average of values: " + (1.0 * sum / value));
}
```

Kun ohjelma suoritetaan monta kertaa sopivilla syötteillä, piilotettu virhe löytyy usein. Sopivien syötteiden keksiminen on taito sinänsä. On tärkeää testata niin sanotut kulma- ja reunatapaukset, eli tilanteet joissa ohjelman suoritus voisi olla poikkeuksellista. Esimerkkinä tästä on tilanne, jossa käyttäjä ei syötä yhtään hyväksyttävää arvoa tai syöttää pelkkiä nollia tai hyvin suuria arvoja.

VASTAUS:  
Viimeinen muuttuja koodissa on nimeltään **value**, kun sen pitäisi olla nimeltään **values**. Kutsuimme muuttujaa, joka oli määritelty silmukan sisällä, emmekä sitä jota halusimme.

