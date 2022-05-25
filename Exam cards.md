---
cards-deck: Předměty::PRG
---

# PRG Exam cards
### Proč se programy v C rozdělují do hlavičkových souborů (.h) a zdrojových souborů (.c)? #card
Rozděluji tak deklarace a implementace. Veřejné deklarace musí být známé všem. Je to jistá specifikace komunikace mezi programy. 
^1653482022211

### Jaký význam má hlavičkový soubor zdrojových souborů programu v C? #card
Rozděluji tak deklarace a implementace. Veřejné deklarace musí být známé všem. Je to jistá specifikace komunikace mezi programy. Umožňuje ostatním programům znát objekty (funkce) v knihovně bez znalosti implementace.
^1653482369161

### Jak probíhá překlad a linkování (sestavení) programu v C? #card
Kompilace vezme lidsky-čitelný textový soubor a vygeneruje objekt s instrukcemi ve strojovém kódu, který odpovídá zdrojovému kódu. Tento objekt ale není spustitelný, to zařídí linker. 
Linker vezme jeden nebo více objektových souborů a vytvoří z nich spustitelný soubor. Hledá odkazy na funkce (syscally nebo z knihoven nebo napříc objekty).
^1653482369165

### Vysvětlete rozdíl mezi překladem zdrojových souborů a linkováním programu? #card 
Kompilace vezme lidsky-čitelný textový soubor a vygeneruje objekt s instrukcemi ve strojovém kódu, který odpovídá zdrojovému kódu. Tento objekt ale není spustitelný, to zařídí linker. 
Linker vezme jeden nebo více objektových souborů a vytvoří z nich spustitelný soubor. Hledá odkazy na funkce (syscally nebo z knihoven nebo napříc objekty).
^1653483434010


### Popište proces vytvoření spustitelného programu ze zdrojových souborů jazyka C. #card
1. Preprocessor - Expandování maker a includenutí headerů
2. Kompilace - Vytvoří assemblerový kód
3. Assembly - Přemění assemblerový kód na objekt
4. Linkování - Přetvoří objekt na spustitelný soubor. Vyřeší reference na funkce.
^1653483434013

### Jaké znáte překladače jazyka C? #card 
Mingw, clang, gcc
^1653483434015


### Jak zajistíme, že se hlavičkový soubor programu v C nevloží při překladu vícekrát? #card
Pomocí preprocessorových příkazů. Kód může vypadat následovně:
```c
#ifndef header_name
#define header_name
/* Code of the header*/
#endif
```
^1653484009288


### Co je to preprocesor a jaká je jeho funkce při překladu zdrojového souboru v jazyce C? #card
Preprocessor je krok procesesu vytváření spustitelného souboru ze zdrojového kódu. Stará se o příkazy začínající pomocí hashtagu například `#include` nebo `#define`. Všechny tyto příkazy popisují nějakou změnu zdrojového kódu ještě před kompilací.. Například `#define KONSTANTA 3` hledá ve zdrojovém kódu řetězec `KONSTANTA` a nahradí ho řetězcem `3`.
^1653484009327

### Jak při překladu programu kompilátorem GCC nebo Clang rozšíříme seznam prohledávaných adresářů s hlavičkovými soubory?
Pomocí kompilační vlajky `-I dir` specifikujeme další adresář, kde hledat.

### Záleží u kompilace programu kompilátorem GCC nebo Clang při specifikaci adresářů s hlavičkovými soubory na jejich pořadí? #card 
Záleží, adresáře z vlajek se procházejí v pořadí zleva-doprava tzn. že pokud bychom měli dva stejně pojmenované headery, byl by použit ten ve více levém adresáři
^1653488688255

### Co způsobí definování makra preprocesoru NDEBUG v souvislosti s používáním funkce assert? #card
Pokud je macro jménem NDEBUG definované při includenutí `<assert.h>`.  Macro assert je vypnuté -> nic nedělá. Pokud je NDEBUG nedefinované macro assert zastaví program a vypíše chybu
^1653488688265

