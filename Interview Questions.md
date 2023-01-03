# Interview Questions 📝

Nesse documento será armazenado perguntas comuns utilizadas em entrevistas para desenvolvedores iOS, totalmente em português. A ideia é adicionar uma ou mais perguntas por dia, até ter respondido todas as perguntas propostas.<br><br><br>

### 1. O que é o App Delegate Life Cycle?

O ponto de início de um aplicativo iOS é o seu *UIApplicationDelegate*, que é um protocolo que o aplicativo tem que carregar para ter informações básicas, tais quais saber quando o aplicativo abre, é minimizado ou fechado, foi aberto através de uma notificação ou link da web, etc.

Quando um aplicativo é iniciado, o primeiro método a ser chamado é: `application: willFinishLaunchingWithOptions:-> Bool`. Este método têm como objetivo o setup inicial do app. A esse ponto, os *storyboards* já foram carregados, mas o *state restoration* (recurso que permite que o usuário volte ao app no exato estado que ele utilizou pela última vez) ainda não.

##### Abertura:

- A partir do anterior, a próxima chamada é: `application: didFinishLaunchingWithOptions: -> Bool`. Esse método de retorno de chamada é chamado quando o app acaba totalmente de ser inicialializado, e o *stored state* também, assim é feita a finalização do processo, como por exemplo a criação da interface de usuário.
- Após isso ou após o app ser considerado como ativo de novo após alguma interrupção do sistema, é chamado o método `applicationWillEnterForeground`.
- `applicationDidBecomeActive`: esse método é chamado após o acima, com o intuito de finalizar a transição do app para primeiro plano novamente.

##### Fechamento:

- `applicationWillResignActive`: é chamado quando o app recebe o retorno de que está para se tornar inativo (quando o usuário volta pra Home, ou recebe uma ligação, por exemplo)
- `applicationDidEnterBackground`: é chamado quando o app entra em estado de segundo plano, após se tornar inativo. Você tem aproximadamente cinco segundos para executar qualquer tarefa necessária para fazer backup, caso o aplicativo seja encerrado mais tarde ou logo após isso.
- `applicationWillTerminate`: é chamado quando o app está para ser limpo da memória do dispositivo. Dessa forma, o uso ideal é chamar qualquer método de limpeza aqui.

Tanto o método `willFinishLaunchingWithOptions` quanto o `didFinishLaunchingWithOptions` servem para identificar se seu app é capaz de enviar notificações por push ou através de um link da web. Caso seja, é necessário retornar ` true`. <br><br>

### 2. Qual a diferença do Swift para o Objective-C?

Ambas as linguagens foram feitas para o desenvolvimento para iOS, no entanto, o Objective-C é considerado ultrapassado e antigo, uma vez que o Swift veio para substituí-lo. Atualmente, aprender Objective-C é um diferencial e provavelmente não se fará necessário, uma vez que a enorme maioria das bibliotecas já foram portadas pra Swift e o que poderia utilizar-se dela seria uma possível tradução para a linguagem mais nova. <br><br>

### 3. Qual é a arquitetura do iOS?

A arquitetura do iOS é baseada em camadas. Em seu nível mais alto, o iOS atua como um intermediário entre o hardware e os apps feitos para ele, através de interfaces desenvolvidas para o sistema. As camadas inferiores são responsáveis por fornecerem serviços básicos das quais os aplicativos necessitam, tais quais acesso a memória e conexões, enquanto as de nível superior são usadas para fornecer gráficos e serviços relacionados a interface.

A Apple fornece a maioria das suas interfaces de sistema em pacotes chamados frameworks. Esta é um diretório que contém uma biblioteca compartilhada dinâmica e cada cada de arquitetura possui um conjunto dessas para o desenvolvedor utilizar quando está programando um app.

Suas camadas são organizadas da seguinte maneira:

