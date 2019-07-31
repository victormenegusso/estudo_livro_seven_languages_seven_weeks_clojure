# Intro

- linguagem funcional
- da familia do lisp
- roda sobre a JVM
- tem uma maneira de trabalhar com concorrencia bem interessante


# Começando com o Clojure

Instalação do [leiningen](https://leiningen.org/), o mesmo serve para a criação e manutenção de códigos em clojure.

Iniciando o Repl do leiningen
```bash
lein repl
```

Playground
```clojure
(println "oi")

(- 1)

(+ 1 1)

(< 1 2 3)

(= 1 1)
```

Condicionais
```clojure
(if (> 1 2) (println "true it is."))
```

Simbols / keywords
?????????

# Estrutura de dados
Em clojure temos as seguintes estruturas de dados: List, Maps Sets and Vectors.

Para todos existem diversas funcionalidades

## lista e Vectors

lista
```clojure
(list 1 2 3)

'(1 2 3)
```

vectors
```clojure
[1 2 3]
```

- listas são usadas para código ( vamos ver mais para frente )
- vectors são usados para data
- vectors são otimizados para acessos randomicos ( acessar uma possição do vetor )

## SET
Semelhante a lista, mas não possui elemento repetido

```clojure
#{:nave1 :nave2 :nave3}
```

## Maps

```clojure
(def mentors {:darth-vader "obi wan", :luke "yoda"})

;; Busca por chave
(mentors :luke)

(:luke mentors)
```

# Primeira Explosão da Mente
- percebe se que um programa em clojure parece uma lista 
- ele não só parece... ele é uma lista
- lisp vem de *List Processing*
- Clojure é uma linguagem homoicônica
  - que é um termo chique que descreve o fato de que os programas Clojure são representados pelas estruturas de dados do Clojure
  - isso é chamado de *data as code*
  - logo programas Clojure podem manipular, transformar e produzir outros programas Clojure.

# Criando Funções
```clojure
(defn force-it 
    [jedi] 
    (str "use the force." jedi))

(force-it "Gafanhoto")
```
# Bindings/Destructuring/

```clojure
(def numeros [[1 2 3] [4 5 6] [7 8 9]])

(defn center [[_ [_ param _] _]] param)

(center numeros)
```

```clojure
(def jogador {:name "Victor", :game "LOL"})

(let [{name :name} jogador]
    (str "nome do jogador " name))

(let [{name :name game :game} jogador]
    (str name game)) 
```

#Funções anonimas

- queremos rodar um map para um vector, aplicando para cada elemento uma função que conta(dobrado) o numero de caracteres que tem o texto.

```clojure
(def series ["SOA", "DEXTER"])

;; para ver o tamanho de um texto
(count "SOA")

;; rodando um map em series
(map count series)

;; escrevendo uma Anonymous Functions que duplica o count, para roda no map
(map (fn [serie] 
    (* 2 (count serie)))
    series)
;; (6 12)

;; outra forma de declar
;; # -> defini uma Anonymous Functions e o % -> é o parametro
(map #(* 2 (count %)) series)

```

# Nem tudo é um Mar de Rosas... o primeiro problema...

Recursividade
```clojure

;; estamos criando uma função recursiva para ver o tamanho de um vector
;; 'inc' é um incrementador https://clojuredocs.org/clojure.core/inc
;; obtem a calda de um vector
(defn size [v] 
    (if (empty? v)
        0
        (inc (size (rest v)))))

(size [1 2 3])
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
```

# Segunda explosão da mente: Macros

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
# Concorrencia 

# defrecord and protocls 

# Lazy Evaluation
????

# Itens não aborados mas interessantes
 - Metadata -> temos essa possibilidade com clojure
 - Java Integration -> forte integração com o java
 - Multimethods -> cara... você consegue fazer polimorfismo com essa parada... então respeita
 - Thread State -> cara podemos salvar um estado unico por thread.

# Conclusões 

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


# Links

*Confira*

[clojure](https://clojure.org/)
[vamos começar?](https://clojure.org/guides/getting_started)
[leiningen](https://leiningen.org/)

[Livro - Clojure for the Brave and True](https://www.braveclojure.com/clojure-for-the-brave-and-true/)

*Artigos*

[Clojure: Entendendo (Infinite) Lazy Sequences](https://medium.com/@antonio.gabriel/clojure-entendendo-infinite-lazy-sequences-2fd87275e048)

[Clojure Alchemy: Reading, Evaluation, and Macros](https://www.braveclojure.com/read-and-eval/)

*Podcasts*

[Tecnologias no Nubank – Hipsters #01](https://hipsters.tech/tecnologias-no-nubank-hipsters-01/)

[Tecnologias no Nubank: 3 anos depois – Hipsters #150](https://hipsters.tech/tecnologias-no-nubank-3-anos-depois-hipsters-150/)

[Programação Funcional (e (clojure)) – Hipsters #158](https://hipsters.tech/tecnologias-no-nubank-3-anos-depois-hipsters-150/)

