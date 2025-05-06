## Exercício Prático – Conversão de CSS para LESS

### Objetivos do Exercício

* Converter o estilo do projeto disponibilizado no material de apoio (em `.css`) para LESS
* Utilizar recursos aprendidos ao longo do módulo:

  * Variáveis
  * Mapas (maps)
  * Escaping
  * Organização em cascata
  * Divisão de arquivos com `@import`
* Criar uma branch específica no repositório chamada `exercicio_less`
* Armazenar os arquivos LESS nessa branch e disponibilizá-los para correção

### Objetivo Geral

Reestruturar o estilo do projeto, originalmente entregue como um arquivo `.css`, e transformá-lo em um código mais organizado e modular utilizando as funcionalidades do pré-processador LESS.

### Tecnologias e recursos utilizados

Durante a conversão, foram aplicados os seguintes recursos do LESS:

* Variáveis para centralizar valores de cor
* Mapas (`#colors`) para agrupar essas variáveis
* Escaping para facilitar o uso de media queries
* Organização em múltiplos arquivos (`main.less` e `mapas.less`)
* Estilização em cascata com o uso de `&` para estruturar blocos como `.menu` e `.projects-list`

### Estrutura do Projeto

O projeto foi organizado dentro da pasta:

```
exercicio_less/
```

E os arquivos `.less` foram armazenados na branch:

```
exercicio_less
```

### Descrição da conversão

* As regras de reset foram mantidas e complementadas com `font-family`
* As cores foram movidas para um mapa no arquivo `mapas.less` e acessadas por `#colors[chave]`
* Os elementos de navegação e os botões foram estilizados com base nessas variáveis
* Os efeitos de hover utilizam transições suaves com valores controlados
* As media queries foram declaradas com escaping e aplicadas para os breakpoints de tablet e mobile
* A grid de produtos se adapta corretamente aos diferentes tamanhos de tela
