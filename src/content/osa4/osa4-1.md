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

3. Varmista, että tiedostossa on oikea **namespace**, jotta voit viitata siihen **Program.cs**-tiedostosta.

Käsittelemme namespacet myöhemmin. Tällä hetkellä, kun luot uuden luokan, **käytä samaa namespacea kuin olemassa olevilla luokilla**.

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

Let's continue with the **Person** class once more. We've decided that we want to calculate people's body mass indexes. To do this, we write methods for the person to set both the height and the weight, and also a method to calculate the body mass index. The new and changed parts of the Person object are as follows:

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
The instance variables **height** and **weight** were added to the person. We can now see the **{ get; set; };** on both of these new variables. We will use them next to be able to tell our program, how tall or heavy a person is.

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

This prints us 

```console
Matti, body mass index is 26.54320987654321
Juhana, body mass index is 20.897959183673468
```

## A parameter and instance variable having the same name!

In our constructor, we use the variable **initialName** rather than just **name**.

```cpp
public Person(string initialName)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  this.name = initialName;
}
```

The parameter's name could also be the same as the instance variable's, so the following would also work:

```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  this.name = name;
}
```

In this case, **name** in the method refers specifically to a parameter named **name** and this.name to an instance variable of the same name. For example, the following example would not work as the code does not refer to the instance variable **name** at all. What the code does in effect is set the **name** variable received as a parameter to the value it already contains:

```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  // DO NOT DO THIS!
  name = name;
}
```

```cpp
public Person(string name)
{
  this.age = 0;
  this.weight = 0;
  this.height = 0;
  // DO THIS INSTEAD!
  this.name = name;
}
```

## Calling an internal method

The object may also call its methods. For example, if we wanted the string representation returned by ToString to also tell of a person's body mass index, the object's own BodyMassIndex method should be called in the ToString method:

```cpp
public override string ToString()
{
      return this.name + ", age " + this.age + " years, my body mass index is " + this.BodyMassIndex();
}
```

So, when an object calls an internal method, the **name of the method** and **this** prefix suffice. An alternative way is to call the object's own method in the form BodyMassIndex(), whereby no emphasis is placed on the fact that the object's own bodyMassIndex method is being called:

```cpp
public override string ToString()
{
      return this.name + ", age " + this.age + " years, my body mass index is " + BodyMassIndex();
}
```

# Tehtävät

<Note>
When creating own classes, make sure to include the correct namespace so you can reference it from your Program.cs file. We'll get to namespaces later. For now, whenever you create a new class, use the same namespace as the Program.cs has.

Some of the exercises require you to make changes to the Main program. Be sure to read the instructions carefully!
</Note>

<Exercise title={'001 First account'}>

The exercise template comes with a ready-made class named Account. The Account object represents a bank account that has balance (i.e. one that has some amount of money in it). The accounts could be used as follows:

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

Write a program that 
- creates an account with a balance of 100.0, 
- deposits 20.0 in it, 
- and finally prints the balance. 

```console
120
```

<Note>Perform all the operations in this exact order.</Note>

</Exercise>

<Exercise title={'002 First transfer'}>

The Account from the previous exercise class is also available in this exercise.

Write a program that:

- Creates an account named "Heikki's account" with the balance 1000.0
- Creates an account named "Personal account" with the balance 0
- Withdraws 100.0 from Heikki's account
- Deposits 100.0 to its own personal account
- Prints account information (ToString) on both, first Heikki's, then Personal:

```console
Heikki's account balance: 900
Personal account balance: 100
```

</Exercise>

<Exercise title={'003 First class'}>

In this exercise, you'll practice creating a class.

Name the class `Dog` (and the file `Dog.cs`)

You have now created a class called `Dog`. 
Add the variables 
- private string name,
- private string breed and 
- private int age   
to the class. As a class diagram, the class looks like this:

![Dog class diagram](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/dogclass.jpg)


</Exercise>

<Exercise title={'004 Classroom'}>

Create a class named `Room` (and file `Room.cs`). Add the variables `private string code` and `private int seats` to the class. Then create a constructor `public Room(string classCode, int numberOfSeats)` through which values are assigned to the instance variables.

![Room class diagram](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/roomclass.jpg)


</Exercise>

<Exercise title={'005 Whistle'}>

Create a class named `Whistle`. Add the variable `private string sound` to the class. After that, create the constructor `public Whistle(string whistleSound)`, which is used to create a new whistle that's given a sound. After that, create a method `public void Sound()` which prints out the sound (using Console.WriteLine).

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

Create a class `Product` that represents a store product. The product should have a `price (double)`, a `quantity (int)` and a `name (string)`.

The class should have:

- the constructor `public Product(string name, double price, int quantity)`
- a method `public void PrintProduct()` that prints product information in the following format:

```console
Banana: price 1.1: 13 pcs
```

The output above is based on the product being assigned the name banana, with a price of 1.1, and a quantity of 13 .

</Exercise>

<Exercise title={'007 Counter'}>

This exercise consists of multiple sections. Each section corresponds to one exercise point.

The exercise template comes with a partially executed class DecreasingCounter:

```cpp
using System;

namespace Exercise007
{
  public class DecreasingCounter
  {
    private int value;   // a variable that remembers the value of the counter

    public DecreasingCounter(int initialValue)
    {
      this.value = initialValue;
    }

    public void PrintValue()
    {
      Console.WriteLine("value: " + this.value);
    }

    public void decrement()
    {
      // write the method implementation here
      // the aim is to decrement the value of the counter by one
    }

    // and the other methods go here
  }
}
```

