
# Rychlý test PHP programátora

## PHP Junior

V testu je uvažováno s PHP 5.6.

Jaký je rozdíl mezi funkcemi `require` a `include`:

1. žádný, obě funkce se chovají stejně
2. při chybějícím souboru vyvolá `include` Warning, `require` vyvolá Fatal Error
3. `include` je zastaralá funkce, doporučuje se použít `require`
4. při chybějícím souboru vyvolá `include` Fatal Error, `require` vyvolá Warning

(2)

---

Zaškrtněte možnosti, kde nabývá `$x` hodnoty `true`:

1. `$x = (10 && 0)`
2. `$x = ('false' || -1)`
3. `$x = (5 === '5')`
4. `$x = !!("NULL" || false)`

(2,4)

---

Co vypíše následující kód
```php
function addThree($x)
{
	$x++;
	return $x + 2;
}

function addTwo(&$x)
{
	$x++;
	return $x + 1;
}

$x = 1;
echo addThree(addTwo($x)) . $x;
```
1. 61
2. 52 
3. 62 
4. 51

(3)

---

Která z podmínek je stejná jako `($a && !$b) || ($a && $b)`

1. `$a`
2. `!!$b`
3. `$a || !$b`
4. `!$b && !!$a`

(1)

---

Pokud máme `$x = 'hello'`, co vypíše `echo $x` a co `echo $$x`

1. `echo $x`  vypíše *hello* a `echo $$x` vyvolá chybu syntaxe
2. `echo $x`  vypíše *hello* a `echo $$x` vypíše adresu v paměti, protože `$$x` je reference
3. `echo $x`  vypíše *$x* a `echo $$x` vypíše *$$x*
4. `echo $x`  vypíše *hello* a `echo $$x` vypíše obsah proměnné `$hello`

tohle ne

rozdil mezi tridou, abs tridou a interfacem, mnohonasobna dedicnost
(4)

---

Kdy se zavolá na objektu konstruktor

1. při deklaraci třídy nebo libovolného jejího potomka
2. jenom při explicitním zavoláním z potomka pomocí `parent::__construct()`
3. při vytvoření instance pokud konstruktor existuje
4. při zavolání jakékoliv metody na instanci nebo potomcích

(3)

---

Co vypíše následující kód
```php
class num {
	public $val;
}
function addThree(num $n)
{
	$n->val += 3; 
	return $n;
}

function addTwo(num &$n)
{
	$n->val += 2 ;
	return $n;
}

$n = new num();
$n->val = 1;
echo addThree(addTwo($n))->val . $n->val;
```
1. 61
2. 51 
3. 62 
4. 66

(4)

---

Co bude výstupem tohoto kódu?

```php
class WarningException extends Exception {};

try {
    throw new WarningException();
    echo 'OK';
} catch (Exception $e) {
    echo 'Chyba';
} catch (WarningException $e) {
    echo 'Varování';
}
```

1. *OK*
2. *Chyba*
3. *Varování*
4. Kód je syntakticky špatně

(2)

---

Máme následující tabulky

*user*

|id | name| role|
|---|---|---|
| 1| Adam|2|
| 2| David|3|
| 3| Filip|2|
| 4| Ondřej|1|

*role*

|id | role|
|---|---|
| 1| Admin|
| 2| Manager|
| 3| User|
| 4| Guest|

Co vypíše následující dotaz:

```sql
SELECT u.id, u.name, r.role
FROM user u
  JOIN role r ON u.role = r.id
```

1. 
|id | name| role|
|--:|---|--:|
| 1| Adam|2|
| 2| David|3|
| 3| Filip|2|
| 4| Ondřej|1|
 
1. 
|id | name| role|
|--:|---|---|
| 1| Adam|Manager|
| 2| David|User|
| 3| Filip|Manager|
| 4| Ondřej|Admin|

1. 
|id | name| role|
|--:|---|---|
| 4| Ondřej|Admin|
| 1| Adam|Manager|
| 2| David|User|
| *null* | *null* |Guest|

1. 
|id | name| role|
|--:|---|---|
| 1| Adam|Admin|
| 2| David|Manager|
| 3| Filip|User|
| 4| Onřej|Guest|

