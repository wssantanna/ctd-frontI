# Aula 18 - CSS: Flexbox 1/2

## Conteúdo Flexível (Pai)

Através do **conteúdo pai**, é possível controla o comportamentos dos itens que são **filhos diretos**.

### `display: flex`

Define o elemento como um **conteúdo flexível**, tornando os seus filhos **itens com propriedades flexíveis**.

```css
.galeria {
    display: flex;
}
```

### `flex-direction: row|row-reverse|column|column-reverse`

Define como deseja posicionar os **itens com propriedades flexíveis**. 

**Nota:** Por padrão os itens se posicionam na horizontal (um ao lado do outro), porém podemos trabalhar com direcionamento vertical (um abaixo do outro).

```css
.galeria {
    display: flex;
}

.galeria.ordem__crescente {
    flex-direction: column;
}

.galeria.ordem__decrescente {
    flex-direction: column-reverse;
}
```

### `flex-wrap: wrap|nowrap|wrap-reverse`

Define o controle de quebra de linhas.

```css
.galeria {
    display: flex;
    flex-wrap: wrap;
}
```
### `justify-content: flex-start|flex-end|center|space-between|space-around`

Distribui horizontalmente os itens.

```css
.galeria {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-between;
}

.galeria.alinhar-horizontalmente__inicio {
    justify-content: flex-start;
}

.galeria.alinhar-horizontalmente__centro {
    justify-content: center;
}

.galeria.alinhar-horizontalmente__final {
    justify-content: flex-end;
}
```

### `align-items: stretch|flex-start|flex-end|center|baseline`

Alinha verticalmente os itens.

```css
.galeria {
    display: flex;
    flex-wrap: nowrap;
    align-items: flex-start;
}

.galeria.alinhar-verticalmente__inicio {
    align-items: flex-start;
}

.galeria.alinhar-verticalmente__centro {
    align-items: center;
}

.galeria.alinhar-verticalmente__final {
    align-items: flex-end;
}

```

### `align-content: stretch|flex-start|flex-end|center|baseline`

Distribui verticalmente os itens.

```css
.galeria {
    display: flex;
    flex-wrap: wrap;
    align-content: stretch;
}
```

**Nota**: Somente é possível visualizar os efeitos caso exista quebra de linha.

**Nota**: Somente é possível visualizar os efeitos caso o **conteúdo pai** possuir dimensão superior a somatória das linhas de itens.