The following is an example of how the main program uses the decreasing counter:

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

* *Section 1 : Implementation of the Decrement() method

Implement the `Decrement()` method in the class body in such a way that it decrements the value variable of the object it's being called on by one. Once you're done with the Decrement() method, the main program of the previous example should work to produce the example output.

* Osa 2 : The counter's value cannot be negative

Improve the Decrement() in such a way that the counter's value never becomes negative. This means that if the value of the counter is 0, it cannot be decremented. A conditional statement is useful here.

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

* Osa 3: Resetting the counter value

Create the method `public void Reset()` for the counter that resets the value of the counter to 0. For example:

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

Create the class `Debt` that has double-typed instance variables of `balance` and `interestRate`. The balance and the interest rate are passed to the constructor as parameters `public Debt(double initialBalance, double initialInterestRate)`.

In addition, create the methods `public void PrintBalance()` and `public void WaitOneYear()` for the class. The method PrintBalance prints the current balance, and the WaitOneYear method grows the debt amount.

The debt is increased by multiplying the balance by the interest rate.

The class should do the following:

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

The example above illustrates the development of a mortgage with an interest rate of one percent.

Prints:

```console
120000
121200
147887.0328416936
```

</Exercise>

<Exercise title={'009 Dalmatian'}>

Create a class called `Dalmatian`. The dalmatian has instance variables `string name` and `int spots`. Both are set in the `public Dalmatian(string name, int spots)` constructor. 

<Note>
Also, give the variables ability for get and set:

Make the variables public rather than private, and add \{ get; set; \} on the declaring lines!
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

Create the class `Gauge`. The gauge has the instance `public int value`, a constructor without parameters (sets the initial value of the meter variable to 0), and also the following three methods:

- Method `public void Increase()` grows the value instance variable's value by one. It does not grow the value beyond five.
- Method `public void Decrease()` decreases the value instance variable's value by one. It does not decrease the value to negative values.
- Method `public bool Full()` returns `True` if the instance variable value has the value five. Otherwise, it returns `False`.

<Note>
Also, give the value ability for get and set:

Make the value public rather than private, and add \{ get; set; \} on the declaring lines!
</Note>

An example of the class in use.

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

The exercise template defines an Agent class, having a first name and last name. The Main method tries to print the introduction for mister Bond, but with no luck. This is what is should do:

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

Agent's ToString now returns an empty string. Fix it to introduce international agents in their proper form.

</Exercise>

<Exercise title={'012 Multiplier'}>

Create a class `Multiplier` that has a:

Constructor `public Multiplier(int number)`
Method `public int Multiply(int number)` which returns the value number passed to it multiplied by the number provided to the constructor.
You also need to create an instance variable in this exercise. When you call the method Multiply, store the changed value into the instance variable!

An example of the class in use:

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

<Note>The value stored in the objects is changed during the first calls!</Note>

The calculations are actually (in order):  
3 \* 2 = 6  
4 \* 2 = 8  
6 \* 1 = 6  
8 \* 1 = 8  
8 \* 3 = 24

</Exercise>

<Exercise title={'013 Statistics'}>

The exercise template includes class `Statistics`

```cpp
namespace Exercise013
{
  public class Statistics
  {
    public int count {get; set;}
    public int sum { get; set; }

    public NumberStatistics()
    {
      // initialize the variable count here
    }

    public void AddNumber(int number) {
        // write code here
    }
  }
}
```

The following program introduces the class' use:

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

Expand the program as follows:
- When a number is added, `count` is increased by one
- When a number is added, `sum` is increased by the number's value

</Exercise>

<Exercise title={'014 Payment card'}>

In this exercise, a class called PaymentCard is created which aims to mimic a cafeteria's payment process.

* Osa 1

The template includes the `Program.cs` and `PaymentCard.cs` files.

- Add a new class to the project called `PaymentCard` in the correct file.
- Fill in the PaymentCard object's constructor, which is passed the opening balance of the card, and which then stores that balance in the object's internal variable. 
- Fill in the ToString method, which will return the card's balance in the form "The card has a balance of X euros".

Here is the template for the PaymentCard:

```cpp
namespace Exercise014
{
  public class PaymentCard
  {
    private double balance;

    public PaymentCard(double openingBalance)
    {
      // write code here
    }

    public override string ToString()
    {
      // write code here
    }
  }
}
```
The following main program tests the class:

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

Expand your answer by adding two methods:
- Method `public void EatLunch()`
- Method `public void DrinkCoffee()`

The method `EatLunch` should decrease the card's balance by 10.60 euros. The method `DrinkCoffee` should decrease the card's balance by 2.0 euros.

The following main program tests the class:

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

xpand your previous answers, so that when an item is bought the balance is checked. If there is not enough money to buy, the balance does not change.

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

Notice how EatLunch did not change the balance, as there was not enough money. DrinkCoffee still worked, as it should.

* Osa 4

Expand your previous answers, so that you can charge money on your card:

```cpp
public void AddMoney(double amount) {
    // write code here
}
```

The purpose of the method is to increase the card's balance by the amount of money given as a parameter. However, the card's balance may not exceed 150 euros. As such, if the amount to be topped up exceeds this limit, the balance should, in any case, become exactly 150 euros.

The following main program tests the class:

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

<Note>You cannot add negative money!</Note>

</Exercise>