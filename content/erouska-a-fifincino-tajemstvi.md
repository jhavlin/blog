+++

title = "eRouška a Fifinčino tajemství"

description = "Proč by se většina lidí nemusela o své soukromí bát, a proč by aplikace mohla vyjít vstříc i těm ostatním."

date = 2020-04-18

weight = 3

[extra]
og_image = "facemasksecret.png"

+++

__Důležité:__ Tento text pojednává o první a již zastaralé verzi aplikace eRouška. Druhá verze funguje již značně odlišně.

----

Po zvážení rizik jsem začal používat aplikaci <a href="https://erouska.cz/" target="_new">eRouška</a>.
Tady jsou postřehy, závěry a náměty.

(Text je zveřejněn poněkud zbrkleji než obvykle. Pokud narazíte na chyby nebo nepřesnosti, dejte mi prosím vědět.)

(Nejsem bezpečnostní expert ani nemám žádný vztah k&nbsp;aplikaci eRouška. Pouze se zajímám o soukromí na internetu a aplikace kryptografických metod.)


# Jak to funguje

Projekt eRouška je zajímavý počin kladoucí si za cíl využít dostupné technologie pro boj s&nbsp;pandemií.

Ústřední myšlenka je geniálně jednoduchá: Detekovat přes bluetooth telefony v&nbsp;blízkém okolí, vyměňovat si s&nbsp;nimi anonymní identifikátory a zaznamenávat tak možné případy nákazy při setkávání lidí.

## Příklad ze života

### Běžný provoz

Představme si situaci, kdy se setkají dva uživatelé této aplikace, říkejme jim třeba Fifinka a Bobík. Telefon každého z&nbsp;nich hledá v&nbsp;okolí (na dosah Bluetooth) další telefony uživatelů eRoušky a vymění si s&nbsp;nimi údaje o sobě.

Jak jsme již zmínili, používají se anonymní identifikátory. Zjednodušeně to proběhne tak, že Bobíkův telefon řekne: „Ahoj, já jsem mobil uživatele s&nbsp;číslem 29091.“ Fifinčin telefon si do „deníčku setkání“ uloží informaci „Dnes jsem potkala uživatele 29091.“ (A k&nbsp;tomu nějaké doplňující informace, třeba o síle signálu, ze které se dá velmi zhruba odhadnout těsnost kontaktu.) A obdobně se představí Fifinčin telefon a Bobíkův telefon si Fifinčin identifikátor zapíše do svého deníčku.

Důležité je, že se neukládají informace o poloze zařízení. Aplikace tedy nesleduje, kde se uživatel pohybuje. A ještě důležitější je, že ani tyto celkem nicneříkající identifikátory se nikam neposílají. Tedy dokud to není potřeba (viz níže). Zůstávají uložené pouze v&nbsp;telefonech uživatelů.

(Aby se navíc identita uživatelů ještě více utajila, každý uživatel střídá více identifikátorů. Dva různí uživatelé tak mají mnohem menší šanci ze svých deníčků setkání vyčíst, že se setkali s&nbsp;tím samým člověkem.)

### Nákaza

Co se stane, když se prokáže, že je nějaký z&nbsp;uživatelů nakažený (nebo když je alespoň velmi dobrý důvod to předpokládat)?

Celý systém trasování nákazy je založen na tom, že hygienické stanice dokáží k&nbsp;anonymním identifikátorům přiřadit telefonní čísla uživatelů. Každý uživatel tedy musí své telefonní číslo uvést při registraci do aplikace. Říkám „musí“, ale používání aplikace je samozřejmě dobrovolné.

Představme si, že Bobíkovi vyšel pozitivní test na nákazu. Pracovníci hygienické stanice se ho zeptají, jestli je ochoten poskytnout informace o svých setkáních. On souhlasí a svůj deníček setkání odešle. Na hygienické stanici pak jeho kontakty vyhodnotí, přiřadí k&nbsp;nim telefonní čísla a příslušné lidi zpraví o tom, že mohli být nakaženi, uvalí na ně karanténu a domluví se s&nbsp;nimi na testování. (Pouze předpokládám, že to probíhá nějak takto, z&nbsp;toho, co jsem zatím četl. Opravte mě, pokud se pletu.)

