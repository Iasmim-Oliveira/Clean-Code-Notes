### 🟦 **Tamanho de Blocos e Identação**

Características de funções bem escritas:
- Elas devem ser pequenas, no máximo 20 linhas.
- Os blocos dentro de instruções `if`, `else`, `while` devem ter apenas a linha de chamada de função dentro de outra função.
- Não devem ter estruturas aninhadas.
- As funções devem fazer apenas 1 coisa e fazê-las bem.

  
**Princípio de responsabilidade única** - um dos princípios SOLID, afirma que uma classe deve ter apenas uma razão para mudar, ou seja, ela deve ser responsável por uma única tarefa ou funcionalidade. Isso torna o código mais fácil de entender, manter e modificar, pois alterações em uma funcionalidade específica não afetam outras partes do sistema.

Se uma função faz apenas alguns passos em um nível abaixo do nome da função, então ela está fazendo apenas 1 coisa. Para saber se uma função faz mais de uma coisa, é verificando se é possível extrair outra função a partir do nome dela sem gerar uma reformulação.

---

### 🟦 **Regra Decrescente**

Não dá para dividir em seções as funções que fazem apenas 1 coisa. É preciso verificar se todas as instruções dentro da função possuem o mesmo nível de abstração, pois vários níveis diferentes dentro da mesma função causam confusão. Código é lido de cima para baixo, onde cada função é seguida de outra no próximo nível de abstração de modo que o programa é lido descendo um nível de abstração por vez enquanto a lista de funções é lida.

> **Abstração:** usar um cenário real e trazer para o programa somente o essencial para seu funcionamento.

---

### 🟦 **Switch**

Por padrão, elas fazem N coisas, então é difícil deixá-las pequenas. Mas, podemos garantir que cada `switch` está em uma classe de baixo nível e nunca é repetido. É usado o polimorfismo pra isso.

> **Polimorfismo:** a mesma variável tem funções diferentes em cada classe mas sem alterar sua estrutura original. 

A solução seria usar o `switch` em uma `abstract factory`.
> **Abstract Factory** - é um padrão de design que cria famílias de objetos relacionados sem especificar suas classes concretas. Ele fornece uma interface para criar objetos de diferentes tipos, garantindo que sejam compatíveis entre si, sem precisar alterar o código cliente.

---

### 🟦 **Nome da Função**

Usar nomes descritivos para as funções. Nomes extensos são melhores que nomes pequenos e confusos ou um comentário. O nome deve explicar o que ela faz. Importante ser consistente na nomeação das funções do módulo. Por exemplo, usar `add` pra toda função que faz a ação de adicionar algo: `addConvenio`, `addProcesso`, etc.

---

### 🟦 **Parâmetros**

Podemos frasear o nome da função. Isso permite uma sequência de fácil dedução. A quantidade ideal de parâmetros para a função é 0. Para ter mais de 3, deve-se ter um bom motivo. Mesmo assim, não deve ser usado. Parâmetros fazem com que o leitor do código precise entender de onde vem aquele parâmetro, pois ele não está no mesmo nível de abstração da função. Eles também deixam os testes mais complicados, pois é necessário escrever um teste para cada combinação de parâmetros. Um parâmetro de entrada é a melhor coisa depois de zero parâmetro.

---

### 🟦 **Formas Mônades Comuns**

Há duas razões para se usar um único parâmetro: quando se está fazendo uma pergunta sobre ele, como `boolean fileExists("MyFile")`; ou quando vamos transformá-lo em outra coisa, como `InputStream fileOpen("MyFile")`.

Outra utilidade de um parâmetro em uma função seria um evento. Aqui tem um parâmetro de entrada, mas nenhum de saída. O programa serve para interpretar a chamada de função como um evento e usar o parâmetro para alterar o estado do sistema `passwordAttemptFailedNtimes(int Attempts)`.

> **Deve ficar claro para o leitor que se trata de um evento. Usar nomes que descrevam exatamente o que faz.** 

---

### 🟦 **Parâmetros Lógicos**

Se a função vai transformar o parâmetro de entrada, a alteração deve aparecer como um valor retornado. São feios, complicam a assinatura do método pois claramente fazem mais que uma coisa (faz 1 se o valor for true e outra se for false).

---

### 🟦 **Funções Díades**

