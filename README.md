# Módulo 17 - LESS

## Menu
[Aula 1 - Conheça o LESS](#aula-1--conheça-o-less)  
[Aula 2](#aula-)  
[Aula 3](#aula-)  
[Aula 4](#aula-)  
[Aula 5](#aula-)  
[Aula 6](#aula-)  

## Aula 1 – Conheça o LESS

### 1. Objetivos da aula

Esta aula tem três objetivos principais:

1. Compreender o papel do LESS como uma ferramenta importante no desenvolvimento front-end.
2. Configurar o LESS em um projeto, incluindo a instalação das dependências necessárias.
3. Explorar a sintaxe do LESS, abordando seletores, variáveis e comentários, e como esses recursos podem ser usados para criar estilos de forma mais eficiente.

### 2. O que é o LESS

O LESS, assim como o Sass, é um pré-processador de CSS.

### 3. Instalação do LESS

Para iniciar, foi feita a instalação global do LESS com o seguinte comando:

```
npm i -g less
```

Em seguida, foi inicializado o projeto com:

```
npm init
```

E depois o LESS foi instalado localmente como uma dependência de desenvolvimento:

```
npm install --save-dev less
```

Também foi criado o arquivo `.gitignore` contendo `node_modules/` para evitar que essa pasta pesada vá para o repositório remoto.

### 4. Estrutura inicial do projeto

O professor iniciou o projeto com um arquivo `index.html` na raiz. O título do documento foi definido como "Página do Zian", mas no meu caso foi alterado para "Página do Mateus".

Depois, criou-se a estrutura de pastas:

* `src/`

  * `styles/`

    * `main.less`

No arquivo `main.less`, foi criada uma variável `@bg-color` com valor `red`, aplicada ao `body`. Isso demonstrou o uso básico de variáveis em LESS.

### 5. Script de compilação com lessc

No arquivo `package.json`, foi adicionado o seguinte script para compilar o LESS:

```
"scripts": {
  "less": "lessc ./src/styles/main.less ./build/styles/main.css"
}
```

Mesmo sem criar as pastas `build/` e `styles/` previamente, o LESS foi capaz de criá-las automaticamente ao executar o comando:

```
npm run less
```

### 6. Comentários e aninhamento

O LESS aceita dois tipos de comentários:

* CSS: `/* comentário */`
* JavaScript: `// comentário`

Assim como o Sass, o LESS também permite o aninhamento de seletores (nesting), facilitando a organização do CSS.

### 7. Adicionando o modo watch

Diferente do Sass, o LESS não possui uma funcionalidade `watch` nativa. Para adicionar esse recurso, foi necessário instalar o seguinte pacote global:

```
npm i -g less-watch-compiler
```

Depois disso, ele também foi instalado localmente como dependência de desenvolvimento:

```
npm install --save-dev less-watch-compiler
```

### 8. Ajustando o script com less-watch-compiler

Com o uso do `less-watch-compiler`, o script no `package.json` foi atualizado para:

```
"scripts": {
  "less": "less-watch-compiler src/styles build/styles"
}
```

Esse comando observa todos os arquivos `.less` em `src/styles` e os compila automaticamente para `build/styles`.

Para observar um arquivo específico (como o `main.less`), o script pode ser ajustado assim:

```
"less": "less-watch-compiler src/styles build/styles main.less"
```

### 9. Correção do link no HTML

Após a configuração, percebi que o HTML estava sem estilização. O problema era a ausência da tag `<link>` para o CSS. Após adicioná-la corretamente, a página passou a exibir os estilos definidos:

```
<link rel="stylesheet" href="./build/styles/main.css">
```

### 10. Teste de gradiente e verificação do watch

Foi feito um teste utilizando gradientes de cor no `main.less`. A cada alteração feita, o arquivo `main.css` era recompilado automaticamente, confirmando que o watch estava funcionando corretamente.

### 11. Conclusão

Com isso, finalizamos a primeira aula do módulo "Introdução ao LESS", com os seguintes tópicos abordados:

* Instalação global e local do LESS
* Estrutura de pastas e criação de arquivos
* Uso de variáveis e comentários
* Compilação manual e com watch
* Configuração de scripts no `package.json`
* Verificação prática do funcionamento do LESS na aplicação

## Aula 2 – Aplique Variáveis no LESS

### 1. Objetivos da aula

1. Declarar variáveis no LESS.
2. Utilizar variáveis para armazenar cores e valores das propriedades CSS.
3. Praticar a importação de variáveis em arquivos LESS para reutilização em diferentes partes do projeto.

---

### 2. Estrutura do HTML e imagem de perfil

Começamos a aula criando a estrutura básica do HTML. Dentro da tag `<header>`, foram incluídos:

* Uma imagem de perfil utilizando o site [**placehold.co**](https://placehold.co/), com a dimensão `200x200`:

  ```html
  <img src="https://placehold.co/200x200" alt="Foto de perfil">
  ```

* Um título principal com `<h1>` contendo o nome.

* Um subtítulo com `<h2>` — no exemplo, “Desenvolvedor Web”.

* Um parágrafo `<p>` com um `lorem10` como texto fictício.

* Uma `<nav>` com uma lista não ordenada (`<ul>`), contendo quatro links dentro de `<li>`:

  * TikTok
  * LinkedIn
  * E-mail
  * GitHub

---

### 3. Escolha das cores e criação de variáveis

Após finalizar o HTML, acessamos o site [Flat UI Colors](https://flatuicolors.com/) para escolher uma paleta de cores.

A paleta escolhida foi **Bridge Palette**, e as seguintes cores foram selecionadas:

* **Cor de fundo**: `Picoloid`

  * Hexadecimal: `#192A56`
  * Nome da variável: `@corDeFundo`

* **Cor dos botões**: `Vanadyl Blue`

  * Hexadecimal: `#0097A6`
  * Nome da variável: `@corDosBotoes`

* **Cor do texto**: `#F5F6FA` (cinza bem claro)

  * Nome da variável: `@corDoTexto`

---

### 4. Organização dos arquivos LESS

Dentro da pasta `src/styles`, foi criado o arquivo `variaveis.less` para centralizar as variáveis do projeto.

Exemplo do conteúdo desse arquivo:

```less
@corDeFundo: #192A56;
@corDosBotoes: #0097A6;
@corDoTexto: #F5F6FA;
```

---

### 5. Importação de variáveis no main.less

Para reutilizar as variáveis definidas em `variaveis.less`, fizemos a importação dentro do arquivo `main.less`:

```less
@import "variaveis.less";
```

**Observações:**

* Diferente do Sass, aqui usamos a extensão completa `.less` no `@import`.
* As variáveis podem ser usadas diretamente após a importação, sem a necessidade de indicar o nome do arquivo onde foram declaradas.

---

### 6. Aplicação das variáveis no CSS

Dentro do seletor `body`, foram aplicadas duas das variáveis:

```less
body {
  background-color: @corDeFundo;
  color: @corDoTexto;
}
```

---

### 7. Conclusão da aula

Nesta aula aprendemos:

* Como declarar variáveis no LESS.
* Como organizar as variáveis em um arquivo separado.
* Como importar arquivos `.less` dentro de outros.
* E como aplicar as variáveis para estilizar o projeto de forma eficiente e reutilizável.


