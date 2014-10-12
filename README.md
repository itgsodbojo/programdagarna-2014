#programdagarna 2014

it-tekniker, nätverkstekniker, devops och andra hackers  


##Linux och Samba

Dagens uppgift är att lära sig tillräckligt mycket linux för att kunna skapa en filserver i linux
som delar filer med andra datorer via cifs, som mest används i windowsvärlden.

Jag har inte träffat er, vet inte förutsättningarna för installationen av linux,
kanske wmwareplayer och någon iso. vi löser det. Annars kör vi min favorit virtualbox och vagrant.
Så får vi se hur vi sätter upp ett nätverk.

###Keyboard

Det finns ett par tangentkombinatationer som ni kan behöva kunna

- tilde ~  
- pipe |
- Ctrl tangent känner ni kanske till, i text brukar den betecknas ^


###Terminal

Vi kommer uteslutande att jobba i en [terminal eller konsol](http://en.wikipedia.org/wiki/Command-line_interface),
inget grafiskt gränsnitt.  Det första ni möts av när ni öppnar en terminal är propmten.
På linux ser den lite annorlunda ut än i windows är konfigurerbar och ges ofta en personlig prägel.

##Linux kommandon

Har ni använt kommadotolken i windows eller ännu hellre powershell är ni en bra bit på väg,
annars går vi igenom det. En bra sida om linux kommandon hittar ni på
[linuxcommand.org](http://linuxcommand.org/lc3_learning_the_shell.php)

###Kommandon

Kommadon i linux eg även windows, kan  bestå av tre delar,kommando option argument

Där
- kommadot är namnet på kommandot, beskriver ofta vad som ska göras
- option är olika flaggor ni kan sätta för att ändra kommandot
- argument beskriver oftast vilken/vilka saker vi jobbar med

**ex Kopiera en fil**

    cp -n filnamn nyttfilnamn

- cp, kommandot copy files
- -n, en option som säger att om filen nyttfilname existerar ska den inte skrivas över
- filnamn, nyttfilnamn  är argument till kommandot, i det här fallet källa och mål

###navigering

**~**

Öppnar ni en ny terminal startar ni oftast i er hemmakatalog, som ligger i en folder home, där andra användare och har sin underkataloger.
Er hemmakatalog, home folder brukar även betecknas ~ (tilde kallas tecknet), det kan också användas som del i ett kommado och expanderar då till att peka på sökvägen till er hemma katalog.

**pwd**

om ni har en prompt som inte visar sökvägen till var ni befinner er visar pwd (print working directory) er sökvagen till aktuell katalog, där ni befinner er.

**cd**

cd, change directory flyttar er tille en annan katalog, följande kommandon är bra att kunna

    cd , enbart kommandot flyttar er till er hemmakatalog
    cd sökväg, flyttar er till katalogen i sökvägen
    cd -, flyttar er till föregående katalog


**relativa sökvägar**

för att göra sökvägen mellan kataloger mer flexibla och använbara finns det några kortvarianter

    .  det är katagen ni står , arbetskatalogen
    .. katalogen ovanför er arbetskatalog

exemplevis om ni kör fäljande två kommandon

    cd
    cd ..

kommer ni efter första kommandot hamna i er hemmafolder och efter det andra en folder upp, /home


**linux filsystem**

det är kanske dags att titta  på linux filsystem, från windows är ni kanske van vid att ha enhetsbeteckningar som ofta hör samman med en disk eller annan lagringsyta
i linux finns enbart en **lagringsyta** /, även kallad roten, eventuellt andra media lagras i foldrar under denna, ex /media /mnt eller var du vill placera dessa.

bra kataloger att känna till är

    /home - under denna finnas alla användare i systemet
    /media, /mnt - används ofta för att koppla ihop andra lagringsytor, ex cd,usb,nätverkslagring
    /etc - inställningsfiler för systemet
    /var/log - logfiler för systemet

**visa kataloginnehåll**

när ni är i en katalog vill ni antagligen veta vad som finns där för att arbeta
med dessa filer. För att visa innehållet i en katalog använde ni ls
, *list directory contents*

följande options och argument är användbara

    ls      visar filnamn och katloger i arbetskatalogen
    ls -a   visar även dolda filer
    ls -l   visar filer i **långt** format, rättigheter,storlek

med argumentet sökväg kan man lista filer i en annan katalog än man står

    ls <option> <sökväg>

ovanståend options och argumnet kan kombinera ex

    ls -l /etc

**läsa filer**

dom flesta filer ni är intresserade av att arbeta med är läsbara textfiler.
för att läsa innehållet kan ni använda cat eller less

cat skriver ut innehållet i en fil, för stora filer är det oftast inte använbart
om det inte kombineras med andra kommandon

för att läsa innehållet i en fil är less mer bekvämt, den har en funktion för
att scrolla upp och ner i texten, pil upp, pil ner fungerar

###Skapa kopiera och flytta

Ibland vill man bara skapa en tom fil. Det går att göra med touch

    touch filnamn   -skapar en fil men namn filnamn

Kataloger kan skapas med mkdir, det finns en option -p som är använbar om ni vill
skape en katalogstruktur av flera katolger som inte tidigare existerat

ex

    mkdir -p programdagarna/2014/linux/konsol

skapar en katalog programdagarna som innehåller en katalog 2014, där finns
katalogen linux som innehåller en katalog konsol.


för att ta bort en fil använd rm

    rm filnamn      -tar bort filnamn

för att ta bort en katalog

    rmdir katalog   -tar bort katalog  


kopier filer med

    cp källfil/katalog målfil/katalog

flytta filer med

    mv källfil/katalog målfil/katalog

med option -R sker borttagning,kopiering och flyttning rekursivt, dvs är det
en katalog tas alla filer och underliggande kataloger bort

-f änvänds för att forcera, ta bort även ej tomma katloger utan varning,

men här en varning, tänk er för innan, det finns ingen enkel undo eller *"papperskorg"*

###rättigheter###

I linux sätts rättigheter på filer efter användare och grupper, rättighterna kan vara
av typen läs,skriv och körbar, det här är viktig att förstå, istället för att hitta på
något eget exempel kollar vi istället på [linuxcommand.org](http://linuxcommand.org/lc3_lts0090.php)


**sudo**

ni bör vara administratör över er dator, förut betydde det att man kunde logga in som root.
inte alla linux system, men vanligt är att man istället för att logga in som root
använder sig av sudo, vilket innebär att man får root rättigheter för ett kommando
genom att skriva sudo ibörjan av kommandot. ex

    sudo apt-get install itsdangerous


###Appstore###

linux eller rättare sagt debian-baserade linux system har haft ett
pakethanteringsystem sedan 1994, dpkg,debian packet management system.
Numera har dom ytterligare ett skal runt detta apt som används för att installera
och hantera installationer


det är enkelt att använda dom viktigaste sakerna är

    apt-get update             -uppdaterar pakethanteringsystem med nya installations kandidater
    apt-cache search paketnamn -söker efter paket med namnet paketnamn
    apt-get install paketnamn  -installerar paketnamn
    apt-get upgrade            -uppdaterar dina installioner till nyaste versionerna
    apt-get dist-upgrade       -uppdatera ditt system till en nyare version

**OBS för att installera kan du behöva vara root annvänd sudo apt-get...

###Editera filer

ganska ofta måste ni editera filer, det görs med en editor. Det finns en hel del
att välja mellan, jag föreslår att ni använder nano som är en bra nybörjar editor och finns på dom flesta system.

###Networking###

Nätverket kommer att sättas upp virtuellt på något sätt. Det kan vara bra att kunna
kolla ip-adresser på erat linux system, ifconfig visar era nätverksanslutningar.



##Samba##

Nu har ni tillräckligt med kunskaper för att följa instruktioner för att installera samba.
En av dom kortare hittar ni [här](https://help.ubuntu.com/14.04/serverguide/samba-fileserver.html)

Den innehåller en bråkdel av möjlighterna med samba, mer dokumentation och möjlighter hittar ni
på samba's hemsida [https://www.samba.org/](https://www.samba.org/)
