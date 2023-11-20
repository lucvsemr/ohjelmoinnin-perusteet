---
title: "Olioiden kertausta"
nav_order: 1
hidden: false
---

Mistä olio-ohjelmoinnissa onkaan kyse? Kelataan vähän taaksepäin.

Tarkastellaan, kuinka kello toimii. Kellolla on kolme viisaria: tuntiviisari, minuuttiviisari ja sekuntiviisari. Sekuntiviisari etenee yhden sekunnin välein, minuuttiviisari 60 sekuntin välein ja tuntiviisari 60 minuutin välein. Kun sekuntiviisarin arvo on 60, sen arvo asetetaan nollaksi ja minuuttiviisarin arvoa kasvatetaan yhdellä. Kun minuuttiviisarin arvo on 60, sen arvo asetetaan nollaksi ja tuntiviisarin arvoa kasvatetaan yhdellä. Kun tuntiviisarin arvo on 24, se asetetaan nollaksi.

Aika esitetään aina muodossa **tunnit:minuutit:sekunnit**, missä tunnit on kahden numeron muodossa (esim. 01 tai 12), minuutit kahden numeron muodossa ja sekunnit myös kahden numeron muodossa.

Alla on toteutus kellosta kokonaislukumuuttujien avulla (tulostus voisi olla eristetty omaan metodiinsa, mutta sitä ei ole tässä tehty).

```cpp
static void Main(string[] args)

int hours = 0;
int minutes = 0;
int seconds = 0;

while (true)
{
  // 1. Ajan tulostus
  if (hours < 10)
  {
    Console.Write("0");
  }
  Console.Write(hours);

  Console.Write(":");

  if (minutes < 10)
  {
    Console.Write("0");
  }
  Console.Write(minutes);

  Console.Write(":");

  if (seconds < 10)
  {
    Console.Write("0");
  }
  Console.Write(seconds);
  Console.WriteLine();

  // 2. Sekuntiviisarin liike
  seconds = seconds + 1;

  // 3. Muiden viisareiden liike kun se on tarpeellista
  if (seconds > 59)
  {
    minutes = minutes + 1;
    seconds = 0;

    if (minutes > 59)
    {
      hours = hours + 1;
      minutes = 0;

      if (hours > 23)
      {
        hours = 0;
      }
    }
  }
}
```

