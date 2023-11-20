---
title: "Olio-ohjelmointi"
nav_order: 1
hidden: false
---

Aloitamme nyt matkamme **olio-ohjelmoinnin** (englanniksi **Object Oriented Programming**, usein lyhennetty **OOP**) maailmaan. Ensin keskitymme kuvailemaan käsitteitä ja dataa käyttäen olioita. Siitä eteenpäin opimme lisäämään toiminnallisuutta, eli metodeja ohjelmaamme.

Olio-ohjelmointi keskittyy ongelmien ratkaisemiseen eristämällä ongelma-alueen käsitteet erillisiksi entiteeteiksi ja käyttämällä näitä entiteettejä ongelmien ratkaisemiseen. Ongelmaan liittyvät käsitteet voidaan ottaa huomioon vasta kun ne on tunnistettu. Toisin sanoen on mahdollista muodostaa ongelmasta abstraktio, joka tekee ongelman lähestymisestä helpompaa.

Kun ongelmaan liittyvät käsitteet on tunnistettu, voimme myös alkaa rakentaa ohjelmia, jotka edustavat niitä. Nämä rakenteet, ja niistä muodostetut yksittäiset instanssit, eli oliot, ovat käytössä ongelman ratkaisemisessa. Lause "ohjelmat rakennetaan pienistä, selkeistä ja yhteistyökykyisistä olioista" ei välttämättä vielä tarkoita paljoakaan. Se alkaa kuitenkin tuntua järkevältä, kun kurssin edetessä pääsemme käsittelemään konkreettisia esimerkkejä.

## Luokat ja oliot

Olemme jo käyttäneet C#-kielen tarjoamia luokkia ja olioita. Luokka määrittelee olioiden ominaisuudet, eli niiden tietoon liittyvät asiat (instanssimuuttujat ja olion ominaisuudet), sekä niiden käyttäytymisen, eli metodit. Olioiden instanssimuuttujien arvot määrittelevät yksittäisen olion sisäisen tilan, kun taas metodit määrittelevät sen tarjoaman toiminnallisuuden.

**Metodi** on osa lähdekoodia joka on nimetty ja jota voidaan kutsua. Metodi on aina jonkin luokan osa ja sitä käytetään usein muokkaamaan olion sisäistä tilaa.

Esimerkiksi, Lista on C#-kielen tarjoama luokka, ja olemme käyttäneet sen tarjoamia olioita ohjelmissamme. Alla luodaan Lista-luokasta olio nimeltä integers ja lisätään siihen muutamia kokonaislukuja.


```cpp
// luomme List-luokasta integers-olion
List<int> integers = new List<int>();

// lisätään arvot 15, 34, 65, 111 integers-olioon
integers.Add(15);
integers.Add(34);
integers.Add(65);
integers.Add(111);

// tulostetaan integers-olion koko
Console.WriteLine(integers.Count);
```

Olio alustetaan aina kutsumalla metodia joka luo objektin, eli konstruktoria käyttäen **new**-avainsanaa.

Luokka määrittelee piirrustukset oliolle, joka alustetaan siitä. Piirretään analogia luokasta ja oliosta johonkin muuhun kuin tietokoneohjelmointiin. Rintamamiestalo on todennäköisesti tuttu monille, ja voimme olettaa että olemassa on piirrustukset jotka määrittelevät mitä rintamamiestalo on. Luokka on piirrustus. Toisin sanottuna se määrittelee mitä luokasta luodut oliot ovat:

![Talon piirrustukset](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/houses.jpg)

Yksittäiset oliot, tässä tapauksessa rintamamiestalot, luodaan samoilla piirrustuksilla -- ne ovat saman luokan instansseja. Yksittäisten olioiden tila, eli ominaisuudet (kuten seinien väri, katon rakennusmateriaali, perustusten väri, ovien materiaali ja väri,...) voivat kuitenkin vaihdella. Seuraava on "rintamamiestalo-luokan olio":

![Yksittäinen talo](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/singlehouse.jpg)

## Luokkien luominen

Luokka määrittää millaisia siitä luodut oliot ovat.

* **olion muuttujat (instanssin muuttujat, englanniksi instance variables)** määrittävät olion sisäistä tilaa
* **olion metodit** määrittävät mitä olio tekee

Tutustaan nyt luokkien luomiseen ja niiden muuttujien ja metodien määrittämiseen.

Luokka on tarkoitettu esittämään jotain merkityksellistä kokonaisuutta, jossa "merkityksellinen kokonaisuus" viittaa usein johonkin reaalimaailman objektiin tai käsitteeseen. Jos tietokoneohjelma käsittelee henkilötietoja, olisi ehkä merkityksellistä määritellä luokka Person, joka sisältää henkilöön liittyviä metodeja ja muuttujia.

Aloitetaan. Esimerkissä käytämme **Exercise001** pohjaa tehtävistä, joten voit seurata mukana. Oletammekin että meillä on projektipohja, jossa on tyhjä pääohjelma, eli **Program.cs**.


```cpp
using System;
namespace Exercise001
{
  class Program
  {
    public static void Main(string[] args)
    {

    }
  }
}
```

Seuraava olsio on tarkoitettu uusien luokkien luomiseen Visual Studio Codessa. Voit toki käyttää mitä tahansa editoria, mutta tämä materiaali on luotu Visual Studio Codelle.

### Uuden luokan luominen

1. Luodaksemme uuden luokan, klikkaa hiiren oikealla painikkeella VSCode Explorerissa ja valitse New File. Tämä luo uuden tiedoston kansioon, joka on auki VSCode:ssa.

Kuten muuttujilla ja metodeilla, luokan nimellä tulisi olla mahdollisimman kuvaava nimi. On tavallista, että luokka elää ja muuttaa muotoaan ohjelman kehittyessä. Tästä syystä luokan nimeä voi joutua muuttamaan myöhemmin.

2. Nimeä tiedostosi **Person.cs**. Tiedoston tulee päättyä .cs-päätteeseen, jotta se tunnistetaan C#-tiedostoksi.

Varmista, että tiedosto **Person.cs** on samassa kansiossa kuin **Program.cs**

3. Varmista, että tiedostossa on oikea **nimiavaruus** (englanniksi **namespace**), jotta voit viitata siihen **Program.cs**-tiedostosta.