tabulky vedle sebe

(2)

---

Máme následující tabulky

*user*

|id | name| role|
|---|---|---|
| 1| Adam|2|
| 2| David|3|
| 3| Filip|2|
| 4| Ondřej|1|

*role*

|id | role|
|---|---|
| 1| Admin|
| 2| Manager|
| 3| User|
| 4| Guest|

Co vypíše následující dotaz:

```sql
SELECT r.role, COUNT(1) as cnt
FROM role r
  LEFT JOIN user u ON u.role = r.id
GROUP BY r.role
```

1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|3|
| Guest|4|
1. 
| role|cnt|
|---|---|
| Admin|Ondřej|
| Manager|Adam, Filip|
| User|David|
| Guest||
1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|1|
| Guest|0|
1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|1|

(3)


## PHP Senior

Jaký návrhový vzor je nejčasťeji použít při implementaci připojení do databáze:

1. Proxy
2. Chain of Responsibility
3. Factory
4. Singleton

(4)

---

Který regulární vyraz vyhledá v následujícím textu jenom řádky, které obsahují informaci o neúspěšném dokončení importu (obsahuje slovo import fail).

```
    [2018-01-01 10:20:31] (IS IMPORT) Init
    [2018-01-01 10:20:31] (DWH IMPORT) Init
    [2018-01-01 10:20:32] (DWH IMPORT) Import start
    [2018-01-01 10:20:32] (IS IMPORT) Import start
    [2018-01-01 10:20:32] (IS IMPORT) Loading of 3 items failed, skipping
    [2018-01-01 10:20:32] (IS IMPORT) Loaded 201 items
>>> [2018-01-01 10:20:33] (DWH IMPORT) Import - failed
    [2018-01-01 10:20:34] (IS IMPORT) 43 items converted
    [2018-01-01 10:20:34] (IS IMPORT) Import finished successfully
    [2018-01-01 10:20:35] (ODD IMPORT2) Init
    [2018-01-01 10:20:37] (ODD IMPORT2) Import start
>>> [2018-01-01 10:20:39] (ODD IMPORT2) Import failed
    [2018-01-01 10:23:37] (ODD EXPORT) Export start
    [2018-01-01 10:23:39] (ODD EXPORT) Export failed
```

zvyraznit radky s failem


1. ```/import\) import (\- )?failed/i```
1. ```/IMPORT.*failed/i```
1. ```/IMPORT\).*\- failed/i```
1. ```/IMPORT\) Import failed/i```

(1)

---

Doplňte kód tak, aby byl funkční

```php
class A
{
	private $x = 0;
	private static $y = 0;
	
	public static function incY($i}
	{
		//todo A
	}

	public function decX($d)
	{
		//todo B
	}
}
```

1. A: ```$this->y += $i;```, B: ```$this->x -= $d;```
1. A: ```self->y += $i;```, B: ```$this::$x -= $d;```
1. A: ```$this->$y += $i;```, B: ```self::x -= $d;```
1. A: ```self::$y += $i;```, B: ```$this->x -= $d;```

(4)

---
Máme následující tabulky

*user*

|id | name| role|
|---|---|---|
| 1| Adam|2|
| 2| David|3|
| 3| Filip|2|
| 4| Ondřej|1|

*role*

|id | role|
|---|---|
| 1| Admin|
| 2| Manager|
| 3| User|
| 4| Guest|

Co vypíše následující dotaz:

```sql
SELECT r.role, COUNT(1) as cnt
FROM role r
  LEFT JOIN user u ON u.role = r.id
GROUP BY r.role
```

1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|3|
| Guest|4|
1. 
| role|cnt|
|---|---|
| Admin|Ondřej|
| Manager|Adam, Filip|
| User|David|
| Guest||
1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|1|
| Guest|0|
1. 
| role|cnt|
|---|---|
| Admin|1|
| Manager|2|
| User|1|

(3)

slozitejsi dotaz na seniora.

odpoved manager ; Adam, Filip - vypsat dotaz

- udelat to interaktivne
- 
