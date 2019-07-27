# Intro

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

*Strings*
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

*Booleanos e Expressões*

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

Simples formas de 'if'
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