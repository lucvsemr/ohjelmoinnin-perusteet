---
title: "Tiedostot ja tiedon lukeminen"
nav_order: 3
hidden: false
---

Huomattava osuus ohjelmistoista käsittelee tavalla tai toisella dataa. Musiikkia soittava ohjelmisto käsittelee musiikkitiedostoja ja kuvankäsittelyohjelmisto kuvatiedostoja. Internetissä ja mobiililaitteilla toimivat sovellukset, kuten Facebook, WhatsApp ja Telegram, käsittelevät käyttäjätietoja, jotka tallennetaan tiedostopohjaisiin tietokantoihin. Näitä kaikkia yhdistää se, että ne lukevat ja käsittelevät dataa tavalla tai toisella. Lisäksi käsiteltävä data tallennetaan lopulta johonkin muotoon yhteen tai useampaan tiedostoon.

## Näppäimistöltä lukeminen

Olemme käyttäneet **Console.ReadLine** -komentoa kurssin alusta alkaen käyttäjän syötteiden lukemiseen. Lukeminen on tapahtunut while-true -silmukassa, jossa lukeminen loppuu tiettyyn syötteeseen.

```cpp
while (true) {
    string line = Console.ReadLine();

    if (line == "end") {
        break;
    }

    // lisää luetun rivin listaan myöhempää
    // käsittelyä varten tai käsittele rivi heti

}
```

Tekstipohjaisissa käyttöliittymissä käyttäjän syöte ohjataan syötevirtaan rivi kerrallaan, jolloin tiedot käsitellään aina kun käyttäjä syöttää uuden rivin.

Käyttäjän syöte luetaan merkkijonona. Jos haluaisimme käsitellä syötteen esimerkiksi kokonaislukuina, pitäisi se muuttaa toiseen muotoon. Alla on esimerkkiohjelma, joka lukee käyttäjältä syötettä niin kauan kunnes käyttäjä syöttää "end". Niin kauan kun syöte ei ole "end", käsitellään syöte kokonaislukuna -- tässä tapauksessa luku vain tulostetaan.

```cpp
while (true) {
    string row = Console.ReadLine();

    if (row == "end") {
        break;
    }

    int number = Convert.ToInt32(row);
    Console.WriteLine(row);
}
```

## Tiedostot ja tiedostojärjestelmä

**Tiedostot** (englanniksi **files**) ovat datakokoelmia jotka asuvat tietokoneen sisällä. Nämä tiedostot sisältävät muun muassa tekstiä, kuvia, musiikkia tai näiden yhdistelmiä. Tiedostomuoto määrittää tiedoston sisällön sekä ohjelman, joka osaa lukea tiedoston. Esimerkiksi PDF-tiedostoja luetaan PDF-tiedostoille sopivalla ohjelmalla ja musiikkitiedostoja luetaan musiikkitiedostoille sopivalla ohjelmalla. Nämä ohjelmat ovat ihmisten -- eli ohjelmoijien -- tekemiä, ja he määrittelevät tiedostomuodon osana työtään.

Tietokoneilla on useita erilaisia ohjelmia tiedostojen selaamiseen. Nämä ohjelmat ovat käyttöjärjestelmäkohtaisia. Kaikki tiedostojen selaamiseen käytettävät ohjelmat käyttävät tietokoneen **tiedostojärjestelmää** (englanniksi **filesystem**) jollain tavalla.

Meidän kehitysympäristömme tarjoaa mahdollisuuden selata projektin tiedostoja. Visual Studio Codessa koko projekti ja kaikki siihen liittyvät tiedostot näkyvät listassa näytön vasemmalla puolella.

Tiedostot sijaitsevat tietokoneen **kovalevyllä** (englanniksi **hard drive**). Kovalevy on suuri kokoelma ykkösiä ja nollia, eli bittejä. Tiedot koostuvat näistä biteistä, esimerkiksi yksi int-tyyppinen muuttuja vie 32 bittiä (eli 32 ykköstä tai nollaa). Nykyaikaiset teratavun kokoiset kovalevyt sisältävät noin 8 biljoonaa bittiä (kirjoitettuna 8 000 000 000 000). Tällä mittakaavalla yksi kokonaisluku on hyvin pieni.