Käsittelemme nimiavaruudet myöhemmin. Tällä hetkellä, kun luot uuden luokan, **käytä samaa nimiavaruuta (namespace) kuin olemassa olevilla luokilla**.

4. Lisää tämä koodi tiedostoosi:

```cpp
using System;

namespace Exercise001
{
  public class Person
  {
    
  }
}
```

Luokka määrittää olion ominaisuudet ja metodit. Päätetään antaa Person-luokalle kaksi ominaisuutta: nimi ja ikä. On luonnollista että nimi on merkkijono, ja ikä on numero. Lisätään nämä "piirrustuksiimme":

```cpp
public class Person {
    private string name;
    private int age;
}
```

Yllä määrittelimme, että jokaisella oliolla joka luodaan Person luokasta, on nimi ja ikä. Luokan sisällä määritellyt muuttujat ovat **instanssimuuttujia**, tai olion attribuutteja. Muitakin nimiä saattaa esiintyä. 

Instanssimuuttujat kirjoitetaan luokan määrittelyn jälkeen, eli rivin **public class Person {** jälkeen. Jokainen muuttuja on edeltävänä **private**-avainsanalla. **private**-avainsana tarkoittaa, että muuttujat ovat "piilossa" olion sisällä. Tätä kutsutaan **kapseloinniksi** (englanniksi **encapsulation**).

Luokkakaaviossa, muuttujat jotka liittyvät luokkaan, määritellään muodossa **"muuttujanNimi: muuttujanTyyppi"**. Miinusmerkki muuttujan nimen edessä tarkoittaa, että muuttuja on kapseloitu (sillä on private-avainsana).**

![Luokkakaavio](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/person.jpg)

Olemme nyt määrittäneet piirrustukset -- luokan -- person -oliolle. Jokainen uusi person-olio sisältää muuttujat **name** ja **age**, jotka voivat pitää sisällään oliokohtaisia arvoja. Person-olion "tila" koostuu sen name- ja age-muuttujien arvoista.

Person ei tee vielä mitään, mutta pääsemme sinne kyllä.

## Konstruktorin määrittäminen

Haluamme asettaa alkutilan luotavalle oliolle. Omat oliomme luodaan samalla tavalla kuin valmiitkin oliot, kuten List, käyttäen **new**-avainsanaa. Olisi kätevää pystyä antamaan oliolle luodessa sen muuttujille alkuarvot. Esimerkiksi person oliolle olisi kätevää pystyä antamaan nimi:

```cpp
    public static void Main(string[] args)
    {
      Person ada = new Person("Ada");
      // ...
    }
```

Tämä saadaan tehtyä määrittämällä metodi, joka luo olion, eli **konstruktori**. Konstruktori määritellään instanssimuuttujien jälkeen. Seuraavassa esimerkissä määritellään konstruktori Person-luokalle, jota voidaan käyttää uuden Person-olion luomiseen. Konstruktori asettaa olion iän 0:aan ja merkkijonon joka sille annetaan parametrina olion nimeksi:


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName) 
  {
    this.age = 0;
    this.name =  initialName;
  }
}
```

Konstruktorin nimi on aina sama kuin luokan nimi. Yllä olevassa esimerkissä luokan nimi on Person, joten konstruktorin nimi on myös Person. Konstruktori saa parametrina nimen luotavalle oliolle. Parametri on sulkujen sisällä ja seuraa konstruktorin nimeä. Sulkeita seuraa aaltosulkeet. Näiden sisällä on lähdekoodi, jota ohjelma suorittaa kun konstruktoria kutsutaan (esim. new Person("Ada")).

**Oliot luodaan aina käyttämällä konstruktoria.**

Muutamia huomioita: konstruktori sisältää lausekkeen **this.age = 0**. Tämä lauseke asettaa vasta luodun olion (eli "tämän" , englanniksi **this** olion) age-instanssimuuttujan arvoksi 0. Toinen lauseke **this.name = initialName** asettaa parametrina annetun merkkijonon olion luodessaan.

![Luokkakaavio konstruktorin kanssa](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/personconstructor.jpg)

Jos ohjelmoija ei määritä luokalle konstruktoria, C#-kääntäjä luo luokalle oletuskonstruktorin. Oletuskonstruktori on konstruktori, joka ei tee mitään muuta kuin luo olion. Olion muuttujat pysyvät alustamattomina (yleensä olion viittaukset ovat null-arvoisia, eli ne eivät osoita mihinkään).

Esimerkiksi olio voidaan luoda alla olevasta luokasta kutsumalla **new Person()**

```cpp
public class Person
{
  private string name;
  private int age;
}
```

Jos konstruktori on määritelty, oletuskonstruktoria ei ole olemassa. Alla olevalle luokalle, kutsu new Person() aiheuttaisi virheen, koska konstruktoria ilman parametreja ei ole määritelty.


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName) {
    this.age = 0;
    this.name =  initialName;
  }
}
```

## Metodin määrittäminen oliolle

