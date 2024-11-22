---
title: "Oliot listassa"
nav_order: 2
hidden: false
---

Listan parametri määrittää listan sisältämien muuttujien tyypin. Esimerkiksi `List<string>` sisältää merkkijonoja, `List<int>` kokonaislukuja ja `List<double>` liukulukuja.

Alla olevassa esimerkissä lisätään merkkijonoja listaan, jonka jälkeen listan merkkijonot tulostetaan yksi kerrallaan.


```cpp
List<string> names = new List<string>();

// merkkijono voidaan ensin tallentaa muuttujaan
string betty = "Betty Jennings";
// sitten lisätä listaan
names.Add(betty);

// merkkijonoja voidaan lisätä suoraan listaan:
names.Add("Betty Snyder");
names.Add("Frances Spence");
names.Add("Kay McNulty");
names.Add("Marlyn Wescoff");
names.Add("Ruth Lichterman");

// useita erilaisia toistorakenteita voidaan
// käyttää listan läpikäymiseen

// 1. while-silmukka ehdolla
int index = 0;
while (index < names.Count)
{
  Console.WriteLine(names[index]);
  index = index + 1;
}

// 2. for-silmukka indeksillä
for (int i = 0; i < names.Count; i++)
{
  Console.WriteLine(names[i]);
}

Console.WriteLine();
// 3. foreach-silmukka (ei indeksiä)
foreach (string name in names)
{
  Console.WriteLine(name);
}
```

## Olioiden lisääminen listaan

Merkkijonot ovat olioita, joten ei pitäisi tulla yllätyksenä, että listoissa voi olla myös muita olioita. Seuraavaksi tarkastellaan listojen ja olioiden yhteispeliä tarkemmin.

Oletetaan että meillä on käytössä alla oleva luokka, joka kuvaa henkilöä.

```cpp
public class Person
{
  public string name { get; }
  public int age { get; set; }
  public int weight { get; set; }
  public int height { get; set; }

  public Person(string name)
  {
    this.age = 0;
    this.weight = 0;
    this.height = 0;
    this.name = name;
  }

  public double BodyMassIndex()
  {
    double heigthPerHundred = this.height / 100.0;
    return this.weight / (heigthPerHundred * heigthPerHundred);
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


  public override string ToString()
  {
    return this.name + ", age " + this.age + " years";
  }
}
```

Olioiden käsittely listassa ei ole mitenkään erilaista kuin aiempi kokemuksemme listoista. Ainoa olennainen ero on vain se, että listaa luodessa määritellään talletettavien olioiden tyyppi.

Alla olevassa esimerkissä luodaan ensin lista, johon talletetaan Person-tyypin olioita, jonka jälkeen henkilöitä lisätään listaan. Lopuksi henkilö-oliot tulostetaan yksi kerrallaan.

```cpp
static void Main(string[] args)
{
  List<Person> persons = new List<Person>();

  // henkilö-olio voidaan luoda ensin
  Person john = new Person("John");
  // ja sitten lisätä listaan
  persons.Add(john);

  // henkilö-olioita voidaan luoda myös "samalla lauseella" kun ne lisätään listaan
  persons.Add(new Person("Matthew"));
  persons.Add(new Person("Martin"));

  foreach (Person person in persons)
  {
    Console.WriteLine(person);
  }
}
```

```console
John, age 0 years
Matthew, age 0 years
Martin, age 0 years
```

## Käyttäjän syöttämien olioiden lisääminen listaan

Aiemmin oppimamme rakenne syötteen lukemiseen on edelleen hyvin käyttökelpoinen.


```cpp
static void Main(string[] args)
{
  List<Person> persons = new List<Person>();

  // Lue henkilöiden nimet käyttäjältä
  while (true)
  {
    Console.Write("Enter a name, empty will stop: ");
    string name = Console.ReadLine();
    if (name == "")
    {
      break;
    }

    // Lisää listaan uusi henkilö
    // jonka nimi on edellinen käyttäjän syöte
    persons.Add(new Person(name));
  }

  // Tulosta syötettyjen henkilöiden lukumäärä, ja niiden yksilölliset tiedot
  Console.WriteLine();
  Console.WriteLine("Persons in total: " + persons.Count);
  Console.WriteLine("Persons: ");

  foreach (Person person in persons)
  {
    Console.WriteLine(person);
  }
}
```

```console
Enter a name, empty will stop: Matt
Enter a name, empty will stop: Mike
Enter a name, empty will stop: Bob
Enter a name, empty will stop: 

Persons in total: 3
Persons: 
Matt, age 0 years
Mike, age 0 years
Bob, age 0 years
```

## Monta konstruktorin parametria

Jos konstruktori vaatii useamman kuin yhden parametrin, voidaan käyttäjältä kysyä lisätietoja. Oletetaan, että luokalla **Person** on seuraava konstruktori.