### Jaký tvar má hlavní funkce programu v C, která se spustí při spuštění programu v prostředí s operačním systémem?
`int main(int argc, char * argv[])`

### Jakou návratovou hodnotou programu v C indikujete úspěšné vykonání a ukončení programu? Proč zvolíte právě tuto hodnotu? #card
Úspěšné vykonání programu indikujeme návratovou hodnotou 0. Ostatní čísla vyjadřují dané chyby. 0 byla zvolena protože správný běh je jen jeden a možných chyb je několik.
^1653488688267

### Jak předáváme parametry programu implementovanému v jazyce C? #card 
Operační systém předá argumenty volání programu z terminálu do argumentů funkce main
- `argc` - počet parametrů
- `argv` - array stringů s parametry
Pozor, první argument je název programu (jak byl volaný z terminálu)
^1653488688269

### Existuje nějaká jiná možnost jak předat uživatelské parametry programu jinak než jako argument programu? #card 
- Pomocí nastavení hodnot preprocessorových konstant při kompilaci programu
- Pomocí standartního uživatelského vstupu po spuštení programu
^1653488688271

### Jaký je rozdíl mezi staticky a dynamicky linkovaným programem implementovaným v jazyce C? #card 
Statické linkování přidá dané knihovny do programu, tím zvýší jeho velkost. Dynamické linkování knihonu slinkuje až při spuštění programu.
^1653488688273

### Linkují ve výchozím nastavení překladače GCC nebo Clang statické nebo dynamické binární spustitelné soubory? #card 
Defaultní chování je dynamické linkování
^1653488688275

### Jak vkládáme do zdrojového souboru programu v C hlavičkové soubory jiných modulů nebo knihoven? #card
pomocí preprocessorového macra `#include`.  `#include <název>` pro systémové headery, v includes dir. `#include "název"`  pro hlavičky ve stejném adresáři jako program. 
^1653488688277

### Jaký rozdíl mezi použitím #include <soubor.h> a #include “soubor.h”? #card
`#include <název>` pro systémové headery, v includes dir. `#include "název"`  pro hlavičky ve stejném adresáři jako program. 
^1653488688279

### Popište rozdíl mezi deklarací a definicí funkce v jazyce C? #card 
Deklarace specifikuje interface funkce. Jak se s ní pracuje. Definice funkci implementuje a definuje kód odpovídající funkci
^1653488688281

### Jak jsou předávány parametry funkci v jazyce C? #card 
Argumenty se push-ou na stack a funkce se zavolá. Argumenty můžou být předávány:
- Hodnotou: Hodnota proměnné se zkopíruje, změna této proměnné neovlivní nic mimo proměnnou funkci
-  Referencí (odkazem): V C implementované pomocí pointerů. Funkci se přidá pointer na proměnnou a tím se dá vnější proměnná měnit z vnitřku funkce.
^1653488688283

### Co je to literál a co tímto pojmem označujeme? #card
Literály jsou konstatní reprezentace proměnných v C kódu. Například:
- `int a = 20`: `20` je int literál
- `float a = 20f` je float literál
-  `double a = 20.0`: `20.0` je double literál
- `char a = 'c'`:  `c` je char literál.
^1653488688285

### Jak lze v jazyce C realizovat předání parametru funkci odkazem? #card
Pomocí předávání pointerem
^1653488688287

### Jak lze v jazyce C omezit viditelnost funkce pouze v rámci jednoho modulu (souboru .c)? #card
Pomocí klíčového slova `static` u deklarace funkce a její neobsažením v headeru
^1653488688289

### Je možné v jazyce C volat funkci ze sebe sama (rekurze)? #card
Ano, ale nezastavené rekurze narazí na zaplnění stacku
^1653488688291

### Při volání funkce v jazyce C jsou předávány argumenty funkce, které se stanou lokálními proměnnými. V jaké části paměti jsou tyto lokální proměnné při běhu programu uloženy? #card
Na stacku
^1653488688294