Osaamme nyt luoda olion ja alustaa sen muuttujat. Olio tarvitsee kuitenkin myös metodeja, jotta se voi tehdä jotain. Kuten olemme oppineet, **metodi** on nimetty lähdekoodin osa luokassa, jota voidaan kutsua.


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName) {
    this.age = 0;
    this.name =  initialName;
  }

  public void PrintPerson() {
    Console.WriteLine(this.name + ", age " + this.age + " years");
  }
}
```

Metodi kirjoitetaan luokassa konstruktorin alapuolelle. Metodin nimi alkaa **public void**, sillä metodin tarkoitus on olla saatavilla ulkopuolisille (**public**) ja se ei palauta mitään arvoa (**void**).

Olemme käyttäneet määritelmää **static** joissain metodeissa joita olemme kirjoittaneet. **Static**-määritelmä tarkoittaa, että metodi ei kuulu mihinkään olioon, eikä sitä voi käyttää olioiden muuttujien arvojen hakemiseen.

Tästä eteenpäin, metodeissamme **ei tule olemaan static-määritelmää**, jos ne käsittelevät tietoa oliosta, joka on luotu jostain luokasta. Jos metodi saa parametreina kaikki ne muuttujat joiden arvoja se käyttää, se voi olla static-metodi.

Luokan nimen, instanssimuuttujien ja konstruktorin lisäksi luokkakaaviossa on nyt myös metodi PrintPerson. Koska metodi tulee **public**-määritelmän kanssa, metodi on merkitty plus-merkillä. Metodin nimen perässä ei ole sulkujen sisällä mitään, koska metodi ei ota parametreja. Metodille on myös merkitty sen palautusarvo (tai tällä kertaa, ettei se palauta mitään), **void**.

![Luokkaakaavio tulostusmetodin kanssa](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/printperson.jpg)

Metodi **PrintPerson** sisältää yhden rivin lähdekoodia, joka käyttää instanssimuuttujia **name** ja **age**. Luokkakaaviossa ei ole mitään tietoa siitä, mitä metodi tekee. Instanssimuuttujiin viitataan etuliitteellä this. Kaikki olion muuttujat ovat näkyvissä ja käytettävissä metodin sisällä.

Luodaan kolme henkilöä pääohjelmassa ja pyydetään heitä tulostamaan itsensä:

```cpp
class Program
{
  static void Main(string[] args)
  {
    Person ada = new Person("Ada");
    Person antti = new Person("Antti");
    Person martin = new Person("Martin");

    ada.PrintPerson();
    antti.PrintPerson();
    martin.PrintPerson();
  }
}
```

Prints:

```console
Ada, age 0 years
Antti, age 0 years
Martin, age 0 years
```

## Instanssimuuttujien arvojen muuttaminen metodissa

Lisätään metodi aiemmin luotuun luokkaan Person, joka kasvattaa henkilön ikää yhdellä vuodella.


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName)
  {
    this.age = 0;
    this.name = initialName;
  }

  public void PrintPerson()
  {
    Console.WriteLine(this.name + ", age " + this.age + " years");
  }

  public void GrowOlder()
  {
    this.age = this.age + 1;
  }
}
```

Metodi on kirjoitettu luokan sisälle, kuten PrintPerson-metodikin. Metodi kasvattaa instanssimuuttujan **age** arvoa yhdellä.

Myös luokkakaavio saa päivityksen.

![Class Diagram With Growth](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/persongrow.jpg)

Kutsutaan metodia ja katsotaan mitä tapahtuu:

```cpp
static void Main(string[] args)
{
  Person ada = new Person("Ada");
  Person antti = new Person("Antti");
  Person martin = new Person("Martin");

  ada.PrintPerson();
  antti.PrintPerson();
  martin.PrintPerson();

  Console.WriteLine();

  ada.GrowOlder();
  antti.GrowOlder();
  antti.GrowOlder();

  ada.PrintPerson();
  antti.PrintPerson();
  martin.PrintPerson();
}
```

Tulostaa

```console
Ada, age 0 years
Antti, age 0 years
Martin, age 0 years

Ada, age 1 years
Antti, age 2 years
Martin, age 0 years
```

Kun nämä kaksi oliota "syntyvät" niillä on molemmilla ikä 0 (**this.age = 0;** suoritetaan konstruktorissa). **ada**-olion GrowOlder-metodia kutsutaan kerran, ja **antti**-olion GrowOlder-metodia kutsutaan kahdesti. Kuten tulostus osoittaa, Adan ikä on 1 vuosi kasvun jälkeen, Antin ikä on 2. Metodin kutsuminen olion kohdalla vastaavasti ei vaikuta toisen henkilö-olion ikään, koska jokainen luokasta instanssioidut oliot ovat omia instanssejaan, kuten Martin.

Metodi voi myös sisältää ehtolauseita tai silmukoita. Alla GrowOlder -metodi on muutettu niin, että se rajoittaa ikääntymisen 100 vuoteen.


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName)
  {
    this.age = 0;
    this.name = initialName;
  }

  public void PrintPerson()
  {
    Console.WriteLine(this.name + ", age " + this.age + " years");
  }

  public void GrowOlder()
  {
    if (this.age < 100)
    {
      this.age = this.age + 1;
    }
  }
}
```

## Arvon palauttaminen metodista

Metodi voi palauttaa arvon. Tähän mennessä luomamme metodit eivät ole palauttaneet mitään. Tämä on merkitty kirjoittamalla metodin määrittelyn yhteyteen **void**-avainsana.


```cpp
public class Door 
{
  public void Knock() 
  {
      // ...
  }
}
```

Avainsana **void** tarkoittaa, että metodi ei palauta mitään arvoa.

Jos haluamme metodin palauttavan arvon, meidän tulee korvata **void**-avainsana muulla. Seuraavassa esimerkissä luokkaan Teacher on lisätty metodi **Grade**, joka palauttaa aina kokonaislukumuuttujan arvon 10. Arvo palautetaan aina **return**-käskyllä:


```cpp
public class Teacher 
{
  public int Grade() 
  {
      return 10;
  }
}
```

Metodi yllä palauttaa **int** tyyppisen muuttujan, jonka arvo on 10. Jotta paluuarvoa voidaan käyttää, se tulee sijoittaa muuttujaan. Tämä tapahtuu samalla tavalla kuin muuttujan arvon sijoittaminen, eli käyttämällä yhtäsuuruusmerkkiä:

```cpp
class Program
{
  static void Main(string[] args)
  {
  Teacher teacher = new Teacher();

  int grading = teacher.Grade();

  Console.WriteLine("The grade received is " + grading);
  }
}
```

```console
The grade received is 10
```

Metodin paluuarvo sijoitetaan **int** -muuttujaan aivan kuten mikä tahansa muukin **int** -arvo. Paluuarvoa voitaisiin käyttää myös osana lauseketta.


```cpp
static void Main(string[] args)
{
Teacher first = new Teacher();
Teacher second = new Teacher();
Teacher third = new Teacher();

double average = (first.Grade() + second.Grade() + third.Grade()) / 3.0;

Console.WriteLine("Grading average " + average);
}
```

```console
Grading average 10
```

Kaikki muuttujat joita olemme tähän mennessä käyttäneet, voidaan palauttaa myös metodista. Yhteenvetona:

* Metodi joka ei palauta mitään arvoa, on määritelty **void**-avainsanalla.

```cpp
public void MethodThatReturnsNothing() {
  // the method body
}
```

* Metodi joka palauttaa kokonaisluvun, on määritelty **int**-avainsanalla.


```cpp
public int MethodThatReturnsAnInteger() {
  // the method body, requires a return statement
}
```

* Metodi joka palauttaa merkkijonon, on määritelty **string**-avainsanalla.

```cpp
public string MethodThatReturnsAString() {
  // the method body, requires a return statement
}
```

* Metodi joka palauttaa liukuluvun, on määritelty **double**-avainsanalla.


```cpp
public double MethodThatReturnsADouble() {
  // the method body, requires a return statement
}
```

Jatketaan Person-luokan kehittämistä ja lisätään siihen **ReturnAge**-metodi, joka palauttaa henkilön iän.

```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string initialName)
  {
    this.age = 0;
    this.name = initialName;
  }

  public void PrintPerson()
  {
    Console.WriteLine(this.name + ", age " + this.age + " years");
  }

  public void GrowOlder()
  {
    if (this.age < 100)
    {
      this.age = this.age + 1;
    }
  }

  // the added method
  public int ReturnAge()
  {
    return this.age;
  }
}
```

![Luokkakaavio palauttavan metodin kanssa](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/personreturn.jpg)

Katsotaan miten metodi toimii:

```cpp
static void Main(string[] args)
{
  Person pekka = new Person("Pekka");
  Person antti = new Person("Antti");

  pekka.GrowOlder();
  pekka.GrowOlder();

  antti.GrowOlder();

  Console.WriteLine("Pekka's age: " + pekka.ReturnAge());
  Console.WriteLine("Antti's age: " + antti.ReturnAge());
  int combined = pekka.ReturnAge() + antti.ReturnAge();

  Console.WriteLine("Pekka's and Antti's combined age " + combined + " years");
}
```

```console
Pekka's age: 2
Antti's age: 1
Pekka's and Antti's combined age 3 years
```

Kuten huomasimme, metodi voi sisältää lähdekoodia samalla tavalla kuin muutkin koodimme osat. Metodit voivat sisältää ehtolauseita tai silmukoita, ja muita metodeita voidaan kutsua niiden sisällä.

Kirjoitetaan nyt metodi, joka määrittää onko henkilö täysi-ikäinen. Metodi palauttaa boolean-arvon, joka on joko **true** tai **false**:


```cpp
class Person
{
  //... Kaikki aiempi koodi on tässä välissä

