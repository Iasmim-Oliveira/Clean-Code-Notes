# Clean-Code-Notes
## Sumário

1. []
2. [Nomes Significativos](#nomes-significativos)
3. [Funções](#funções)
4. [Comentários](#comentários)

# Nomes Significativos

Nomeamos muitas coisas na programação, e como fazemos muito isso, é bom que façamos bem. Escolher bons nomes leva tempo, mas economiza mais. Algumas regrinhas para criação de bons nomes são:


### 🟣 **Nomes que Demonstram seu Propósito**

O nome de uma variável deve dizer tudo sobre ela. Se ele precisa de um comentário, então não é um bom nome.


### 🟣 **Evitar Informações Erradas**

Deve-se evitar passar dicas falsas que confundam o sentido do código. Por exemplo, usar palavras que possam ser confundidas com o nome de outras coisas. No livro, há o exemplo de palavras que são usadas como nomes de plataformas Unix.

Também devemos ter cuidado ao usar nomes parecidos para duas coisas diferentes, pois fica difícil de distinguir a diferença entre eles. Exemplo: `XYZControllerForEfficientHandlingOfStrings` e `XYZControllerForEfficientStorageOfStrings` são muito semelhantes.


### 🟣 **Faça Distinções Significativas**

Alterar um nome de maneira arbitrária, só porque o nome que você quer usar já está em uso, não é o bastante. Se os nomes precisam ser diferentes, então eles devem ter significado distinto. Exemplo: chamar uma variável de `oLivro` só porque já existe a variável `livro`.

Usar números sequenciais em nomes não é expressivo o suficiente, pois esse tipo de nome não nos diz nada sobre o que o programa faz.


### 🟣 **Use Nomes Pronunciáveis**

Crie nomes pronunciáveis, se não puder pronunciá-lo, será difícil discutí-lo sem parecer um idiota (ele conta uma história sobre isso o livro e eu rachei demais). Isso é importante, porque programação também é uma atividade social.

É importante fazer a distinção de nomes de uma forma que o leitor compreenda a diferença e entenda rapidamente o que aquela variável faz.


### 🟣 **Use Nomes Passíveis de Busca**

Usar nomes pronunciáveis e passíveis de busca, que não sejam confundidos com outras coisas. Usar apenas uma letra `a` para nomear algo é uma escolha ruim, pois é uma letra comum e caso seja preciso fazer uma busca, ela vai aparecer em todo o texto. Nomes longos se sobressaem aos curtos. 

> O tamanho de um nome deve ser proporcional ao tamanho do escopo.


### 🟣 **Evite Codificações**

Já temos de lidar com bastante codificação e não precisamos acrescentar mais. Codificar informações do escopo ou tipos em nomes simplesmente adiciona uma tarefa extra de decodificação. Além de raramente serem pronunciáveis, é fácil de escrevê-los incorretamente.


### 🟣 **Evite o Mapeamento Mental**

Evitar o mapeamento mental, onde o leitor precisa ler todo o código para entender o que é a variável (que pode estar declarada apenas com 1 letra).

> Uma diferença entre um programador esperto e um programador profissional é que este entende que clareza é fundamental. Os profissionais usam seus poderes para o bem, e escrevem códigos que outros possam entender.


### 🟣 **Nomes de Classes**

Classes e objetos devem ter nome substantivos.


### 🟣 **Nomes de Métodos**

Nomes de métodos devem ter verbos (get, post, delete, etc). 

Podemos usar *factory methods* quando os construtores estiverem sobrecarregados com nomes que descrevam os parâmetros. Para forçar o uso, torne os construtores correspondentes como privados.


### 🟣 **Selecione uma Palavra por Conceito**

Escolher uma palavra por cada conceito abstrato e permanecer com ela até o fim. É confuso ter diferentes palavras como métodos equivalentes de classes diferentes (`fetch, retrieve` e `get`, por exemplo).


### 🟣 **Não Faça Trocadilhos**

Não usar a mesma palavra para 2 propósitos.

[⬆️Voltar ao Topo](#sumário)


# Funções
### 🔵 **Tamanho de Blocos e Identação**

Características de funções bem escritas:
- Elas devem ser pequenas, no máximo 20 linhas.
- Os blocos dentro de instruções `if`, `else`, `while` devem ter apenas a linha de chamada de função dentro de outra função.
- Não devem ter estruturas aninhadas.
- As funções devem fazer apenas 1 coisa e fazê-las bem.

  
**Princípio de responsabilidade única** - um dos princípios SOLID, afirma que uma classe deve ter apenas uma razão para mudar, ou seja, ela deve ser responsável por uma única tarefa ou funcionalidade. Isso torna o código mais fácil de entender, manter e modificar, pois alterações em uma funcionalidade específica não afetam outras partes do sistema.

Se uma função faz apenas alguns passos em um nível abaixo do nome da função, então ela está fazendo apenas 1 coisa. Para saber se uma função faz mais de uma coisa, é verificando se é possível extrair outra função a partir do nome dela sem gerar uma reformulação.


### 🔵 **Regra Decrescente**

Não dá para dividir em seções as funções que fazem apenas 1 coisa. É preciso verificar se todas as instruções dentro da função possuem o mesmo nível de abstração, pois vários níveis diferentes dentro da mesma função causam confusão. Código é lido de cima para baixo, onde cada função é seguida de outra no próximo nível de abstração de modo que o programa é lido descendo um nível de abstração por vez enquanto a lista de funções é lida.

> **Abstração:** usar um cenário real e trazer para o programa somente o essencial para seu funcionamento.


### 🔵 **Switch**

Por padrão, elas fazem N coisas, então é difícil deixá-las pequenas. Mas, podemos garantir que cada `switch` está em uma classe de baixo nível e nunca é repetido. É usado o polimorfismo pra isso.

> **Polimorfismo:** a mesma variável tem funções diferentes em cada classe mas sem alterar sua estrutura original. 

A solução seria usar o `switch` em uma `abstract factory`.
> **Abstract Factory** - é um padrão de design que cria famílias de objetos relacionados sem especificar suas classes concretas. Ele fornece uma interface para criar objetos de diferentes tipos, garantindo que sejam compatíveis entre si, sem precisar alterar o código cliente.


### 🔵 **Nome da Função**

Usar nomes descritivos para as funções. Nomes extensos são melhores que nomes pequenos e confusos ou um comentário. O nome deve explicar o que ela faz. Importante ser consistente na nomeação das funções do módulo. Por exemplo, usar `add` pra toda função que faz a ação de adicionar algo: `addConvenio`, `addProcesso`, etc.


### 🔵 **Parâmetros**

Podemos frasear o nome da função. Isso permite uma sequência de fácil dedução. A quantidade ideal de parâmetros para a função é 0. Para ter mais de 3, deve-se ter um bom motivo. Mesmo assim, não deve ser usado. Parâmetros fazem com que o leitor do código precise entender de onde vem aquele parâmetro, pois ele não está no mesmo nível de abstração da função. Eles também deixam os testes mais complicados, pois é necessário escrever um teste para cada combinação de parâmetros. Um parâmetro de entrada é a melhor coisa depois de zero parâmetro.


### 🔵 **Formas Mônades Comuns**

Há duas razões para se usar um único parâmetro: quando se está fazendo uma pergunta sobre ele, como `boolean fileExists("MyFile")`; ou quando vamos transformá-lo em outra coisa, como `InputStream fileOpen("MyFile")`.

Outra utilidade de um parâmetro em uma função seria um evento. Aqui tem um parâmetro de entrada, mas nenhum de saída. O programa serve para interpretar a chamada de função como um evento e usar o parâmetro para alterar o estado do sistema `passwordAttemptFailedNtimes(int Attempts)`.

> **Deve ficar claro para o leitor que se trata de um evento. Usar nomes que descrevam exatamente o que faz.** 


### 🔵 **Parâmetros Lógicos**

Se a função vai transformar o parâmetro de entrada, a alteração deve aparecer como um valor retornado. São feios, complicam a assinatura do método pois claramente fazem mais que uma coisa (faz 1 se o valor for true e outra se for false).


### 🔵 **Funções Díades**

São mais complicadas de entender, pois precisamos “processar” na nossa cabeça o 1° parâmetro, e depois seguir por 2°. E acabamos deixando de lado o 1°. Dois parâmetros podem ser necessários quando, por exemplo, temos uma função que recebe eixos cartesianos. Nesse caso, os dois parâmetros são componentes de um único valor.


### 🔵 **Funções Tríades**

Sempre que possível, tentar convertê-las em mônades. São muito difíceis de entender. Todos os problemas encontrados nas outras triplicam aqui.


### 🔵 **Objetos como Parâmetros**

Quando uma função precisa de mais de um parâmetro, significa que alguns deles podem ficar em uma classe própria. Então é melhor criar uma classe para eles.

`Circle makeCircle(double x, double y, double radius);`


### 🔵 **Listas como Parâmetros**

Às vezes precisamos passar um número variável de parâmetros para uma função. Caso eles sejam todos tratados da mesma forma, então eles são equivalentes a um único parâmetro do tipo `list`.


### 🔵 **Verbos no Nome da Função**

Um bom nome para função pode ir desde explicar seu propósito à ordem e a finalidade dos parâmetros. Na mônade, deve formar um par verbo/substantivo: `write(name)`.


### 🔵 **Palavra-chave**

Ao usar esse formato, codificamos os nomes dos parâmetros no nome da função `writeField(name)`.


### 🟦 **Evitar Efeitos Colaterais**

São mentiras. A função promete fazer apenas uma coisa, mas faz outras escondidas. E isso acaba gerando acoplamentos temporários e dependências. 
> **Acoplamentos temporários** - ocorrem quando duas partes do código se tornam dependentes por um curto período, mas essa dependência não é permanente. Embora às vezes inevitáveis, devem ser minimizados, pois podem tornar o código mais difícil de manter e modificar.

### 🔵 **Parâmetros de Saída**

Deve-se evitar seu uso. Caso a função precise alterar o estado de algo, então ela deve alterar o estado do objeto ao qual ela pertence.


### 🔵 **Separação Comando-Consulta**

A função ou responde algo ou faz uma consulta, não deve fazer as duas coisas.


### 🔵 **Exceções a Retorno de Códigos de Erro**

Funções que retornam códigos de erros é uma violação da separação comando-consulta, pois os comandos são usados como expressões de comparação em estruturas `if`. Quando usamos o retorno de erros, é criado um problema com o qual o chamador precisará lidar. Já com tratamento de exceção, o código de tratamento pode ficar separado e ser simplificado.


### 🔵 **Extrair os try-catch**

Os blocos `try-catch` devem ficar em suas próprias funções, porque são feios e confundem a estrutura do código.


### 🔵 **Tratamento de Erro**

Funções que tratam erros devem tratar apenas erros. Ou seja, depois do `catch/finally`, não se deve ter mais código. Quando se usa exceções invés de erros, as novas exceções são derivadas da classe `Exception` e não é necessário recompilar.

Este é um exemplo do Princípio de Aberto-Fechado (OCP, sigla em inglês [PPP02]).


### 🔵 **Evitar Repetição de Código**

Com o código repetido, é necessário modificar as funções toda vez que ocorrer uma alteração no algoritmo. E também são oportunidades para omissão de erros.

**O Princípio do Não Se Repita (DRY - Don't Repeat Yourself)**: evitar repetição de código ao máximo. Cada pedaço de conhecimento deve ter uma única, inequívoca, e autoritativa representação dentro de um sistema. Isso não só facilita a manutenção, mas também reduz as chances de erro.


### 🔵 **Programação Estruturada**

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

### 🟢 **Exlique-se no código**

Pode ser necessário esclarecer o significado de alguns parâmetros ou valores retornados obscuros para algo inteligível. Devemos tentar esclarecer esse parâmetro ou valor retornado, mas caso não seja possível, então um comentário se faz útil.
Também é bom sempre se certificar que ele é preciso e se não tem outra opção a não ser fazer um comentário.

### 🟢 **Alerta de consequêcias**

Pode ser útil alertar os coleguinhas de algumas consequências. Por exemplo, se há uma função no código que demora para se concluir, então podemos deixar um comentário avisando.

### 🟢 **Comentários ToDo**

Ás vezes pode ser o caso de usar um `//todo.` Eles são tarefas que os programadores acham que devem ser efetuadas, mas que não podem ser feitas no momento. Algumas IDEs ajudam a encontrar com mais facilidade esse tipo de comentário, mas mesmo assim, devemos procurá-los regularmente e eliminar os que puder. A maioria deles é suporte ou desculpas para um código de baixa qualidade ou justificativas para a falta de decisões.

### 🟢 **Comentários ruins**

Se optar por criar um comentário, então gaste tempo necessário para fazê-lo bem. Usar um comentário só porque acha que deve ou porque o processo o requer é besteira.
> Qualquer comentário que o obrigue a analisar outro módulo em busca de um significado falhou em transmitir sua mensagem e não vale os bits que consome.


[⬆️Voltar ao Topo](#sumário)
