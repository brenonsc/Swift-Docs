# 100 Days of Swift 🗓️

Nesse documento será armazenado os conhecimentos adquiridos no site Hacking with Swift, no proposto desafio, disponível em: https://www.hackingwithswift.com/100

Obs: Aqui abordarei mais casos de uso mais incomuns, não incluindo por exemplo definição ou uso básico de variáveis, ifs, loops, etc. <br><br>

## TIPOS COMPLEXOS:

- ### **SET**

Espécie de array, mas desordenado e que não permite itens duplicados. **Sintaxe:** `let colors = Set(["red", "green", "blue"])`. Usado especialmente em situações onde é necessário buscar um item na coleção, que é encontrado de forma muito mais rápida que em um array.<br><br>

- ### **TUPLES**

Outra forma de array, porém a tupla possui tamanho fixo e não é possível adicionar ou excluir itens nela ou mudar seu tipo de dado.

**Sintaxe:** 

1. Para criar a tupla

`var name = (first: "Taylor", last: "Swift")`

2. Para acessar dados

`name.0` ou

`name.first` <br><br>

- ### **DICTIONARY DEFAULT**

O Swift por padrão ao buscar um item que não existe em um dicionário, retorna `nil`, mas é possível adicionar uma resposta automática ao se buscar um item que não existe.

**Sintaxe:**

`favoriteIceCream["Charlotte", default: "Unknown"]`

Nesse caso, é buscado o item “Charlotte” no dicionário, e se o mesmo não for encontrado, é retornado “Unknown”. <br><br>

- ### **EMPTY COLLECTIONS**

É possível criar coleções vazias, para serem preenchidas posteriormente pelo programa.

**Sintaxe:**

1. Dictionary

`var teams = [String: String]()` ou

`var scores = Dictionary<String, Int>()`

e posteriormente adicionar itens:

`teams["Paul"] = "Red"`

2. Array

`var results = [Int]()` ou

`var results = Array<Int>()`

3. Set

`var words = Set<String>()` <br><br>

- ### **ENUMERATIONS**

Enumeration é uma forma de definir um grupo de resultados relacionados de forma a deixá-los mais fácil de serem usados. Dessa forma, não há o risco de se ter um resultado inesperado, com formas diferentes de se dizer a mesma coisa.

**Exemplo sem enums:**

`let result = "failure"`

`let result2 = "failed"`

`let result3 = "fail"`

Como mostrado, os 3 resultados são os mesmos, porém, descritos de forma diferente. Para resolver isso, podemos utilizar as enumerations.

**Sintaxe:**

```swift
enum Result 
{
	case success
	case failure
}
```

E dessa forma, quando formos representar um resultado:

`let result4 = Result.failure` <br><br>

- ### **ENUM ASSOCIATED VALUES**

Assim como enums podem armazenar tipos simples de dados, os mesmos podem também mostrar dados de forma associada. Dessa forma, é possível colocar um valor, e o que se associa a ele.

**Sintaxe:**

```swift
enum Activity 
{
	case bored
	case running(destination: String)
	case talking(topic: String)
	case singing(volume: Int)
}
```

Assim é possível colocarmos as coisas de forma mais específica, como por exemplo, falando sobre futebol:

`let talking = Activity.talking(topic: "football")` <br><br>

- ### **ENUM RAW VALUES**

É possível também acessar um dado de enum pela posição dele na estrutura. Nesse caso, é necessário fazer a associação a um número inteiro na declaração, e contar os dados iniciando de 0, assim como um vetor.

**Sintaxe:**

```swift
enum Planet: Int 
{
	case mercury
	case venus
	case earth
	case mars
}
```

Nesse caso, Mercúrio 0, Vênus 1, Terra 2, Marte 3, então, para termos o valor da Terra, acessamos dessa forma:

`let earth = Planet(rawValue: 2)`

Porém, como esse enum trata-se de planetas, não é muito natural pensarmos que a Terra é o planeta número 2, sendo assim, podemos resolver dessa forma:

```swift
enum Planet: Int 
{
	case mercury = 1
	case venus
	case earth
	case mars
}
```

Definimos Mercúrio como planeta 1, e todos abaixo seguem a sequência, então agora para acessarmos Terra, utilizamos o inteiro 3. <br><br><br>

## OPERADORES E CONDIÇÕES:

- ### **TERNARY OPERATORS**

O Swift tem um operador raramente usado que chamamos de operador ternário. Com ele, se torna possível verificar um valor e retornar uma resposta de forma simples e rápida, sem necessidade de criar um if somente pra isso.

**Sintaxe:**

```swift
let firstCard = 11
let secondCard = 10
print(firstCard == secondCard ? "Cards are the same" : "Cards are different")
```

