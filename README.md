# Pràctica LP: Mini Scheme

Aquesta pàgina descriu la pràctica de GEI-LP (edició 2024-2025 Q1). En aquesta pràctica has d'escriure un intèrpret per una versió simplificada de Scheme utilitzant Python i ANTLR. 

Scheme és un llenguatge de programació funcional, derivat de Lisp, conegut per la seva simplicitat i la seva estructura basada en expressions. Aquest és un exemple de programa en Mini Scheme:

```scheme
; programa que llegeix dos nombres i en calcula el seu màxim comú divisor

(define (mcd a b)
  (if (= b 0)
      a
      (mcd b (mod a b))))

(define (main)
  (display "Introdueix dos nombres: ")
  (let ((a (read))
        (b (read)))
    (display "El màxim comú divisor és: ")
    (display (mcd a b))
    (newline)))
```

## Mini Scheme

A continuació es dóna un breu resum dels conceptes bàsics de Scheme. Pots trobar més informació a la [documentació oficial de Scheme](https://docs.scheme.org/). A més, aquesta secció també afita les construccions de Scheme que caldrà implementar en aquesta pràctica.

### Sintaxi bàsica

En Scheme, les expressions són llistes on el primer element és una funció i els següents elements són els arguments. La sintaxi bàsica té la forma:

```scheme
(funció argument1 argument2 ...)
```

Per exemple, per operar tres nombres:

```scheme
(+ (* 2 3) 5)
```

- Primer s'avalua `(* 2 3)`, que dóna `6`.
- Després s'afegeix `5`, donant un resultat final de `11`.

### Operacions bàsiques

A més de la suma, Scheme té altres operacions bàsiques com:

- Restar: `(- 5 2)` (resulta en `3`)
- Multiplicar: `(* 2 3)` (resulta en `6`)
- Dividir: `(/ 6 2)` (resulta en `3`)

Els operadors artimètics requerits són `+`, `-`, `*` i `/`. Els operadors relacionals requerits són `>`, `<`, `>=`, `<=`, `=`, `<>`.

### Definició de funcions

En Scheme, es poden definir funcions mitjançant la funció `define`. Per exemple, per definir una funció que sumi dos números:

```scheme
(define (suma x y)
  (+ x y))
```

Aquesta funció, `suma`, agafa dos arguments `x` i `y`, i retorna la seva suma. Pots utilitzar-la així:

```scheme
(suma 3 4)  ; Resultat: 7
```

Com veus, els comentaris en Scheme són fets amb `;`.

Per senzilla, en aquesta pràctica, suposarem que totes les funcions s'han de definir globalment, no hi ha funcions locals a d'altres funcions. Tampoc hi ha funcions anònimes/lambda.

### Definició de constants

En Scheme, es poden definir constants amb la paraula clau `define`. Per exemple:

```scheme
(define x 5)
```

Per senzilla, en aquesta pràctica, suposarem que totes les constants s'han de definir globalment, no hi ha constants locals a d'altres funcions. També suposarem que les variables s'han de definir abans de ser utilitzades i no poden ser reassignades.

De fet, la definició de constants és una forma especial de definició de funcions, on la funció no té paràmetres!

### Condicionals

Scheme té la instrucció `if` per controlar les condicions. La sintaxi és:

```scheme
(if condició
    valor_si_cert
    valor_si_fals)
```

Per exemple:

```scheme
(if (> 3 2)
    "sí"
    "no")  ; Resultat: "sí"
```

### Condicions múltiples amb `cond`

Si tens diverses condicions, pots utilitzar `cond`, que és similar a un `switch` o un conjunt de `if` encadenats:

```scheme
(cond
  ((> 3 5) "major")
  ((< 3 5) "menor")
  (#t "igual"))
```

Aquesta expressió comprovarà les condicions en ordre i retornarà el primer resultat que tingui una guarda certa. 

### Llistes

Les llistes són una estructura de dades fonamental a Scheme. Es poden crear amb parèntesis:

```scheme
(define llista '(1 2 3 4 5))
```

L'apòstrof `'` abans de la llista indica que és una llista literal, és a dir, no s'avalua com una expressió. Això és útil per definir llistes de dades.

Una llista pot ser manipulada amb diverses funcions:

- Car (`car`) retorna el primer element d'una llista:

  ```scheme
  (car llista) ; Resultat: 1
  ```

- Cdr (`cdr`) retorna la cua de la llista (tots els elements excepte el primer):

  ```scheme
  (cdr llista) ; Resultat: (2 3 4 5)
  ```

- Cons (`cons`) afegeix un element al principi d'una llista:

  ```scheme
  (cons 0 llista) ; Resultat: (0 1 2 3 4 5)
  ```

  Així, `'(1 2 3)` no és altra cosa que `(cons 1 (cons 2 (cons 3 '())))`.

- Null (`null?`) comprova si una llista és buida:

  ```scheme
  (null? '()) ; Resultat: #t
  (null? llista) ; Resultat: #f
  ```

### Recursivitat

La recursivitat és una tècnica molt utilitzada en Scheme per tractar llistes (i altres estructures). Per exemple, una funció recursiva per sumar tots els elements d'una llista seria:

```scheme
(define (suma-llista llista)
  (if (null? llista)
      0
      (+ (car llista) (suma-llista (cdr llista)))))
```

### Noms locals amb `let`

La instrucció `let` permet definir variables locals dins d'una expressió. La sintaxi és:

```scheme
(let ((variable1 valor1)
      (variable2 valor2)
      ...)
  expressió)
```

I llavors _expressió_ pot utilitzar _variable1_ i _variable2_. Per exemple:

```scheme
(let ((x 5)
      (y 3))
  (+ x y))  ; Resultat: 8
```

### Entrada/sortida

Per llegir valors des de l'entrada estàndard en Scheme, es fa servir la funció `read`. Per escriure valors a la sortida estàndard, es fa servir la funció `display`. A més, `newline` imprimeix una nova línia.

Aquí tens una funció senzilla que llegeix dos valors de l'usuari, els suma i mostra el resultat:

```scheme
(define (sumar-dos-valors)
  (display "Introdueix dos valors: ")
  (let ((val1 (read))
        (val2 (read)))
     (display "La suma és: ")
     (display (+ val1 val2))
     (newline)))
```

### Booleans

En Scheme, `#t` representa `true` i `#f` representa `false`. Pots utilitzar-los en expressions condicionals:

- `and`: Retorna `#t` si tots els arguments són certs.
- `or`: Retorna `#t` si almenys un dels arguments és cert.
- `not`: Retorna el valor contrari (`#t` es converteix en `#f` i viceversa).

Per exemple:

```scheme
(and (> 3 2) (< 5 10))  ; Resultat: #t
(or (> 3 2) (< 1 0))    ; Resultat: #t
(not (> 3 2))           ; Resultat: #f
```

### Funcions d'ordre superior

Una funció d'ordre superior pot prendre una funció com a argument i aplicar-la a diferents valors:

```scheme
(define (aplica-dos-cops f x)
  (f (f x)))
```

Aquesta funció, `aplica-dos-coops`, accepta una funció `f` i un valor `x`, i aplica la funció `f` dos cops al valor `x`.

Exemple d'ús:

```scheme
(define (dobla x) (* x 2))
(aplica-dos-cops dobla 5)  ; Resultat: 20
```

La funció `map` aplica una funció a cada element d'una llista i retorna una nova llista amb els resultats. Aquí tens una implementació simple de `map`:

```scheme
(define (map func llista)
  (cond
    ((null? llista) '())
    (else (cons (func (car llista)) (map func (cdr llista))))))

; Exemple d'ús:
(map dobla '(1 2 3 4))  ; Retorna (2 4 6 8)
```

La funció `filter` filtra els elements d'una llista, retornant una nova llista amb els elements que compleixen una condició, expressada com un predicat. Aquí tens una implementació de `filter`:

```scheme
(define (filter predicat llista)
  (cond
    ((null? llista) '())  ;
    ((predicat (car llista))
     (cons (car llista) (filter predicat (cdr llista))))
    (#t (filter predicat (cdr llista)))))  

; Exemple d'ús:
(define (parell? x) (= (mod x 2) 0))
(filter parell? '(1 2 3 4))  ; Retorna (2 4)
```

## La vostra feina

Heu d'escriure un intèrpert de Mini Scheme utilitzant ANTLR i Python. Aquest intèrpret ha de ser capaç de llegir i avaluar expressions de Scheme, així com definir i cridar funcions. Heu d'utilitzar ANTLR per escriure la gramàtica i els visitadors necessaris. Cal que la vostra implementació sigui compatible, com a mínim, amb la sintaxi i les característiques de Scheme descrites anteriorment.

El vostre programa s'ha de preparar amb un cop de `make`. Llavors, el vostre intèrpret s'ha d'invocar amb la 
 comanda `python3 scheme.py` tot passant-li com a paràmetre el nom del fitxer que conté el codi font (l'extensió dels fitxers per programes en scheme és `.scm`). Per exemple:

```bash
make
python3 scheme.py programa.scm
```

El programa sempre ha de començar per la funció `main`. L'entrada-sortida ha de ser via stdin/stdout. Així es podran utilitzar operadors de redirecció i *pipes*:

```bash
python3 scheme.py programa.scm < entrada.txt > sortida.txt
```

### Jocs de proves

El vostre projecte ha d'incloure jocs de proves que demostrin que el vostre intèrpret funciona correctament. Aquests jocs de proves han de ser fitxers amb extensió `.scm` que continguin programes vàlids en Scheme. La qualitat (però no la quantitat) dels jocs de proves serà un factor important en l'avaluació de la pràctica. Els jocs de proves poden venir acompayats de fitxers d'entrada (`.inp`) i de sortida (`.out`) per facilitar la seva repetició.

### Llibreries

Utilitzeu `ANTLR` per escriure la gramàtica i l'intèrpret. Podeu utilitzar lliurament qualsevol llibreria **estàndard** de Python. No podeu usar cap altra llibreria no estàndard.

### Errors

Si el programa en Scheme conté errors sintàctics, cal reportar-ho.

En canvi, per senzilla, en aquesta pràctica, suposarem que no es dónen mai errors semàntics ni errors de tipus. En cas de donar-se, l'efecte del programa és indefinit.

Igualment, suposarem que mai es donen errors d'execució (com ara divisions per zero, agafar el cdr d'una llista buida, ètc). En cas de donar-se, l'efecte del programa és indefinit.

## Lliurament

Heu de lliurar la vostra pràctica al Racó. Només heu de lliurar un fitxer ZIP que, al descomprimir-se generi:

- Un fitxer `README.md` que documenti el vostre projecte.

  - vegeu, per exemple, https://www.makeareadme.com/.

- Un fitxer `Makefile` tal que, quan s'executi `make`, es crein els fitxers necessaris per executar el vostre projecte.

- Un fitxer `scheme.g4` amb la gramàtica del LP.

- Un fitxer `scheme.py` amb el programa principal de l'intèrpret.

- Més fitxers `.py` amb les classes, visitadors i funcions auxiliars.

- Jocs de proves en fitxers `.scm` amb entrades en fitxers `.inp` i sortides en fitxers `.out`.

- Res més. 

Observacions:

- Els vostres fitxers de codi en Python han de seguir les regles d'estı́l PEP8, tot i que podeu oblidar les restriccions sobre la llargada màxima de les lı́nies. L'ús de tabuladors en el codi queda prohibit (zero directe).

- El termini de lliurament és el **dimecres 8 de gener a les 08:00**.

- Per evitar problemes de còpies, no pengeu el vostre projecte en repositoris públics.

- El vostre lliurament no ha d'incloure els fitxers que genera ANTLR, aquests s'han de crear via `make`.

- Si no heu realitzat alguna part de la pràctica, o sabeu que aquest té algun error en alguna part, deixeu-ho escrit al `README.md`.

## Avaluació

L'avaluació de la vostra pràctica tindrà en compte diversos aspectes clau, entre els quals es destaquen els següents:

1. **Qualitat de la gramàtica**: Es valorarà la qualitat de la gramàtica ANTLR, incloent la seva _completitud_, _precisió_, _concisió_ i _robustesa_. La gramàtica ha de ser capaç de reconèixer correctament els programes i les expressions de Mini Scheme, així com de manegar els diferents literals i operadors que es poden realitzar en aquest llenguatge. 

2. **Qualitat del codi**: S'examinarà el codi font tenint en compte diversos factors, com ara la _correctesa_, la _completitud_, la _llegibilitat_, l'_eficiència_, el _bon ús dels identificadors_, ètc. També es tindrà en compte la _bona estructuració_ del codi, és a dir, l'ús adequat de funcions, classes, mòduls i altres elements que afavoreixin la redacció, la comprensió i el manteniment del codi a llarg termini. Es valorarà negativament l'ús de funcions llargues o poc clares, funcions incomprensibles sense especificació, la presència de codi duplicat o innecessari, acoblament fort, variables globals o atributs de classe erronis, comentaris excessius, i altres pràctiques nocives. Per aquesta pràctica, l'eficiència és secundària, però no s'admetran disbarats.

3. **Qualitat de la documentació**: S'analitzarà la documentació del projecte, amb especial atenció a la seva _claredat_, _precisió_ i _completesa_, alhora que la seva _concisió_. La documentació hauria de descriure adequadament el funcionament del codi, les seves funcions i característiques principals, així com qualsevol altre aspecte rellevant que faciliti la comprensió i l'ús del projecte. La documentació també ha de deixar clares les decisions de disseny preses.

4. **Qualitat dels jocs de proves**: Es valorarà l'existència, la _cobertura_ i la _fiabilitat_ dels jocs de proves dissenyats per verificar el correcte funcionament del codi. Els jocs de proves han de ser suficientment amplis i variats per garantir que el codi respon de manera adequada a diferents situacions i casos d'ús. Tanmateix, els jocs de proves han de ser _limitats, _concisos_ i _eficaços_, evitant la redundància i la repetició innecessària. Alhora, el propòsit dels jocs de proves ha de ser _fàcil de comprendre_. Han de ser fàcils d'_executar_, i han de proporcionar una _sortida clara_ que permeti identificar ràpidament qualsevol problema o error.

En definitiva, és important recordar que es tracta d'un projecte de programació i, per tant, s'espera que el codi segueixi _bones pràctiques de programació_. 

