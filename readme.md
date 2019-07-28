# Intro

Resumo do capitulo *7. Clojure* do livro **Seven Languages in Seven Weeks** do *Bruce A. Tate*

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
;; false

(class true)
;; java.lang.Boolean

(class (= 1 1))
;; java.lang.Boolean

```

*Simples formas de 'if'*

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

*Lista*

São uma coleção ordenada, sendo que os elementos podems ser qualquer coisa. No Clojure listas são usadas para código e vetores são usados para data. 

```clojure
(1 2 3)
;;falha pois  Listas são avaliadas como função, por isso não conseguimos fazer desta maneira, para ter a lista temos que

(list 1 2 3)

;; ou 

'(1 2 3)
```

Operações

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

*Vectors*

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

*SETs*

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

*Maps*

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
(def mentors {:darth-vador "obi wan", :luke "yoda"})
;; #'user/mentors

;; Busca por chave
(mentors :luke)
;; "yoda"

(:luke mentors)
;; "yoda"
```

*Definindo funções*

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

*Bindings*

