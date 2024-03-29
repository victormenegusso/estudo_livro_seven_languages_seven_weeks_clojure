# Intro

Temos uma guilda para a leitura do livro **Seven Languages in Seven Weeks** do *Bruce A. Tate*,

# Apresentação
[roteiro para apresentação](roteiro-apresentacao.md)

# Resumo 
Resumo do capitulo *7. Clojure*

## Sobre o Clojure / LISP

Lisp é uma família de linguagens de programação concebida por John McCarthy em 1958, O seu nome vem de List Processing *(a lista é a estrutura de dados fundamental desta linguagem)*. Tanto os dados como o programa são representados como listas, o que permite que a linguagem manipule o código fonte como qualquer outro tipo de dados.

Existem diversos dialetos de Lisp, sendo os mais conhecidos: Common Lisp, Scheme e Clojure
https://pt.wikipedia.org/wiki/Lisp

**Todos os Lisps**
- Depois de Fortran, Lisp é a mais velha linguagem ativa comercialmente.
- É uma linguagem funcional, mas não pura
- O seu nome vem de List Processing
 - uma chamada de função é o primeiro elemento da lista
 - usa sua própria 'Estrutura de dados' para expressar código. *data as code*
 - Esses dois primeiros pontos, fazem que o lisp seja uma linguagem ideal para metaprogramação.

**JVM**
 - podemos reaproveitar tudo da JVM

**Concorrencia**
 O clojure trabalha muito bem com concorrencia, existe um conceito chamado 'Transactional memory' que funciona semelhante a 'Transactional database'.

## Day 1: Training Luke

*Instalação*

No livro é utilizada a versão 1.2.
https://app.assembla.com/wiki/show/clojure/Getting_Started -> pagina desatualizada

Utilizase o leiningen, para facilitar a criação/manutenção dos projetos em clojure
https://leiningen.org/

**Obs:** tenha o java instalado


*Criando o projeto*

```bash
lein new seven-lenguages
cd seven-lenguages
```

*Iniciando o console do clojure*
```bash
lein repl
```

Este comando vai fazer com que o leiningen instale as dependencias, inicie/chamar o java com alguma jars do clojure.

**obs:** ao iniciar o console do clojure pode ocorrer o seguinte erro: ```Failed to write core dump. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again``` para corrigir basta executar: ```ulimit -c unlimited```.
*ver mais sobre o problema*

### Chamando funções
```clojure
(println "oi")

(- 1)
(+ 1 1)

;; divisões funcionam um pouco diferente
(/ 1 3)
;; 1/3

(/ 2.0 4)
;; 0.5

(class (/ 1 3))
;; clojure.lang.Ratio

;; clojure.lang.Ratio -> para evitar a perda de precisão o cloujure tem um tipo chamado clojure.lang.Ratio

(mod 5 4)
;; 1
```

Esta forma de chamar operações se chama *'prefix notation'*, isso pode assustar muita gente no começo, mas tem suas vantagens:

```clojure
(/ (/ 12 2) (/ 6 2))
;; 2 

(+ 2 2 2 2)
;; 8

(/ 8 2 2) ;; -> (8 / 2 ) / 2 -> (/ (/ 8 2) 2)
;; 2

(< 1 2 3)
;; true

(< 1 3 2 4)
;; false
```

```clojure
;; ver como explicar a questão do forms

(+ 3.0 5)
;; 8.0

(+ 3 5.0)
;; 8.0
```

### Strings
```clojure
(println "mestre yoda\nluke\ndarth vader")

(str 1)

(str "mestre yoda " "luke " "darth vader ")

(str "1" 2 "3" 4)

;; chars são representados com o \ precedido do char
(str \f \o \r \c \e)

(= "a" \a)
;; false -> pois char é diferente de string

(= (str \a) "a")
;; true
```

### Booleanos e Expressões

```clojure
(= 1 1.0)
;; false

(= 1 1)
;; true

(class true)
;; java.lang.Boolean

(class (= 1 1))
;; java.lang.Boolean

```

#### Simples formas de 'if'

```clojure
(if true (println "true it is."))
;; true it is.
;; nil

(if (> 1 2) (println "true it is."))
;; nil

(if false (println "true") (println "false"))
;; false
;; nill 
```


### List, Maps Sets and Vectors