  public bool IsOfLegalAge()
  {
    if (this.age < 18)
    {
      return false;
    }

    return true;
  }

  /*
  Metodi olisi voinut olla kirjoitettu myös seuraavasti:
  public bool IsOfLegalAge() 
  {
    return this.age >= 18;
  }
  */
}
```

Kokeillaanpa:

```cpp
static void Main(string[] args)
{
  Person pekka = new Person("Pekka");
  Person antti = new Person("Antti");

  int i = 0;
  while (i < 27)
  {
    pekka.GrowOlder();
    i = i + 1;
  }

  antti.GrowOlder();

  if (antti.IsOfLegalAge())
  {
    Console.Write("of legal age: ");
    antti.PrintPerson();
  }
  else
  {
    Console.Write("underage: ");
    antti.PrintPerson();
  }

  if (pekka.IsOfLegalAge())
  {
    Console.Write("of legal age: ");
    pekka.PrintPerson();
  }
  else
  {
    Console.Write("underage: ");
    pekka.PrintPerson();
  }
}
```

```console
underage: Antti, age 1 years
of legal age: Pekka, age 27 years
```

Hienosäädetään ratkaisua vielä hieman. Nykyisellään henkilö voidaan "tulostaa" vain siten, että tulostetaan sekä nimi että ikä. Tilanteita kuitenkin esiintyy, joissa halutaan tietää vain henkilön nimi.

Monessa ohjelmointikielessä tähän käytetään **get-metodia**. C#-kielellä, olioiden ominaisuuksia, kuten henkilön **age** ja **name**, voidaan käyttää automaattisesti toteutettujen ominaisuuksien, eli [**Auto Implementation Property**](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties) kautta.


```cpp
public string name { get; }
```

Avataan tätä hieman. "Konepellin alla", yllä oleva koodi kertoo **C#-kääntäjälle** että meidän **name**-ominaisuudella on "sisäänrakennettu" metodi arvon hakemiseen ja asettamiseen. Koodi yllä on toiminnallisesti sama kuin:

```cpp
string _name;
public string name
{
  get
  {
    return _name;
  }
}
```

Tässä esimerkissä, meillä on nyt myös rivi **string _name;**, ja molemmilla meidän alkuperäisellä **string name** on nyt **public**. **string _name;** tunnetaan englanninkielisellä termillä [**Backing field**](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties#properties-with-backing-fields), josta voit lukea lisää linkistä. Meidän ei tarvitse huolehtia niistä nyt.

Metodin kirjoittamisen sijaan, kuten teimme **age** kanssa:

```cpp
public string ReturnAge() {
  return age;
}
```

Meillä on nyt hyvin lyhyt vaihtoehto:

```cpp
public string name { get; }
```

<Note> 
Meidän pitää muuttaa merkkijonan nimi julkiseksi (private -> public), jotta se on käytettävissä pääohjelmassa, tai muissa luokissa. On tapoja suojata ominaisuus, mutta palaamme siihen myöhemmin.
</Note>

Käytetään tätä uutta tapaa iälle:

```cpp
static void Main(string[] args)
{
  Person pekka = new Person("Pekka");
  Person antti = new Person("Antti");

  int i = 0;
  while (i < 27)
  {
    pekka.GrowOlder();
    i = i + 1;
  }

  antti.GrowOlder();

  if (antti.IsOfLegalAge())
  {
    Console.WriteLine(antti.name + " is of legal age");
  }
  else
  {
    Console.WriteLine(antti.name + " is underage");
  }

  if (pekka.IsOfLegalAge())
  {
    Console.WriteLine(pekka.name + " is of legal age");
  }
  else
  {
    Console.WriteLine(pekka.name + " is underage ");
  }
}
```

```console
Antti is underage
Pekka is of legal age
```

Kuten huomataan, nyt voimme kutsua henkilön nimeä suoraan lisäämällä **.name** olion nimen perään, kuten **antti.name**. Päivitetään vielä **age** omaamaan myös **get-metodi**, ja poistetaan vanha **ReturnAge**-metodi. Nyt luokkamme näyttää tältä:


```cpp
public class Person
{
  public string name { get; }
  public int age { get; set; }

