# Nomes Significativos

Nomeamos muitas coisas na programação, e como fazemos muito isso, é bom que façamos bem. Escolher bons nomes leva tempo, mas economiza mais. Algumas regrinhas para criação de bons nomes são:

---

### **Nomes que Demonstram seu Propósito**

O nome de uma variável deve dizer tudo sobre ela. Se ele precisa de um comentário, então não é um bom nome.

---

### **Evitar Informações Erradas**

Deve-se evitar passar dicas falsas que confundam o sentido do código. Por exemplo, usar palavras que possam ser confundidas com o nome de outras coisas. No livro, há o exemplo de palavras que são usadas como nomes de plataformas Unix.

Também devemos ter cuidado ao usar nomes parecidos para duas coisas diferentes, pois fica difícil de distinguir a diferença entre eles. Exemplo: `XYZControllerForEfficientHandlingOfStrings` e `XYZControllerForEfficientStorageOfStrings` são muito semelhantes.

---

### **Faça Distinções Significativas**

Alterar um nome de maneira arbitrária, só porque o nome que você quer usar já está em uso, não é o bastante. Se os nomes precisam ser diferentes, então eles devem ter significado distinto. Exemplo: chamar uma variável de `oLivro` só porque já existe a variável `livro`.

Usar números sequenciais em nomes não é expressivo o suficiente, pois esse tipo de nome não nos diz nada sobre o que o programa faz.

---

### **Use Nomes Pronunciáveis**

Crie nomes pronunciáveis, se não puder pronunciá-lo, será difícil discutí-lo sem parecer um idiota (ele conta uma história sobre isso o livro e eu rachei demais). Isso é importante, porque programação também é uma atividade social.

É importante fazer a distinção de nomes de uma forma que o leitor compreenda a diferença e entenda rapidamente o que aquela variável faz.

---

### **Use Nomes Passíveis de Busca**

Usar nomes pronunciáveis e passíveis de busca, que não sejam confundidos com outras coisas. Usar apenas uma letra `a` para nomear algo é uma escolha ruim, pois é uma letra comum e caso seja preciso fazer uma busca, ela vai aparecer em todo o texto. Nomes longos se sobressaem aos curtos. 

> O tamanho de um nome deve ser proporcional ao tamanho do escopo.

---

### **Evite Codificações**

Já temos de lidar com bastante codificação e não precisamos acrescentar mais. Codificar informações do escopo ou tipos em nomes simplesmente adiciona uma tarefa extra de decodificação. Além de raramente serem pronunciáveis, é fácil de escrevê-los incorretamente.

---

### **Evite o Mapeamento Mental**

Evitar o mapeamento mental, onde o leitor precisa ler todo o código para entender o que é a variável (que pode estar declarada apenas com 1 letra).

> Uma diferença entre um programador esperto e um programador profissional é que este entende que clareza é fundamental. Os profissionais usam seus poderes para o bem, e escrevem códigos que outros possam entender.

---

### **Nomes de Classes**

Classes e objetos devem ter nome substantivos.

---

### **Nomes de Métodos**

Nomes de métodos devem ter verbos (get, post, delete, etc). 

Podemos usar *factory methods* quando os construtores estiverem sobrecarregados com nomes que descrevam os parâmetros. Para forçar o uso, torne os construtores correspondentes como privados.

---

### **Selecione uma Palavra por Conceito**

Escolher uma palavra por cada conceito abstrato e permanecer com ela até o fim. É confuso ter diferentes palavras como métodos equivalentes de classes diferentes (`fetch, retrieve` e `get`, por exemplo).

---

### **Não Faça Trocadilhos**

Não usar a mesma palavra para 2 propósitos.

---