Tiedostot voivat sijaita kovalevyllä missä tahansa. Tiedostojärjestelmän tehtävä on pitää kirjaa tiedostojen sijainnista kovalevyllä sekä tarjota mahdollisuus luoda uusia tiedostoja ja muokata niitä. Tiedostojärjestelmän päätehtävä on abstrahoida kovalevyn todellista rakennetta; tiedoston käyttäjän tai ohjelman ei tarvitse välittää siitä, miten tai missä tiedosto on todellisuudessa tallennettu.

## Tiedostosta lukeminen

Tiedoston lukeminen tapahtuu **File**-luokan avulla, joka löytyy **System.IO**-nimisestä nimiavaruudesta. Keskitymme tässä tekstitiedostoihin, eli tiedostoihin jotka sisältävät merkkijonoja.

Esimerkeissämme (ainakin toistaiseksi) oletamme, että meillä on tiedostot **text.txt** ja **records.csv** samassa kansiossa kuin **Program.cs**. Tiedosto text.txt sisältää seuraavaa:


```console
This is a line
This is second line
This is 3rd
This includes a double, 3.25
This has "quotes"
```

Ja records.csv sisältää seuraavaa:

```console
sebastian,22
matt,21
rebecca,23
```

On monia tapoja lukea tiedosto. Tässä (ensimmäiset) kaksi niistä:


```cpp

using System.IO;

static void Main(string[] args)
{
  // Esimerkki #1
  // Lue tiedosto yhtenä merkkijonona.
  string text = File.ReadAllText("text.txt");

  // Näytä tiedoston sisältö konsolissa. Muuttuja text on merkkijono.
  Console.WriteLine("This was done with ReadAllText.");
  Console.WriteLine(text);

  // Tyhjä rivi helpomman lukemisen vuoksi
  Console.WriteLine();

  // Esimerkki #2
  // Lue tiedosto rivi kerrallaan ja tallenna jokainen rivi taulukkoon.
  // Taulukon jokainen alkio on yksi tiedoston rivi.
  Console.WriteLine("This was done with ReadAllLines.");
  string[] lines = File.ReadAllLines("text.txt");

  // Näytä tiedoston sisältö konsolissa käyttäen foreach-silmukkaa.
  foreach (string line in lines)
  {
    Console.WriteLine(line);
  }
}
```

Ohjelma tulostaa

```console
This was done with ReadAllText.
This is a line
This is second line
This is 3rd
This includes a double, 3.25
This has "quotes"

This was done with ReadAllLines.
This is a line
This is second line
This is 3rd
This includes a double, 3.25
This has "quotes"
```

Katsotaan molempia vähän tarkemmin.


### File.ReadAllText()

Ensimmäinen esimerkki on melko itsestäänselvä. Määrittelemme muuttujan **string text** ja käytämme metodia **File.ReadAllText()** (karkeasti suomennettuna **lue kaikki teksti tiedostosta**) lukemaan tekstitiedosto ja tallentamaan sen muuttujaan. Tämä tallentaa tekstin tiedostosta muuttujaan **sellaisena kuin se on** tiedostossa, sisältäen kaikki rivinvaihdot. Kuten näet, kun tulostamme muuttujan, se tulostaa jokaisen rivin erikseen, kuten pitääkin.

### File.ReadAllLines()

Toinen esimerkki on melko samanlainen kuin ensimmäinen. Sen sijaan, että tallentaisimme tiedoston sisällön yhtenä merkkijonona, tallennamme sen taulukkoon komennolla **File.ReadAllLines()** (karkeasti suomennettuna **lue kaikki rivit tiedostosta**). Nyt taulukon alkiot ovat tekstin rivejä.