### Jaké znáte kategorie proměnných z hlediska jejich umístění v paměti? #card 
Lokální proměnné -> Na stacku.
Dynamicky alokované -> na heap.
Statické/globální -> data část paměti.
^1653488688296

### Je součástí jazyka C přímá podpora (tj. klíčové/á slovo jazyka) dynamická alokace paměti? #card 
Ano, `malloc` 
^1653488688298


### Jak v jazyce C dynamicky alokovat paměť za běhu programu? #card 
Pomocí `malloc(size)` vrátí pointer na dynamicky alokovanou pamět velikosti `size`.
^1653488688301

### Je v jazyce C nutné uvolňovat dynamicky alokovanou paměť? Pokud ano, jak to uděláte? #card 
Není to vždy třeba, protože se o to většinou postará operační systém, ale je to dobrá praxe. Můžeme to udělat pomocí `free(pointer)`
^1653488688303

### Jak zjistíme velikost reprezentace datovýchtypů v jazyce C? #card 
Pomocí `sizeof(typ)` např. `sizeof(int)`
^1653488688305

### Je vždy v jazyce C velikost proměnné typu int 32 bitů? #card
Bývá to pravidlem, ale nemusí to být vždycky pravda. Je třeba kontrolovat pomocí `sizeof(int)
^1653488688307

### Kdy je velikost ukazatele v jazyce C 32-bitů a kdy 64-bitů? #card 
Záleží na architektuře procesoru 32-bit nebo 64-bit
^1653488688309

### Jak funguje modifikátor static při použití v definici lokální proměnné funkce v jazyce C? #card 
Lokální proměnná nebude alokovaná na stacku ale v části data. Znamená to v praxi, že ve všech voláních funkce se nebude hodnota proměnné resetovat, ale zůstane stejná. 
^1653488688311

### Jak funguje modifikátor extern při definici globální proměnné v jazyce C? #card 
`extern` řekne kompilátoru, že tato proměnná je z externího zdroje a slíbíme, že bude známá při linkování
^1653488688312

### Jaké znáte základní znaménkové celočíselné typy v jazyce C? #card 
char, short, int, long, long long
^1653488688314

### Rozlišuje jazyk C znaménkové a neznaménkové celočíselné typy? Pokud ano, co z toho plyne? #card 
Ano, rozlišuje. V praxi to znamená jiné chování při přetékání. (Zároveň taky definované chování při přetečení). A možnost dosáhnout větších kladných čísel (dvojnásobně větších). Takže pokud máme jistotu, že číslo nebude menší než 0 vyplatí se použít unsigned.
^1653488688316

### Jaké znáte neceločíselné typy v jazyce C? Jaká je jejich vnitřní reprezentace (velikost)? #card 
- float: 32 bitů
- double: aspoň 64 bitů
- long double: aspoň 80 bitů
^1653488688318

### Je součástí jazyka C typ logické hodnoty ,,true/false''? Pokud ano, jak se používá? Pokud ne, jak jej definujete? #card 
Existuje standartní header stdbool.h, kde jsou hodnoty true/false definované jako 1/0 (buď char nebo int v závislosti na headeru). Pracuje se s nimi tedy jako s čísly, hlavně pro if statementy, kde se dají použít pro rozhodování.
^1653488688320

### Jak v C definujete ukazatel na proměnnou, např. typu int? #card 
```C
int n = 10;
int * n_ptr = &n;
```
^1653488688321

### Jaké jsou v C omezení pro názvy proměnných a funkcí? #card 
Můžeme používat alfanumerické znaky a podtržítka. Názvy musí začínat písmenem. 
^1653488688323

### Jaké znáte escape sekvence používané v C pro řídicí znaky? #card 
- `\n` : newline
- `\r` : carriage return
- `\b` : backspace
- `\t`: tab 
^1653488688325

### Jak jsou v C reprezentovány textové řetězce? #card 
Jako array charů zakončený null terminátorem -> `\0`.
^1653488777736


### Jak v C zapisujeme identifikátory (jména funkcí a proměnných)? #card 
Co to vůbec znamená?
^1653488777744

### Jakými dvěma způsoby lze v C vytvářet konstanty? #card
^1653488777746
1. Pomocí preprocesorové direktivy `#define`
2. Pomocí klíčového slova `const`

