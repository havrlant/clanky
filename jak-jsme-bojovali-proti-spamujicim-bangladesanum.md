Dlouhou dobu si naše [fórum][1] vystačilo s klasickým jednoduchým antispamem: povinná registrace, kdy byla uživateli předložena otázka, kterou za něj ale odpověděl Javascript. Uživatel tak o ničem nevěděl a roboti, kteří typicky Javascript neinterpretují, byli v háji. To ale stačilo jen do jisté doby.

Na fóru se postupně začalo objevovat více spamů a ze začátku mi nebylo úplně jasné, jak se vlastně tito spammeři dostali přes tuto ochranu. Začal jsem tak pokusy o registrace logovat a ti roboti, kteří se dostali dále, měli více méně společné tyto vlastnosti:

*   Podle hlaviček měli moderní prohlížeč, žádný IE 5.5 jako ti roboti, kteří neprošli. 
*   Antispamovou otázku napsali správně na první pokus. 

Takže buď někdo cíleně útočil na fórum a znal odpovědi na otázky, nebo ti roboti interpretovali Javascript. Pravděpodobnější byla druhá verze, takže jsem přidal na fórum nějaké kusy Javascriptu, abych to ověřil. Výsledkem bylo, že všechny změny, které prováděl jen Javascript, se u těch robotů, kteří prošli, projevovaly.

Nainstaloval jsem nějaký skript, který uměl z IP adresy poznat, z jaké země se uživatel přihlašuje. Většina úspěšných robotů měla Bangladéšskou IP adresu.

Zkusil jsem se zeptat [moudřejších][2], jestli mají nějakou radu. Dostalo se mi hlavně popostrčení -- možná to nejsou roboti, ale živí lidé. Z masa, kostí a rýže. A za dolar na týden a kus bambusu mi spamují fórum. Že podobné služby existují je [celkem známo][3], ač v tomto případě se jedná jen o přepis CAPTCHA.

Dobře, takže je možné, že na mě neútočí jen tupí roboti, ale také chytří Bangladéšané.

Jak ale vytvořit antispam tak, aby jím neprošel živý člověk z Bangladéše? Chtěl jsem především nějaké elegantní řešení, žádné technické zrůdnosti, ani něco, co by obtěžovalo validní uživatele. V té době tam byla otázka typu *Spočítej 5+17*, což je ale celkem univerzální otázka v tom smyslu, že ji dokáže pochopit a zároveň na ni odpovědět i Bangladéšan.

Změnil jsem otázku tak, aby z ní nebylo zřejmé, na co se ptám, tj. něco jako *Jaký je den mezi pátkem a nedělí?* a nastavil jsem, že každý, kdo se nepřihlašuje z CZ nebo SK na tu otázku při registraci **musí** odpovědět. Tuhle otázku Bangladéšan nepochopí a nebude na ni znát odpověď. Zároveň na ni odpoví každý Čech a Slovák, což jsou prakticky všichni uživatelé fóra.

A za pár dní jsme měli na fóru dalšího spamujícího Bangladéšana. Nejzajímavější byl log, který říkal, že jeden z Bangladéšanů se tam dostal tak, že postupně zkoušel přibližně tyto odpovědi:

1.  saterday
2.  saturday
3.  sobota

Evidentně používal nějaký překladač, který mu přeložil otázku, ale Bangladéšan nejprve odpověděl anglicky a udělal překlep, pak se opravil a až pak mu došlo, že musí odpovědět česky, takže si ještě saturday přeložil do češtiny. A byl na fóru.

Hmm.

Takže česká otázka nestačí, Bangladéšané používají překladač. Nyní už to začíná být zajímavější. Jak upravit antispam tak, aby běžného uživatele neotravoval a Bangladéšan přes něj nepřešel ani s překladačem?

V podstatě se vše zredukovalo na to vymyslet nějakou otázku, na kterou zná odpověď každý Čech nebo Slovák (včetně puberťáků!), ale Bangladéšan ji znát nebude a to ani když použije překladač a následně Google. To je překvapivě složitý úkol. Něco z toho, co nás napadlo a zavrhli jsme:

*   Přísloví. *Kdo jinému jámu kopá, sám do ní [doplň]*. Bohužel často [stačí frázi vložit do Googlu a odpověď je na světě][4].
*   Aby odpověď vyžadovala diakritiku. Kromě toho, že tím znemožníme registraci pravověrným linuxákům :-), tak tu odpověď lze zkopírovat třeba z Googlu a validní lidé, kteří se chtějí registrovat z ciziny, nemusí mít českou klávesnici. 
*   Otázky typu: *jaká je nejvyšší hora ČR?* jsou úplně jednoduše dohledatelné asi úplně kdekoliv, subjektivnější otázky typu *Jak se jmenuje nejznámější český zpěvák* jsou v podstatě podobně dohledatelné: první dvě slova prvního výsledku jasně říkají: [Karel Gott][5].
*   Zajímavá byla otázka *Kdo vynalezl telefon těsně po Bellovi?* Našeho nejslavnějšího vynálezce by možná nešlo tak lehce vygooglit, ale zase těžko chtít po dvanáctiletých puberťačkách, které mají problémy s domácím úkolem, aby znaly Járu Cimrmana. 
*   Popkulturní odkazy jako *Paroubek jinak na pět*. Přestože je možností mnoho (Jyrka, prase), tak to zase nebude znát každý. Puberťačky tím spíše. Hlášky z filmů jsou většinou dohledatelné stejně jako přísloví nebo Karel Gott.
*   Otázka na gramatiku: *Přepište následující větu bez gramatických chyb: "ženy souložili"* Tohle byl celkem dobrý nápad, asi by byl použitelný, ale nejvíc jsem se bál toho, že by to někdo nevěděl. Na druhou stranu -- možná by to nebyla žádná škoda :-D. Teoreticky by se ještě dal použít nějaký checker, třeba z Wordu. 

Výsledek? No, v podstatě žádný. Některé otázky by byly použitelné, pokud bychom předpokládali, že Bangladéšan buď vůbec nepoužije Google nebo to bude zkoušet jen chvíli. Celkem zajímavé cvičení je předpokládat, že to ten Bangladéšan bude zkoušet dlouho. Napadá vás nějaká otázka, na které by si Bangladéšan vylámal zuby i s Googlem, ale Čech/Slovák by znal odpověď?

Nakonec pomohla změna formy dotazu. Máme web, 21. století -- co takhle použít nějaká multimédia? Stačí například přiložit obrázek a zeptat se, co je na něm? Případně nějaké audio/video.

Problém: Google má hledání obrázků a když si tam člověk nechá vyhledat obrázek něčeho známého, tak mu Google zároveň řekne, co by to tak mohlo být. U notoricky známé fotky Karlova mostu to u mě napíše: [Best guess for this image: charles bridge][6] a totéž pro Agátu: [Best guess for this image: agáta hanychová][7].

Ale to by až tak nevadilo. Obrázek lze trochu poškodit nebo použít nějaký, z kterého Google nepozná o co jde. A jsme v cíli. Zbývá už jen vymyslet něco, co by tom obrázku mělo být, aby to poznal puberťák i důchodce.

Nakonec jsem zvolil … Karla Gotta. Snad je natolik velká legenda, že ho znají i dnešní puberťáci. Použil jsem nějakou zakopanou fotku, kterou jsem ještě různě zdeformoval, aby Google nenašel žádný podobný obrázek a neuhádl, kdo na fotce je. Lze použít i více obrázků s tím, že uživatel musí poznat aspoň někoho. Takže pro mladší lze použít třeba tu Agátu.

Pro jistotu jsem soubor s obrázkem lstivě pojmenoval marek_vasut.jpg. A ne nadarmo, za tu dobu, co je tento antispam nasazený, zkoušeli Marka Vašuta tři lidé a několik dalších zkoušelo jen Marek. Bangladéšané nejsou tak úplně blbí! Jednou tam byl vyplněný i Havel (ale Klaus ne, to zase bude ukřivděný).

Takže rozuzlení -- jaká je účinnost Káji Gotta? Antispam s Kájou byl nasazen v červnu roku 2012 a nejsem si vědom toho, že by se tam zaregistroval nějaký zlý Bangladéšan. Hurá! Kolik validních uživatelů přes antispam neprošlo? Těžko říci, jeden z nich mi napsal email. Byl to Američan a chtěl kontaktovat někoho z fóra, víc mi nepsal. Emailem jsem mu prozradil odpověď. Víc nevím, moc jich snad není.

Nakonec máme po technické stránce triviální antispam, který ale funguje. Alespoň zatím. Držte palce, ať funguje dále nebo navrhněte nějaké jiné jednoduché, ale neprůstřelné řešení :-)

 [1]: http://forum.matweb.cz/
 [2]: http://diskuse.jakpsatweb.cz/?action=vthread&amp;forum=9&amp;topic=134245
 [3]: http://www.root.cz/clanky/potrebujete-obejit-captcha-zaplatte-si-armadu-indu/
 [4]: https://www.google.cz/search?q=%22Kdo+jin%C3%A9mu+j%C3%A1mu+kop%C3%A1%2C+s%C3%A1m+do+n%C3%AD%22
 [5]: https://www.google.cz/search?q=most+famous+czech+singer
 [6]: http://goo.gl/Amh5j
 [7]: http://goo.gl/Q0STP