  public Person(string initialName)
  {
    this.age = 0;
    this.name = initialName;
  }

  public void PrintPerson()
  {
    Console.WriteLine(this.name + ", age " + this.age + " years");
  }

  public void GrowOlder()
  {
    if (this.age < 100)
    {
      this.age = this.age + 1;
    }
  }

  public bool IsOfLegalAge() 
  {
    return this.age >= 18;
  }
}
```

Huomataan, että nyt **age**-muuttujalla on myös **set-metodi**. Tämä johtuu siitä, että muutamme **Person**-luokan **age**-muuttujan arvoa **GrowOlder**-metodissa. Palaamme **set-metodiin** myöhemmin.

## Olion merkkijonoesitys ja ToString-metodi

Olemme nyt syyllistyneet huonoon ohjelmointityyliin, luomalla metodin tulostamista varten, eli **PrintPerson** metodin. Parempi tapa on määritellä metodi oliolle, joka palauttaa olion "merkkijonoesityksen". Metodi joka palauttaa merkkijonoesityksen on aina **ToString** C#:ssa. Määritellään tämä metodi person-oliolle seuraavassa esimerkissä:


```cpp
public class Person
{
  // ..
  public override string ToString() 
  {
      return this.name + ", age " + this.age + " years";
  }
}
```

Metodi **ToString** toimii kuten **PrintPerson**. Kuitenkin, se ei tulosta mitään, vaan **palauttaa** merkkijonoesityksen, jonka kutsuva metodi voi tulostaa tarvittaessa.

Metodia voidaan käyttää vähän yllättävälläkin tavalla:


```cpp
static void Main(string[] args)
{
  Person pekka = new Person("Pekka");
  Person antti = new Person("Antti");

  int i = 0;
  while (i < 27)
  {
    pekka.GrowOlder();
    i = i + 1;
  }

  antti.GrowOlder();

  Console.WriteLine(pekka); // Sama kuin Console.WriteLine(pekka.ToString() )
  Console.WriteLine(antti); // Sama kuin Console.WriteLine(antti.ToString() )
}
```

Periaatteessa, **Console.WriteLine**-metodi pyytää olion merkkijonoesitystä ja tulostaa sen. Kutsu **ToString**-metodiin, joka palauttaa merkkijonoesityksen, ei tarvitse olla kirjoitettu erikseen, koska C# lisää sen automaattisesti. Kun ohjelmoija kirjoittaa:


```cpp
Console.WriteLine(antti);
```

C# laajentaa kutsun ajonaikana seuraavaan muotoon:

```cpp
Console.WriteLine(antti.ToString());
```

Sellaisenaan, kutsu **Console.WriteLine(antti)** kutsuu **antti**-olion **ToString**-metodia ja tulostaa sen palauttaman merkkijonoesityksen.

Voimme nyt poistaa turhan **PrintPerson**-metodin **Person**-luokasta.

## Metodin parametrit

Jatketaan vielä luokan Person kehittämistä. Olemme päättäneet, että haluamme laskea ihmisten painoindeksit. Tätä varten kirjoitamme metodit henkilön pituuden ja painon asettamiseksi, ja myös metodin painoindeksin laskemiseksi. Person-olion uudet ja muutetut osat ovat seuraavat:

```cpp
public class Person
{
  public string name { get; }
  public int age { get; set; }
  public int weight { get; set; }
  public int height { get; set; }

  public Person(string initialName)
  {
    this.age = 0;
    this.weight = 0;
    this.height = 0;
    this.name = initialName;
  }

  public double BodyMassIndex()
  {
    double heigthPerHundred = this.height / 100.0;
    return this.weight / (heigthPerHundred * heigthPerHundred);
  }

  // ...
}
```

Instanssimuuttujat **height** ja **weight** lisättiin person-oliolle. Nyt näemme **{ get; set; };** molemmilla näillä uusilla muuttujilla. Käytämme niitä seuraavaksi kertomaan ohjelmalle, kuinka pitkä tai painava henkilö on.


```cpp
static void Main(string[] args)
{
  Person matti = new Person("Matti");
  Person juhana = new Person("Juhana");

  matti.height = 180;
  matti.weight = 86;

  juhana.height = 175;
  juhana.weight = 64;

  Console.WriteLine(matti.name + ", body mass index is " + matti.BodyMassIndex());
  Console.WriteLine(juhana.name + ", body mass index is " + juhana.BodyMassIndex());

}
```

Tämä tulostaa

```console
Matti, body mass index is 26.54320987654321
Juhana, body mass index is 20.897959183673468
```

## Parametrilla ja instanssimuuttujalla voi olla sama nimi!

Konstruktorissamme, olemme käyttäneet muuttujaa **initialName** sen sijaan, että olisimme käyttäneet **name**. 

```cpp
public Person(string initialName)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  this.name = initialName;
}
```

Parametrin nimi voisi olla myös sama kuin instanssimuuttujan nimi, joten seuraava toimisi myös:

```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  this.name = name;
}
```

Tässä tapauksessa **name** metodissa viittaa nimenomaan parametriin nimeltä **name** ja **this.name** instanssimuuttujaan samalla nimellä. Esimerkiksi seuraava esimerkki ei toimisi, koska koodi ei viittaa instanssimuuttujaan **name** ollenkaan. Koodi asettaa parametrina saadun **name**-muuttujan arvoksi sen arvon, joka sillä jo on:


```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  // EI IKINÄ NÄIN!
  name = name;
}
```

```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  // TÄMÄ ON OIKEIN!
  this.name = name;
}
```

## Sisäisen metodin kutsuminen

Olio voi myös kutsua omia metodeitaan. Esimerkiksi jos haluamme merkkijonoesityksen sisältävän myös painoindeksin, olisi **ToString**-metodin kutsuttava **BodyMassIndex**-metodia:

```cpp
public override string ToString()
{
      return this.name + ", age " + this.age + " years, my body mass index is " + this.BodyMassIndex();
}
```

Eli kun olio kutsuu omaa metodiaan, metodin nimi ja etuliite **this** riittävät. Vaihtohteinena olisi kutsua olion omaa **BodyMassIndex**-metodia muodossa **BodyMassIndex()**, jolloin ei korosteta sitä, että kutsutaan olion omaa **BodyMassIndex**-metodia:


```cpp
public override string ToString()
{
      return this.name + ", age " + this.age + " years, my body mass index is " + BodyMassIndex();
}
```

# Tehtävät

<Note>
Kun luodaan omia luokkia, varmista, että sisällytät oikean nimiavaruuden, jotta voit viitata siihen Program.cs-tiedostosta. Palaamme nimiavaruuksiin myöhemmin. Toistaiseksi, kun luot uuden luokan, käytä samaa nimiavaruutta kuin Program.cs-tiedostossa on.

Joissain tehtävissä sinun tulee muuttaa Main-metodia. Lue ohjeet huolellisesti!
</Note>

<Exercise title={'001 First account'}>

Tehtäväpohjassa on valmiina luokka nimeltä Account. Account-olio edustaa pankkitiliä, jolla on saldoa (eli tilillä on rahaa). Tiliä voisi käyttää seuraavasti:

```cpp
Account heikkisAccount = new Account("Heikki's account", 100.00);
Account heikkisSwissAccount = new Account("Heikki's account in Switzerland", 1000000.00);

