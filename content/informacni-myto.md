+++

title = "Informační mýto"

description = "Úvaha o tom, jestli nám může kryptografie nabídnout kompromis mezi bezpečím a soukromím"

date = 2020-02-16

+++

Nedávné zprávy o chystaném (a utajovaném) záměru evidovat průjezdy všech automobilů mýtnými branami vyvolaly pochopitelnou vlnu diskuzí o přiměřenosti tohoto opatření. Jeho odpůrci poukazovali na snadnou zneužitelnost takových dat, podle zastánců by bylo naopak nerozumné plýtvat takovými informacemi, které by byly jistě užitečné při vyšetřování nejednoho kriminálního činu.

Je opravdu nutné volit mezi soukromím a bezpečím? Není nic mezi? Nemohly by při hledání kompromisu pomoci současné kryptografické techniky? Nedalo by se dokonce nějak zařídit, aby se váha těchto principů dala nastavit podle společenské dohody?

Protože je to moc hezká úložka na návrh informačního systému, pokusíme se naznačit několik řešení, která by takové vlastnosti mohla nabídnout. A nebojte, budeme se pohybovat po povrchu, do žádné složité matematiky zabrušovat nebudeme.

Upozornění: Nejsem matematik ani odborník na kryptografii a zabezpečení. Za upozornění na chyby ve svém úsudku budu rád.


## 0. Výchozí varianta

Začneme tím, jak by mohlo vypadat systém na evidenci pohybu vozidel zcela bez snahy o omezení možnosti zneužití.

To, o čem se budeme bavit, je schéma dat, tedy struktura informací, které zaznamenáme o každém průjezdu vozidla mýtnou branou.

V nejjednodušší variantě může vypadat třeba takto:

```
značka: registračni značka vozidla
brána:  identifikátor mýtné brány
čas:    datum a čas průjezdu branou
```

***Výhody:*** Velmi jednoduše zpracovatelná data. Při vyšetřování trestného činu snadno zjistíte, jak se automobily podezřelých osob pohybovaly.

***Nevýhody:*** Data jsou jednoduše také zneužitelná. Pokud Vás jako úřední osobu bude například zajímat, kdy a kudy jezdí váš úhlavní politický oponent nebo nepohodlný šéf otravné neziskovky, máte to jako na talíři.


## 1. Varianta pro ověřování

### Nezbytné základy (programátoři a matematici mohou přeskočit)

V této variantě vyjdeme z&nbsp;předpokladu, že při vyšetřování zločinů vycházíme z&nbsp;nějakých podezření, která potřebujeme ověřit.

