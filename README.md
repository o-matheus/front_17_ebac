# Módulo 17 - LESS

## Menu
[Aula 1 - Conheça o LESS](#aula-1--conheça-o-less)  
[Aula 2 - Aplique variáveis no LESS](#aula-2--aplique-variáveis-no-less)  
[Aula 3 - Aplique o escaping](#aula-3--aplique-o-escaping)  
[Aula 4 - Utilize Mixins](#aula-4---utilize-mixins)  
[Aula 5 - Crie mapas](#aula-5---crie-mapas)  
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

## Aula 3 – Aplique o Escaping

### 1. Objetivos da aula

1. Conceituar escaping no LESS.
2. Usar o arroba (`@`) para definir variáveis de imagem no LESS.
3. Praticar a organização de estilos condicionais com base em resolução de tela.
4. Entender como a ordem das regras de mídia afeta a aplicação dos estilos no LESS.

---

### 2. Estruturação do container

O professor reorganizou a estrutura do HTML para incluir uma `div.container` que engloba os seguintes elementos:

* `<header>` (com `img`, `h1`, `h2` e `p`)
* `<nav>` (que foi reposicionada para dentro do mesmo container)

Inicialmente, o plano era envolver apenas o `<header>`, mas decidiu-se por colocar a `div.container` desde antes da `<header>` até depois do `<nav>`, garantindo que **todo o topo da página** estivesse centralizado com o uso do container.

---

### 3. Estilização do `.container`

No arquivo `main.less`, foram adicionadas as seguintes propriedades para `.container`:

```less
.container {
  max-width: 960px;
  width: 100%;
  margin: 0 auto;
}
```

Essas regras centralizam o conteúdo horizontalmente e limitam a largura do container.

---

### 4. Preparando a responsividade

Para tornar o projeto responsivo, o professor introduziu o uso de **escaping no LESS** com variáveis de media queries. Esse recurso facilita o controle de estilos para diferentes tamanhos de tela.

---

### 5. Criando as variáveis de breakpoint

#### 5.1 Breakpoint para celular:

```less
@breakpointMobile: ~"(max-width: 767px)";
```

#### 5.2 Breakpoint para tablet:

Inicialmente:

```less
@breakpointTablet: ~"(max-width: 1023px)";
```

Mais adiante, para evitar conflitos com o mobile:

```less
@breakpointTablet: ~"(min-width: 768px) and (max-width: 1023px)";
```

Essas variáveis foram colocadas logo abaixo do `@import` de `variaveis.less`.

---

### 6. Uso dos breakpoints com @media

As media queries no LESS podem ser aninhadas dentro dos seletores, como `.container`, dessa forma:

```less
.container {
  max-width: 960px;
  width: 100%;
  margin: 0 auto;

  @media @breakpointTablet {
    width: 80%;
    background-color: blue; // teste visual
  }

  @media @breakpointMobile {
    width: 70%;
    background-color: red; // teste visual
  }
}
```

---

### 7. Efeito cascata e importância da ordem

O professor demonstrou que, como o CSS funciona com **efeito cascata**, a ordem das media queries influencia no resultado final.

#### Problema:

Se o `@breakpointTablet` (até 1023px) for declarado **depois** do `@breakpointMobile` (até 767px), ele pode sobrescrever as regras do mobile — já que 767px também está dentro de 1023px.

#### Solução:

1. Usar `min-width` + `max-width` no tablet.
2. Garantir a **ordem correta** no código: declarar **tablet primeiro**, depois **mobile**, para que o CSS seja mais específico no final.

---

### 8. Conclusão

Nesta aula, aprendemos:

* A importância do **escaping** com `~""` no LESS.
* Como declarar e reutilizar variáveis de media queries.
* Como tornar o layout responsivo para celular e tablet.
* Como evitar conflitos usando `min-width` e cuidando da ordem das media queries.
* Como aplicar media queries **dentro de seletores**, aproveitando o poder de aninhamento do LESS.

## Aula 4 - Utilize Mixins

### Fontes e Reset
No início da aula, acessamos o Google Fonts para escolher a fonte principal do projeto. O professor optou pela **Roboto**, então a adicionamos diretamente no arquivo `main.less` com a propriedade `font-family`. Também aplicamos o reset CSS com as seguintes propriedades:

```less
margin: 0;
padding: 0;
box-sizing: border-box;
font-family: 'Roboto', sans-serif;
````

### Estilização do Header

Em seguida, começamos a estilização do `header`, aplicando:

* `padding: 24px;`
* Criamos a classe `.profile-avatar`, aplicada à imagem de perfil, com:

```less
display: block;
margin: 0 auto 24px;
border-radius: 50%;
```

### Estrutura do Perfil

No `index.html`, criamos uma `div` com a classe `profile-bio`, contendo:

* `h1` com classe `.profile-bio-name`
* `h2` com classe `.profile-bio-subtitle`
* `p` com classe `.profile-bio-description`

No LESS, usamos o prefixo comum com **aninhamento**:

```less
.profile-bio {
  text-align: center;

  &-name {
    font-size: 16px;
    margin: 8px 0;
  }

  &-subtitle {
    font-size: 14px;
    margin: 8px 0;
    opacity: 0.7;
  }

  &-description {
    font-size: 14px;
    opacity: 0.7;
  }
}
```

O uso do `&` evita repetição de nomes e facilita a leitura do código. A imagem do perfil foi ajustada para o tamanho padrão de **96x96px**, conforme referência do Linktree.

### Uso de Mixins

Os **mixins** no LESS funcionam como classes reutilizáveis. Criamos um mixin da seguinte forma:

```less
.margin-bottom-8 {
  margin-bottom: 8px;
}
```

Para utilizá-lo, aplicamos no seletor desejado com parênteses:

```less
.profile-bio-name {
  .margin-bottom-8();
}
```

A chamada se parece com uma função, mesmo que o mixin não tenha parâmetros.

Esse recurso é útil para **evitar repetição** e manter o **código organizado**. Apesar do Sass ter integração mais nativa com ferramentas como Autoprefixer, o LESS também permite automação com plugins externos — basta atenção à estrutura e à escrita correta.


## Aula 5 - Crie mapas

### Estilização da lista de ícones

Nesta aula, começamos a estilizar a lista da página, utilizando ícones SVG para representar redes sociais. O professor sugeriu o uso do site [feathericons.com](https://feathericons.com/), de onde baixamos ícones como **Instagram**, **Twitter**, **Facebook** e **Email**.

Contudo, o ícone do **TikTok** não estava disponível nesse site, então ele foi buscado em outra fonte na internet. Isso trouxe um desafio: os ícones baixados tinham tamanhos e proporções diferentes. No primeiro momento, para resolver rapidamente, foi aplicado um `style="width: 24px"` diretamente na tag HTML do ícone do TikTok.

Mais adiante, durante a aula, o professor explicou que um arquivo SVG é, na verdade, um **arquivo de marcação XML**, que pode ser editado como texto. Inicialmente, o VS Code abriu o SVG como imagem renderizada, mas depois que o editor foi ajustado para **abrir como "Text Editor"**, foi possível visualizar e editar o conteúdo interno do SVG.

Com esse entendimento, foi feita uma nova abordagem: **em vez de manter o `style` inline no HTML**, o SVG do TikTok foi modificado diretamente no código para que tivesse:

```xml
width="24px" height="24px"
```

Após esse ajuste, o `style` foi removido do HTML, e o SVG passou a ficar visualmente padronizado com os demais ícones. Esse processo representou um ganho de organização e clareza no código — além de um aprendizado prático sobre como lidar com arquivos SVG de fontes diferentes.

### Código LESS para os ícones

Com os ícones organizados, criamos a classe `.social-links` no `main.less` para estilizar a lista:

```less
.social-links {
  display: flex;
  justify-content: space-between;
  max-width: 240px;
  width: 100%;
  margin: 0 auto;

  li {
    list-style: none;

    img {
      transition: all 0.3s ease;

      &:hover {
        transform: scale(1.3);
      }
    }
  }
}
```

Essa estrutura aplica espaçamento entre os ícones, remove os marcadores da lista e adiciona um efeito de **zoom suave** ao passar o mouse, deixando a interface mais interativa.

### Introdução aos Mapas no LESS

Depois disso, foi apresentado o conceito de **mapas no LESS**, que servem para **agrupar variáveis relacionadas**, como cores, em uma estrutura compacta e bem organizada.

#### Criação do mapa

Foi criado um novo arquivo chamado `mapas.less`, contendo:

```less
#colors() {
  backgroundColor: @background-color;
  buttonColor: @button-color;
  textColor: @text-color;
}
```

#### Importação no projeto

O mapa foi importado no `main.less` com:

```less
@import "mapas.less";
```

#### Acesso aos valores do mapa

Para usar os valores definidos no mapa:

```less
background-color: #colors[backgroundColor];
```

A sintaxe lembra a de um objeto JavaScript, usando colchetes para acessar os pares chave-valor.

### Reflexão sobre o uso de mapas

No início, o uso dos mapas parecia um pouco exagerado. Afinal, com um projeto pequeno, **variáveis simples com comentários já resolveriam**. Porém, ficou clara uma **vantagem importante em projetos grandes**:

* Como os mapas funcionam como blocos, eles podem ser **recolhidos no editor (como no VS Code)**.
* Isso torna a navegação no código muito mais fácil, especialmente quando há muitas variáveis agrupadas por tema (cores, espaçamentos, tamanhos, etc.).
* Além disso, o acesso por `#colors[backgroundColor]` deixa claro de onde aquela variável vem, reforçando a organização.

> **Comentário pessoal:** Agora entendi melhor por que o LESS torna o acesso às variáveis mais prático e como os mapas ajudam quando o projeto é maior. Embora a sintaxe pareça mais "complicada" no início, ela **facilita muito a manutenção em projetos escaláveis**. Em projetos menores como o nosso, não faria tanta diferença usar mapas, mas entendo que o professor está usando essa oportunidade para ensinar o recurso e mostrar o seu potencial.