Em Clojure Listas, Mapas e Vetores são as grandes estrutura de dados

#### Lista

São uma coleção ordenada, sendo que os elementos podems ser qualquer coisa. No Clojure listas são usadas para código e vetores são usados para data. 

```clojure
(1 2 3)
;;falha pois  Listas são avaliadas como função, por isso não conseguimos fazer desta maneira, para ter a lista temos que

(list 1 2 3)

;; ou 

'(1 2 3)
```

##### Operações

```clojure
(first '(1 2 3))
;; 1

(last '(1 2 3))
;; 3

(rest '(1 2 3))
;; (2 3)

(cons 0 '(1 2 3))
;; (0 1 2 3)
```

obs:
```clojure
(class '(1 2 3))
;; clojure.lang.PersistentList
```

#### Vectors

Semelhante a lista, mas são otimizadops para acessos randomicos *(acessar qualquer posição do vertor)*

```clojure
[1 2 3]
;; [1 2 3]

(class [1 2 3])
;; clojure.lang.PersistentVector
```

```clojure
(first [1 2 3])
;; 1

(nth [10 20 30] 2)
;; 30

(nth [10 20 30] 0)
;; 10

(last [1 2 3])
;; 3

(rest [1 2 3])
;; (2 3)

;; vetores tambem são funções, passar o index como arg
([1 2 3] 2)
;; 3

(concat [1] [2])
;; (1 2)
```

#### SETs

Semelhante as listas, mas não possue elementos repetidos.

```clojure

#{:nave1 :nave2 :nave3}
;; #{:nave2 :nave3 :nave1}

(class #{:nave1 :nave2 :nave3})
;; clojure.lang.PersistentHashSet

(def espacoaereo #{:nave1 :nave2 :nave3})
;; #'user/espacoaereo

(count espacoaereo)
;; 3

(sort espacoaereo)
;; (:nave1 :nave2 :nave3)

(sorted-set 2 3 1)
;; #{1 2 3}

(clojure.set/union #{:luke} #{:vader})
;;#{:vader :luke}

(clojure.set/difference #{1 2 3} #{2})
;; #{1 3}

(#{1 2 3} 2)
;; (#{1 2 3} 2)

(#{1 2 3} 5)
;; nil
```

#### Maps

Semelhante as outras linguagens, 'Chave Valor'

```clojure
{:chewie :wookie :lea :human}
;; {:chewie :wookie, :lea :human}


{:chewie :wookie :lea}
;; Syntax error reading source at (REPL:1:23).
;;Map literal must contain an even number of forms


;; uma forma mais fácil de ler
{:chewie :wookie, :lea :human}
;; {:chewie :wookie, :lea :human}

```

```clojure
(def mentors {:darth-vader "obi wan", :luke "yoda"})
;; #'user/mentors

;; Busca por chave
(mentors :luke)
;; "yoda"

(:luke mentors)
;; "yoda"
```

### Definindo funções

A forma para definir as funções `(defn [params] body)`

```clojure
(defn force-it [] (str "use the force." "Luke."))


;; adicionando um DOC a função
(defn force-it 
    "The first function a young Jedi needs"
    [] 
    (str "use the force." "Luke."))

(doc force-it)
;;([])
;;  The first function a young Jedi needs
;; nil

;; adicionando um parametro na função
(defn force-it 
    "The first function a young Jedi needs"
    [jedi] 
    (str "use the force." jedi))
```

### Bindings

Binding -> o processo de atribuição de parâmetros com base nos argumentos de entrada.
https://clojuredocs.org/clojure.core/binding

destructuring -> é uma maneira de vincular nomes aos valores dentro de uma estrutura de dados. A desestruturação nos permite escrever códigos mais concisos e legíveis.
https://clojure.org/guides/destructuring


```clojure
(def line [[0 0] [10 20]])
;;'user/line

(defn line-end [ln] (last ln))

(line-end line)
[10 20]

;; outra forma de montar a função usando destructuring
;; usamos o _ para ignorar um paramentro
(defn line-end [[_ second]] second)


(defn print-first-second
    [[first second]] 
    (println (str first second)))

(print-first-second [1 2 3])
;;12


(def numeros [[1 2 3] [4 5 6] [7 8 9]])

(defn center [[_ [_ param _] _]] param)

(center numeros)
;; 5

;; outra forma de definir
(defn center [[_ [_ param]]] param)

;; outra forma
(defn center [vetor]
    (let [[_ [_ param]] vetor] param))

```

