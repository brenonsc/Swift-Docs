## 100 Days of Swift 🗓️

Nesse documento será armazenado os conhecimentos adquiridos no site Hacking with Swift, no proposto desafio, disponível em: https://www.hackingwithswift.com/100

Obs: Aqui abordarei mais casos de uso mais incomuns, não incluindo por exemplo definição básica de variáveis, ou uso de ifs, loops, etc.

### Tipos complexos:

- **SET**

Espécie de array, mas desordenado e que não permite itens duplicados. **Sintaxe:** **`let** colors = Set(["red", "green", "blue"])`. Usado especialmente em situações onde é necessário buscar um item na coleção, que é encontrado de forma muito mais rápida que em um array.

- **TUPLES**

Outra forma de array, porém a tupla possui tamanho fixo e não é possível adicionar ou excluir itens nela ou mudar seu tipo de dado.

**Sintaxe:** 

1. Para criar a tupla

**`var** name = (first: "Taylor", last: "Swift")`

2. Para acessar dados

`name.0` ou

`name.first`

- **DICTIONARY DEFAULT**

O Swift por padrão ao buscar um item que não existe em um dicionário, retorna `nil`, mas é possível adicionar uma resposta automática ao se buscar um item que não existe.

**Sintaxe:**

`favoriteIceCream["Charlotte", **default**: "Unknown"]`

Nesse caso, é buscado o item “Charlotte” no dicionário, e se o mesmo não for encontrado, é retornado “Unknown”.

- **********************************EMPTY COLLECTIONS**********************************

É possível criar coleções vazias, para serem preenchidas posteriormente pelo programa.

******************Sintaxe:******************

1. Dictionary

**`var** teams = [String: String]()` ou

**`var** scores = Dictionary<String, Int>()`

e posteriormente adicionar itens:

`teams["Paul"] = "Red"`

1. Array

**`var** results = [Int]()` ou

**`var** results = Array<Int>()`

1. Set

**`var** words = Set<String>()`

- ************************ENUMERATIONS************************

Enumeration é uma forma de definir um grupo de resultados relacionados de forma a deixá-los mais fácil de serem usados. Dessa forma, não há o risco de se ter um resultado inesperado, com formas diferentes de se dizer a mesma coisa.

************************************Exemplo sem enums:************************************

**`let** result = "failure"`

**`let** result2 = "failed"`

**`let** result3 = "fail"`

Como mostrado, os 3 resultados são os mesmos, porém, descritos de forma diferente. Para resolver isso, podemos utilizar as enumerations.

****************Sintaxe:****************

```swift
enum Result 
{
	case success
	case failure
}
```

E dessa forma, quando formos representar um resultado:

**`let** result4 = Result.failure`

- **ENUM ASSOCIATED VALUES**

Assim como enums podem armazenar tipos simples de dados, os mesmos podem também mostrar dados de forma associada. Dessa forma, é possível colocar um valor, e o que se associa a ele.

******************Sintaxe:******************

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

**`let** talking = Activity.talking(topic: "football")`

- **************************ENUM RAW VALUES**************************

É possível também acessar um dado de enum pela posição dele na estrutura. Nesse caso, é necessário fazer a associação a um número inteiro na declaração, e contar os dados iniciando de 0, assim como um vetor.

************Sintaxe:************

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

**`let** earth = Planet(rawValue: 2)`

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

Definimos Mercúrio como planeta 1, e todos abaixo seguem a sequência, então agora para acessarmos Terra, utilizamos o inteiro 3.