```cpp
public class Person
{
  public string name { get; }
  public int age { get; set; }
  public int weight { get; set; }
  public int height { get; set; }

  public Person(string name, int age)
  {
    this.age = age;
    this.name = name;
    this.weight = 0;
    this.height = 0;
  }

  // Loput koodista on sama kuin aiemmin
}
```

Tässä tapauksessa olio luodaan kutsumalla kaksiparametrista konstruktoria.

Jos haluamme kysyä käyttäjältä tällaisia olioita, niin jokaiselta parametrilta täytyy kysyä erikseen. Esimerkissä alla kysytään ensin nimi ja sitten ikä. Tyhjä nimi lopettaa lukemisen.

Henkilöt tulostetaan sen jälkeen kun ne on luettu.


```cpp
static void Main(string[] args)
{
  List<Person> persons = new List<Person>();

  // Lue henkilöiden nimet käyttäjältä
  while (true)
  {
    Console.Write("Enter a name, empty will stop: ");
    string name = Console.ReadLine();
    if (name == "")
    {
      break;
    }

    // Lue henkilön ikä
    Console.Write("Enter the age of the person " + name + ": ");

    int age = Convert.ToInt32(Console.ReadLine());

    // Lisää listaan uusi henkilö
    // jonka nimi ja ikä ovat edellinen käyttäjän syötteet
    persons.Add(new Person(name, age));
  }

  // Tulosta syötettyjen henkilöiden lukumäärä, ja niiden yksilölliset tiedot
  Console.WriteLine();
  Console.WriteLine("Persons in total: " + persons.Count);
  Console.WriteLine("Persons: ");

  foreach (Person person in persons)
  {
    Console.WriteLine(person);
  }
}
```

```console
Enter a name, empty will stop: Mike Modeler 
Enter the age of the person Mike Modeler: 42
Enter a name, empty will stop: Nelson M
Enter the age of the person Nelson M: 1000
Enter a name, empty will stop: Harry Booter
Enter the age of the person Harry Booter: 1
Enter a name, empty will stop: 

Persons in total: 3
Persons: 
Mike Modeler, age 42 years
Nelson M, age 1000 years
Harry Booter, age 1 years
```

Yllä olevassa esimerkissä vaadittiin käyttäjältä tietoja rivi riviltä. Ei missään nimessä ole mahdotonta kysyä syötettä tietynlaisessa muodossa, esim. pilkulla eroteltuna.

Jos nimi ja ikä olisivat eroteltu pilkulla, niin ohjelma voisi toimia seuraavasti.


```cpp
static void Main(string[] args)
{
  List<Person> persons = new List<Person>();

  // Lue henkilön tiedot käyttäjältä
  while (true)
  {
    Console.WriteLine("Enter the person details separated by a comma, e.g.: Randall, 2");
    string details = Console.ReadLine();
    if (details == "")
    {
      break;
    }

    string[] parts = details.Split(",");
    string name = parts[0];
    int age = Convert.ToInt32(parts[1]);
    persons.Add(new Person(name, age));
  }

  // Tulosta syötettyjen henkilöiden lukumäärä, ja niiden yksilölliset tiedot
  Console.WriteLine();
  Console.WriteLine("Persons in total: " + persons.Count);
  Console.WriteLine("Persons: ");

  foreach (Person person in persons)
  {
    Console.WriteLine(person);
  }
}
```



```console
Enter the person details separated by a comma, e.g.: Randall, 2
Matt, 23
Enter the person details separated by a comma, e.g.: Randall, 2
Mike Pence, 3
Enter the person details separated by a comma, e.g.: Randall, 2


Persons in total: 2
Persons: 
Matt, age 23 years
Mike Pence, age 3 years
```

## Valikoiva tulostus listasta

Voit myös tarkastella listan sisältöä, kun käyt listaa läpi. Alla olevassa esimerkissä kysytään ensin ikärajaa, jonka jälkeen tulostetaan kaikki ne oliot, joiden ikä on vähintään käyttäjän antama luku.

```cpp
// Tehdään lista, jossa on pari henkilöä
List<Person> persons = new List<Person>();
persons.Add(new Person("Martin", 11));
persons.Add(new Person("Matthew", 12));

// Kysytään ikäraja
Console.Write("What is the age limit? ");
int ageLimit = Convert.ToInt32(Console.ReadLine());

// Tulostetaan vain ne, joiden ikä on vähintään ikäraja
foreach (Person person in persons) {
  if (person.age >= ageLimit)
  { 
    Console.WriteLine(person);
  }
}
```

```console
What is the age limit? 12
Matthew, age 12 years
```

# Tehtävät

<Exercise title={'015 Main class'}>

Täytä `Program`luokan metodi `Main`, joka kuvaillaan alla.

<Note>Älä muokkaa luokkaa Item</Note>

Kirjoita ohjelma, joka lukee käyttäjältä esineiden nimiä. Jos nimi on tyhjä, ohjelma lopettaa lukemisen. Muussa tapauksessa annettu nimi käytetään uuden esineen luomiseen, jonka lisäät sitten esineiden listaan.