Zde se hodí udělat malou matematickou zastávku a vysvětlit si pojem [„kryptografická hashovací funkce“](https://cs.wikipedia.org/wiki/Kryptografick%C3%A1_ha%C5%A1ovac%C3%AD_funkce) (dále jen hashovací funkce, ale pozor, ne každá hashovací funkce je kryptografická). Velmi zjednodušeně řečeno, je to taková funkce, která pro vstupní data (představte si číslo, slovo, nebo text) vrátí výstupní data takovým způsobem, že není prakticky možné z&nbsp;výstupních dat zjistit, jaká byla data vstupní.

```
Například pro hashovací funkci SHA256 bude výsledek vypadat takto:
SHA256(Krteček) = 924CDF20D9F9229998EBE4E749EBFAAD9FBFB7418A3147EA9EBAAB0F552332AE
```

Jestli vám připadá, že je to ta nejméně užitečná funkce na světě (například v&nbsp;porovnání s&nbsp;funkcemi jako _sinus_ nebo _logaritmus_), nemáte úplně pravdu. Taková funkce se náramně hodí právě při ověřování hodnot, které se nemůžete nebo nechcete pamatovat, ale chcete je s&nbsp;něčím porovnat.

Hashovací funkce se používají (nebo by alespoň měly) při ukládání uživatelských hesel v&nbsp;databázích. Kvůli možnému zneužití nebo krádeži dat nechceme ukládat informaci o tom, že uživatel Fifinka má heslo "Myšpuleen@Třesk0prsky", ale můžeme toto heslo prohnat hashovací funkcí a uložit si pouze výsledek, takzvaný _hash_.  Až se Fifinka bude potřebovat do své oblíbené aplikace přihlásit, zeptáme se jí na heslo, získáme jeho hash, a až ten porovnáme s&nbsp;hodnotou v&nbsp;databázi. Neporovnáváme tedy přímo hesla, ale jejich hashe. (Ve skutečnosti je to trošku komplikovanější, ale o tom později.)


### Schéma s&nbsp;hashem značky

Hashovací funkci nyní můžeme využít i při návrhu našeho schématu. Do databáze můžeme místo značky ukládat hash značky.

```
hash_značka: hash registrační značky vozidla
brána:       identifikátor mýtné brány
čas:         datum a čas průjezdu branou
```

***Výhody:*** Nelze jednoduše získat seznam projíždějících aut, což nám dává vyšší míru soukromí.

***Výhody (pro policii):*** Pro ověření průjezdů stejně snadno použitelné jako u základní varianty, jen místo značek podezřelých vozidel používáme jejich hashe.

***Nevýhody:*** Dá se velmi snadno obejít. Stačí mít pro každou registrační značku spočítaný její hash, a pak je jedno, jestli pracujeme s registrační značkou, nebo s&nbsp;hashem. Tyto informace se dají jednoznačně spárovat 1:1.

***Výhody (pro zkorumpovatelné úřední osoby):*** Mnohem lepší než základní varianta. Doporučuje 10 z&nbsp;10 populistických politiků. Tato úprava totiž nic neřeší, a navíc dává občanům falešný pocit soukromí. Své oponenty stále můžete sledovat stejně snadno, jen místo registrační značky jejich vozidel použijete hashe těchto značek.


### Osolené schéma s&nbsp;hashem

Výše uvedený problém není ničím novým. Přirozenou nevýhodou tohoto řešení je to, že nedokáže zakrýt, že dva shodné hashe vznikly (velmi, velmi pravděpodobně) zahashováním dvou totožných vstupních dat.

To představuje problém i při zmíněném ukládáním hashů hesel. Je totiž jisté, že nechceme, aby bylo dohledatelné, že dva různí uživatelé mají stejné heslo. A právě při ukládání hesel se používá technika nazývaná jako [„solení“](https://cs.wikipedia.org/wiki/S%C5%AFl_(kryptografie)).

Podstatou solení je to, že vstupní data „dochutíme“ dalšími náhodnými daty tak, aby byl výsledek pozměněn. Tato náhodná data si ovšem musíme uložit, abychom je mohli později použít při porovnávání s&nbsp;původním vstupním řetězcem.

```
Příklad:
heslo:   Krteček
sůl:     Tgoq1i9I6G (získaná z vhodného generátoru náhodných dat)
SHA256(KrtečekTgoq1i9I6G) = 9A61B397E999CE9D9C7D15D9AE6A1925B9CA71BF0FC301AFBEE4C24067027289

Při ověřování hesla potom zkontrolujeme, že
SHA256({zadané heslo}Tgoq1i9I6G) = 9A61B397E999CE9D9C7D15D9AE6A1925B9CA71BF0FC301AFBEE4C24067027289
```

Lepší schéma by pak mohlo vypadat takto:

```
hash_značka+sůl: hash registrační značky vozidla a soli
sůl:             data použitá pro solení značky
brána:           identifikátor mýtné brány
čas:             datum a čas průjezdu branou
```

(Pro jistotu připomínám, že pro každý záznam je třeba vygenerovat novou sůl, jinak by to celé nemělo smysl.)

Jak se takovými daty pracuje? Potřebujete-li zjistit, zda dané vozidlo projelo danou bránou, získáte z&nbsp;databáze záznamy pro tuto bránou (za požadované časové období). Pro každý z&nbsp;nich pak získáte hash daného vozidla a soli uvedené v&nbsp;záznamu. Porovnáte ho s&nbsp;hashem v&nbsp;záznamu a pokud se rovnají, průjezd vozidla byl ověřen.

Aby to bylo celé fungovalo, musíme předpokládat, že dat o průjezdech je tolik, že ověřování je prakticky použitelné jen pro jednotlivá vozidla. Ověřit všechny registrační značky pro všechny záznamy o průjezdech by pak bylo tak výpočetně náročné a pomalé, že by to bylo nepoužitelné.

***Výhody:*** Není možné plošné „preventivní“ sledování všech občanů. Zneužití je stále možné, ale už vyžaduje větší úsilí a znalosti.

***Nevýhody:*** Větší úsilí je nutné i při oprávněném zpracování dat.


### Ještě osolenější schéma aneb sůl nad zlato

Pokud by se varianta s&nbsp;osolenou značkou ukázala jako nedostatečná, neboli získání dat by bylo příliš snadné a umožnilo by i plošné sledování, je možné schéma ještě různě vytunit.

Například:

```
hash_značka+brána+sůl: hash registrační značky a brány a soli
sůl:                   data použitá pro solení
čas:                   datum a čas průjezdu branou
```

Nebo dokonce:

```
hash_značka+brána+čas+sůl: hash registrační značky a brány a času a soli
sůl:                       data použitá pro solení
den:                       datum průjezdu branou
```

Kde čas, podle toho, jak si to chceme zkomplikovat, může obsahovat jen hodinu, nebo i minutu, a dokonce i vteřinu.


### Což takhle si sůl nejdříve vydolovat?

Solení je hezká věc, ale může být stále příliš snadná. Místo uložení soli přímo v&nbsp;databázi bychom mohli uložit zadání nějakého náročnějšího výpočtu, jehož výsledek pak použijeme jako sůl. Aby to fungovalo, musí být vymyšlení zadání jednodušší než jeho řešení.

Příkladem takové úlohy může být například faktorizace, neboli rozložení čísla na součin prvočísel. Vynásobit několik prvočísel a uložit výsledek je jednoduché, ale spočítat z&nbsp;výsledku, jaká prvočísla byla použita, již tak snadné není a vyžaduje to určitý výpočetní čas.

```
Například, spočítat součin je snadné:
2*2*5*5*5*7*31*37 = 4014500

Ale zkuste číslo 4014500 rozložit na součin prvočísel.
To už vyžaduje větší úsilí i pro člověka, i pro počítač.
```

(Toto je velmi jednoduchý příklad, obecně by mělo jít o takovou úlohu, která hledá hodnotu splňující vlastnosti popsané daným zadáním.)

Výhodou takového řešení by byla konfigurovatelnost, tedy nastavení složitosti výpočtu tak, aby odpovídala výpočetní síle současného hardwaru.

Otázkou je, jestli se dá vymyslet vhodná úloha. Pokud by byla příliš jednoduchá, dají se hodnoty předpočítat a výsledná složitost se tak příliš neliší od základního solení. Když budeme složitost zvyšovat tak, aby předvýpočet již nebyl praktický, můžeme se dostat k&nbsp;až tak složitým výpočtům, že nebude proveditelný ani při oprávněným použití.

Kdyby se to povedlo, schéma by vypadalo nějak takto:

```
hash_značka+výsledek: hash registrační značky a výsledku kontrolního výpočtu
zadání:               zadání kontrolního výpočtu
brána:                identifikátor mýtné brány
čas:                  datum a čas průjezdu branou
```

***Výhody:*** Jako solení, a navíc kontrolovatelná složitost zpracování dat.

***Nevýhody:*** Možnost nastavení nízké složitosti tak, aby byly informace snadněji zneužitelné. To se špatně ověřuje a kontroluje, a ja tak možné vyvolat v&nbsp;občanech falešný pocit soukromí.


## 2. Trajektorie pohybu

Další alternativou je nesledovat průjezdy konkrétních vozidel, ale zaznamenávat ujeté trasy takovým způsobem, aby se nedalo zjistit, jaká konkrétní vozidla je urazila. (Analogie bitcoinové peněženky, kde jsou všechny transakce dohledatelné, ale nedá se zjistit, jakému člověku patří.)

Zde by bylo potřeba, aby spolu dokázaly komunikovat sousední brány. V&nbsp;okamžiku, kdy brána zaznamená vozidlo, které předchozí branou v&nbsp;daném směru neprojelo, přiřadí jeho registrační značce identifikátor. Další brána v&nbsp;pořadí po průjezdu tohoto vozidla ověří průjezd u předchozí brány. Ta předá druhé bráně tento identifikátor a sama ho zapomene. Druhá brána zaznamená průjezd pod tímto identifikátorem a dočasně ho uloží pro případ, že by se třetí brána v&nbsp;pořadí identifikátor pro tuto registrační značku vyžádala.


Schéma:
```
id_trajektorie:       identifikátor průjezdu vozidla
brána:                identifikátor mýtné brány
čas:                  datum a čas průjezdu branou
```

Toto je zdá se technicky složitější, ale v&nbsp;praxi nemusí komunikovat brány mezi sebou, ale něco podobného může dělat centrální systém. Nebude ukládat registrační značky přímo, ale jejich dočasně přidělené identifikátory.

Mohla by se taková data hodit? Mohla by být užitečná informace, kam mířila auta po spáchání trestného činu v&nbsp;určitém místě? Možná by bylo takových dat příliš mnoho. Ale možná by se dala vhodně zkombinovat s&nbsp;informacemi z&nbsp;varianty pro ověřování. (Ovšem zase tak, aby informace nebyly až příliš snadno zpracovatelné.)


## 3. Je libo fotku na památku

Kromě průjezdů vozidel je sporné i ukládání fotografií pořízených na branách. Kdo s&nbsp;kým kam jezdí by měla být soukromá věc a šťourat by se v&nbsp;ní mělo opět jenom ve vzácných případech. Tedy když by se policii hodilo vědět, jestli byl podezřelý v&nbsp;autě sám nebo třeba vezl podezřelý náklad.

Pokud použijeme techniku založenou na ověřování, tedy takovou, že všechny údaje nejsou z&nbsp;databáze snadno čitelné, můžeme fotografii zašifrovat a jako klíč použít ony informace, které v&nbsp;databázi chybí a vyvstanou až po ověření. Konkrétně, každou fotografii můžeme zašifrovat registrační značkou auta, ke které patří. Případně použít složitější sadu informací v&nbsp;případě, že by toto bylo nedostatečné kvůli tomu, že seznam všech registračních značek je dostupný a není dostatečně velký.


## Závěr

Nedokáži příliš dobře posoudit a vyhodnotit, které z&nbsp;uvedených postupů by byly ve skutečnosti použitelné a užitečné, ale snad toto zamyšlení naznačilo směry, kterými se vydat při hledání kompromisu.

Asi není moc pravděpodobné, že by si policie nadšeně pořizovala drahý superpočítač, který by nastartovala jen při vyšetřování zločinu, a to navíc proto, že potřebuje „rozluštit“ informace, která si předtím sama zašifrovala kvůli ochraně před sama sebou. (A to, že se někdo z&nbsp;takových dat pokouší něco vytáhnout, by bylo jednoduše poznat podle toho, že v&nbsp;budově policie pohasínají světla kvůli zvýšenému odběru energie.)

Ale v&nbsp;ideálním světě by to tak nějak bylo a můžeme se bavit o tom, jak se k&nbsp;tomuto stavu pokusit přiblížit.