Díky tomu se i Fifinka může včas dozvědět, že šíří nákazu, třeba ještě předtím, než se u ní projeví příznaky.


# Co se může zvrtnout

Hodnocení rizik by nebylo příliš důvěryhodné, kdyby neprošlo ty nejčernější scénáře.

V rámci běžného provozu jsou údaje z&nbsp;aplikace distribuované v&nbsp;telefonech uživatelů a nedají se nijak zpracovat a zneužít. Horší je to ale se zpracováním informací v&nbsp;okamžiku, kdy je potřebujeme odtajnit z&nbsp;podstaty věci, tedy při trasování nákazy.

## Když náhoda hraje proti nám

Teď si dovolím uvést velmi nepravděpodobný a vykonstruovaný příklad, tak to prosím berte s&nbsp;rezervou.

Na hygienické stanici měl zrovna službu Myšpulín, když se řešil Bobíkův případ. Bobík dal jako zodpovědný občan souhlas ke zpracování údajů ze svého telefonu, Myšpulín k&nbsp;nim přiřadil telefonní čísla uživatelů a v&nbsp;jednom z&nbsp;nich poznal telefonní číslo Fifinky, která je ovšem již tři týdny v&nbsp;lázních. Proč by za ní Bobík jezdil bez ostatních kamarádů a ani jim to nedal vědět? Ohrozí toto zjištění křehkou rovnováhu ve vztazích správňácké čtveřice? A co kdyby měl zrovna službu Pinďa, tou dobou ve finančních potížích, a získanou informaci prodal bulváru?

Protiargument: Opravdu potřebovali Pinďa a Myšpulín další indicie k&nbsp;tomu, aby pochopili, že Bobík je pěkné prase?

## Zobecnění

Při trasování nákazy může dojít k&nbsp;odkrytí skutečné identity uživatelů.

Věřím však, že na hygienických stanicích pracují lidé s&nbsp;nejvyššími morálními standardy a zveřejnění informací o kontaktech mezi lidmi nebo jiné formy zneužití informací nehrozí. Jsou jasně daná pravidla na to, kdo má k&nbsp;údajům přístup, jak se ukládají a po jaké době se musí smazat, a předpokládám, že se dodržují.


# Jak vyjít vstříc těm, co se bojí

I když si sám nemyslím, že by se data z&nbsp;aplikace dostala do špatných rukou, mám jisté pochopení pro lidi, kteří ztratili důvěru ve státní instituce. Vzhledem k&nbsp;tomu, kolik předních státních představitelů má problémy se zákonem nebo pravdomluvností, bych se je neodvážil označit za přehnaně podezíravé.

Část lidí také nemusí mít úplně čisté svědomí a bojí se, že by se údaje z&nbsp;aplikace mohly obrátit proti nim.

Co by se dalo udělat pro to, aby byli ochotní si aplikaci také nainstalovat a zvýšit tak účinnost celého systému?


## Marketingové řešení

Při propagování aplikace se může vyzdvihovat, že se dá aplikace kdykoliv vypnout a data smazat. To by mohlo zvýšit počet uživatelů, i když část z&nbsp;nich bude aplikaci používat pouze v&nbsp;omezeném, opatrném režimu.

Nástřel něčeho takového uvádím v&nbsp;Příloze 1.

Pokud by se lidé báli, že zapomenou aplikaci v&nbsp;choulostivých situacích vypnout, mohla by nabídnout nějaké nastavení pro automatické zapnutí a vypnutí, třeba v&nbsp;určené časové období.


## Technické řešení

Nejednoho nadšence do informačních systémů a kryptografie asi zarazilo, že aplikace, která se chlubí vysokou mírou ochrany soukromí a anonymity, uživatele požádá o telefonní číslo. Zvlášť v&nbsp;době, kdy se mluví o zákazu anonymních SIM karet.

