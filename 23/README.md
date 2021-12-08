# Aula 23 - Sass

## Instalação

### Node.js

```
npm install -g sass
```

### Windows (Chocolatey)

```
choco install sass
```

### Mac OS X ou Linux (Homebrew)

```
brew install sass/sass/sass
```

## Processamento

```
sass entrada.scss saida.css
```

ou 

```
sass --watch entrada.scss saida.css
```

**Nota:** É possível compilar multiplos arquivos utilizando `sass`, conforme o exemplo a seguir

```
sass app/sass:public/stylesheets
```

ou 

```
sass --watch app/sass:public/stylesheets
```

## Sintaxe

**Pré compilado**

input.scss

```scss
.nav {
    
    ...

    &__item {
        ...
    }

    &__link {
        ...
    }
}
```

**Pós processamento**

output.css

```scss
.nav { ... }

.nav__item { ... }

.nav__link { ... }
```

## Variáveis

**Pré compilado**

```scss
$fonte-padrao: Helvetica, sans-serif;

body {
    font: 100% $fonte-padrao;
}
```

**Pós processamento**

```css
body {
    font: 100% Helvetica, sans-serif;
}
```

## Fragmentação

**Pré compilado**

_variaveis.scss

```scss
$fonte-padrao: Helvetica, sans-serif;
$cor-primaria: orange;
```

main.scss

```scss
@import 'variaveis';

body {
    font-family: $fonte-padrao;
    color: $cor-primaria;
}
```

**Pós processamento**

style.css

```css
body {
    font-family: Helvetica, sans-serif;
    color: orange;
}
```

## Módulos

**Pré compilado**

_tipografia.scss

```scss
$fonte-padrao: Helvetica, sans-serif;
```

main.scss

```scss
@use 'tipografia';

body {
    font-family: tipografia.$fonte-padrao;
}
```

**Pós processamento**

```css
body {
    font-family: Helvetica, sans-serif;
}
```

## Mixins

**Pré compilado**

```scss
@mixin centralizar {
    margin-left: auto;
    margin-right: auto;
}

.l-conteudo {
    max-width: 960px;
    @include centralizar;
}
```

**Pós processamento**

```css
.l-conteudo {
    max-width: 960px;
    margin-left: auto;
    margin-right: auto;
}
```

## Herança

**Pré compilado**

```scss
%hover {
    transition: transform .5s;
    transform: translateX(-5px) scale(1.1);
}

.botao {
    background-color: green;
    padding: 10px 20px;
    @extend %hover;
}

.foto {
    borde: 1px solid lightgray;
    border-radius: 5px;
    @extend %hover;
}

```

**Pós processamento**

```css
.botao {
    background-color: green;
    padding: 10px 20px; 
}

.foto {
    borde: 1px solid lightgray;
    border-radius: 5px;
}

.botao, .foto {
    transition: transform .5s;
    transform: translateX(-5px) scale(1.1);
}

```