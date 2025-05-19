# Clean-Code-Notes
## Sumário

1. []
2. [Nomes Significativos](#nomes-significativos)
3. [Funções](#funções)
4. [Comentários](#comentários)
5. [Formatação](#formatação)
6. [Objetos e Estruturas de Dados](#objetos-e-estruturas-de-dados)
7. [Tratamento de erro](#tratamento-de-erro)
8. [Limites](#limites)
9. [Testes de unidade](#testes-de-unidade)
10. [Classes](#classes)
11. [Sistemas](#sistemas)

# Nomes Significativos

Nomeamos muitas coisas na programação, e como fazemos muito isso, é bom que façamos bem. Escolher bons nomes leva tempo, mas economiza mais. Algumas regrinhas para criação de bons nomes são:

#
## **Nomes que Demonstram seu Propósito**

O nome de uma variável deve dizer tudo sobre ela. Se ele precisa de um comentário, então não é um bom nome.
```php
<?php
//Ruim
$n = "Iasmim"; 

//Bom
$name = "Iasmim";
?>
```
#
## **Evitar Informações Erradas**

Deve-se evitar passar dicas falsas que confundam o sentido do código. Por exemplo, usar palavras que possam ser confundidas com o nome de outras coisas. No livro, há o exemplo de palavras que são usadas como nomes de plataformas Unix.

Também devemos ter cuidado ao usar nomes parecidos para duas coisas diferentes, pois fica difícil de distinguir a diferença entre eles. Exemplo: `XYZControllerForEfficientHandlingOfStrings` e `XYZControllerForEfficientStorageOfStrings` são muito semelhantes.

```php
<?php
//Ruim
$dtTime = "2025-01-20";

//Bom
$dateString = "2025-01-20";
?>
```

#
## **Faça Distinções Significativas**

Alterar um nome de maneira arbitrária, só porque o nome que você quer usar já está em uso, não é o bastante. Se os nomes precisam ser diferentes, então eles devem ter significado distinto. Exemplo: chamar uma variável de `oLivro` só porque já existe a variável `livro`.

Usar números sequenciais em nomes não é expressivo o suficiente, pois esse tipo de nome não nos diz nada sobre o que o programa faz.

```php
<?php
//Ruim
$product1 = "Livro";
$product2 = "Caderno";

//Bom
$book = "Livro";
$notebook = "Caderno";
?>
```
#
## **Use Nomes Pronunciáveis**

Crie nomes pronunciáveis, se não puder pronunciá-lo, será difícil discutí-lo sem parecer um idiota (ele conta uma história sobre isso o livro e eu rachei demais). Isso é importante, porque programação também é uma atividade social.

É importante fazer a distinção de nomes de uma forma que o leitor compreenda a diferença e entenda rapidamente o que aquela variável faz.

```php
<?php
//Ruim
$dtStr = "2025-01-20"

//Bom
$dateString = "2025-01-20";
?>
```

#
## **Use Nomes Passíveis de Busca**

Usar nomes pronunciáveis e passíveis de busca, que não sejam confundidos com outras coisas. Usar apenas uma letra `a` para nomear algo é uma escolha ruim, pois é uma letra comum e caso seja preciso fazer uma busca, ela vai aparecer em todo o texto. Nomes longos se sobressaem aos curtos. 

> O tamanho de um nome deve ser proporcional ao tamanho do escopo.

```php
<?php
//Ruim
$a = 10;
$b = 20

//Bom
$firstNumber = 10;
$secondNumber = 20
?>
```
#
## **Evite Codificações**

Já temos de lidar com bastante codificação e não precisamos acrescentar mais. Codificar informações do escopo ou tipos em nomes simplesmente adiciona uma tarefa extra de decodificação. Além de raramente serem pronunciáveis, é fácil de escrevê-los incorretamente.

#
## **Evite o Mapeamento Mental**

Evitar o mapeamento mental, onde o leitor precisa ler todo o código para entender o que é a variável (que pode estar declarada apenas com 1 letra).

> Uma diferença entre um programador esperto e um programador profissional é que este entende que clareza é fundamental. Os profissionais usam seus poderes para o bem, e escrevem códigos que outros possam entender.

#
## **Nomes de Classes**

Classes e objetos devem ter nome substantivos.
```php
<?php
class UserManager
{
  //código da classe
}
?>
```

#
## **Nomes de Métodos**

Nomes de métodos devem ter verbos (get, post, delete, etc). 

Podemos usar *factory methods* quando os construtores estiverem sobrecarregados com nomes que descrevam os parâmetros. Para forçar o uso, torne os construtores correspondentes como privados.
```php
<?php
class UserManager
{
  public function getUserData()
  {
    //código do método
  }
}
?>
```

#
## **Selecione uma Palavra por Conceito**

Escolher uma palavra por cada conceito abstrato e permanecer com ela até o fim. É confuso ter diferentes palavras como métodos equivalentes de classes diferentes (`fetch, retrieve` e `get`, por exemplo).

#
## **Não Faça Trocadilhos**

Não usar a mesma palavra para 2 propósitos.
```php
<?php
//Ruim
$bankAccount = "123456";
$riverBank = "Amazon River"

//Bom
$bankAccountNumber = "123456";
$riverSide = "Amazon River"
?>
```

[⬆️Voltar ao Topo](#sumário)


# Funções
Neste capítulo, Robert C. Martin (Uncle Bob) explora como escrever funções limpas, claras e eficazes — que são blocos fundamentais de qualquer código bem estruturado.

> A ideia central é:
“Funções devem fazer uma única coisa, e fazê-la bem.”

#
## **Tamanho de Blocos e Identação**

Características de funções bem escritas:
- Elas devem ser pequenas, no máximo 20 linhas.
- Os blocos dentro de instruções `if`, `else`, `while` devem ter apenas a linha de chamada de função dentro de outra função.
- Não devem ter estruturas aninhadas.
- As funções devem fazer apenas 1 coisa e fazê-las bem.

#
##**Princípio de responsabilidade única** - um dos princípios SOLID, afirma que uma classe deve ter apenas uma razão para mudar, ou seja, ela deve ser responsável por uma única tarefa ou funcionalidade. Isso torna o código mais fácil de entender, manter e modificar, pois alterações em uma funcionalidade específica não afetam outras partes do sistema.

Se uma função faz apenas alguns passos em um nível abaixo do nome da função, então ela está fazendo apenas 1 coisa. Para saber se uma função faz mais de uma coisa, é verificando se é possível extrair outra função a partir do nome dela sem gerar uma reformulação.

#
## **Regra Decrescente**

Não dá para dividir em seções as funções que fazem apenas 1 coisa. É preciso verificar se todas as instruções dentro da função possuem o mesmo nível de abstração, pois vários níveis diferentes dentro da mesma função causam confusão. Código é lido de cima para baixo, onde cada função é seguida de outra no próximo nível de abstração de modo que o programa é lido descendo um nível de abstração por vez enquanto a lista de funções é lida.

> **Abstração:** usar um cenário real e trazer para o programa somente o essencial para seu funcionamento.

#
## **Switch**

Por padrão, elas fazem N coisas, então é difícil deixá-las pequenas. Mas, podemos garantir que cada `switch` está em uma classe de baixo nível e nunca é repetido. É usado o polimorfismo pra isso.

> **Polimorfismo:** a mesma variável tem funções diferentes em cada classe mas sem alterar sua estrutura original. 

A solução seria usar o `switch` em uma `abstract factory`.
> **Abstract Factory** - é um padrão de design que cria famílias de objetos relacionados sem especificar suas classes concretas. Ele fornece uma interface para criar objetos de diferentes tipos, garantindo que sejam compatíveis entre si, sem precisar alterar o código cliente.

#
## **Nome da Função**

Usar nomes descritivos para as funções. Nomes extensos são melhores que nomes pequenos e confusos ou um comentário. O nome deve explicar o que ela faz. Importante ser consistente na nomeação das funções do módulo. Por exemplo, usar `add` pra toda função que faz a ação de adicionar algo: `addConvenio`, `addProcess`, etc.

#
## **Parâmetros**

Podemos frasear o nome da função. Isso permite uma sequência de fácil dedução. A quantidade ideal de parâmetros para a função é 0. Para ter mais de 3, deve-se ter um bom motivo. Mesmo assim, não deve ser usado. Parâmetros fazem com que o leitor do código precise entender de onde vem aquele parâmetro, pois ele não está no mesmo nível de abstração da função. Eles também deixam os testes mais complicados, pois é necessário escrever um teste para cada combinação de parâmetros. Um parâmetro de entrada é a melhor coisa depois de zero parâmetro.

#
## **Formas Mônades Comuns**

Há duas razões para se usar um único parâmetro: quando se está fazendo uma pergunta sobre ele, como `boolean fileExists("MyFile")`; ou quando vamos transformá-lo em outra coisa, como `InputStream fileOpen("MyFile")`.

Outra utilidade de um parâmetro em uma função seria um evento. Aqui tem um parâmetro de entrada, mas nenhum de saída. O programa serve para interpretar a chamada de função como um evento e usar o parâmetro para alterar o estado do sistema `passwordAttemptFailedNtimes(int Attempts)`.

> **Deve ficar claro para o leitor que se trata de um evento. Usar nomes que descrevam exatamente o que faz.** 


### **Parâmetros Lógicos**

Se a função vai transformar o parâmetro de entrada, a alteração deve aparecer como um valor retornado. São feios, complicam a assinatura do método pois claramente fazem mais que uma coisa (faz 1 se o valor for true e outra se for false).


### **Funções Díades**

São mais complicadas de entender, pois precisamos “processar” na nossa cabeça o 1° parâmetro, e depois seguir por 2°. E acabamos deixando de lado o 1°. Dois parâmetros podem ser necessários quando, por exemplo, temos uma função que recebe eixos cartesianos. Nesse caso, os dois parâmetros são componentes de um único valor.


### **Funções Tríades**

Sempre que possível, tentar convertê-las em mônades. São muito difíceis de entender. Todos os problemas encontrados nas outras triplicam aqui.


### **Objetos como Parâmetros**

Quando uma função precisa de mais de um parâmetro, significa que alguns deles podem ficar em uma classe própria. Então é melhor criar uma classe para eles.

`Circle makeCircle(double x, double y, double radius);`


### **Listas como Parâmetros**

Às vezes precisamos passar um número variável de parâmetros para uma função. Caso eles sejam todos tratados da mesma forma, então eles são equivalentes a um único parâmetro do tipo `list`.


### **Verbos no Nome da Função**

Um bom nome para função pode ir desde explicar seu propósito à ordem e a finalidade dos parâmetros. Na mônade, deve formar um par verbo/substantivo: `write(name)`.


### **Palavra-chave**

Ao usar esse formato, codificamos os nomes dos parâmetros no nome da função `writeField(name)`.


### **Evitar Efeitos Colaterais**

São mentiras. A função promete fazer apenas uma coisa, mas faz outras escondidas. E isso acaba gerando acoplamentos temporários e dependências. 
> **Acoplamentos temporários** - ocorrem quando duas partes do código se tornam dependentes por um curto período, mas essa dependência não é permanente. Embora às vezes inevitáveis, devem ser minimizados, pois podem tornar o código mais difícil de manter e modificar.

### **Parâmetros de Saída**

Deve-se evitar seu uso. Caso a função precise alterar o estado de algo, então ela deve alterar o estado do objeto ao qual ela pertence.


### **Separação Comando-Consulta**

A função ou responde algo ou faz uma consulta, não deve fazer as duas coisas.


### **Exceções a Retorno de Códigos de Erro**

Funções que retornam códigos de erros é uma violação da separação comando-consulta, pois os comandos são usados como expressões de comparação em estruturas `if`. Quando usamos o retorno de erros, é criado um problema com o qual o chamador precisará lidar. Já com tratamento de exceção, o código de tratamento pode ficar separado e ser simplificado.


### **Extrair os try-catch**

Os blocos `try-catch` devem ficar em suas próprias funções, porque são feios e confundem a estrutura do código.


### **Tratamento de erros**

Funções que tratam erros devem tratar apenas erros. Ou seja, depois do `catch/finally`, não se deve ter mais código. Quando se usa exceções invés de erros, as novas exceções são derivadas da classe `Exception` e não é necessário recompilar.

Este é um exemplo do Princípio de Aberto-Fechado (OCP, sigla em inglês [PPP02]).


### **Evitar Repetição de Código**

Com o código repetido, é necessário modificar as funções toda vez que ocorrer uma alteração no algoritmo. E também são oportunidades para omissão de erros.

**O Princípio do Não Se Repita (DRY - Don't Repeat Yourself)**: evitar repetição de código ao máximo. Cada pedaço de conhecimento deve ter uma única, inequívoca, e autoritativa representação dentro de um sistema. Isso não só facilita a manutenção, mas também reduz as chances de erro.


### **Programação Estruturada**

Alguns programadores seguem a regra de Edsger Dijkstra ([SP72]), que cada função e cada bloco dentro dela tenha uma entrada e uma saída. Dessa forma, cada função só teria um `return`. Porém, isso oferece pouca vantagem quando a função é pequena. Escrever uma função é como escrever um artigo. O primeiro rascunho fica horrível, mas aos poucos vai sendo refinado.

> **Uncle Bob:** "Mas jamais se esqueça de que seu objetivo verdadeiro é contar a história do sistema, e que as funções que você escrever precisam estar em perfeita sincronia e formar uma linguagem clara e precisa para lhe ajudar na narração."

[⬆️Voltar ao Topo](#sumário)

# Comentários

> Não insira comentários num código ruim, reescreva-o.
> — Brian W. Kernighan e P. J. Plaugher

Os comentários são um mal necessário da programação. Se as linguagens de programação fossem expressivas o suficiente, não seria necessário nenhum comentário.O  uso adequado de comentários é compensar nosso fracasso em nos expressar no código.
Antes de usar um comentário, é melhor pensar bem e ver se não há como se expressar melhor através do código.
- Quanto mais antigo e mais longe do código ele estiver, mais provável que esteja errado.
- Comentários imprecisos são piores do que nenhum.
- Ao invés de gastar tempo fazendo comentários, melhor gastar refazendo o código.
- Ás vezes, a criação de uma função cujo nome seja bem descritivo evita o uso de um comentário.
- Ás vezes um comentário pode ser apenas a explicação da intenção por trás de uma decisão.

### **Exlique-se no código**

Pode ser necessário esclarecer o significado de alguns parâmetros ou valores retornados obscuros para algo inteligível. Devemos tentar esclarecer esse parâmetro ou valor retornado, mas caso não seja possível, então um comentário se faz útil.
Também é bom sempre se certificar que ele é preciso e se não tem outra opção a não ser fazer um comentário.

### **Alerta de consequêcias**

Pode ser útil alertar os coleguinhas de algumas consequências. Por exemplo, se há uma função no código que demora para se concluir, então podemos deixar um comentário avisando.

### **Comentários ToDo**

Ás vezes pode ser o caso de usar um `//todo.` Eles são tarefas que os programadores acham que devem ser efetuadas, mas que não podem ser feitas no momento. Algumas IDEs ajudam a encontrar com mais facilidade esse tipo de comentário, mas mesmo assim, devemos procurá-los regularmente e eliminar os que puder. A maioria deles é suporte ou desculpas para um código de baixa qualidade ou justificativas para a falta de decisões.

### **Comentários ruins**

Se optar por criar um comentário, então gaste tempo necessário para fazê-lo bem. Usar um comentário só porque acha que deve ou porque o processo o requer é besteira.
> Qualquer comentário que o obrigue a analisar outro módulo em busca de um significado falhou em transmitir sua mensagem e não vale os bits que consome.


[⬆️Voltar ao Topo](#sumário)

# Formatação

Devemos seguir um padrão de formatação durante todo o projeto e aplicá-la de forma consistente. A formatação é muito importante, pois é ela quem permite a legibilidade correta para os próximos desenvolvedores do projeto. 
> Seu estilo e disciplina sobrevivem, mesmo que seu código não.


### Formatação vertical 

O tamanho máximo deve ser 500 linhas. Embora não seja uma regra fixa, é bom levá-la em conta, pois arquivos pequenos são mais fáceis de se entender.

### Metáfora do jornal

No jornal (para aqueles que nunca viram um jornal impresso, dá um google ai), temos no topo o título, seguido de uma introdução e depois vem a história detalhada. O jornal é lido verticalmente. É assim que um código fonte deve ser. O nome em si já deve ser o suficiente para nos dizer se aquele é o módulo certo ou não.

### Espaçamento vertical entre conceitos

As partes superiores do código devem fornecer os conceitos e algoritmos de alto nível. Os detalhes devem surgir conforme descemos o código, até encontrarmos as funções de baixo nível. Cada grupo de linhas no código representa um pensamento. E esses pensamentos devem ser separados por uma linha em branco.

### Continuidade vertical

Linhas de código que estão relacionadas devem aparecer verticalmente unidas (nada de ter comentários entre elas). Comentários inúteis entre elas dificultam a leitura.


### Distância vertical

É frustrante navegar por códigos complexos, tentando entender como as funções e variáveis se relacionam, o que pode ser confuso e demorado. A recomendação é manter conceitos intimamente relacionados próximos uns dos outros no código, preferencialmente no mesmo arquivo-fonte, para facilitar a compreensão, a menos que haja uma boa razão para o contrário. Além disso, evita-se usar variáveis protegidas. O objetivo é melhorar a inteligibilidade do código e reduzir a necessidade de navegar por vários arquivos-fonte e classes.

- Declaração de variáveis: devem ficar o mais próximas possível de onde serão usadas. As variáveis locais devem ficar no topo de cada função.
```php
<?php
function readPreferences() {
    $filePath = getPreferencesFile();
    $preferences = getPreferences();
    $properties = new Properties($preferences);

    try {
        $is = fopen($filePath, 'r');
        if ($is === false) {
            throw new Exception("Failed to open file: $filePath");
        }

        $properties->load($is);
        setPreferences($properties);
    } catch (Exception $e) {
        try {
            if ($is) {
                fclose($is);
            }
        } catch (Exception $e1) {
        }
    }
}
?>
```

- Devem-se declarar as variáveis de controle para loops dentro da estrutura de iteração. Em casos raros, pode-se declarar uma variável  no início de um bloco ou depois de um loop em uma função longa.
```php
<?php
public function countTestCases{
  $count = 0;
  foreach ($this->test as $each) {
    $count += $each->countTestCases();
  }
  return $count;
}
?>
```
- Variáveis de instância: devem ser declaradas no início da classe. Isso não aumenta a distância vertical entre elas pois provavelmente elas são usadas por quase todos os métodos. Muito já se falou sobre onde declará-las, mas o que importa é que elas sejam declaradas em um local bem conhecido, para que todos saibam onde buscar as declarações.
- Funções dependentes: se uma função chama outra, elas devem ficar verticalmente próximas, e a que chama deve ficar acima da função que vai ser chamada.
- Afinidade conceitual: quanto maior a afinidade, mais próximos eles devem ficar. Essa afinidade deve-se basear em uma dependência direta (uma função chamando outra, uma função usando uma variável). Um grupo de funções que efetuam operações parecidas também se encaixam aqui.

### Ordenação vertical

De modo geral, é desejável que as chamadas de função apontem para baixo, pois isso cria um fluxo natural no código. Isso nos permite passar os olhos nos arquivos-fonte e obter uma idéia de algumas das primeiras funções, sem ter de mergulhar nos detalhes.

### Formatação horizontal

Não tem um limite ideal, mas devemos nos esforçar para manter as linhas curtas. Ultrapassar 120 caracteres é uma falta de cuidado, apenas.

### Espaçamento e continuidade horizontal 

Usamos para associar coisas que estão intimamente relacionadas e para desassociar outras fracamente relacionadas. Podemos colocar os operadores de atribuição entre espaço em branco para destacá-los.
```php
<?php
function measureLine($line) {
    global $lineCount, $totalChars, $lineWidthHistogram; 
    $lineCount++;
    $lineSize = strlen($line);
    $totalChars += $lineSize; //fica mais fácil a leitura
    $lineWidthHistogram->addLine($lineSize, $lineCount);
    recordWidestLine($lineSize);
}
?>
```
Mas não devemos colocar espaços entre nomes de funções e os parênteses de abertura, pois eles são intimamente relacionados. Podemos separar os parâmetros dentro dos parênteses com espaço, para realçar a vírgula.

### Alinhamento horizontal

Não é um alinhamento prático, pois a leitura dele é mais demorada e podemos nos confundir. Se tivermos listas longas de declarações que precisem ser alinhadas, o problema está no tamanho das listas e não na falta de alinhamento.

### Identação

Um arquivo possui níveis diferentes de hierarquia, e para tornar visível essa hierarquia, indentamos as linhas de acordo com sua hierarquia. Ela permite que façamos uma leitura mais pratica e rápida do código.
    - instruções no nível do arquivo (classes, por exemplo) não são indentadas;
    - métodos dentro das classes são indentados a um nível à direita delas (dá um tab);
    - implementação de método são indentados a um nível à direita da declaração do método;
    - implementação de blocos são implementados a um nível à direita do bloco que as contém; e assim por diante.
    
Às vezes, ficamos tentados a não usar a indentação em estruturas pequenas. Mas pode-se usar uma linha em branco entre as declarações, para expandir o escopo.
```php
<?php
public function CommentWidget() {
};

public function render() {
}
?>
```

### Regra de equipes

Uma equipe de desenvolvedores deve escolher um único estilo de formatação e todos os membros devem usá-la, para que o software tenha um estilo consistente.
> Um bom sistema é composto por uma série de documentos de fácil leitura. Eles precisam ser consistentes e sutis.

[⬆️Voltar ao Topo](#sumário)

# Objetos e Estruturas de Dados

Declaramos nossas variáveis como privadas pois não queremos ninguém dependendo delas, para que possamos alterá-las da forma que quisermos.

### Abstração de dados

Abstração de dados é esconder como os dados são armazenados e manipulados, expondo apenas o que o usuário precisa saber. Isso evita que a implementação interna fique exposta, tornando o código mais flexível e fácil de manter.

Não basta criar getters e setters → O ideal é criar uma interface que represente o conceito dos dados, não apenas seus valores crus.
Vantagem: O código fica mais flexível e menos dependente da implementação interna.

### Antissimetria data/objeto

Objetos usam abstrações para esconder seus dados e expõem as funções que operam em tais dados. Já as estruturas de dados expõem seus dados e não possuem funções significativas.

O código procedural (usado em estruturas de dados) facilita a adição de novas funções sem precisar alterar as estruturas de dados existentes. O código orientado a objeto (OO), por outro lado, facilita a adição de novas classes sem precisar alterar
as funções existentes.

Porém, o código procedural dificulta a adição de novas estruturas de dados, pois todas as funções teriam de ser alteradas. O código OO dificulta a adição de novas funções, pois todas as classes teriam de ser alteradas.
> O que é difícil para OO é fácil para procedural, e vice-versa.

### Lei de Deméter

É uma heurística: um objeto deve ter conhecimento apenas de seus próprios componentes ou objetos intimamente relacionados a ele, e não deve expor a estrutura interna de seus componentes. É literalmente sobre não falar com estranhos.

Um objeto deve interagir apenas com seus vizinhos imediatos e não com os vizinhos de seus vizinhos. Isso reduz a dependência, tornando o código mais modular e fácil de manter.
```php
<?php
class Motor {
    public function ligar() {
        echo "Motor ligado!\n";
    }
}

class Carro {
    private Motor $motor;

    public function __construct() {
        $this->motor = new Motor();
    }

    public function getMotor(): Motor {
        return $this->motor; //Expõe a estrutura interna
    }
}

class Pessoa {
    private Carro $carro;

    public function __construct() {
        $this->carro = new Carro();
    }

    public function dirigir() {
        $this->carro->getMotor()->ligar(); //A Pessoa acessa o Motor diretamente, isso quebra o encapsulamento
    }
}
?>
```
### Train Wrecks

São chamados assim pois parecem vários carros de trem acoplados. Elas são consideradas descuidadas e devem ser evitadas. O código acima poderia ser dividido como:
```php
<?php
$opts = $ctxt->getOptions();
$scratchDir = $opts->getScratchDir();
$outputDir = $scratchDir->getAbsolutePath();
?>
```
Se esse código viola a Lei de Deméter? depende se `ctxt`, `Options` e `ScracthDir` são ou não objetos ou estrutura de dados. Se forem objetos, é uma violação clara da lei; se forem estrutura de dados sem atividades, então a lei não se aplica.

O uso de funções de acesso confunde essas questões.
Isso não seria tão confuso se as estruturas de dados tivessem variáveis públicas e nenhuma função, enquanto objetos tivessem apenas variáveis privadas e funções públicas. Mas alguns frameworks exigem que estruturas de dados simples tenham métodos acessores e de alteração.

### Híbridos

São estruturas que são metade objetos e metade estrutura de dados. Elas possuem funções que fazem algo, e também variáveis ou métodos de acesso e de alteração públicos, que por sua vez tornam as variáveis privadas em públicas.
Com isso, outras funções externas podem usar essas variáveis da forma como um programa procedimental usaria uma estrutura de dados.
> ás vezes chama-se Feature Envy em Refatoração: ocorre quando um método de uma classe acessa os campos de outra classe com mais frequência do que seus próprios campos.

### Objetos de transferência de dados

A forma perfeita de uma estrutura de dados é uma classe com variáveis públicas e nenhuma função. Também chamado de DTO. São estruturas úteis, principalmente para se comunicar com banco de dados, por exemplo.
Geralmente são os primeiros numa série de estágios de tradução que convertem dados brutos num BD em objetos no código.

### Active Record

São formas especiais de DTOs. São estruturas de dados com variáveis públicas; mas possuem métodos de navegação, como save e find. Basicamente, são traduções diretas das tabelas de bancos de dados de outras fontes de dados.
Não podemos tratá-los como objetos, pois isso acaba criando um híbrido. Devemos tratá-los como um estrutura de dados e criar objetos separados que contenham as regras de negócio e que ocultem seus dados internos.


[⬆️Voltar ao Topo](#sumário)

# Tratamento de Erro

As coisas podem dar errado. Para isso, usamos o tratamento de erros.
Alguns códigos possuem muitos tratamentos de erros, o que torna difícil ver o que o código faz. Esse recurso é importante, mas se obscurecer a lógica, está errado.

#
## Use exceções ao invés de retornar códigos

No passado, haviam linguagens que não suportavam exceções, o que tornava o tratamento de erro limitado. Ou era criado uma flag de erro ou retornava um código de erro que o chamador pudesse verificar.
Porém, essas técnicas enchiam o chamador, que precisava realizar as verificações logo após a chamada. Geralmente, também esqueciam de fazer isso.
Por isso, o ideal é lançar a exceção, o código de chamada fica mais limpo e a lógica fica clara.

#
## Crie primeiro a estrutura try-catch-finally 

As exceções definem um escopo dentro do programa. Ao executar um código na parte `try`, é declarado que aquela execução pode ser cancelada a qualquer momento e então continuar no `catch`.

Os blocos `try` são como transações, então o `catch` deve deixar o programa num estado consistente, independente do que aconteça no `try`. Por isso, uma boa prática é começar com uma estrutura `try-catch-finally` quando for escrever um código que talvez lance exceções. Isso ajuda a definir o que se deve esperar do código, independente do que ocorra de errado n código executado pelo `try`.

#
## Exceções não verificadas

São aquelas que o compilador não força o tratamento ou declaração. Em muitas linguagens, só há as exceções não verificadas. 

### Por que não usar exceções verificadas?

A ideia aqui é não usar exceções verificadas, pois elas possuem 3 problemas:
- **Violam o Princípio Aberto-Fechado**: classes devem estar abertas para extensão, e fechadas para modificação. Com as exceções verificadas, quando um método lança a exceção, é obrigatória a modificação dos métodos que fazem parte da cadeia de chamadas (desde onde há o lançamento até o ponto onde ela é tratada).
- **Cascata de alterações**: quando uma função de nível inferior é alterada para lançar uma nova exceção, todos os métodos que chamam essa função devem ser alterados para lidar com a nova exceção. Dessa forma, as alterações podem se propagar por toda a aplicação.
- **Encapsulamento**: elas quebram o encapsulamento porque forçam os métodos intermediários a conhecerem detalhes específicos das exceções lançadas por métodos inferiores, mesmo que os métodos intermediários não precisem o não devam lidar com eles.
As exceções verificadas podem ser úteis em situações específicas, como criação de bibliotecas críticas. Em outros usos, seus custos superam as vantagens.

#
## Forneça exceções com contexto

Cada exceção lançada precisa de um contexto suficiente para determinar a fonte e localização de um erro.
É ideal criar mensagens de erro informativas e passá-las junto com as exceções. Mencione a operação que falhou e o tipo de falha.

#
## Defina as classes de exceções segundo as necessidades do chamador

É importante definir classes de exceções de acordo com as necessidades do seu chamador (quem captura e trata as exceções).
Para evitar repetição de código e capturas de exceções genéricas, pode-se usar o `wrapper`, que encapsula e converte todas as exceções específicas em uma única exceção genérica. Isso deixa o código mais limpo e flexível.

#
## Defina o fluxo normal

Com essa estrutura de código usando exceções, reduzimos a complexidade causada pelo tratamento de exceções, porém é alta a detecção de erro no programa, já que temos várias capturas.
Para evitar isso, podemos usar o Special Case Pattern, que captura exceções excepcionais e impede que o código fique poluído.
Dessa forma, a lógica do código principal **não precisa mais se preocupar com exceções** nem lidar com "casos especiais". A decisão sobre o que retornar fica encapsulada dentro da implementação da classe.

#
## Não retorne nem passe `null`

Não retornar `null` pelas funções também é errado, pois basta esquecermos uma verificação `null` para quebrar o código.
Também é horrível passar `null` para os métodos, a menos que tenha alguma API que espere receber `null`.

[⬆️Voltar ao Topo](#sumário)


# Limites

Basicamente, o capítulo fala sobre a integração limpa entre códigos externos, sejam eles pacotes de outros fabricantes, com o código que está sendo desenvolvido por nós.

#
## Explorando e aprendendo sobre limites
Códigos de terceiros podem nos ajudar a obter funcionalidades em menos tempo, mas é bom criar testes para esses códigos que forem usados.

Entender código de terceiros é difícil e integrá-los também. Então, pode-se criar testes para explorar nosso conhecimento sobre esse código. Jim Newkirk chama isso de *teste de aprendizagem.*

Nesses testes, chamam a API do código externo como faríamos ao usá-la na nossa aplicação. O teste foca no que desejamos saber sobre a API.

#
## Os testes de aprendizagem são melhores do que de graça

No fim, eles acabam não custando nada. é necessário aprender sobre a API e escrever os testes foi uma forma fácil de obter o conhecimento. Eles são experimentos precisos que ajudam no nosso entendimento.

Além de serem de graça, possuem um retorno positivo. Quando houver nossas distribuições daquele pacote externo, podemos executar os testes para ver se há diferenças nas atividades.

Você precise ou não do conhecimento proporcionado pelos testes de aprendizagem, deve-se definir um limite claro por meio de uma série de testes externos que experimentem a interface da mesma forma que seu código faria.

#
## Limites limpos

Um código sempre tem alterações com o passar do tempo. Bons projetos de software acomodam modificações sem muito investimento ou trabalho. Quando usa-se códigos que não possuem limites bem definidos, é preciso verificar nosso investimento e garantir que uma mudança futura não custe tanto.

O código precisa de um limite bem claro e testes que definem o que é esperado dele.

Deve-se evitar que grande parte do código enxergue as particularidades de códigos terceiros (vide [Capítulo 6](#objetos-e-estruturas-de-dados) ).
> É melhor depender de algo que você controle do que pegar algo que acabe controlando você.

[⬆️Voltar ao Topo](#sumário)

# Testes de Unidade

Este capítulo traz o conceito de TDD, com seus usos e boas práticas.

TDD é uma abordagem de desenvolvimento de software onde o teste é escrito antes do código. Ele segue um ciclo:

- Red → Escrever o teste para a nova feature. Como o código real ainda não foi escrito, o teste irá falhar.
- Green → Escreva apenas o código suficiente para passar no teste.
- Refactor → Melhore o código enquanto mantém o teste aprovado.

Isso permite a escrita de um código limpo, com manutenibilidade e sem bugs, garantindo que tudo é testado antes de ser implementado.

#
## As 3 leis do TDD

1° → Não se deve escrever o código de produção até criar um teste de unidade de falhas.

2° → Não se deve escrever mais de um teste de unidade do que o necessário para falhar, e não compilar é falhar.

3° → Não se deve escrever mais códigos de produção do que o necessário para aplicar o teste de falha atual.

#
## Como manter os testes limpos

Fazer um teste de maneira rápida e mal feita, sem pensar muito nas boas práticas de um desenvolvimento de testes, é pior do que não ter teste nenhum.

Os testes precisam evoluir junto com o código de produção. Quanto pior o teste, mais difícil é mudá-lo. Quanto mais confuso for o teste, maiores as chances de gastar mais tempo escrevendo novos testes do que desenvolvendo o código de produção. 

Conforme o código de produção é modificado, os testes antigos começam a falhar e a bagunça no código de teste dificulta fazê-lo funcionar de novo. Assim, os testes começam a ser vistos como um problema.

O código de testes requer cuidado, raciocínio e planejamento. é preciso mantê-lo tão limpo quanto o código de produção.
> Os códigos de testes são tão importantes quanto o código de produção.

#
## Os testes habilitam as “-idades”

Caso os testes não estejam limpos, eles serão perdidos. E sem testes, perde-se a flexibilidade do código. São eles quem mantém o código reutilizável e passíveis de manutenção. 

Se há testes, não há medo de realizar alterações no código. Sem testes, cada alteração pode criar um bug. Não importa o grau de flexibilidade da arquitetura, sem os testes há uma relutância em realizar alterações por conta de bugs inesperados. 

Então, ter uma coleção de testes que cubram todo o código de produção ajuda a manter o projeto mais limpo.
> Quanto pior for o teste, pior o código se torna. No final, você perde os testes e seu código se degrada.

#
## Testes limpos

O que torna os testes limpos é a legibilidade. E como ter legibilidade no teste? Tendo clareza, simplicidade e consistência de expressão. Os testes devem ir direto ao ponto e usar apenas os dados e funções que precisa.
> Num teste você quer dizer muito, com o mínimo de expressões possíveis.

#
## Um padrão duplo

O ambiente de teste e o de produção possuem requisitos diferentes. Geralmente, o ambiente de produção pode ter alguma restrição de CPU ou memória. Mas no de testes, não há restrição alguma. 
Há coisas que não podem ser feitas no de produção que esteja perfeitamente bem no de teste. Geralmente é mais sobre eficiência de memória e CPU.

#
## Uma afirmação por teste

Há uma escola de pensamento que diz que cada função deve ter apenas uma instrução de afirmação (assert). Esses testes são mais fáceis e rápidos de entender. Caso não seja possível ter só uma, o ideal é minimizar ao máximo as afirmações.

#
## Um único conceito por teste

A melhor regra é um conceito em cada função de teste. Caso tenha um teste com mais de um conceito sendo testado, é ideal minimizar o número de confirmações por conceito e testar apenas um conceito por teste.

#
## F.I.R.S.T

Testes limpos seguem mais 5 regras:

Fast → devem ser rápidos. 

Independent → os testes não devem depender um dos outros.

Repeatable → deve-se poder repetir os testes em qualquer ambiente. 

Self-Validating → devem ter uma saída booleana. 

Timely → precisam ser escritos em tempo hábil. Devem ser criados antes do código de produção onde serão aplicados.

[⬆️Voltar ao Topo](#sumário)

# Classes

#
## Organização das classes

Aqui, o Uncle Bob fala de uma convenção padrão Java para declaração de classes. Porém, não é aplicável às outras linguagens. Mas há alguns conceitos que são comuns à todas elas, como: manter a consistência do projeto, manter o padrão escolhido pela equipe, escrever um código legível e fácil de entender.

#
## Encapsulamento

Não é ideal que todas as variáveis e funções sejam privadas. Às vezes é preciso tornar uma variável ou função protegida para que ela possa ser acessada por testes. Aqui, o teste é prioridade. Entretanto, primeiro procuramos uma forma de manter a privacidade. Perder o encapsulamento é o último recurso.

#
## As classes devem ser pequenas!

Primeira regra: as classes devem ser pequenas.

Segunda regra: as classes devem ser menores ainda.

O tamanho é determinado contando as responsabilidades da classe.

O nome da classe precisa descrever quais responsabilidades ela faz, e esse nome é a primeira forma de ajudar a determinar o tamanho dela. Quanto mais ambíguo for o nome, maior a chance de a classe ter muitas responsabilidades.

> 📝 Devemos conseguir descrever a classe com cerca de 25 palavras sem usar “se”, “e”, “ou” ou “mas”. Se tiver alguma dessa conjunções, então a classe tem mais responsabilidades do que deveria.

#
## O Princípio da Responsabilidade Única

A classe deve ter um, e apenas um, motivo para mudar. Isso dá uma definição de responsabilidade e uma orientação sobre o tamanho da classe. Ela deve ter uma responsabilidade e um motivo para mudar.

O SRP é um dos conceitos mais importantes em OO. Queremos que os sistemas sejam compostos por muitas classes pequenas, e não poucas classes grandes. Cada classe pequena contribui com outras para obter os comportamentos desejados no sistema. 

> ⚠️ O projeto não termina se o programa funciona. É preciso melhorá-lo, torná-lo modular e escalável, deixá-lo com fácil manutenção. Por isso, o SRP é tão importante.

#
## Coesão

As classes devem ter poucas instâncias de variáveis. Cada método da classe deve manipular uma ou mais dessas variáveis. Quanto mais variáveis um método manipular, mais coeso o método é para a classe. Uma classe onde cada variável é utilizada por um método é totalmente coesa. 

Porém, não é aconselhável e nem possível criar essas classes totalmente coesas, mas também é desejável alcançar o máximo de coesão. 

Ás vezes, quando tentamos manter as funções pequenas e listas de parâmetros curtas, acabamos criando muitas instâncias de variáveis que são usadas por vários métodos. É necessário sempre tentar separar as variáveis e os métodos em duas ou mais classes de modo que as novas classes sejam mais coesas.

#
## Como organizar para alterar

Em muitos sistemas, mudanças são constantes, e a cada alteração existe o risco de quebrar algo. Em um sistema limpo, organizamos as classes de modo a reduzir os riscos nas alterações. 

> As classes devem ser abertas para expansão, mas fechadas para alteração.

#
## Como isolar das alterações

As necessidades mudam, e o código também. Em POO, há classes concretas, que detalham a implementação, e classes abstratas, que são apenas conceitos. Uma classe que depende de detalhes concretos corre perigo quando tais detalhes são modificados. Então, podemos oferecer interfaces e classes abstratas para isolar o impacto desses detalhes.

Depender de detalhes concretos também gera desafios aos testes.

Então, o uso de interfaces e classes abstratas desacoplam o projeto, facilitando manutenção, entendimento e testes.

[⬆️Voltar ao Topo](#sumário)

#
# Sistemas

A construção é um processo diferente de utilização. A lógica de negócio (uso) deve estar separada da lógica de montagem (construção) do sistema.

*Os sistemas devem separar o processo de inicialização - criação de objetos e conexão entre dependências - da lógica em tempo de execução que vem após a inicialização.* 

Muitos sistemas não fazem essa separação, o código de processo de inicialização é misturado na lógica em tempo de execução. Isso muitas vezes causa dependências codificadas, atrapalhando a compilação e testes.

Então, mais uma vez, é ideal que o código seja o mais modular possível. O processo de inicialização da construção e atribuição de um objeto não são exceções, também precisam ser modularizados. 

#
## Separação do Main

Uma maneira de separar a construção do uso e isolar todos os aspectos da construção no `main` ou em módulos chamados por ele, e seguir modelando o sistema assumindo que todos os objetos foram construídos e atribuídos adequadamente.

> 📝 A ideia é: o método ou arquivo principal (main, index.php, app.php, etc.) não deve conter lógica de negócio. Ele deve apenas montar o sistema, ou seja, construir os objetos e conectá-los.


### Por quê?

O `main()` é o ponto de entrada do sistema. Ele constrói os objetos necessários e então os passa ao aplicativo, que simplesmente usa. Isso deixa o sistema:

- Modular
- Testável
- Manutenível
- Flexível para mudanças

### Exemplo

**Errado:**

```php
// index.php
$repo = new MySQLUserRepository();
$service = new UserService($repo);
$service->create(['name' => 'Ana']);

//index.php está executando a lógica de criação de usuário.
```

**Certo:**
```php
// index.php
require 'system.php';

$service = buildUserService();
$service->handleRequest($_POST); // uso separado da montagem

//apenas chama funções que montam o sistema
```

```php
// system.php (ou outro arquivo de configuração)
function buildUserService() {
    $repo = new MySQLUserRepository();
    return new UserService($repo);
}

//lógica de construção
```
#
## Factories

Algumas vezes pode ser preciso passar o controle par o aplicativo quando um objeto for criado. Podemos usar o padrão de Factories para isso, mas mantendo os detalhes dessa construção separada do código do aplicativo.


> ℹ️ Factories são **objetos ou funções responsáveis por criar outros objetos**. Em vez de instanciar classes diretamente com `new`, você delega essa responsabilidade a uma **fábrica**.

### Por que usar?

- Isolamento de lógica de criação de objetos
- Facilidade de troca de implementações
- Redução de acoplamento
- Centralização da configuração

#
## Injeção de dependência

É uma boa maneira de separar construção do uso.

É um princípio de design onde uma classe não cria suas próprias dependências, mas as recebe de fora (no construtor, método ou via setter). A DI ajuda a dividir responsabilidades, evitando que a classe tenha que gerenciar a criação de objetos. Por esse motivo, classes pequenas e coesas são melhores.

A DI é uma consequência prática do DIP - o D de SOLID. 

>ℹ️ Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.

A DI torna o código:

- Mais testável - possibilita testes isolados de classes.
- Menos acoplado
- Mais flexível

#
## Desenvolvimento gradual

Um sistema deve ser desenvolvido gradualmente, implementando apenas os fatos de hoje, e então refatorar e expandir o sistema, implementando novos fatos amanhã. Essa é a essência das agilidades iterativa e incremental.

Porém, a estrutura de sistema requer um pré-planejamento, de toda forma. 

>📝Os sistemas de software são únicos, e suas arquiteturas podem crescer gradualmente se mantivermos uma separação devida de preocupações.

#
## Testes na arquitetura do sistema

Aqui é enfatizado a importância de testes automatizados na arquitetura do sistema e propõe que a testabilidade seja um critério de design natural.

Uma boa arquitetura facilita os testes, pois permite que as regras de negócio sejam testadas isoladamente sem depender de Banco de Dados, Frameworks, etc. Isso significa que os testes podem ser rápidos, confiáveis e executados com frequência.

Outro ponto importante é que o sistema deve ser projetado para que seja fácil de se realizar testes. Isso envolve:

- Injeção de dependência
- Separação de responsabilidades
- Criação de interfaces

Os testes podem ser uma força motivadora para a construção de uma boa arquitetura, pois se há uma preocupação em tornar o sistema fácil de testar, isso naturalmente leva a um código mais coeso, desacoplado e limpo.

>⚠️ Projetar sistemas pensando nos testes **melhora automaticamente a arquitetura**.

#
## Otimize a tomada de decisões

Modularidade e separação de preocupações descentralizam o gerenciamento e possibilitam a a tomada de decisões. Em um projeto grande, ninguém pode tomar todas as decisões. Então, é melhor designar essas decisões Às pessoas mais qualificadas.

Muitas vezes é esquecido que, às vezes, é melhor adiar algumas decisões até o último momento. Isso permite uma tomada de decisão com a maior quantidade de informações possíveis, o que pode resultar numa decisão melhor.

>ℹ️ Os sistemas devem ser limpos. Uma arquitetura invasiva afeta a agilidade e sobrepuja a lógica do domínio que, quando ofuscada, perde qualidade. Se a agilidade é comprometida, a produtividade também será.

[⬆️Voltar ao Topo](#sumário)