### Popište výčtový typ jazyka C. Uveďte vlastnosti, které považujete za důležité? #card 
`enum dny {PO, UT, ST, CT, PA, SO, NE}`
přiřadí číselné hodnoty pojmenovaným konstantám. To napomáhá čitelnosti kódu. Dále se dá využít k vytvoření vlajek, které umožňují několik nastavení v jednom čísle:
``` C
enum options {
   A = 1,
   B = 2,
   C = 4,
   D = 8, 
}

int option = 0;
option &= A; // Přidá option A a C do int option.
option &= C; 
if (option & A){
 /*do stuff*/
}
```

### Jaké znáte logické operátory jazyka C? Jak se zapisují? #card 
- AND: `&&`
- OR: `||`
- NOT: `!`


### Jaké znáte bitové operátory jazyka C? Jak se zapisují? #card 
- AND: `&`
- OR: `|`
- XOR: `^`
- complement: `-`
- shift left: `<<`
- shift right: `>>`

### Jak v C realizujete dělení a násobení dvěma s využitím operátorů bitového posunu? #card
```C
int a = 10;
int l = a << 1; // l = 20
int r = a >> 1; // r = 5
```

### Jak v C definujete složený typ (struct)? #card 
``` C
struct struktura {
	int a;
	char b;
};
```

### Jak zavedeme nový typ struktury, např. pojmenovaný my_struct_s. #card 
``` C
typedef struct my_struct {
	int a;
	char b;
} my_struct_s;

```

### Co je v jazyce C pointerová (ukazatelová) aritmetika a jak se používá? #card 
Při přičítání odčítání čísel od pointeru můžeme posunout místo kam ukazuje v paměti o jednu velikost proměnné na kterou ukazuje. Např pokud int má velikost 4 bajty, zvýší se hodnota adresy v paměti o 8 pokud uděláme `n_ptr += 2`. Praktické využítí je například při přičítání k ukazateli na začátek pole.

### Jak se v C liší proměnná typu ukazatel a typu pole[] (VLA - pole variabilní délky)? #card 
Deklarace `char str[] = "Ahoj PRGC"` překopíruje hodnotu literálu do str, která je uložená na stacku. Pokud bychom udělali `char * str = "Ahoj PRGC"` neměli bychom upravovat hodnotu, protože ukazatel ukazuje na string literál někde v paměti, která nemusí být writeable. Zároveň můžeme měnit velikost `char str[]` (VLA), narozdíl od pointeru, kde bychom museli využít dynamickou paměť.

### Jak v C přistupujeme k datovým položkám složeného typu (struct)? #card 
Pomocí `.` například `my_struct.polozka`.

### Uveďte příklad přístupu k položkám proměnné složeného typu (struct) a proměnné typu ukazatel na složený typ. #card 
```C
// Typ je složený typ
int polozka = my_struct.polozka;
// Typ je ukazatel na slozeny typ
int polozka = my_struct->polozka;
```

### Jaký v C rozdíl mezi typy struct a union? #card 
Union slouží k deklaraci proměnné která může mít různý typ, například `int` nebo `char`. Union by poté měla velikost intu (toho největšího typu). Struct ukládá několik typů za sebou. Například `int` a `char`. Má poté velikost `sizeof(int) + sizeof(char)`

### Stručně popište typ union používaný v jazyce C. #card 
Union slouží k deklaraci proměnné která může mít různý typ, například `int` nebo `char`. Union by poté měla velikost intu (toho největšího typu).
```C
union data {
   int i;
   char c;
}

sizeof(union data) // equals to sizeof(int)
```

Jak se v jazyce C používá operátor přetypování?
```C
int n = 20;
int n_ptr = &n;
char * n_bytes = (char *) n_ptr; // přemění int na array jeho bajtů 
```