Mohlo by to celé fungovat, kdyby hygienické stanice neměly přístup k&nbsp;telefonním číslům uživatelů? (Nebo přesněji, kdyby se část uživatelů rozhodla telefon neposkytnout. Znalost telefonního čísla věc nejspíše značně usnadňuje, a proto by mělo zůstat dobrovolným a doporučeným údajem.)

Zkusím tedy popsat návrh řešení, který vypadá celkem funkční (po několika neúspěšných pokusech), ale je možné, že mi případné nedostatky jen unikají. Budu rád, když mi dáte vědět, jestli jste našli nějakou chybu v&nbsp;mém úsudku.

### Princip tajného identifikátoru a jeho veřejného hashe

- Každému uživateli aplikace vygeneruje vhodný náhodný identifikátor a spočítá jeho
<a href="https://cs.wikipedia.org/wiki/Kryptografick%C3%A1_ha%C5%A1ovac%C3%AD_funkce" target="_new">kryptografický hash</a>. (Velmi zjednodušeně, hash je hodnota jednoznačně spočítaná z&nbsp;nějaké vstupní hodnoty, která má tu vlastnost, že se&nbsp;z ní nedá odvodit ona původní hodnota.)
- Při setkání si telefony vymění jen hashe, samotné identifikátory si nechají nadále pro sebe.
- Existuje centrální neveřejná databáze lidí, kteří by se měli ozvat hygieně. Ta obsahuje zase jenom hashe, ne přímo identifikátory.
- V&nbsp;případě potvrzené nákazy může uživatel odeslat seznam hashů uživatelů, se kterými byl v&nbsp;kontaktu, na hygienu. Ti ho vloží do centrální databáze hashů, kteří se mají ozvat.
- Aplikace se pravidelně, třeba jednou za den, dotazuje ověřovacího serveru, jestli její uživatel není v&nbsp;seznamu lidí, kteří se mají ozvat hygieně. To funguje tak, že aplikace tentokrát odešle původní identifikátor. Pro ten se na serveru spočítá hash a ověří, jeslti je uveden v&nbsp;centrální databázi. Díky tomu nikdo jiný než samotný uživatel nemůže zjisit, že daný hash má důvod řešit něco s&nbsp;hygienou. Nikdo jiný ten identifikátor nezná, všichni ostatní znají jen hash, a z&nbsp;toho se identifikátor nedá spočítat.
- Výhodou je, že dokonce ani v&nbsp;případě úniku centrální databáze, což je věc, ke které by nemělo nikdy dojít, se nedá zjistit, kdo je nakažený. Máte jen seznam hashů lidí, co mají nějaký důvod ozvat se hygieně. I když dokážete přiřadit člověka k&nbsp;hashi, třeba protože jste ho potkali a znáte díky tomu jeho hash, nevíte nic o jeho zdravotním stavu. (Tedy víte, že mohl být v&nbsp;kontaktu s&nbsp;někým nakaženým, ale to pořád jen v&nbsp;nepravděpodobném případě úniku databáze.)

### Výhoda pro Fifinčino tajemství

A jak by celá kauza s&nbsp;podezřelou návštěvou v&nbsp;lázních mohla proběhnout s&nbsp;použitím navrženého anonymnějšího přístupu? Bobík zpřístupní svá data hygienické stanici. U hashe identifikátoru Fifinky není uvedeno telefonní číslo, a tak se automaticky vloží do centrální databáze hashů k&nbsp;ověření. Fifinčin telefon při pravidelném ověřování zjistí, že její hash se objevil v&nbsp;databázi a na Fifinku vyskočí upozornění, aby se ozvala na příslušnou hygienickou stanici. Pak už záleží na ní, jaká data poskytne a co vše na sebe prozradí.