São mais complicadas de entender, pois precisamos “processar” na nossa cabeça o 1° parâmetro, e depois seguir por 2°. E acabamos deixando de lado o 1°. Dois parâmetros podem ser necessários quando, por exemplo, temos uma função que recebe eixos cartesianos. Nesse caso, os dois parâmetros são componentes de um único valor.

---

### 🟦 **Funções Tríades**

Sempre que possível, tentar convertê-las em mônades. São muito difíceis de entender. Todos os problemas encontrados nas outras triplicam aqui.

---

### 🟦 **Objetos como Parâmetros**

Quando uma função precisa de mais de um parâmetro, significa que alguns deles podem ficar em uma classe própria. Então é melhor criar uma classe para eles.

`Circle makeCircle(double x, double y, double radius);`

---

### 🟦 **Listas como Parâmetros**

Às vezes precisamos passar um número variável de parâmetros para uma função. Caso eles sejam todos tratados da mesma forma, então eles são equivalentes a um único parâmetro do tipo `list`.

---

### 🟦 **Verbos no Nome da Função**

Um bom nome para função pode ir desde explicar seu propósito à ordem e a finalidade dos parâmetros. Na mônade, deve formar um par verbo/substantivo: `write(name)`.

---

### 🟦 **Palavra-chave**

Ao usar esse formato, codificamos os nomes dos parâmetros no nome da função `writeField(name)`.

---

### 🟦 **Evitar Efeitos Colaterais**

São mentiras. A função promete fazer apenas uma coisa, mas faz outras escondidas. E isso acaba gerando acoplamentos temporários e dependências. 
> **Acoplamentos temporários** - ocorrem quando duas partes do código se tornam dependentes por um curto período, mas essa dependência não é permanente. Embora às vezes inevitáveis, devem ser minimizados, pois podem tornar o código mais difícil de manter e modificar.

---

### 🟦 **Parâmetros de Saída**

Deve-se evitar seu uso. Caso a função precise alterar o estado de algo, então ela deve alterar o estado do objeto ao qual ela pertence.

---

### 🟦 **Separação Comando-Consulta**

A função ou responde algo ou faz uma consulta, não deve fazer as duas coisas.

---

### 🟦 **Exceções a Retorno de Códigos de Erro**

Funções que retornam códigos de erros é uma violação da separação comando-consulta, pois os comandos são usados como expressões de comparação em estruturas `if`. Quando usamos o retorno de erros, é criado um problema com o qual o chamador precisará lidar. Já com tratamento de exceção, o código de tratamento pode ficar separado e ser simplificado.

---

### 🟦 **Extrair os try-catch**

Os blocos `try-catch` devem ficar em suas próprias funções, porque são feios e confundem a estrutura do código.

---

### 🟦 **Tratamento de Erro**

Funções que tratam erros devem tratar apenas erros. Ou seja, depois do `catch/finally`, não se deve ter mais código. Quando se usa exceções invés de erros, as novas exceções são derivadas da classe `Exception` e não é necessário recompilar.

Este é um exemplo do Princípio de Aberto-Fechado (OCP, sigla em inglês [PPP02]).

---

### 🟦 **Evitar Repetição de Código**

Com o código repetido, é necessário modificar as funções toda vez que ocorrer uma alteração no algoritmo. E também são oportunidades para omissão de erros.

**O Princípio do Não Se Repita (DRY - Don't Repeat Yourself)**: evitar repetição de código ao máximo. Cada pedaço de conhecimento deve ter uma única, inequívoca, e autoritativa representação dentro de um sistema. Isso não só facilita a manutenção, mas também reduz as chances de erro.

---

### 🟦 **Programação Estruturada**

Alguns programadores seguem a regra de Edsger Dijkstra ([SP72]), que cada função e cada bloco dentro dela tenha uma entrada e uma saída. Dessa forma, cada função só teria um `return`. Porém, isso oferece pouca vantagem quando a função é pequena. Escrever uma função é como escrever um artigo. O primeiro rascunho fica horrível, mas aos poucos vai sendo refinado.

> **Uncle Bob:** "Mas jamais se esqueça de que seu objetivo verdadeiro é contar a história do sistema, e que as funções que você escrever precisam estar em perfeita sincronia e formar uma linguagem clara e precisa para lhe ajudar na narração."

---