Console.WriteLine("Intial state");
Console.WriteLine(heikkisAccount);
Console.WriteLine(heikkisSwissAccount);

heikkisAccount.Withdrawal(20);
Console.WriteLine("The balance of Heikki's account is now: " + heikkisAccount.balance);
heikkisSwissAccount.Deposit(200);
Console.WriteLine("The balance of Heikki's other account is now: " + heikkisSwissAccount.balance);

Console.WriteLine("End state");
Console.WriteLine(heikkisAccount);
Console.WriteLine(heikkisSwissAccount);
```

Kirjoita ohjelma, joka
- luo tilin, jolla on saldoa 100.0,
- tallettaa tilille 20.0,
- ja tulostaa tilin saldon.


```console
120
```

<Note>Suorita operaatiot tarkasti oikeassa järjestyksessä</Note>

</Exercise>

<Exercise title={'002 First transfer'}>

Edellisestä tehtävästä tuttu Account on käytettävissä tässäkin tehtävässä.

Kirjoita ohjelma, joka

- Luo tilin nimellä "Heikki's account" saldolla 1000.0
- Luo tilin nimellä "Personal account" saldolla 0.0
- Nostaa tililtä "Heikki's account" 100.0
- Tallettaa tilille "Personal account" 100.0
- Tulostaa molempien tilien tiedot, ensin Heikin tilin ja sitten Personal tilin

```console
Heikki's account balance: 900
Personal account balance: 100
```

</Exercise>

<Exercise title={'003 First class'}>

Tässä tehtävässä harjoitellaan luokan luomista.

Nimeä luokka `Dog` (ja tiedosto `Dog.cs`)

Lisää luokalle oikea namespace, jotta voit käyttää sitä pääohjelmasta.
Lisää luokalle seuraavat muuttujat:

- private string name,
- private string breed and 
- private int age   

Luokkakaaviona luokka näyttää tältä:

![Dog class diagram](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/dogclass.jpg)

Huomaa, että luokka ei vielä oikein tee mitään. Se vain määrittelee mitä tietoja koirasta tallennetaan.

</Exercise>

<Exercise title={'004 Classroom'}>

Luo luokka nimeltä `Room` (ja tiedosto `Room.cs`). Lisää luokkaan muuttujat `private string code` ja `private int seats`. Tämän jälkeen luo konstruktori `public Room(string classCode, int numberOfSeats)`, joilla voidaan antaa arvot luokan muuttujille.


![Luokan luokkakaavio](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/roomclass.jpg)


</Exercise>

<Exercise title={'005 Whistle'}>

Luodaan luokka `Whistle`. Lisää luokkaan muuttuja `private string sound`. Tämän jälkeen luo konstruktori `public Whistle(string whistleSound)`, jolla voidaan luoda uusi pilli, jolle annetaan ääni. Tämän jälkeen luo metodi `public void Sound()`, joka tulostaa äänen (käyttäen Console.WriteLine).

```cpp
Whistle duckWhistle = new Whistle("Kvaak");
Whistle roosterWhistle = new Whistle("Peef");

duckWhistle.Sound();
roosterWhistle.Sound();
duckWhistle.Sound();
```

```console
Kvaak 
Peef 
Kvaak
```

</Exercise>

<Exercise title={'006 Product'}>

Luo luokka `Product` joka edustaa kaupan tuotetta. Tuotteella on hinta `price (double)`, määrä `quantity (int)` ja nimi `name (string)`.

Luokalla tulee olla:

- konstruktori `public Product(string name, double price, int quantity)`
- metodi `public void PrintProduct()` joka tulostaa tuotteen tiedot seuraavassa muodossa:

```console
Banana: price 1.1: 13 pcs
```

Yllä oleva esimerkki tulostaa tuotteen, jonka **name** on "Banana", **price** on 1.1 ja **quantity** on 13.

</Exercise>

<Exercise title={'007 Counter'}>

Tämä tehtävä koostuu useammasta osasta. Jokainen osa on yhden pisteen arvoinen.

Tehtäväpohjassa on osittain valmiina luokka DecreasingCounter.

```cpp
using System;

namespace Exercise007
{
  public class DecreasingCounter
  {
    private int value;   // muuttuja joka sisältää laskurin arvon

    public DecreasingCounter(int initialValue)
    {
      this.value = initialValue;
    }

    public void PrintValue()
    {
      Console.WriteLine("value: " + this.value);
    }

    public void Decrement()
    {
      // kirjoita metodin toteutus tänne 
      // tavoite on vähentää laskurin arvoa yhdellä
    }