*Destructuring em MAP* 

```clojure
(def jogador {:name "Victor", :game "LOL"})

(let [{name :name} jogador]
    (str "nome do jogador " name))
;; "nome do jogador Victor"

(let [{name :name game :game} jogador]
    (str name game)) 
;; "VictorLOL"
```

*Destructuring Combinando MAP e Vector*

```clojure
(def personagens 
    [{:nome "jax teller" :serie "SOA"} {:nome "jon snow" :serie "GOT"}])

(let [[_ {nome :nome}] personagens] 
    (str "nome do segundo personagem: " nome))    
;; "nome do segundo personagem: jon snow"

```

### Anonymous Functions

Forma de criar `fn [parameters*] body`

```clojure
(def series ["SOA", "DEXTER"])

;; para ver o tamanho de um texto
(count "SOA")
;; 3

;; rodando um map em series
(map count series)
;; (3 6)

;; escrevendo uma Anonymous Functions que duplica o count, para roda no map
(map (fn [serie] 
    (* 2 (count serie)))
    series)
;; (6 12)

;; outra forma de declar
;; # -> defini uma Anonymous Functions e o % -> é o parametro
(map #(* 2 (count %)) series)
;; (6 12)

```

*Apply e filter*

```clojure
(def v [3 2 1])

(apply + v)
;; 6

(apply max v)
;; 3

(filter odd? v)
;; (3 1)

(filter #(< % 3) v)
;; (2 1)
```

### Entrevista

...

## Day 2: Yoda and the Force

### Recursion with loop and recur

```clojure

;; estamos criando uma função recursiva para ver o tamanho de um vector
;; 'inc' é um incrementador https://clojuredocs.org/clojure.core/inc
;; obtem a calda de um vector
(defn size [v] 
    (if (empty? v)
        0
        (inc (size (rest v)))))

(size [1 2 3])
;; 3
```