Mikä on siis ero, miksi tarvitsemme kaksi tapaa? Kun haluamme päästä käsiksi jokaiseen yksittäiseen tekstin riviin, käyttäisimme todennäköisesti jälkimmäistä. Jos kaikki teksti on tallennettu yhteen muuttujaan, sieltä tietyn osan löytäminen olisi vaikeampaa. Toisaalta, jos tarvitsemme tiedon yhtenä kokonaisuutena, käyttäisimme ensimmäistä.

On olemassa muitakin tapoja lukea tiedostoja, kuten datavirrat (englanniksi **streams**). Niistä lisää myöhemmin.

## Tiedon lukeminen tietyssä formaatissa tiedostosta

Maailma on täynnä dataa joka liittyy toisiin dataan -- nämä muodostavat kokoelmia. Esimerkiksi henkilötiedot sisältävät nimen, syntymäajan, puhelinnumeron. Osoitetiedot taas sisältävät maan, kaupungin, katuosoitteen, postinumeron ja niin edelleen.

Dataa tallennetaan usein tiedostoihin tietyssä formaatissa. Yksi tällainen formaatti on meille jo tuttu, eli pilkuilla erotetut arvot (englanniksi **comma-separated values**, CSV). Tämä tarkoittaa, että tiedostossa oleva data on eroteltu pilkuilla.

```cpp
while (true)
{
  Console.WriteLine("Enter name and age separated by a comma:");
  string input = Console.ReadLine();
  if (input == "")
  {
    break;
  }
  string[] pieces = input.Split(",");
  Console.WriteLine("Name: " + pieces[0] + ", age: " + pieces[1]);
}
```

Ohjelma toimii seuraavasti:

```console
Enter name and age separated by a comma:
sebastian,22
Name: sebastian, age: 22
Enter name and age separated by a comma:
matt,21
Name: matt, age: 21
Enter name and age separated by a comma:
```

Saman datan lukeminen tiedostosta nimeltä **records.csv** näyttäisi tältä:

```cpp
string[] lines = File.ReadAllLines("records.csv");
foreach (string line in lines)
{
  string[] pieces = line.Split(",");
  Console.WriteLine("Name: " + pieces[0] + ", age: " + pieces[1]);
}
```

Tämä tulostaa

```console
Name: sebastian, age: 22
Name: matt, age: 21
Name: rebecca, age: 23
```

Kuten näkyy, käytämme nyt metodia **ReadAllLines**, koska haluamme päästä käsiksi jokaiseen rivin erikseen.
 
Olisimme voineet käyttää myös **ReadAllText**, mutta olisimme joutuneet ensin **pilkkomaan merkkijono taulukoksi** päästäksemme käsiksi kaikkiin riveihin... Ja kuten näet, tällä tavalla taulukko on jo olemassa, mikä säästää ylimääräiseltä vaiheelta.

## Olioiden lukeminen tiedostosta

Olioiden luominen tiedostosta on suoraviivaista. Oletetaan, että meillä on luokka nimeltä **Person** ja sama data kuin aiemmin.

Olion tietojen lukeminen tiedostosta onnistuu seuraavasti:


```cpp
static void Main(string[] args)
{
  List<Person> people = new List<Person>();

  string[] lines = File.ReadAllLines("records.csv");
  foreach (string line in lines)
  {
    string[] pieces = line.Split(",");
    string name = pieces[0];
    int age = Convert.ToInt32(pieces[1]);

    people.Add(new Person(name, age));
  }
  Console.WriteLine("Total amount read: " + people.Count);
}
```

```console
Total amount read: 3
```

# Tehtävät

<Exercise title={'019 Reading strings'}>

Kertauksena, yksinkertainen ohjelma syötteen lukemiseen.

Kirjoita ohjelma joka lukee käyttäjältä merkkijonoja kunnes käyttäjä syöttää merkkijonon "end". Kun käyttäjä syöttää "end", ohjelman tulee tulostaa kuinka monta merkkijonoa syötteessä oli. Merkkijono "end" ei kuulu merkkijonojen lukumäärään. Alla on muutamia esimerkkejä ohjelman toiminnasta.


