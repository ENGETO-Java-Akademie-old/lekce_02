<p align="center">
  <img src="https://engeto.cz/wp-content/uploads/2019/01/engeto-square.png" width="200" height="200">
</p>

# Java - 2. lekce

## Co bychom měli mít hotové

 - Po první hodině bychom měli mít zprovozněné vývojové prostředí a umět si v něm vytvořit projekt.
 
 - Měli bychom vědět, co je to proměnná, jak se vytváří a jak se s ní pracuje.
 
 - Měli bychom vědět, co je to datový typ, mít ponětí o tom, že máme dvě skupiny datových typů (primitivní a referenční), vědět, čím se liší a co znamená, že Java je silně typovaný programovací jazyk.
 
 - Měli bychom znát základní operátory, umět z nich sestavit výraz, který bude představovat námi požadovaný výpočet.

## Co nás čeká

- [Třídy a jejich atributy](#třídy-a-jejich-atributy)

- [Konstruktory](#konstruktory)

- [Metody](#metody)

- [Konvence](#konvence)

- [Výčtové typy](#výčtové-typy)

## Třídy a jejich atributy

V první lekci jsme si řekli, že co to jsou datové typy a že je jich teoreticky nekonečno ač jsme si jich ukázali pouze deset. Ty datové typy by nám stačily, když bychom si chtěli uložit jednu zprávu (String), nebo provést jednoduchý výpočet, ale co když budeme chtít v programu pracovat s něčím složitějším? Třeba s automobily. U každého auta budeme v rámci našeho programu chtít evidovat několik základních údajů - značku, model, rok výroby, SPZ, výkon motoru a datum příští technické kontroly.

Jistě, šlo by to udělat nějak takto:

```java
String auto1 = "Škoda, Rapid, 2015, 4B7 2233, 64kW, 3.7.2021";
String auto2 = "Hyundai, i30, 2018, 8B8 0999, 88kW, 15.11.2022";
```

Ale co pak, když s těmi údaji budeme chtít pracovat? Budeme pořád dokola rozparsovávat ten String, ve kterém máme uložené všechny údaje, abychom našli datum příští technické kontroly? 
Nebo takto:

```java
String znackaPrvnihoAuta = "Škoda";
String modelPrvnihoAuta = "Rapid";
short rokVyrobyPrvnihoAuta = 2015;
String spzPrvnihoAuta = "4B7 2233";
short vykonPrvnihoAutaVkW = 64;
LocalDate datumPristiTechnickeKontrolyDruhehoAuta = LocalDate.of(2021, 7, 3);
String znackaDruhehoAuta = "Hyundai";
String modelDruhehoAuta = "i30";
short rokVyrobyDruhehoAuta = 2018;
String spzDruhehoAuta = "8B8 0999";
short vykonDruhehoAutaVkW = 88;
LocalDate datumPristiTechnickeKontrolyDruhehoAuta = LocalDate.of(2022, 11, 15);
```

A co když si pořídíme další auto? Nebo jedno prodáme? Budeme mazat / přidávat proměnné do našeho programu vždy, když se něco takového stane?

<b>Ne</b>. Je tu lepší cesta. A ta se jmenuje třída (class). Třída v Javě představuje popis nějakého objektu - údajů, které o něm uchováváme (atributy), věcí, které s ním můžeme provést (metody) a způsobů, jak jej můžeme vytvořit (konstruktory).

V našem případě by třída pro uložení těch údajů o autě, které jsme si vypsali, mohla vypadat takto.
```java
import java.time.LocalDate;

public class Auto {

  private String znacka;
  private String model;
  private short rokVyroby;
  private String spz;
  private short vykonVkW;
  private LocalDate datumPristiTechnickeKontroly;

}
```

A voilá, máme třídu, kterou dokážeme dokonale popsat naše auta.

Naše třída referenčním datovým typem, což vysvětluje tu narážku na takřka nekonečný počet datových typů - referenční datové typy jsme totiž schopni si vytvářet sami a když máme datový typ, tak nám nic nebrání v tom, abychom si vytvořili proměnnou, které bude právě tohoto datového typu.

```java
private Auto naseFaro;
```

Super. Máme proměnnou naseFaro s datovým typem Auto, ale co dál? Do proměnné s datovým typem int si přiřadíme celé číslo, do proměnné s datovým typem String zase nějaký řetězec, ale co přiřadit sem? Nebo, lépe řečeno, jak si to naše auto vytvořit?

```java
private int naseCislo = 7;
private String nasRetezec = "Auta jsou cool.";
private Auto naseAuto = Javo, prosim, prosim, vyrob nam auto; //tak tohle nám fungovat nebude
```

Pro vytváření jednotlivých instancí tříd, v našem případě tedy jednotlivých aut, mají třídy tzv. konstruktory.

## Konstruktory

Konstruktory nám umožňují vytvářet jednotlivé instance dané třídy. Tedy pokud tu naši třídu Auto rozšíříme o konstruktor:

```java
import java.time.LocalDate;

public class Auto {

  private String znacka;
  private String model;
  private short rokVyroby;
  private String spz;
  private short vykonVkW;
  private LocalDate datumPristiTechnickeKontroly;

  public Auto() {
  
  }

}
```

tak budeme moct napsat toho:

```java
private Auto naseAuto = new Auto();
```

čímž si vytvoříme novou instanci té třídy auto představující to naše auto a uložíme si ji do proměnné naseAuto.

Než pokročíme dál, tak si uvedeme několik pravidel:

 - zápis každého konstruktoru začíná vždy klíčovým slovem specifikujícím jeho viditelnost (public, protected, private) - pokud bychom žádné klíčové slovo neuvedli, tak se použije defaultní: package-private, následuje název té třídy, pro kterou konstruktor vytváříme, jednoduché závorky, ve kterých můžou být uvedeny parametry a nakonec složené závorky ohraničující tělo konstruktoru představující akce, které se provedou při vytvoření nové instance té třídy (vějšinou jde o vhodné naplnění atributů hodnotami, které si předáme jako parametry konstruktoru)
 
 - pakliže třídě sami nespecifikujeme aspoň jeden konstruktor, tak se jí při kompilaci vytvoří defaultní konstruktor, který je public, nemá žádné parametry a nic ve svém těle neprovádí (pro naši třídu Auto by tedy vypadal úplně stejně jako ten, který jsme si vytvořili my sami)
 
 - třída může mít víc konstruktorů, ale všechny se musí lišit v parametrech - nastačí jen v názvech parametrů, ale musí se lišit v datových typech parametrů
 
 - v těle konstruktoru můžeme zavolat jiný konstruktor
 
 Řekli jsme si, že v konstruktoku jsme schopni si nastavit hodnoty atributů na nějaké "vhodné" hodnoty a že jsme schopni si tyto "vhodné" hodnoty předat jako parametry konstruktoru, a protože těžko budeme do našeho systému přidávat nové auto, aniž bychom o něm věděli aspoň základní údaje, tak si můžeme vytvořit nějaký vhodnější konstruktor.
 
 Řekněme, že vždy víme, že o jakou půjde značku, model, jak výkoný motor má a kdy bylo vyrobené, ale třeba ještě nemusí být přihlášené, tak nemusíme znát SPZ a datum příští technické kontroly.
 
 Naše třída Auto by mohla vypadat nějak takto:
 
 ```java
 import java.time.LocalDate;

public class Auto {

  private String znacka;
  private String model;
  private short rokVyroby;
  private String spz;
  private short vykonVkW;
  private LocalDate datumPristiTechnickeKontroly;

  public Auto(String znacka, String model, short rokVyroby, short vykon) {
    this.znacka = znacka;
    this.model = model;
    this.rokVyroby = rokVyroby;
    vykonVkW = vykon;
  }

}
 ```

Každý parametr konstruktoru má vždy specifikované dvě věci - datový typ a jméno, pomocí kterého s tímto parametrem v konstruktoru pracujeme. Je možné, aby se naše parametry jmenovaly stejně, jako atributy naší třídy, ale pak platí, že vždy, když v konstruktoru někde použijeme toto jméno, tak se odkážeme na parametr, protože jde o nejbližší výskyt - pokud bychom chtěli přistoupit ke stejně pojmenovanému atributu, museli bychom použít klíčové slovo this, které v rámci konstruktorů a metod představuje odkaz na daný objekt, jehož konstruktor nebo metoda je volána a následně bychom se ke kontrétnímu atributu tohoto objektu dostali pomocí tečkové notace - <b>this.jmenoAtributu</b>.
Pokud ale máme jinak pojmenované atributy a parametry konstruktoru, tak klíčové slovo this používat nemusíme - viz náš příklad a přiřazení parametru vykon do atributu vykonVkW.

Řekli jsme si, že jedna třída může mít i víc konstruktrorů - řekněme, že pracujeme stejně často s auty, která právě sjela z výrobní linky jako s těmi, která jsou už jsou přihlášená a mají SPZku a technickou.

Naše třída by pak vypadala nějak takto:

```java
 import java.time.LocalDate;

public class Auto {

  private String znacka;
  private String model;
  private short rokVyroby;
  private String spz;
  private short vykonVkW;
  private LocalDate datumPristiTechnickeKontroly;

  public Auto(String znacka, String model, short rokVyroby, short vykon) {
    this.znacka = znacka;
    this.model = model;
    this.rokVyroby = rokVyroby;
    this.vykon = vykon;
  }

  public Auto(String znacka, String model, short rokVyroby, String spz, short vykon,
              LocalDate datumPristiTechnickeKontroly) {
    this.znacka = znacka;
    this.model = model;
    this.rokVyroby = rokVyroby;
    this.spz = spz;
    this.vykon = vykon;
    this.datumPristiTechnickeKontroly = datumPristiTechnickeKontroly;
  }

}
```

Nemohli bysme ale mít třeba takovéto konstruktory, protože se liší pouze názvem parametrů.

```java
public class Auto {

  private String znacka;
  private String model;

  public Auto(String znacka) {
    this.znacka = znacka;
  }

  public Auto(String model) {
    this.model = model;
  }

}
```

Protože při volání konstruktoru pouze spefikujeme hodnoty parametrů..

```java
Auto naseAuto = new Auto("Mercedes");
```
Java se podívála na datové typy parametrů, které jsme předali, což je jeden String a podle toho by chtěla vybrat odpovídající konstruktor - my tu máme ale dva takové a Java nedovede rozlišit, jestli jsme mysleli zmečku nebo model a proto není vůbec umožněno vytvářet konstruktory (a ani jiné metody), které by se lišily pouze v názvu parametrů.

Řekli jsme si také, že můžeme volat jeden konstruktor v druhém - to se nám může hodit, když máme konstruktory, které se liší jen drobně a zároveň v těle obsahují stejný kód - pak by šlo naše dva konstruktory zapsat takto, čímž bychom ušetřili několik řádků kódu.

```java
 import java.time.LocalDate;

public class Auto {

  private String znacka;
  private String model;
  private short rokVyroby;
  private String spz;
  private short vykonVkW;
  private LocalDate datumPristiTechnickeKontroly;

  public Auto(String znacka, String model, short rokVyroby, short vykon) {
    this(znacka, model, rokVyroby, null, vykon, null);
  }

  public Auto(String znacka, String model, short rokVyroby, String spz, short vykon,
              LocalDate datumPristiTechnickeKontroly) {
    this.znacka = znacka;
    this.model = model;
    this.rokVyroby = rokVyroby;
    this.spz = spz;
    this.vykon = vykon;
    this.datumPristiTechnickeKontroly = datumPristiTechnickeKontroly;
  }

}
```

Zde je důležité si zapamtovat jedno pravidlo - pokud voláme konstruktor v konstruktoru, tak jej voláme jako <b>this(parametr1, parametr2, parametr3)</b> a ne jako <b>JmenoTridy(parametr1, parametr2, parametr3)</b>.

## Metody

Umíme si vytvořit instanci nějaké třídy a pomoci vlastního konstruktoru umíme i nastavit výchozí hodnoty atributům naší třídy, ale k čemu by nám to bylo, pokud bychom se k atributům už nijak nedostali? K ničemu.

Pokud by atributy měly modifikátor viditelnosti public, tak bychom se k nim mohli dostat pomocí tečkové notace takto:

```java
Auto naseFaro = new Auto("BMW", "M235i");
System.out.println(naseFaro.znacka);
```

To by sice fungovalo, ale porušili bychom tím základní koncept Javy - <b>zapouzdření</b>, které říká, že vnitřní stav objektu (jeho atributy) by měl být ukryt před okolím a s objektem bychom měli interagovat jen pomocí rozhraní - metod, které daný objekt nabízí.

Víme tedy, jak to nedělat, tak pojďme ukázat, jak je to správně.

Přístup k atributům nějaké třídy je něco natolik rozšířeného, že pro něj existuje nejen konvence, ale velmi často i klávesová zkratka ve vývojovém studiu, která tyto metody pro práci s atributy vygeneruje za nás - Idea v tomto případě není výjimkou - klávesová zkratka pro jejich vygenerování je: <b>Alt + Insert</b>.

Před tím, než si ale podíváme na konkrétní metody k získávání a nastavování atributů - tzv. gettery a settery, se podíváme, jak vlastně metoda vypadá:

```java
modifikátorViditelnosti návratovýTyp jménoMetody(datovýTypPrvníhoParametru jménoPrvníhoParametru,
      datovýTypDruhéhoParametru jménoDruhéhoParametru) {
  // zde je tělo naší metody, které obsahuje samotný kód - říká, co vlastně naše bude dělat, když ji zavoláme
}
```

- <b>Modifikátor viditelnosti</b> - říká, stejně jako jsme si už řekli u proměnných, to, odkud půjde tato metoda vidět a tedy zavolat - můžeme opět použít ty stejné, jako u proměnných (public, protected, private)

- <b>Návratový typ</b> - specifikuje, jaký datový typ bude mít výsledek, který nám metoda vrátí - může jít buď nějakáý z datových typů, který jsme si už zmínili, nebo o klíčové slovo <b>void</b>, které říká, že tato metoda nevrací žádný výsledek

- <b>Jméno metody</b> - jméno metody, pomocí kterého tuto metodu budeme volat - je zde stejná konvence, jako v případě proměnných - camel case a jméno metody my mělo popisovat, co metoda sama dělá

- <b>Paramtery</b> - stejně jako konstruktory, i metody mohou, ale nemusí mít parametry - u nich vždy specifikujeme jejich datový typ a jméno, pomocí kterého s tímto parametrem pak pracujeme v těle metody

- <b>Tělo metody</b> - tělo metody již obsahuje samotný kód - výpočty, výpisy, přiřazení - tělo může také obsahovat volání jiných metod

Teď, když se víme, z čeho se skládá definice metody, se můžeme podívat na dvě metody pro práci s atributy.

```java
public class Auto {

  private String brand;
  
  public Auto(String brand) {
    this.brand = brand;
  }
  
  public String getBrand() {
    return brand;
  }

  public void setBrand(String brand) {
    this.brand = brand;
  }

}
```

Metoda pro získání hodnoty nějakého atributu má vždy návratový typ odpovídající datovému typu atributu, který získáváme, v našem případě String, její název začíná slovem get a za ním následuje jméno atributu - s tím, že celý název metody je psaný v camel case a tedy i když jméno našeho atributu začíná malým písmenem, tak v názvu metody bude začínat velkým. Pak následují paramtetry - tím, že pouze získáváme hodnotu atributu, nedává smysl si předávat nějaký parametr - proto následují prázdné závorky. Pak už následuje tělo naší metody se samotným kódem. My chceme pouze vrátit hodnotu našeho atributu. K vracení hodnot slouží klíčové slovo <b>return</b>, které vrátí hodnotu uvedenou za tímto klíčovým slovem (return hodnotaKterouChciVratit;) a provádění metody ukončí - pokud byste měli v metodě ještě nějaké příkazy za return, tak se vůbec neprovedou.

Metoda pro nastavení hodnoty nějakého atributu nevrací žádnou hodnotu - má tedy jako návratový typ uvedeno klíčové slovo <b>void</b>. Následuje jméno, pro které platí stejná pravidla jako pro metodu pro získání hodnoty atributu s tím rozdílem, že začíná slovem "get" místo "set". Následují závorky s parametry metody - chceme nastavit hodnotu atributu a proto potřebujeme vědět, co za hodnotu tam máme nastavit - tato metoda tedy bude mít vždy jeden parametr, který bude mít stejný datový typ, jako atribut, jehož hodnotu nastvujeme. Následuje pak tělo metody, ve kterém chceme nastavit novou hodnotu atributu - to provedeme stejně, jako když jsme hodnotu nastavovali v konstruktoru - pakliže se náš parametr jmenuje stejně jako atribut, tak opět použijeme klíčové slovo <b>this</b>.

Samotné volání našich metod pak bude vypadat takto:
```java
Auto naseAuto = new Auto("Mercedes");

// získáme a vypíšeme hodnotu atributu brand našeho auta - "Mercedes"
System.out.println(naseAuto.getBrand());

// nastavíme novou hodnotu atributu brand našeho auta
naseAuto.setBrand("Škoda");


// získáme a vypíšeme novou hodnotu atributu brand našeho auta - "Škoda"
System.out.println(naseAuto.getBrand());
```

Metody ale nemusí sloužit pouze k získávání a nastavování hodnot atributů. Naše třída Auto by mohla mít třeba metodu, která nám vrátí základní, hezky naformátované údaje o autě, nebo třeba metodu, které zjistí, za jestli nemáme prošlou technickou.

```java
public String ziskejZakladniInformace() {
  return "Značka: " + znacka + " Model: " + model + " Rok výroby " + rokVyroby + " SPZ: " + spz;
}

public String jePlatnaTechnicka() {
  return !datumPristiTechnickeKontroly.isBefore(LocalDate.now());
}
```

## Konvence

V případě proměnných jsme si řekli v podstatě jen dvě konvence: 

- při pojmenovávání proměnné používáme <b>Camel case</b> - první slovo malými písmeny a každé další slovo v názvu pak s počátečním velkým písmenem "mojeDeravePonozky"

- při pojmenovávání konstant pak píšeme celý název velkými písmeny a jednotlivá slova oddělujeme podtržítky "POCET_MESICU_V_ROCE"

Camel case si dobře zapamatujte, protože se s ním budeme setkávat často.

S třídami, jejich atributy a jejich metodami nám přibylo spoustu dalších konvencí, které je vhodné si připomenout a dodržovat.

- jméno tříd píšeme pomocí tzv. <b>Pascal case</b> - tento styl je skoro stejný, jako nám už známý Camel case - jediný rozdíl je ten, že i provní slovo v názvu začíná velkým písmenem "StudentStredniSkoly"

- jména atributů píšeme, stejně jako jména promenných, pomocí <b>Camel case</b> a jméno by mělo vždy vyjadřovat, co daný atribut obsahuje

- jména metod pojmenováváme také pomocí <b>Camel case</b> a jméno by mělo vždy vyjadřovat, co daná metoda dělá

- metody by měly dělat vždy jen jednu věc a být rozumně dlouhé - neexistuje pevně daný počet řádků a ne vždy je snadné je rozdělit, ale nepsaným pravidlej je, že by nikdy nemělo být potřeba scrollovat, aby sis zobrazil jednu metodu na monitoru - pokud ji máš delší, nebo dělá víc věcí, je dobré ji rozdělit na víc metod (použít pomocné metody, které si v té hlavní metodě zavoláš)

- když si vytváříš metodu, která má sloužit pouze jako pomocná, použij modifikátor viditelnosti <b>private</b>

- kód se bežně píše v Angličtině a i při případném použití jiného jazyka se vynechává diakritika

- existují i pravidla na to, jak uspořádat třídu uvnitř - nejběžnejší upořádání je: 1.)atributy, 2.) konstruktory, 3.) metody s tím, že atributy, konstruktory a metody mezi sebou bývají uspořádané buď podle viditelnosti(public->protected->private), nebo podle skupin, jak k sobě patří

- vždy ale platí zlaté pravidlo řídit se konvencemi týmu, či firmy, ve které zkončíte a snad nikdy není správně se zuby nehty držet toho, co jsme si teď řekli, pokud byste byli jediní, kdo by se té konvence držel

## Výčtové typy

Výčtové typy, neboli <b>enum</b>y slouží v Javě k vytváření vlastních datových typů, kdy každý takový datový typ může nabývat vždy jen předem specifikovaných hodnot a používají se opět právě pro reprezentaci nějakých, při tvorbě programu známých množin hodnot o nihž se nečeká, že se budou příliš, či vůbec měnit - třeba dnů v týdnu, kdy bychom měli výčtový typ Den a jeho možné hodnoty by pak byly jednotlivé dny v týdnu, nebo v našem případě třeba výčtový typ, který by reprezentoval typ motoru v tom našem autě.

Výčtový typ se vytváří podobně, jako třída - jen při vytváření zvolíme "enum" místo "class" a i svoji strukturou bude třídu připomínat.

```java
public enum Den {
  PONDELI,
  UTERY,
  STREDA,
  CTVRTEK,
  PATEK,
  SOBOTA,
  NEDELE
}
```

Stejně jako u třídy definice začíná modifikátorem viditelnosti, následuje klíčové slovo <b>enum</b>, kterým říkáme, že vytváříme enum, pak následuje jméno našeho enumu - to píšeme stejně jako jména tříd za pomocí Pascal case a nakonec už samotné tělo enumu, které obsahuje výčet hodnot - konstant, které tento enum může nabývat. Tím, že jde o konstanty, používáme při jejich pojmenovávání stejný styl, jako když jsme si vytvářeli proměnnou, která byla <b>final</b> - všechna písmena jsou v názvech velká a jednotlivá slova v názvu jsou oddělená podtržítkem.

Řekli jsme si, že jde o datový typ a tedy si můžeme vytvořit proměnnou s tímto datovým typem:
```java
Den den = Den.STREDA;
```

Všimněte si, jak se dostáváme k jednotlivým hodnotám toho enumu - přes těčkovou notaci, kdy napíšeme jméno enumu, tečka, a pak následuje konkrétní hodnota toho enumu.

Tady ale podoba s třídou nekončí - enumy, stejně jako třídy, mohou mít i vlastní atributy, konstruktory, i metody a platí pro ně i stejná pravidla s jednou výjimkou - že konstruktory si vytváříme s modifikátorem viditelnosti <b>private</b>, protože ten konstruktor slouží vždy jen k vytvoření hodnot, kterých může tento enum nabývat.

Kupříkladu u jednotlivých dnů si budeme moct evidovat to, jestli jde o pracovní den, nebo ne.

```java
public enum Den {
  PONDELI(true),
  UTERY(true),
  STREDA(true),
  CTVRTEK(true),
  PATEK(true),
  SOBOTA(false),
  NEDELE(false);
  
  private boolean jePracovni;
  
  private Den(boolean jePracovni) {
    this.jePracovni = jePracovni;
  }
  
  public boolean jePracovni() {
    return jePracovni;
  }
  
}
```