Kuten yllä on demonstroitu, kolmen kokonaislukumuuttujan avulla toteutetun kellon toiminta ei ole kovin selkeää. Ohjelmakoodia lukiessa ei oikein "näe", mitä tapahtuu. Tunnettu [**ohjelmistokehittäjä**](https://fi.wikipedia.org/wiki/Kent_Beck) on joskus todennut *"Any fool can write code that a computer can understand. Good programmers write code that humans can understand"*.

Tarkoitus on tehdä ohjelmasta ymmärrettävämpi.

Koska kellon viisari on itsessään selkeä konsepti, hyvä idea ohjelman ymmärrettävyyden kannalta olisi tehdä siitä oma luokkansa. Tehdään **ClockHand**-luokka, joka kuvaa kelloviisaria, joka sisältää tietoa sen arvosta, ylärajasta (eli kohdasta, jossa viisarin arvo palaa nollaan) ja tarjoaa metodeja viisarin eteenpäin siirtämiseen, arvon katsomiseen ja arvon tulostamiseen merkkijonona.


```cpp
public class ClockHand
{
  public int value { get; set; }
  public int limit { get; set; }

  public ClockHand(int limit)
  {
    this.limit = limit;
    this.value = 0;
  }

  public void Advance()
  {
    this.value = this.value + 1;

    if (this.value >= this.limit)
    {
      this.value = 0;
    }
  }

  public override string ToString()
  {
    if (this.value < 10)
    {
      return "0" + this.value;
    }

    return "" + this.value;
  }
}
```

Kun olemme luoneet luokan ClockHand, kellostamme tulee selkeämpi. Nyt kellon, eli viisareiden, tulostaminen on suoraviivaista, ja viisareiden eteneminen on piilotettu ClockHand-luokkaan. Koska viisarin paluu alkuun tapahtuu automaattisesti ClockHand-luokan määrittelemän ylärajamuuttujan avulla, viisareiden yhteistoiminta on hieman erilaista kuin kokonaislukumuuttujien avulla toteutetussa ohjelmassa. Kokonaislukumuuttujia käyttävä ohjelma tarkasteli, ylittyikö viisaria kuvaavan kokonaisluvun arvo ylärajan, jonka jälkeen sen arvo asetettiin nollaksi ja seuraavaa viisaria kuvaavan kokonaisluvun arvoa kasvatettiin. Kelloviisareiden ollessa kyseessä minuuttiviisari etenee, kun sekuntiviisarin arvo on nolla, ja tuntiviisari etenee, kun minuuttiviisarin arvo on nolla.


```cpp
static void Main(string[] args)
{
  ClockHand hours = new ClockHand(24);
  ClockHand minutes = new ClockHand(60);
  ClockHand seconds = new ClockHand(60);

  while (true)
  {
    // 1. Tulostetaan aika
    Console.WriteLine(hours + ":" + minutes + ":" + seconds);

    // 2. Edistetään sekuntiviisaria
    seconds.Advance();

    // 3. Edistetään muita viisareita kun tarpeellista
    if (seconds.value == 0)
    {
      minutes.Advance();

      if (minutes.value == 0)
      {
        hours.Advance();
      }
    }
  }
```

**Olio-ohjelmointi on pääasiassa erilaisten käsitteiden eristämistä omiin kokonaisuuksiinsa eli abstraktioiden luomista.** Edellisessä esimerkissä saattaa tuntua turhalta luoda olio, joka sisältää vain yhden kokonaisluvun, koska saman asian voisi tehdä suoraan kokonaislukumuuttujilla. Näin ei kuitenkaan ole aina.

Konspetin erottaminen omaan luokkaansa on monella tapaa hyvä idea. Ensinnäkin tiettyjä yksityiskohtia (kuten käsien pyörittäminen) voidaan piilottaa luokan sisälle eli **abstrahoida**. Käyttäjän ei tarvitse kirjoittaa if-lausetta ja sijoitusoperaatiota, vaan kellokäden käyttäjän tarvitsee kutsua selkeästi nimettyä metodia **Advance()**. Tuotettua kellokättä voidaan käyttää myös rakennuspalikkana muissa ohjelmissa - luokka voisi olla esimerkiksi nimeltään **CounterLimitedFromTop**. Eli erillisen käsitteen luomalla luokalla voi olla useita käyttötarkoituksia. Toinen valtava etu on, että koska kellokäden toteutuksen yksityiskohdat eivät ole käyttäjän nähtävillä, niitä voidaan muuttaa haluttaessa.

Ymmärsimme kellon sisältävän kolme viisaria, eli se koostuu kolmesta käsitteestä. Itse asiassa kello on käsite sinänsä. Eli voimme luoda siitäkin luokan. Seuraavaksi luomme luokan **Clock**, joka piilottaa sisäänsä kellon viisarit.


```cpp
public class Clock
{
  private ClockHand hours;
  private ClockHand minutes;
  private ClockHand seconds;

  public Clock()
  {
    this.hours = new ClockHand(24);
    this.minutes = new ClockHand(60);
    this.seconds = new ClockHand(60);
  }

  public void Advance()
  {
    this.seconds.Advance();

    if (this.seconds.value == 0)
    {
      this.minutes.Advance();

      if (this.minutes.value == 0)
      {
        this.hours.Advance();
      }
    }
  }

  public override string ToString()
  {
    return hours + ":" + minutes + ":" + seconds;
  }
}
```

Täten ohjelmistomme toiminta tulee entistä selkeämmäksi. Kun vertaamme alla olevaa ohjelmaa alkuperäiseen joka toimi kokonaisluvuilla, huomaammekin, että ohjelman luettavuus on aivan eri tasolla.


```cpp
static void Main(string[] args)
{
  Clock clock = new Clock();

  while (true)
  {
    Console.WriteLine(clock);
    clock.Advance();
  }
}
```

Toteuttamamme kello on olio jonka toiminto perustuu "yksinkertaisempiin" olioihin eli kellon viisareihin. Tämä on juuri **se hieno idea, joka olio-ohjelmoinnissa on: ohjelma rakentuu pienistä ja erillisistä olioista, jotka toimivat yhdessä**.

## Olio

**Olio** viittaa itsenäiseen entiteettiin jolla on dataa (instanssimuuttujat) ja käyttäytymistä (metodit) liitettynä siihen. Oliot voivat erota rakenteeltaan ja toiminnaltaan paljonkin: toiset kuvaavat ongelma-aluetta ja toiset koordinoivat eri olioiden välistä vuorovaikutusta. Oliot vuorovaikuttavat keskenään metodikutsujen avulla - metodikutsuja käytetään sekä tiedon pyytämiseen oliolta että ohjeiden antamiseen sille. Yleisesti ottaen jokaisella oliolla on selkeästi määritellyt rajat ja käyttäytyminen, ja jokainen olio tietää vain ne oliot, joita se tarvitsee tehtävänsä suorittamiseen. Toisin sanoen olio piilottaa sisäiset toimintonsa ja tarjoaa käyttöliittymän käyttäytymiseen selkeästi määriteltyjen metodien avulla. Lisäksi olio on riippumaton niistä olioista, joita se ei tarvitse tehtävänsä suorittamiseen.

Edellisessä osassa käsittelimme olioiden kuvausta henkilöiden avulla, jotka oli määritelty "Person" luokassa. Kertauksen vuoksi on hyvä muistaa luokan tarkoitus: **luokka** sisältää tarvittavan rakenteen olioiden luomiseen, ja määrittelee myös olioiden muuttujat ja metodit. Olio luodaan luokan konstruktorin perusteella.

Henkilö-oliollamme oli nimi, ikä, paino ja pituus, sekä muutama metodi. Jos mietimme henkilö-olion rakennetta enemmän, voisimme keksiä sille lisää henkilöön liittyviä muuttujia, kuten henkilötunnuksen, puhelinnumeron, osoitteen ja silmien värin.

Todellisuudessa henkilöön liittyy kaikenlaista tietoa ja asioita. Kuitenkin kun rakennamme sovellusta, joka käsittelee henkilöitä, **henkilöön liittyvä toiminnallisuus ja ominaisuudet kerätään sovelluksen käyttötarkoituksen mukaan**. Esimerkiksi elämänhallinta-sovellus voisi pitää kirjaa edellä mainitusta iästä, painosta ja pituudesta, ja tarjota mahdollisuuden laskea painoindeksi ja maksimisyke. Toisaalta viestintään keskittyvä sovellus tallentaisi henkilöiden sähköpostiosoitteet ja puhelinnumerot, mutta ei tarvitsisi painoa tai pituutta.

**Olion tila** on sen sisäisten muuttujien arvo tietyllä hetkellä.

Esimerkissämme henkilö-olio (Person) jolla on nimi, ikä, paino ja pituus, ja metodit jotka mahdollistavat painoindeksin (englanniksi body mass index, BMI) sekä maksimisykkeen (maximum heart rate) laskemisen, näyttää seuraavalta. Alla pituus ja paino on ilmaistu liukulukuina - pituuden yksikkö on metri.

```cpp
public class Person
{
  private string name;
  private int age;
  private double weight;
  private double height;

  public Person(string name, int age, double weight, double height)
  {
    this.age = age;
    this.name = name;
    this.weight = weight;
    this.height = height;
  }

  public double BodyMassIndex()
  {
    return this.weight / (this.height * this.height);
  }

  public double MaximumHeartRate()
  {
    return 206.3 - (0.711 * this.age);
  }

  public void GrowOlder()
  {
    if (this.age < 100)
    {
      this.age = this.age + 1;
    }
  }

  public override string ToString()
  {
    return this.name + ", BMI: " + this.BodyMassIndex()
          + ", maximum heart rate: " + this.MaximumHeartRate();
  }
}
```

Maksimisykkeen ja painoindeksin laskeminen onnistuu helposti Person-luokan avulla.


```cpp
static void Main(string[] args)
{
  Console.WriteLine("What's your name?");
  string name = Console.ReadLine();
  Console.WriteLine("What's your age?");
  int age = Convert.ToInt32(Console.ReadLine());
  Console.WriteLine("What's your weight?");
  double weight = Convert.ToDouble(Console.ReadLine());
  Console.WriteLine("What's your height?");
  double height = Convert.ToDouble(Console.ReadLine());

  Person person = new Person(name, age, weight, height);
  Console.WriteLine(person);
}
```

```console
What's your name?
Laura Palmer
What's your age?
21
What's your weight?
50.4
What's your height?
173.4
Laura Palmer, BMI: 0.0016762251409825073, maximum heart rate: 191.369
```

## Luokka

Luokka määrittelee olioiden rakenteen. Se sisältää olioiden sisäiset muuttujat jotka kuvaavat olion dataa, konstruktorin tai konstruktoreita joilla olioita luodaan, sekä metodit jotka kuvaavat niiden toimintaa. Rectangle-luokka (suorakaide) kuvattuna alla on hyvä esimerkki luokasta.

```cpp
// luokka
public class Rectangle
{

  // instanssimuuttujat
  private int width;
  private int height;

  // konstruktori
  public Rectangle(int width, int height)
  {
    this.width = width;
    this.height = height;
  }

  // metodit
  public void Widen()
  {
    this.width = this.width + 1;
  }

  public void Narrow()
  {
    if (this.width > 0)
    {
      this.width = this.width - 1;
    }
  }

  public int SurfaceArea()
  {
    return this.width * this.height;
  }

  public override string ToString()
  {
    return "(" + this.width + ", " + this.height + ")";
  }
}
```

Jotkin metodit yllä eivät palauta arvoja (metodit joissa on määritelty avainsana void), kun taas toiset palauttavat (metodit joissa on määritelty palautettavan arvon tyyppi). Luokka määrittelee myös toString-metodin, joka palauttaa olion tulostamiseen käytettävän merkkijonon.

Oliot luodaan luokan konstruktorin avulla käyttämällä avainsanaa new. Alla luodaan kaksi suorakaide-oliota ja tulostetaan niiden tietoja.


```cpp
static void Main(string[] args)
{
  Rectangle first = new Rectangle(40, 80);
  Rectangle rectangle = new Rectangle(10, 10);
  Console.WriteLine(first);
  Console.WriteLine(rectangle);

  first.Narrow();
  Console.WriteLine(first);
  Console.WriteLine(first.SurfaceArea());
}
```

```console
(40, 80)
(10, 10)
(39, 80)
3120
```

# Tehtävät

<Exercise title={'001 One minute'}>

Tehtäväpohjassa on valmiina materiaalissa esitelty `ClockHand`-luokka. Toteuta ajastin, eli `Timer`-luokka materiaalissa esiteltyä `Clock`-luokkaa hyödyntäen.

Ajastimessa on kaksi viisaria, yksi sadasosasekunteille ja toinen sekunneille. Kun ajastin etenee, sadasosasekuntiviisari etenee yhdellä. Kun sadasosasekuntiviisarin arvo saavuttaa arvon 100, sen arvo asetetaan nollaksi ja sekuntiviisarin arvo kasvaa yhdellä. Vastaavasti kun sekuntiviisarin arvo saavuttaa arvon 60, sen arvo asetetaan nollaksi.

- `public Timer()` luo uuden ajastimen.
- `public override string ToString()` palauttaa ajastimen merkkijonoesityksen. Tämän tulisi olla muodossa "sekuntit: sadasosasekuntit", jossa molemmat esitetään aina kahdella numerolla. Esimerkiksi "19:83" edustaa aikaa 19 sekuntia, 83 sadasosaa.
- `public void Advance()` edistää ajastinta yhdellä sadasosasekunnilla.

Voit kokeilla ajastimen toimintaa pääohjelmassa halutessasi. Alla oleva esimerkkikoodi tarjoaa sinulle ohjelman, jossa ajastin tulostetaan ja se etenee yhdellä sadasosasekunnilla.


```cpp
static void Main(string[] args)
{
  // Luo uusi ajastin
  Timer timer = new Timer();
  // Silmukka joka etenee niin kauan kunnes se keskeytetään
  // Voit keskeyttää silmukan yhdistelmällä CTRL + C
  while (true)
  {
    Console.WriteLine(timer);
    timer.Advance();
    // Vähän virheenkorjausta, tämä käsitellään myöhemmin
    // Tunnetaan nimellä try-catch
    try
    {
      // Odota sadasosasekunti
      // Sleep(1000) odottaa yhden sekunnin, jos haluat testata hitaammalla tahdilla. 
      System.Threading.Thread.Sleep(10);
    }
    // Try-catch:n toinen puoli.
    // Tämäkin käsitellään myöhemmin. 
    catch (Exception e)
    {
      Console.WriteLine("Error happened: +" + e);
    }
  }
}
```

</Exercise>

<Exercise title={'002 Cube'}>

Luo luokka kuutiolle, eli `Cube`-luokka. Luo konstruktori `public Cube(int edgeLength)`, joka ottaa kuution sivun pituuden parametrinaan.

Luo metodi `public int Volume()`, joka laskee ja palauttaa kuution tilavuuden. Kuution tilavuus lasketaan kaavalla `edgeLength * edgeLength * edgeLength`. Lisäksi luo metodi `public override string ToString()`, joka palauttaa kuution merkkijonoesityksen. Merkkijonoesityksen tulee olla muodossa "The length of the edge is l and the volume v", jossa `l` on sivun pituus ja `v` on tilavuus - molemmat kokonaislukuina.

</Exercise>

<Exercise title={'003 Fitbyte'}>

[**Karvosen kaava**](https://fi.wikipedia.org/wiki/Karvosen_kaava) antaa laskukaavan tavoitesykkeelle (target heart rate) harjoittelun aikana. Tavoitesyke lasketaan kaavalla `(maximum heart rate - resting heart rate) * (target heart rate percentage) + resting heart rate`, missä tavoitesyke annetaan prosenttina maksimisykkeestä (maksimum heart rate).

Esimerkiksi, jos henkilön maksimisyke on 200, leposyke 50 ja tavoitesyke 75% maksimisykkeestä, tavoitesyke on noin ((200-50) * (0.75) + 50), eli 162.5 lyöntiä minuutissa.

Luo "harjoitusavustaja", tai ennemmin luokka `FitByte`. Sen konstruktori ottaa parametreina iän ja leposykkeen.  Harjoitusavustajan tulee tarjota metodi `TargetHeartRate`, jolle annetaan parametrina prosentuaalinen osuus maksimisykkeestä (doublena), arvo välillä 0-1. Luokan tulee sisältää:

- Konstruktori `public Fitbyte(int age, int restingHeartRate)`
- Metodi `public double TargetHeartRate(double percentageOfMaximum)`, joka laskee ja palauttaa tavoitesykkeen.

Käytä kaavaa 206.3 - (0.711 \* age) maksimisykkeen laskemiseen.
Käytä kaavaa (maxHeartRate - restingHeartRate) \* percentageOfMaximum + restingHeartRate tavoitesykkeen laskemiseen.

Esimerkki:


```cpp
public static void Main(string[] args)
{
  Fitbyte assistant = new Fitbyte(30, 60);
  double percentage = 0.5;

  while (percentage < 1.0)
  {
    double target = assistant.TargetHeartRate(percentage);
    Console.WriteLine("Target " + (percentage * 100) + "% of maximum: " + target);
    percentage = percentage + 0.1;
  }
}
```

```console
Target 50% of maximum: 122.48500000000001
Target 60% of maximum: 134.98200000000003
Target 70% of maximum: 147.479
Target 80% of maximum: 159.976
Target 89.99999999999999% of maximum: 172.473
Target 99.99999999999999% of maximum: 184.97000000000003
```

</Exercise>