# Aula 20 - CSS: Grid layout

## Conteúdo em Grade (Pai)

Através do **conteúdo pai**, é possível controlar o comportamento dos itens que são **filhos direto**. Diferente do **flexbox**, o modelo por grade permite controlar os elementos filhos horizontalmente e verticalmente simuntâneamente.

### `display: grid`

Define o elemento como um **modelo de grade**, tornando os seus filhos **itens com propriedades compatíveis com a grade**.

```css
.aplicativo {
    display: grid;
}
```

### `grid-template-columns: dimensao dimensao...`

Define o número total de colunas e suas respectivas dimensões, para criação da grade.

```css
.aplicativo {
    display: grid;
    grid-template-columns: 250px 1fr 25%;
}
```

#### `minmax(dimensão_mínima, dimensão_máxima)`

Define o tamanho mínimo e o tamanho máximo de uma coluna utilizando o método `minmax()`. 

```css
.aplicativo {
    display: grid;
    /*
        Três colunas são criadas, a primeira terá no mínimo 200px de largura e no máximo 1fr(isso significa que após 200px ela se expande da mesma forma que as outras colunas). As outras duas colunas vão ter 1fr.
    */
    grid-template-columns: minmax(200px, 1fr) 1fr 1fr;
}
```

#### `repeat(número_de_repetições, dimensão)`

Define o número de repetições que um determinado valor se repetirá.

```css
.aplicativo {
    display: grid;
    /*
        Cria 3 colunas com 1fr de tamanho. O repeat seria a mesma coisa que escrever grid-template-columns: 1fr 1fr 1fr.
    */
    grid-template-columns: repeat(3, 1fr);
}
```

**Nota:** Caso não possua um valor padrão de colunas, podemos definir um valor dinâmico com a palavra-chave `auto-fit`.

```css
.aplicativo {
    display: grid;
    /*
        Cria automaticamente um total de colunas que acomode itens com no mínimo 100px de largura.
    */
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
}
```

### `grid-template-rows: dimensao dimensao..`

Define o número total de linhas e suas respectivas dimensões, necessárias para criação da grade.

```css
.aplicativo {
    display: grid;
    grid-template-rows: 100px 1fr 50px;
}
```

### `grid-area: nome_do_fragmento` & `grid-template-areas: "fragmento1 fragmento2..."`

```css

.nav {
    background-color: orange;
    grid-area: nav;
}

.conteudo {
    background-color: red;
    grid-area: conteudo;
}

.rodape {
    background-color: gray;
    grid-area: rodape;
}

.aplicativo {
    display: grid;
    grid-template-areas: 
        "nav        nav         nav"
        "conteudo   conteudo    nav-lateral"
        "rodape     rodape      rodape"
}

```

**Nota:** Caso seja necessário, para definir um espaçamento entre os itens, temos a propriedade `gap`.

## Itens da Grade (Filho)

### grid-column: posicao_inicial/posicao_final

Define a posição e quantas colunas o item irá ocupar da grade.

### grid-row: posicao_inicial/posicao_final

Define a posição e quantas linhas o item irá ocupar da grade.

### grid-area: nome_do_fragmento

Define o nome da área/fragmento/componente para ser utilizado posteriormente com a propriedade `grid-template-areas`.