```console
> I 
> have
> a
> feeling
> that
> I
> have
> written
> this
> wrong
> before
> end 
11
```

```console
> end 
0
```

</Exercise>

<Exercise title={'020 Reading integers'}>

Kirjoita ohjelma joka lukee käyttäjältä merkkijonoja kunnes käyttäjä kirjoittaa "end". Niin kauan kun syöte ei ole "end", ohjelman pitäisi käsitellä syöte kokonaislukuna ja tulostaa annetun numeron kuutio (eli numero \* numero \* numero). Alla pari esimerkkiä ohjelman toiminnasta.

```console
> 3 
27 
> -1 
-1 
> 11 
1331 
> end
```

```console
> end
```

Muista muuttaa syöte kokonaisluvuksi ennen kuin käsittelet sitä.

</Exercise>

<Exercise title={'021 Reading file'}>

Kirjoita ohjelma joka tulostaa tiedoston "data.txt" sisällön siten, että jokainen tiedoston rivi tulostetaan omalle rivilleen.


Jos tiedoston sisältö on seuraava:

In a world   
Where code is built   

Tulosteen tulisi olla seuraava:

```console
In a world
Where code is built
```

<Note>
Voit olettaa että tiedosto on samassa kansiossa kuin Program.cs
</Note>

</Exercise>

<Exercise title={'022 File names'}>

Kirjoita ohjelma joka kysyy käyttäjältä merkkijonoa, ja tulostaa tiedoston jonka nimi on sama kuin käyttäjän syöte. Voit olettaa että käyttäjä syöttää tiedoston nimen joka löytyy. Sinun ei tarvitse huolehtia virheistä, eli tiedoston nimi on aina oikein.

Tehtäväpohjassa on tiedostot "data.txt" ja "song.txt", joita voit käyttää ohjelman testaamiseen. Ohjelman tulostus näyttää seuraavalta kun käyttäjä syöttää merkkijonon "song.txt". Tulostus tulee tiedostosta "song.txt". Ohjelman tulee toimia myös muilla tiedostonimillä, olettaen että tiedosto löytyy.


```console
Which file should have its contents printed? 
> song.txt 

No option for duality 
The old is where we come 
Clockspeed is fast, but we'll survive 
The new will overcome 
We are challengers, not followers 
We take the ball to build 
Easy safe services 
Are here to stay

Value for society 
Value for life 
For you and me 
Tieto is here allright!
```

<Note>
Voit olettaa että tiedosto on samassa kansiossa kuin Program.cs
</Note>

</Exercise>

<Exercise title={'023 Guestlist text file'}>

Tehtäväpohjassa on valmiina toiminallisuus vieraslistasovellukselle. Se tarkistaa onko käyttäjän syöttämä nimi vieraslistalla.

Ohjelmasta kuitenkin puuttuu toiminnallisuus jolla vieraslista luetaan tiedostosta. Muokkaa ohjelmaa siten että nimet luetaan tiedostosta.

    
<Note>
Tehtävä olettaa että sinulla on merkkijono nimeltä "names" johon olet tallentanut tiedoston!
</Note>    
    
Esimerkki ohjelman toiminnasta:    

```console
Name of the file: 
> guestlist.txt

Enter names, an empty line quits. 
> Chuck Norris 
The name is not on the list. 
> Jack Baluer 
The name is not on the list. 
> Jack Bauer 
The name is on the list. 
> Jack Bower 
The name is on the list.
>
Thank you!
```

<Note>
Tehtäväpohjassa on kaksi tiedostoa, "names.txt" ja "other-names.txt", joissa on seuraava sisältö. Älä muuta tiedostojen sisältöä!
</Note>

names.txt:

ada  
arto  
leena  
test  
heikki  
   
other-names.txt:
  
leo   
jarmo   
alicia  
mike  
potato  

<Note>
Voit olettaa että tiedosto on samassa kansiossa kuin Program.cs
</Note>

</Exercise>