Kun kaikki nimet on luettu, tulosta kaikki esineet käyttämällä Item-luokan ToString-metodia. Item-luokan toteutus pitää kirjaa esineen luomisajasta, lisäksi esineellä on nimi.

<Note>Listan nimen on pakko olla "items" jotta testit toimivat!</Note>

Esimerkkituloste:

```console
Name: Hammer
Name: Radio
Name: Hot Potato
Name: 

Hammer (created at: 9.2.2020 13.48.16)
Radio (created at: 9.2.2020 13.48.18)
Hot Potato (created at: 9.2.2020 13.48.21)
```

</Exercise>

<Exercise title={'016 Personal information'}>

Tässä kuvailtu ohjelma tulee toteuttaa `Program`luokan metodiin `Main`.

<Note>Älä muokkaa luokkaa PersonalInformation</Note>

Kun käyttäjä on syöttänyt kaikki tiedot, eli tyhjän merkkijonon, poistu toistorakenteesta.

Tulosta yksi tyhjä rivi selkeyden vuoksi.

Sitten tulosta kaikkien henkilöiden tiedot siten, että ne tulostetaan oikeassa formaatissa: etunimi ja sukunimi välilyönnillä erotettuna (älä tulosta henkilötunnusta). Esimerkki ohjelman toiminnasta on annettu alla:



```console
First name: 
> Jean 
Last name: 
> Bartik 
Identification number: 
> 271224 
First name: 
> Betty 
Last name: 
> Holberton 
Identification number: 
> 070317 
First name:
>

Jean Bartik 
Betty Holberton
```

Voit (ja kannattaa) pyytää henkilötunnusta merkkijonona.

</Exercise>

<Exercise title={'017 Television guide'}>

Tehtäväpohjassa on valmiina luokka `TelevisionProgram`, joka kuvaa televisio-ohjelmaa. Luokalla on oliomuuttujat `name` ja `duration`, konstruktori sekä muutama metodi.

Luo ohjelma (`Main` metodissa) joka lukee käyttäjältä televisio-ohjelmia ja niiden pituuksia. Kun käyttäjä syöttää tyhjän merkkijonon, lukeminen lopetetaan.

Tämän jälkeen käyttäjältä kysytään ohjelman maksimikestoa. Kun maksimikesto on saatu, ohjelma listaa kaikki ne ohjelmat, joiden kesto on pienempi tai yhtä suuri kuin maksimikesto.

Ohjelman tulee toimia kuten alla:

```console
Name: Rick and Morty 
Duration: 25 
Name: Two and a Half Men 
Duration: 30 
Name: Love it or list it 
Duration: 60 
Name: House 
Duration: 60
Name:

Program's maximum duration? 30 
Rick and Morty, 25 minutes 
Two and a Half Men, 30 minutes
```

</Exercise>

<Exercise title={'018 Book class'}>

<Note>Tämä tehtävä on 2 pisteen arvoinen, ilman erillisiä osioita.</Note>

Kirjoita ohjelma joka lukee käyttäjältä kirjoja. Kysyttäviin tietoihin kuuluu kirjan nimi, sivumäärä sekä julkaisuvuosi. Syötteen lukeminen lopetetaan kun käyttäjä syöttää tyhjän merkkijonon.

Tämän jälkeen käyttäjältä kysytään, mitä halutaan tulostaa. Jos käyttäjä antaa "everything", kaikki yksityiskohdat tulostetaan: kirjojen nimet, sivumäärät ja julkaisuvuodet. Jos käyttäjä antaa syötteen "title", vain kirjojen nimet tulostetaan. Jos tuloste on jotain muuta, ohjelma ei tulosta mitään.

- Toteuta luokka Book.
- Toteuta toiminnallisuus Main-metodissa.

Esimerkki ohjelman Main-metodin toiminnasta:

```console

Name: To Kill a Mockingbird 
Pages: 281 
Publication year: 1960 
Name: A Brief History of Time 
Pages: 256 
Publication year: 1988 
Name: Beautiful Code 
Pages: 593 
Publication year: 2007 
Name: The Name of the Wind 
Pages: 662 
Publication year: 2007 
Name:

What information will be printed? everything 
To Kill a Mockingbird, 281 pages, 1960 
A Brief History of Time, 256 pages, 1988 
Beautiful Code, 593 pages, 2007 
The Name of the Wind, 662 pages, 2007
```

```console
Name: To Kill a Mockingbird 
Pages: 281 
Publication year: 1960 
Name: A Brief History of Time 
Pages: 256 
Publication year: 1988 
Name: Beautiful Code 
Pages: 593 
Publication year: 2007 
Name: The Name of the Wind 
Pages: 662 
Publication year: 2007 
Name:

What information will be printed? title 
To Kill a Mockingbird 
A Brief History of Time 
Beautiful Code 
The Name of the Wind
```
</Exercise>