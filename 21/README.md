# Aula 21 - Design adaptativo

## Sobre adaptatividade

### Resolução de Tela vs. Resolução Vieweport

Resolução da tela = 
- Densidade de píxel (ppi pixels per inch - pixels por polegada) Tela
- Densidade de pontos (dpi dots per inch - pontos por polegada) Impressão
Resolução da Viewport = Dimensão da janela do navegador.

## `<meta name="viewport" content="">`

### `width`

### `with-device=width`

### `initial-scale`

### `maximum-scale`

### `minimum-scale`

### `user-scalable`

**Nota:** user-scalable causa problemas de acessidibilidade

## Media Query

Em tradução livre, `consulta de mídia` é, de modo geral um condição, ou mais, que define quais regras CSS melhor adaptaram o documento a mídia e/ou dipositivo.

A interpretação dessas condições podem variar muito, sendo possível que envolvam duas ou mais condições para se chegar ao resultado desejado. Seguindo essa premissa, deve-se entender que quanto mais específico for as informações de dispositivo alvo, mais específicas serão as `media queries`.

### Sintaxe

```css
@media(condional) { ... }
```

#### Propriedades 

##### `min-width`

```css
@media(min-width: 480px) { ... }
```

##### `max-width`

```css
@media(max-width: 728px) { ... }
```

##### `orientation: landscape|portrait`
```css
@media(max-width: 728px) and (orientation: landscape) { ... }
```

## Unidades de medida responsivas

Todas as unidades de medida responsivas de um valor de contexto. Normalmente os valores utilizados como contexto são definidos como padrão pelo navegador e dispositivo, porém é possível alterar esses valores e se beneficiar do recurso.

Cada tipo de unidade de medida tem sua própria forma de interpretar o contexto, como podemos ver a seguir.

### `%`

Sempre irá considerar o seu `elemento pai` como **contexto**. O elemento filho irá se basear nos valor de `width` e/ou `height`.

**CSS**
```css
.conteudo-pai {
    width: 1280px
}

.conteudo-filho {
    /* 
        Considerando o contexto de uma dimensão de 1280px,
        o conteúdo filho sumirá a dimensão de 640px. 
    */
    width: 50%;
}
```

**HTML**
```html
<div class="conteudo-pai">
    <div class="conteudo-filho">...<div>
    <div class="conteudo-filho">...<div>
</div>
```

**Nota:** A formula para calcular a porcentagem do elemento filho é `dimensaoDoFilho * 100 / dimensaoDoPai = valorDaPorcentagemDoFilho`.

**Nota:** A formula para calcular o valor em píxel do elemento filho é `dimensaoDoPai * valorDaPorcentagemDoFilho / 100`.

### `em`

Muito semelhante com a unidade de medida `%`, por considerar o seu `elemento pai` como **contexto**. Tem como diferença o contexto calulado a partir da propriedade `font-size`, invés das propriedades `width` e `height`. 

```css
.cabecalho {
    font-size: 18px;
}

.cabecalho__titulo {
    /*
        Considerando o contexto de 18px do elemento pai .cabecalho,
        o valor do título irá calcular 18px * 1.77, logo seu valor final 
        será de 31,86px, ou aproximadamente 32px;
    */
    font-size: 1.77em;
}

.cabecalho__subtitulo {
    /*
        Considerando o contexto de 18px do elemento pai .cabecalho,
        o valor do título irá calcular 18px * 1.33, logo seu valor final 
        será de 24.84px, ou aproximadamente 24px;
    */
    font-size: 1.33em;

}

.cabecalho__descricao {
    /*
        Considerando o contexto de 18px do elemento pai .cabecalho,
        o valor do paragrafo irá calcular 18px * 1, logo o seu valor final 
        será de 18px.  
    */
    font-size: 1em;
}
```

```html
<header class="cabecalho">
    <h1 class="cabecalho__titulo">Título</h1>
    <h2 class="cabecalho__subtitulo">Subtítulo</h2>
    <p class="cabecalho__descricao">Descrição</p>
</header>
```

O benefício de se utilizar a unidade de medida `em` esta na possibilidade de ajustar todo tamanho de fonte a partir do elemento pai.

```css

body {
    font-size: 24px;
}

p {
    /*
        O tamanho padrão do paragrafo seguirá o contexto de 24px, 
        até a resolução de 768px, a parti de 769px, o valor se ajustará
        para 16px.
    */
    font-size 1em;
}

@media(min-width: 768px) {
    body {
        font-size: 16px;
    }
}
```

**Nota:** Caso não seja definido um valor de `font-size` para o elemento pai, será utilizado o valor padrão do documento, que normalmente é de **16px**.

#### Pros

- É possível controlar o tamanho de todos os elementos filhos a partir do elemento pai.

#### Contras

- O valor é acumulativo, ou seja, se mal desenvolvido pode gerar conflitos que atrapalhariam a interpretação do valor final do elemento. 

**Exemplo**

```css
.elemento-pai {
    font-size: 20px;
}

.elemento-filho {
    /*
        20px * 2 = 40px;
    */
    font-size: 2em; 
}

.elemento-neto {
    /*
        Como o elemento esta dentro do .elemento-filho
        seu contexto passa ser o resultado anterior, 
        ou seja, 1em passou a ser 40px por conta 
        do contexto acumulado.
    */
    font-size: 1em;
}

```

```html
<!-- Contexto 20px -->
<div class="elemento-pai">
    <!-- Contexto 2em, ou seja, 20px * 2em = 40px -->
    <div class="elemento-filho">
        <!-- Contexto 40px, ou seja, 40px * 1em = 40px -->
        <div class="elemento-neto"></div>
    </h1>
</div>
```

### `rem`

A unidade de medida `rem` corrige os possíveis conflitos gerados na unidade de medida `em`, pois independente do valor base do seu `elemento pai direto`, sempre irá se basear no contexto do documento, ou seja, do elemento `<html>`.

```css
html {
    font-size: 18px;
}

h1 {
    /*
        18px * 1.77rem = 31.86px
    */
    font-size: 1.77rem;
}

p {
    /*
        18px * 1rem = 18px
    */
    font-size: 1rem;
}
```

### `vw`

Retorna a porcentagem da largura relativa a `viewport`, ou seja, a largura da janela.

```css
.aplicativo {
    width: 100vw;
}
```

### `vh`

Retorna a porcentagem da altura relativa a `viewport`, ou seja, o altura da janela.

```css
.aplicativo {
    height: 100vh;
}
```

## Dicas
- [Artigo: A diferença entre ppi e dpi](https://designculture.com.br/a-diferenca-entre-ppi-e-dpi/)
- [Artigo: A pixel is not a pixel is not a pixel](https://www.quirksmode.org/blog/archives/2010/04/a_pixel_is_not.html)
- [Ferramenta: My Device](https://www.mydevice.io/)