I zde jsou ale komplikace s&nbsp;tím, že je hash vysílán veřejně. Tedy pokud Myšpulín dokáže zjistit, jaký hash patří Fifince a že se objevil na Bobíkově seznamu, podezření pojme podobně, jako kdyby poznal telefonní číslo. Toto nebezpečí zmírní to, že jeden uživatel nepoužívá jeden identifikátor, ale střídá jich více.


### Nevýhody řešení s&nbsp;tajným identifikátorem

Toto řešení je technicky náročnější, je nezbytné provozovat ověřovací server, který musí zvládnout poměrně intenzivní zátěž.

Také se nedá příliš mluvit o trasování. Hygienici nemají informace o tom, kdo se s&nbsp;kým setkal. Jen jim volají lidé, jejichž hash identifikátoru se z&nbsp;nějakého důvodu objevil v&nbsp;databázi, ale třeba jim nechtějí sdělit žádné další podrobnosti. Ale alespoň se na testování a případné karanténě mohou domluvit i lidé, kteří by aplikaci třeba nepoužívali, kdyby museli uvést telefonní číslo.

Bylo by dobré vědět, kolik lidí by takové řešení přesvědčilo k&nbsp;instalace aplikace, aby tvorba a správa komplikovanější varianty systému nebyla zbytečná.


# Závěr

Abych to shrnul, princip fungování eRoušky je velmi chytrý a poměry robustnosti řešení, rychlosti dodání a míry ochrany soukromí jsou vynikají. Za to si jistě tvůrci zaslouží uznání.

Až se doladí důležitější detaily, jako další krok by stálo za to vyhodnotit, kolika lidem vadí nutnost uvést telefonní číslo, a pokusit se případně nějak vyjít vstříc i jim. To by mohlo rozprášit obavy o ochranu soukromých údajů a zvýšit počet zapojených uživatelů.


# Příloha 1: Návod pro nevěrníky, podvodníky a vlastizrádce

Vaše zdraví by mi mohlo být celkem ukradené, ale protože pro fungování systému je lepší, když se zapojí více lidí, předkládám sadu doporučení i pro vás.

- Tento odstavec nečtěte před manželkou / před vyšetřovateli / v&nbsp;senátu.
- Aplikaci zapínejte jen na veřejných místech, kde se setkáváte s&nbsp;cizími lidmi, a kde stejně vaše kontakty všichni vidí.
- Případně si zřiďte nové telefonní číslo vyhrazené pro tento účel.
- Pokud jste při setkání, které jste chtěli utajit, zapomněli aplikaci vypnout, vymažte svá data z&nbsp;aplikace. (A požádejte o totéž i ostatní zúčastněné osoby.) Zatím se nic nestalo, údaje se samy nikam neodesílají.
- Pokud máte milence/milenku, aplikaci může používat bez omezení alespoň jeden z&nbsp;vás. V&nbsp;případě nákazy se můžete diskrétně informovat jiným kanálem.<br>
  <small>Uvážíme-li, že člověk může mít více milenců/milenek, rodí se nám zde myslím hezká úložka na bipartitní párování v&nbsp;grafu :-)</small>


# Příloha 2: Nestrukturované poznámky

Další složité věci jsou v&nbsp;technických detailech. Jak poznat podle síly Bluetooth signálu a doby kontaktu, že mohlo dojít k&nbsp;nákaze? Jak nevyplácat celou baterku za půl hodiny?

Zabýval jsem se pouze ochranou soukromí co se týká spravovaných informací. Ochranu samotné aplikace před napadením ani zabezpečení komunikace mezi telefony nebo zabezpečení bluetooth protokolu neumím posoudit, ale předpokládám, že zde (na pravidelně aktualizovaných telefonech) nebezpečí nehrozí.

Lidé se mohou obávat i úniku seznamu telefonních čísel. Stálo by za to uvést, jak vypadá typický telefonát z&nbsp;hygieny a na jaké informace se mohou hygienici po telefonu ptát? Nebo by to více pomohlo lumpům, kteří by se za hygieniky mohli vydávat?