| [**Cocoa Touch**](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/OSX_Technology_Overview/CocoaApplicationLayer/CocoaApplicationLayer.html) |
| :----------------------------------------------------------: |
| [**Media Layer**](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/OSX_Technology_Overview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40001067-CH273-SW1) |
| [**Core Services**](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/OSX_Technology_Overview/CoreServicesLayer/CoreServicesLayer.html#:~:text=The%20technologies%20in%20the%20Core,on%20the%20app's%20user%20interface.) |
| [**Core OS**](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/OSX_Technology_Overview/CoreOSLayer/CoreOSLayer.html) | 

<br><br>
### 4. Qual a diferença entre *await* e *async let*?

Ambos são formas de executar operações assíncronas, mas trabalham de forma diferente. Quando utilizamos o *await*, o programa aguarda obter um certo resultado para continuar, enquanto o *async let*, não.
Dessa forma, quando for necessário a obtenção de um resultado que será utilizada logo em seguida para a próxima operação, é utilizada a primeira expressão e quando não há necessidade, a segunda.<br><br>

### 5. Qual a diferença entre Abstração e Encapsulamento?

Tanto abstração quanto encapsulamento são conceitos usados em **Programação Orientada a Objetos** (**POO**). A abstração se refere à parte de criação de uma classe, ou seja, um molde para criação de objetos, baseado em algo do mundo real, com seus respectivos atributos e métodos. Por padrão, os atributos da classe podem ser acessados de forma aberta publicamente, e é aí que entra o encapsulamento. Para realizá-lo, tornamos os atributos privados, e criamos métodos para acessá-los, de forma que só é possível acessar o que definimos no método, dentro da própria classe, e não fora dela.<br><br>

### 6. Qual a diferença entre *struct* e *class*? Cite um exemplo do mundo real e coloque o código para mostrar a diferença

Tanto a classe quanto a *struct* são formas de abstração. Suas diferenças:

- A classe permite herança de métodos e atributos de outras classes, a *struct* não;
- Classes possuem o conceito de "desinicializadores", utilizando o método `deinit()`. Dentro desse método, há um código que é executado quando uma instância de uma classe é destruída;
- As classes também podem ter uma ou mais referências para uma única instância.

Essa última, já citando um exemplo do mundo real também, podemos criar um objeto, definindo seus atributos. Feito isso, criamos um segundo objeto, igualando ele ao primeiro, para que ambos tenham os mesmos atributos, e logo após, alterarmos apenas um atributo do primeiro objeto. Posteriormente, se mandarmos o programa printar esse atributo alterado dos dois objetos, temos resultados diferentes, dependendo do tipo de abstração utilizado. 

Caso seja uma *struct*, os atributos serão exibidos da forma que queremos, como pedimos que o programa fizesse. 

**Código:**

```swift
struct Cachorro
{  
	var nome: String  
  var cor: String  
  var idade: Int   
  
  init(nome: String, cor: String, idade: Int) 
  {    
    self.nome = nome    
    self.cor = cor   
    self.idade = idade  
  }
}

var cachorro1 = Cachorro.init(nome: "Pituca", cor: "Preto", idade: 7) 
var cachorro2 = cachorro1
cachorro1.nome = "Bombom" 

print(cachorro1.nome) // Bombom
print(cachorro2.nome) // Pituca
```

Já se for uma classe, teremos os dois atributos com o exato mesmo valor que gostaríamos de ter alterado apenas para o primeiro objeto. <br>

**Código:**

```swift
struct Cachorro
{  
	var nome: String  
  var cor: String  
  var idade: Int   

  init(nome: String, cor: String, idade: Int) 
  {    
    self.nome = nome    
    self.cor = cor   
    self.idade = idade  
  }
}

var cachorro1 = Cachorro.init(nome: "Pituca", cor: "Preto", idade: 7) 
var cachorro2 = cachorro1
cachorro1.nome = "Bombom" 

print(cachorro1.nome) // Bombom
print(cachorro2.nome) // Bombom
```

 Isso acontece pois ao igualarmos os objetos, os mesmos ficam associados por referência, então quando tentamos acessar um método associado, ele é alterado para todas os objetos referenciados.<br><br>

### 7. O que é a View Lifecycle?

View Lifecycle é basicamente o que o próprio nome diz, o ciclo de vida de uma View (ou tela) no iOS, que inclui métodos para fazer a View aparecer, alterar o estado dela quando for desaparecer, etc.

**Diagrama do View Lifecycle:**

![](https://miro.medium.com/max/1400/1*jb1Y17gwQCRi2XCKy7_QHQ.png)

<br><br>

