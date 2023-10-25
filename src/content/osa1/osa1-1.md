---
title: 'Tulostaminen ja lukeminen'
nav_order: 1
hidden: false
---

Ohjelman perusrunko on seuraava:

```cpp
using System;

public class Program
{
    public static void Main(string[] args)
    {
        // Koodisi tulee tähän väliin
    }
}
```

Ohjelman suoritus alkaa ensimmäisestä rivistä **public static void Main(string[] args) {** ja päättyy sulkevaan **}** sulkeeseen. Kaikki niiden välissä suoritetaan yksi rivi kerrallaan. Esimerkiksi ohjelmoijan yleisin aloitusohjelma, **Hello World!**, menisi näin:


```cpp
public class Program {
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
    }
}
```

Tässä esimerkissä ainoa suoritettava lauseke on **Console.WriteLine("Hello World!");**, joka tulostaa

```console
Hello World!
```

Keskitymme myöhemmin lausekkeisiin **public class** ja **public static void**, joten sinun ei tarvitse huolehtia niistä vielä.

Materiaalissa koko koodirakenne saattaa olla esitettyä pienempi, ellei sitä nimenomaan tarvita. Yllä oleva esimerkki voitaisiin esittää myös seuraavasti:


```cpp
Console.WriteLine("Hello World!");
```

materiaalissa. Harjoituksissa ensimmäisille viikoille annetaan perusrakenne, joten sinun ei tarvitse vielä huolehtia sen ulkoa opettelusta.

## Tulostaminen

Kuten aiemmin mainittiin, ohjelmointikielissä on sisäänrakennettuja lauseita. **Console.WriteLine** on yksi niistä. Lause on melko itsestään selvä. Se kertoo tietokoneelle **kirjoita rivi konsoliin**. Voit muuttaa **Hello World!** tilalle minkä tahansa haluamasi tekstin, kunhan itse komentoa ei muuteta, ja se toimii.

Harjoitusten vaatimukset ovat hyvin tarkkoja. Esimerkiksi, jos rivi tarvitsee päättyä huutomerkkiin, sitä ei voida jättää pois.

Ohjelmat luodaan (ja luetaan) käsky kerrallaan, missä jokaisen käskyn on oltava omalla rivillään. Seuraavassa esimerkissä kutsutaan **Console.WriteLine** kahdesti, mikä tarkoittaa, että tulostuskomento suoritetaan kahdesti.


```cpp
public class Program {
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
        Console.WriteLine("... and Pietarsaari!");
    }
}
```

Tämä tulostaisi:

```console
Hello World!
... and Pietarsaari!
```

Tarkennettuna komento **Console.WriteLine("esimerkkiteksti");** tulostaa tekstin **esimerkkiteksti** ja rivinvaihdon. Rivinvaihdon voi myös hoitaa erikoismerkillä **\n**, joka kirjoitetaan tulostettavan tekstin osana.


```cpp
public class Program {
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello World!\n... and Pietarsaari!");
    }
}
```

<Note> Tyhjää tilaa \n ympärillä ei ole. Tekstissä jokainen merkki, mukaan lukien tyhjät, on osa tekstiä. Jos laittaisit tyhjää tilaa rivinvaihdon ympärille, ensimmäinen rivi päättyisi tyhjään merkkiin ja toinen alkaisi sillä.
</Note>

Joskus teksti voi olla varsin pitkiä, ja sen lukeminen yhdestä rivistä voi olla melko vaikeaa. On mahdollista jakaa **merkkijono** (englanniksi **string**) useisiin osiin ja sitten yhdistää ne yhteen **+** -operaattorilla. Yllä oleva esimerkki voisi olla:


```cpp
public class Program {
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello World!\n" +
        "... and Pietarsaari!");
    }
}
```

Tämä tulostaa täsmälleen saman informaation kuin aiemmin. Ensimmäiseen ratkaisuun verrattuna tämä on tehokkaampi, koska tulostuskomentoa tarvitsee kutsua vain kerran. Toiseen ratkaisuun verrattuna tämä on helpompi lukea.

Tähän asti kaikki, mitä olemme tulostaneet, on päättynyt rivinvaihtoon. Jos haluaisimme tulostaa jotain ilman, että rivi vaihtuu lopussa, käyttäisimme **Console.Write("En vaihda riviä");**

Näin ollen tulostamiseen on kaksi lausetta:

- **Console.WriteLine()** tulostaa tekstin ja vaihtaa rivin
- **Console.Write()** tulostaa tekstin, mutta pitää samalla rivillä

Tulostetussa tekstissä voi olla erikoismerkkejä, kuten **\n**. On myös [**muita erikoismerkkejä (täällä)**](https://en.wikipedia.org/wiki/Escape_character), joihin saattaa olla hyödyllistä tutustua.


## Komennon parametrit

Kun haluamme tulostaa jotain, meidän on annettava se tieto **parametrina** tulostuskäskyllemme. Parametrit annetaan komennolle **()** sisällä. Esimerkiksi tulostaaksemme **Pidän ohjelmoinnista**, annamme parametrin lainausmerkeissä seuraavasti: **Console.Write("Pidän ohjelmoinnista")**.


## Puolipiste erottaa komennot

Puolipisteellä **;** erotetaan komennot toisistaan. Voisimme kirjoittaa esimerkkimme yhdelle riville, mutta ne eivät olisi kovin luettavia.


```cpp
Console.Write("Hello "); Console.Write("World!"); Console.Write("\n");
```

Tämä tulostaisi:

```console
Hello World!
```

## Koodilohkot (code blocks)

Koodi koostuu **koodilohkoista**. Koodilohko tarkoittaa koodin osaa, joka on erotettu **{}** suluilla. Usein yhdessä ohjelmassa on useita näitä, kuten voitiin jo nähdä perusrakenteestamme.

Esimerkiksi rivi **public static void Main(string[] args)**, joka määrittelee, mistä ohjelman suoritus alkaa, määrittelee lohkon siitä, mitä suoritetaan, kun ohjelma käynnistyy.


```cpp
public class Program
{  // Luokan koodilohko alkaa

  public static void Main(string[] args)
  {  // Pääohjelman koodilohko alkaa

  // Koodisi tulee tähän väliin

  } // Pääohjelman koodilohko päättyy

} // Luokan koodilohko päättyy
```

Esimerkki näyttää lohkon toisen lohkon sisällä. Lohkoja voidaan käyttää ohjelman rakenteen määrittämiseen. **class** -lohko sisältää koko ohjelman rakenteen, kun taas **main** -lohko sisältää lähdekoodin, joka suoritetaan, kun ohjelma käynnistyy.

Lohko avataan aina **{** ja suljetaan **}**. Jos jompikumpi niistä puuttuu, koodi ei käänny ja sitä ei suoriteta.


## Kommentit (comments)

Kuten olet ehkä huomannut, meillä on jo **kommentteja** koodissamme. Kommentit ovat tekstejä, jotka eivät käännä, ja siksi niitä ei suoriteta. Kommentteja voidaan käyttää esimerkiksi tietyissä koodielementeissä kommentointiin tai osan koodista **väliaikaiseen** kommentointiin vianjäljitystarkoituksiin. On olemassa kahdenlaisia kommentteja:

- **// yksirivinen kommentti**
- **/\* monirivinen kommentti \*/**

Kuten näet, yksirivinen kommentti alkaa **//**, mutta sillä ei ole lopetusmerkkiä. Monirivinen kommentti alkaa **/\*** ja päättyy **\*/**. Kaikki niiden välissä oleva tulkitaan kommentiksi kääntäjän toimesta.


## Koodin tyyli

Vaikka tietokoneella tai valitsemallamme kielellä ei ole tyylirajoituksia, on suuri etu pitää koodi siistinä ja helppolukuisena. Jokaiselle kielelle on olemassa laajalle levinneitä [**koodauskäytäntöjä (täällä)**](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions). Sisennys ja muuttujien nimeämiskäytännöt ovat hyödyllisimmät seikat, jotka on hyvä pitää mielessä.

Voimme kirjoittaa ohjelmamme esimerkiksi seuraavasti:


```cpp
public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello World!\n" +
        "... and Pietarsaari!");
    }
}
```

kuten myös:

```cpp
public class Program { public static void Main(string[] args) { Console.WriteLine("Hello World!\n" +
"... and Pietarsaari!");  }
                                        }
```

Kuten näet, jälkimmäinen ei ole yhtä helppo lukea, ja esimerkiksi eri koodilohkojen ymmärtäminen on vaikeampaa. **Pitäkää koodinne siistinä ja puhtaana!**

<Note>Omasta koodista saa helposti luettavampaa, kun käyttää koodin kirjoittamisen jälkeen näppäinyhdistelmää ALT + SHIFT + F. Tämä sisentää tekstin automaattisesti!</Note>

## Merkkijonon tulostaminen

Nyt kun ymmärrämme koodin perusrakenteen, mennään hieman syvemmälle. Tähän mennessä olemme tulostaneet yksinkertaisia tekstirivejä. Nämä tekstit ovat itse asiassa **merkkijonoliteraaleja** (englanniksi **string literals**). Näitä literaaleja voidaan tallentaa **merkkijonomuuttujiin** (englanniksi **string variables**). Kun tuomme muuttujan ohjelmaan, annamme sille yleensä **arvon** (englanniksi **value**). Arvo annetaan seuraamalla muuttujaa **=** merkillä, arvolla ja lopettamalla rivi jälleen puolipisteellä, **;**. Esimerkiksi, jos haluamme merkkijonomuuttujan nimeltään **message** arvolla **I am learning**, antaisimme sen näin:


```cpp
string message = "I am learning";
```

Muuttujan luominen antaa meille mahdollisuuden viitata muuttujaan ohjelman sisällä. Voisimme käyttää muuttujaa tulostamiseen:


```cpp
string message = "Print me";
Console.WriteLine(message);
```

Ja tällöin saisimme:

```console
Print me
```

Jos nyt käyttäisimme lainausmerkkejä muuttujan nimen ympärillä, tulostaisimme sen merkkijonoliteraalina.


```cpp
string message = "Print me";
Console.WriteLine("message");
```

```console
message
```

Kuten aiemmin yhdistimme useita tekstirivejä, myös merkkijonomuuttujia voidaan liittää yhteen osana tulostamista.


```cpp
string name = "Doctor Octopus";
Console.WriteLine("We meet again, " + name);
```

```console
We meet again, Doctor Octopus
```

Sama voidaan tehdä myös osissa:

```cpp
string name = "Doctor Octopus";
string greeting = "We meet again, ";
Console.WriteLine(greeting + name + "!");
```

```console
We meet again, Doctor Octopus!
```

Voisimme myös luoda merkkijonomuuttujan useista literaaleista:


```cpp
string counting = "One" + "\n" + "Two" + "\n" + "Three";
Console.WriteLine(counting);
```

```console
One
Two
Three
```

## Merkkijonon kysyminen käyttäjältä

Tähän mennessä olemme käyttäneet suoraan lähdekoodiin kirjoitettuja merkkijonoja. Olisi hyvä, jos voisimme kertoa ohjelmalle, mitä haluamme tulostaa joka kerta. Tämä voidaan tehdä toisella sisäänrakennetulla komennolla, **ReadLine**.


```cpp
public class Program
{
    public static void Main()
    {
    // Tulosta kysymys
    Console.Write("Give a message: ");

    // Määritä uusi string-muuttuja ja lue merkkijono käyttäjältä
    string message = Console.ReadLine();

    // Tulosta vastaus
    Console.WriteLine(message);
    }
}
```

Tämä näyttäisi joltakin tältä, syötteellä **I want to print this**:


```console
Give a message: I want to print this
I want to print this
```

Tämä on sama esimerkki, mutta yhdistämällä syöttöviestin **Give me a message:**:


```cpp
public class Program
{
   public static void Main()
   {
    // Tulosta kysymys
    Console.Write("Give a message: ");

    // Määritä uusi string-muuttuja ja lue merkkijono käyttäjältä
    string message = Console.ReadLine();

    // Tulosta vastaus
    Console.WriteLine("Your message was: " + message);
   }
}
```

Tämä näyttäisi jotakuinkin tältä syötteellä **I want to print this**:


```console
Give a message: I want to print this
Your message was: I want to print this
```

# Tehtävät

<Note>Huom! Tee harjoitukset englanniksi, katso mallia harjoitusten esimerkeistä, miten koodin tulee toimia ja mitä sen tulee tulostaa (englanniksi)</Note>

<Note>Muista ajaa ohjelmat itse konsolissa, komennolla dotnet run!</Note>

<Exercise title={'001 Hello World!'}>
Ohjelman perusrunko on annettu tehtävänannossa:

```cpp
using System;

namespace Exercise001
{
    class Program
    {
        public static void Main(string[] args)
        {
            // Koodisi tulee tänne
            
        }
    }
}
```

Rivi `\\Koodisi tulee tänne:` on kommentti. Kääntäjä ei käännä sitä, joten siitä ei tarvitse välittää. Voit poistaa sen, jos haluat.

Luo ohjelma, joka tulostaa tekstin `Hello World!` komentoriville. Ohjelma sisältää yllä kuvaillun perusrakenteen.

</Exercise>




<Exercise title={'002 Bonnie Tyler'}>

Tehdään hieman lisää! Bonnie Tyler laului joskus tunteista, joka soveltuu myös koodaukseen:
```
Once upon a time
I was falling in love
Now I'm only falling apart
```
Kirjoita ohjelma, joka tulostaa yllä olevat lyriikat käyttämällä komentoa `Console.WriteLine` kolme kertaa.

</Exercise>

<Exercise title={'003 Bonnie Tyler with line changes'}>

Hienosäädetään ohjelmaamme. Tulosta sama viesti:
  
```
Once upon a time
I was falling in love
Now I'm only falling apart
```
Tällä kertaa vain käyttämällä kerran komentoa `Console.WriteLine`.

</Exercise>

<Exercise title={'004 First variable'}>

Tehtävässä on valmiina seuraava runko:

```cpp
using System;
 
namespace Exercise004
{
    public class Program
    {
        public static void Main(string[] args)
        {
            string message = "Passport and floss!";
            Console.WriteLine(message);
        }
    }
}
```

Muokkaa sitä niin, että se tulostaa `Passport and a toothbrush!`
Älä muokkaa riviä joka alkaa `Console.WriteLine`, muokkaa vain muuttujan sisältöä!

</Exercise>

<Exercise title={'005 Ada Lovelace'}>

Tehtävässä on valmiina seuraava runko:
  
```cpp
using System;

namespace Exercise005
{
    class Program
    {
        public static void Main(string[] args)
        {
            string name = "Ada Lovelace";
            // Write your code here:           
        }
    }
}
```

Muokkaa koodia että se tulostaa `Hello Ada Lovelace!`
Älä muokkaa muuttujaa!

</Exercise>

<Exercise title={'006 Print input'}>

Luo ohjelma, joka pyytää käyttäjältä merkkijonoa. Kun käyttäjä on antanut merkkijonon (kirjoittanut tekstin ja painanut Enter), ohjelma tulostaa annetun rivin. Esimerkki tulosteesta syötteellä `Hello` (syöte on merkitty `>` selkeyden vuoksi):



```console
Give input!
> Hello
Hello
```

</Exercise>

<Exercise title={'007 Triple hello'}>

Luo ohjelma, joka pyytää käyttäjältä merkkijonoa. Kun käyttäjä on antanut merkkijonon (kirjoittanut tekstin ja painanut Enter), ohjelma tulostaa annetun rivin 3 kertaa. Esimerkki tulosteesta syötteellä `Hello`:



```console
Give input!
> Hello
Hello
Hello
Hello
```

</Exercise>

<Exercise title={'008 Greeting'}>

Luo ohjelma, joka kysyy käyttäjältä heidän nimeään ja tervehtii heitä. Esimerkki tulosteesta syötteellä `Ada`:



```console
What is your name?
> Ada
Hello Ada!
```
<Note>Huomaa huutomerkki!</Note>

</Exercise>

<Exercise title={'009 Conversation'}>

Luo ohjelma, joka simuloi pientä keskustelua. Ohjelma tulostaa kolme lausetta ja odottaa kaksi käyttäjän syötettä. Esimerkki tulosteesta:



```console
Hello, how are you?
> Fine, thanks.
That's interesting, tell me more
> I learn coding
Thank you for sharing!
```

</Exercise>

<Exercise title={'010 Name and profession'}>

Luo ohjelma, joka kysyy käyttäjältä nimen ja ammatin. Tämän jälkeen ohjelma kirjoittaa pienen tarinan näillä tiedoilla. Tässä esimerkkitarina syötteillä `Ada` ja `Data Scientist`:



<Note>Jokainen Ada ja Data Scientist tarinassa ovat käyttäjän antamia syötteitä. Muista tallentaa käyttäjältä kysytyt syötteet muuttujiin ja käyttää niitä tarinassa!  </Note>

```console
I will tell a story, but I need some information.
Give a name for main character:
> Ada
Give the character a profession:
> Data Scientist
Here is the story:
Once upon a time there was a Data Scientist called Ada
On her way to work, Ada often pondered what being Data Scientist meant to them.
When you work as a Data Scientist you meet interesting people.
Ada enjoys their work as Data Scientist, The end.
```

</Exercise>