    // muut metodit tulevat tänne
  }
}
```

Seuraavassa on esimerkki ohjelman käytöstä:

```cpp
public static void Main(string[] args)
{
  DecreasingCounter counter = new DecreasingCounter(10);
  counter.PrintValue();

  counter.Decrement();
  counter.PrintValue();

  counter.Decrement();
  counter.PrintValue();
}
```

```console
value: 10
value: 9
value: 8
```

* Osa 1 : Implementoi metodi Decrement()

Toteuta metodi `public void Decrement()` siten, että se vähentää laskurin arvoa yhdellä kun metodia kutsutaan. Kun olet toteuttanut metodin, yllä oleva esimerkki pitäisi toimia kuten esitetty.

* Osa 2 : Laskurin arvo ei voi olla negatiivinen

Paranna metodia `Decrement()` siten, että laskurin arvo ei voi koskaan olla negatiivinen. Tämä tarkoittaa sitä, että jos laskurin arvo on 0, sen arvoa ei voi vähentää. Tässä voi olla hyötyä ehtolauseesta.

```cpp
public static void Main(string[] args)
{

  DecreasingCounter counter = new DecreasingCounter(2);
  counter.PrintValue();

  counter.Decrement();
  counter.Decrement();
  counter.PrintValue();

  counter.Decrement();
  counter.PrintValue();
}
```

```console
value: 2
value: 0
value: 0
```

* Osa 3: Laskurin arvon nollaaminen

Luo metodi `public void Reset()` joka nollaa laskurin arvon. Tämä tarkoittaa sitä, että metodia kutsuttaessa laskurin arvo muutetaan arvoksi 0.


```cpp
public static void Main(string[] args)
{

  DecreasingCounter counter = new DecreasingCounter(20);
  counter.PrintValue();

  counter.Reset();
  counter.PrintValue();
}
```

```console
value: 20
value: 0
```

</Exercise>

<Exercise title={'008 Debt'}>

Luodaan luokka `Debt` joka edustaa velkaa. Velalla on saldo `balance (double)` ja korko `interestRate (double)`. Korko ja saldo annetaan konstruktorissa parametreina `public Debt(double initialBalance, double initialInterestRate)`.

Lisäksi luodaan metodit `public void PrintBalance()` ja `public void WaitOneYear()` luokalle. Metodi `PrintBalance` tulostaa saldon, ja `WaitOneYear` kasvattaa velan määrää. Velan määrä kasvaa kertomalla saldo korkoprosentilla. Esimerkiksi seuraava koodi:

```cpp
public static void Main(string[] args)
{

  Debt mortgage = new Debt(120000.0, 1.01);
  mortgage.PrintBalance();

  mortgage.WaitOneYear();
  mortgage.PrintBalance();

  // Wait 20 years
  int years = 0;
  while (years < 20)
  {
    mortgage.WaitOneYear();
    years = years + 1;
  }

  mortgage.PrintBalance();
}
```

Esimerkki näyttää koron vaikutuksen velan määrään kun korko on yksi prosentti vuodessa.

```console
120000
121200
147887.0328416936
```

</Exercise>

<Exercise title={'009 Dalmatian'}>

Luo luokka `Dalmatian` joka edustaa dalmatialaista koiraa. Koiralla on nimi `name (string)` ja täplien määrä `spots (int)`. Nimi ja täplien määrä annetaan konstruktorissa parametreina `public Dalmatian(string name, int spots)`.

<Note>
Anna muuttujille myös get ja set:

Tee muuttujista public, ja lisää \{ get; set; \} muuttujan määrittelyriviin!
</Note>

```cpp
Dalmatian spotty = new Dalmatian("Spot", 306);
Console.WriteLine(spotty.name + " is a very good dog. He has " + spotty.spots + " darker spots in his fur");
```

```console
Spot is a very good dog. He has 306 darker spots in his fur
```

</Exercise>

<Exercise title={'010 Gauge'}>

Luodaan mittariluokka `Gauge`. Mittarilla on instanssimuuttuja `public int value`, konstruktori ilman parametreja (asettaa mittarin arvoksi 0), ja seuraavat kolme metodia:

- Metodi `public void Increase()` kasvattaa instanssimuuttujan arvoa yhdellä. Arvoa ei voi kasvattaa suuremmaksi kuin viisi.
- Metodi `public void Decrease()` vähentää instanssimuuttujan arvoa yhdellä. Arvoa ei voi muuttaa negatiiviseksi.
- Metodi `public bool Full()` palauttaa `True` jos instanssimuuttujan arvo on viisi. Muutoin palautetaan `False`.

<Note>
Anna muuttujalle myös get ja set:

Tee muuttujista public, ja lisää \{ get; set; \} muuttujan määrittelyriviin!
</Note>

Esimerkki luokan toiminnasta:

```cpp
public static void Main(string[] args)
{
  Gauge g = new Gauge();

  while (!g.Full())
  {
    Console.WriteLine("Not full! Value: " + g.value);
    g.Increase();
  }

  Console.WriteLine("Full! Value: " + g.value);
  g.Decrease();
  Console.WriteLine("Not full! Value: " + g.value);
}
```

```console
Not full! Value: 0
Not full! Value: 1
Not full! Value: 2
Not full! Value: 3
Not full! Value: 4
Full! Value: 5
Not full! Value: 4
```

</Exercise>

<Exercise title={'011 Agent'}>

Tehtäväpohjassa määritellään luokka `Agent`, jolla on etunimi ja sukunimi. Main-metodi yrittää tulostaa esittelyn agentista Bond, mutta ei onnistu. Tämä on mitä sen pitäisi tehdä:

```cpp
public static void Main(string[] args)
{
  Agent bond = new Agent("James", "Bond");
  Console.WriteLine(bond);

  Agent bourne = new Agent("Jason", "Bourne");
  Console.WriteLine(bourne);
}
```

```console
My name is Bond. James Bond.
My name is Bourne. Jason Bourne.
```

Agentin ToString palauttaa tällä hetkellä tyhjän merkkijonon. Korjaa se niin, että se esittelee kansainväliset superagentit asiallisesti (kuten yllä).

</Exercise>

<Exercise title={'012 Multiplier'}>

Luo luokka `Multiplier` jolla on:

Konstruktori `public Multiplier(int number)`
Metodi `public int Multiply(int number)` joka palauttaa arvon number kerrottuna konstruktorissa annetulla luvulla.
Tarvitset myös instanssimuuttujan tässä tehtävässä. Kun kutsut metodia Multiply, tallenna muuttuneet arvot instanssimuuttujaan!

Esimerkki luokan toiminnasta:


```cpp
public static void Main(string[] args)
{
  Multiplier multiplyByThree = new Multiplier(3);

  Console.WriteLine("multiplyByThree.Multiply(2): " + multiplyByThree.Multiply(2));

  Multiplier multiplyByFour = new Multiplier(4);

  Console.WriteLine("multiplyByFour.Multiply(2): " + multiplyByFour.Multiply(2));
  Console.WriteLine("multiplyByThree.Multiply(1): " + multiplyByThree.Multiply(1));
  Console.WriteLine("multiplyByFour.Multiply(1): " + multiplyByFour.Multiply(1));
  Console.WriteLine("multiplyByFour.Multiply(3): " + multiplyByFour.Multiply(3));
}
```

```console
multiplyByThree.Multiply(2): 6
multiplyByFour.Multiply(2): 8
multiplyByThree.Multiply(1): 6
multiplyByFour.Multiply(1): 8
multiplyByFour.Multiply(3): 24
```

<Note>
Talletettu arvo muuttuu metodin kutsujen aikana!
</Note>

Laskut ovat oikeasti (järjestyksessä):

3 \* 2 = 6  
4 \* 2 = 8  
6 \* 1 = 6  
8 \* 1 = 8  
8 \* 3 = 24

</Exercise>

<Exercise title={'013 Statistics'}>

Tehtäväpohjassa on valmiina luokka `Statistics`

```cpp
namespace Exercise013
{
  public class Statistics
  {
    public int count {get; set;}
    public int sum { get; set; }