**Importante**
Diferente das outras linguagens funcionais que trabalham com recursão em calda *( https://en.wikipedia.org/wiki/Tail_call )* por padrão. O Clojure não suporta implicitamente isso, por causa de limitações da JVM. Para isso devemos usar o `loop` e `recur`

https://clojure.org/about/functional_programming#_recursive_looping

```clojure
(loop [x x-initial-value, y y-initial-value] (do-something-with xy))
```

```clojure
(defn size [v] 
    (loop [l v, c 0]
    (if (empty? l)
        c
        (recur (rest l) (inc c)))))


(size [1 2 3])
;; 3
```

### Sequences

Sequences encapsula todas collections *(set, maps, vectors e semelhantes)* , strings, file system structures *(strams, directoreies)*

https://clojure.org/reference/sequences

#### Tests

```clojure
;; Returns true if (pred x) is logical true for every x in coll, else false. https://clojuredocs.org/clojure.core/every_q
(every? number? [1 2 3 :four])
;; false

;; se algum da lista ser verdade é retornado true
(some nil? [1 2 nil])
;; true

(not-every? odd? [1 2 3])

(not-any? number? [:one :two :three])
;; true
```

#### Changin a sequence

```clojure
(def words ["luke" "chewie" "han" "lando"])

(filter (fn [word] (> (count word) 4)) words)
;; ("chewie" "lando")

(map (fn [x] (* x x)) [1 1 2 3 5])
;; (1 1 4 9 25)

(reduce + [1 2 3 4])
;; 10

```

### Lazy Evaluation

```clojure
;; uma sequencia finita
(range 1 10)
;; (1 2 3 4 5 6 7 8 9)

;; uma sequencia infinita - Returns a lazy
(repeat 1)

;; com sequencias infinitas, precisamos obter um subconjuto finito, para isso usamos o 'take'
(take 3 (repeat "123 testando"))

(defn fib-pair [[a b]] )


;; 
(defn factorial [n] (apply * (take n (iterate inc 1)))

(factorial 5)
;;120

``` 
### defrecord and protocls

Para o clojure, as melhores partes da OO são os tipos e protocolos ( interface ) e a pior coisa é a herança.

Com o defrecord e protocol, estamos escrevendo código nativo para JVM sem Java.

```clojure
;; especie de interface....
;; estamos falando que bussola, tem 3 funções 
(defprotocol Bussola
    (direcao [c])
    (esquerda [c])
    (direita [c]))

(def direcoes [:norte :leste :sul :oeste])

;; rem -> % do java
(defn virar [base montante]
    (rem (+ base montante) (count direcoes)))

(virar 1 1)
;; 2

;; implementando o protocolo
(defrecord BussolaBacana
    [rolamento]
    Bussola)
```

### Macros

```clojure
(defn unless 
    [test body] 
    (println "da funcao")
    (if (not test) 
        (body)))

;; gostariamos que só rodasse o print, caso a função seja false...
(unless true (println "parametro"))
;;parametro
;;da funcao
;;nil

;; Como avaliamos o paramentro antes de executar a função, o print 'parametro' foi executado primeiro

(defmacro unless 
    [test body]
    (println "da funcao")
    (list 'if (list 'not test) body))

(defn unless [test body] (if (not test) body))

(unless true (println "parametro"))
;;da funcao
;;nil

(unless false (println "parametro"))
;;da funcao
;;parametro
;;nil

```


## Day 3: An Eye for Evil

O Clojure lida com estados mutaveis/concorrencia com o *STM -> Software Transactional Memory*

### References and Transactional Memory

Quando queremos mudar o estado de uma referenciam devemos usar um escopo de transação.

Vamos ver sobre References, atoms e agents,
estes durante a operação de leitura não realizam lock ou block.

#### References

```clojure
;; criando uma referencia
(ref "SONS")

;; criando uma referencia e atribuindo a uma 'variavel'
(def serie (ref "SONS"))

;; obtendo o valor da referencia
(deref serie)

;; obtendo o valor da referencia ( segunda maneira)
@serie

;; tentativa de mudar uma referencia -> falha por não estar em um escopo de transação
(alter serie str " OF")
;; Execution error (IllegalStateException) at user/eval2015 (REPL:1).
;;No transaction running

(dosync (alter serie str " OF"))


```

Mesmo sendo trabalhoso evitamos problemas como 'race conditions' e 'deadlocks'

#### Working with Atoms

Em Clojure Atoms são ,bit de estado encapsulado, podemos utilizalos quando temos uma referencia e queremos ter thread safety.

```clojure
(atom "atom maneiro")

(def cuidado (atom "atom maneiro"))

(reset! cuidado "atom paia")
```

##### Building an Atom Cache

#### Working with Agents

Agents são semelhante aos atoms, são um wrapped de data.
Este garante que apenas 1 thread vai mudar o valor o dado por vez, ele bloqueia a execução dos demais ( parece um semaforo )

```clojure
(defn duplicado [x] (* 2 x))

;; definindo um agente 
(def agente1 (agent 1))

(send agente1 duplicado)
```

### Futures

Uma resposta a Thread

```clojure
(def marotagem (future (Thread/sleep 5000) "Dando um Time ai Galera"))

;; execução de forma sincrona
@marotagem
```

### Itens não aborados mas interessantes
 - Metadata -> temos essa possibilidade com clojure
 - Java Integration -> forte integração com o java
 - Multimethods -> cara... você consegue fazer polimorfismo com essa parada... então respeita
 - Thread State -> cara podemos salvar um estado unico por thread.

## Wrapping Up Clojure

 - The Lisp Paradox -> com Multimethods, macros temos um poder de flexibilidade pesado. Mas isso é sua fraqueza tambem, macros são poderosa para desenvolvedores com experiencia, nas mãos erradas.... "Grandes poderes Grandes Responsabilidades" 
 - Pontos fortes
   - A Good Lisp -> muitos consideram o Clojure um dos melhores lisps, tem redução do numero de  pararenteses. 
   - O Ecosistema -> ta usando a JVM e isso é mais que suficiente.
   - Concorrência -> O Clojure tira da mão do DEV o controle de concorrência
   - Integração com o java
   - Lazy Evaluation -> reduz o ovehead de computação
   - Data as Code -> Programas são listas.
 - Pontos Fracos
   - legibilidade ( eu ainda tenho a opnião que legibilidade vai do costume do peão)
   - Curva de Aprendizado -> é não é facil.
   - Lisp Limitado -> temos o problema com recursão em caldo. Não tem Reader Macros.