Nesse caso, temos um print com uma condição para escrever dada a condição de a variável *firstCard* ser igual à *secondCard*. Caso sim, é printado "Cards are the same", senão "Cards are different". Isso é o mesmo que digitar o seguinte código:

```swift
if firstCard == secondCard 
{
    print("Cards are the same")
} 
else 
{
    print("Cards are different")
}
```

Concluindo, o operador torna comparações simples mais fáceis e compactas. <br><br>

- ### **RANGE OPERATORS**

Os operadores de alcance são dois: **...** e **..<**

O primeiro, identifica o alcance incluindo o último valor descrito, enquanto o segundo deixa o mesmo de fora.

**Sintaxe:**

```swift
let score = 85

switch score 
{
  case 0...49:
      print("You failed badly.")
  case 50..<85:
      print("You did OK.")
  default:
      print("You did great!")
}
```

Nesse código, podemos ver os dois casos. No primeiro, é printado "You failed badly." se a *score* for entre 0 e 49, "You did OK.", se o número for entre 50 e 84 (nota-se que o 85 não entra no alcance devido ao operador) e "You did great!", que é o caso de ser maior que 84, o que seria o resultado do código cima se executado. <br><br>

## LOOPING:

- ### **EXITING MULTIPLE LOOPS**

Em casos onde são colocados um loop dentro do outro, também é possível usar um `break`, mas isso faz com que o algoritmo saia do loop em questão. Então, caso queiramos que o código saia dos dois loops simultaneamente, utilizamos o comando `outerLoop`.

**Sintaxe:**

```swift
outerLoop: for i in 1...10 
{
  for j in 1...10 
  {
    let product = i * j
    print ("\(i) * \(j) is \(product)")

    if product == 50 
    {
      print("It's a bullseye!")
      break outerLoop
    }
  }
}
```

Como é possível notar, indicamos para o Swift qual é o `outerLoop`(inclusive, podemos dar o nome que quisermos a ele) no primeiro  `for`, e então, no momento em que atingimos o valor 50 na variável `product` dentro do segundo loop, encerramos a execução de ambos. Caso usássemos somente o `break`, a execução retornaria para o primeiro loop.<br><br>

- ### SKIPPING ITEMS

No Swift, o `break`é utilizado para encerrarmos a execução de um loop, mas caso seja necessário pular um item, utilizamos o `continue`.

**Sintaxe:**

```swift
for i in 1...10 
{
    if i % 2 == 1
  	{
        continue
    }

    print(i)
}
```

No caso desse `loop`, percorremos os números de 1 a 10, e caso os mesmos sejam *ímpares*, eles são pulados, dessa forma, só é exibido na tela os números *pares* da sequência.<br><br>

## FUNCTIONS:

- ### OMITTING PARAMETER LABELS

É possível, ao chamar uma função, omitir os nomes de parâmetros dela, para que não seja necessário escrever todas as vezes que realizar a chamada.

**Sintaxe:**

```swift
func greet(_ person: String) 
{
    print("Hello, \(person)!")
}
```

Como demonstrado, é utilizado o *underscore* ou `_`, para omitir o `person` ao realizar a chamada da função, ficando assim:

```swift
greet("Taylor")
```

Caso não houvesse o `_`, teria que ser escrito: `greet(person: "Taylor")`<br><br>

- ### DEFAULT PARAMETERS

Ao criar uma função, podemos definir um parâmetro padrão para a mesma.

**Sintaxe:**

```swift
func greet(_ person: String, nicely: Bool = true) 
{
    if nicely == true 
  	{
        print("Hello, \(person)!")
    } 
  	else 
  	{
        print("Oh no, it's \(person) again...")
    }
}
```

Aqui, como exemplo, criamos uma função que necessita receber como parâmetro uma *String* com um nome, e tem como parâmetro padrão uma variável *booleana*, que caso não seja alterada na chamada, sempre será considerada como *true*.

```swift
greet("Taylor")
greet("Taylor", nicely: false)
```

Assim, é possível chamarmos a função dessas duas formas. <br><br>

- ### VARIADIC FUNCTIONS

No Swift, é possível criarmos funções que permitem um número infinito de parâmetros, assim como funciona a própria *String* dentro do sistema, transformando a variável em um *array* da mesma.

**Sintaxe:**

```swift
func square(numbers: Int...) 
{
    for number in numbers 
  	{
        print("\(number) squared is \(number * number)")
    }
}
```

Como pode ser observado, para transformarmos um parâmetro em infinito, utilizamos o `...`, e podemos chamar logo após a função dessa forma:

```swift
square(numbers: 1, 2, 3, 4, 5)
```

Assim, obteremos como resultado os quadrados de 1 a 5. <br><br>