    public NumberStatistics()
    {
      // alusta muuttuja count täällä
    }

    public void AddNumber(int number) {
        // lisää koodia
    }
  }
}
```

Seuraava koodi esittelee valmiin koodin käyttöä:

```cpp
Statistics statistics = new Statistics();
statistics.AddNumber(3);
statistics.AddNumber(5);
statistics.AddNumber(1);
statistics.AddNumber(2);
Console.WriteLine("Count: " + statistics.count);
Console.WriteLine("Sum: " + statistics.sum);
```

```console
Count: 4
Sum: 11
```

Laajenna ohjelmaa seuraavasti:

- Kun numero lisätään, `count`-muuttujan arvo kasvaa yhdellä
- Kun numero lisätään, `sum`-muuttujan arvo kasvaa lisättävän numeron arvolla

</Exercise>

<Exercise title={'014 Payment card'}>

Tässä tehtävässä, luokka nimeltä `PaymentCard` luodaan, joka pyrkii jäljittelemään kahvilan maksuprosessia.

* Osa 1

Pohjassa on valmiina tiedostot `Program.cs` ja `PaymentCard.cs`.

- Lisää luokka `PaymentCard` projektiin oikeaan tiedostoon.
- Täytä luokalle konstruktori, joka ottaa parametrinaan kortin alkusaldon, ja asettaa sen kortin sisäiseen muuttujaan.
- Täytä metodi `ToString` joka palauttaa kortin saldon muodossa "The card has a balance of X euros".


Tässä on luokalle vähän pohjaa:

```cpp
namespace Exercise014
{
  public class PaymentCard
  {
    private double balance;

    public PaymentCard(double openingBalance)
    {
      // Kirjoita tähän koodia
    }

    public override string ToString()
    {
      // Kirjoita tähän koodia
    }
  }
}
```

Seuraava koodi testaa luokkaa:

```cpp
public static void Main(string[] args)
{
  PaymentCard card = new PaymentCard(50);
  Console.WriteLine(card);
}
```

```console
The card has a balance of 50 euros
```

* Osa 2

Laajenna vastaustasi lisäämällä kaksi metodia:
- Metodi `public void EatLunch()`
- Metodi `public void DrinkCoffee()`

Metodi `EatLunch` vähentää kortin saldoa 10.60 eurolla. Metodi `DrinkCoffee` vähentää kortin saldoa 2.0 eurolla.

Seuraava koodi testaa luokkaa:

```cpp
public static void Main(string[] args)
{
  PaymentCard card = new PaymentCard(50);
  Console.WriteLine(card);

  card.EatLunch();
  Console.WriteLine(card);
  
  card.DrinkCoffee();
  Console.WriteLine(card);
}
```

```console
The card has a balance of 50 euros
The card has a balance of 39.4 euros
The card has a balance of 37.4 euros
```

* Osa 3

Laajenna vastaustasi, niin että kun ostoksia tehdään, tarkistetaan myös saldo. Jos kortilla ei ole tarpeeksi rahaa, saldo ei muutu.


```cpp
public static void Main(string[] args)
{
  PaymentCard card = new PaymentCard(10);
  Console.WriteLine(card);

  card.EatLunch();
  Console.WriteLine(card);
  
  card.DrinkCoffee();
  Console.WriteLine(card);
}
```

```console
The card has a balance of 10 euros
The card has a balance of 10 euros
The card has a balance of 8 euros
```

Huomaa kuinka `EatLunch` ei muuttanut saldoa, koska rahaa ei ollut tarpeeksi. `DrinkCoffee` toimi kuten pitää.

* Osa 4

Laajenna vastaustasi, niin että kortille voi ladata rahaa. 

```cpp
public void AddMoney(double amount) {
    // Kirjoita tähän koodia
}
```

Metodin tarkoituksena on lisätä kortin saldoa parametrina annetulla summalla. Kuitenkin, kortin saldo ei saa ylittää 150 euroa. Jos ladattava summa on suurempi kuin 150, kortin saldo on 150 euroa. Seuraava koodi testaa luokan toimintaa:

```cpp
public static void Main(string[] args)
{
  PaymentCard card = new PaymentCard(100);
  Console.WriteLine(card);

  card.AddMoney(49.99);
  Console.WriteLine(card);

  card.AddMoney(10000.0);
  Console.WriteLine(card);

  card.AddMoney(-10);
  Console.WriteLine(card);
}
```

```console
The card has a balance of 100 euros
The card has a balance of 149.99 euros
The card has a balance of 150 euros
The card has a balance of 150 euros
```

<Note>Et voi lisätä negatiivista summaa!</Note>

</Exercise>