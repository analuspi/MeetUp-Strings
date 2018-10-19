<!DOCTYPE html>
<html>
  <head>
    <title>Manipulação de Strings no R</title>
    <meta charset="utf-8">
    <meta name="author" content="Ana Lu Spinola, R-ladies" />
    <link href="libs/remark-css-0.0.1/default.css" rel="stylesheet" />
    <link href="libs/remark-css-0.0.1/rladies.css" rel="stylesheet" />
    <link href="libs/remark-css-0.0.1/rladies-fonts.css" rel="stylesheet" />
  </head>
  <body>
    <textarea id="source">
class: center, middle, inverse, title-slide

# Manipulação de Strings no R
### Ana Lu Spinola, R-ladies
### 15 de outubro de 2018

---

class: center, middle
# O que vamos fazer?

Algumas definições

Ver as funções básicas 

Falar de expressões regulares

---
# Básico de strings

Use **'** ou **"** para delimitar strings. Aspas duplas são preferiveis.


```r
s1 &lt;- "Hello, World"
s1
```

```
## [1] "Hello, World"
```

```r
s2 &lt;- 'Eu não gosto de aspas simples, mas vou usar para mostrar que dá no mesmo'
s2
```

```
## [1] "Eu não gosto de aspas simples, mas vou usar para mostrar que dá no mesmo"
```

```r
s3 &lt;- c("mulher", "linda", "poderosa")
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```
---
# Alguns caracteres especiais

Para incluir caracteres especiais em uma string, você tem que que sinaliza-los com uma barra invertida:

&lt;table&gt;
        &lt;tbody&gt;
        &lt;tr&gt;
            &lt;th&gt;Símbolo&lt;/th&gt;
            &lt;th&gt;Significado&lt;/th&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;\n&lt;/td&gt;
            &lt;td&gt;parágrafo&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;\t&lt;/td&gt;
            &lt;td&gt;tab&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
        &lt;td&gt;\"&lt;/td&gt;
        &lt;td&gt;aspas&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td&gt;\'&lt;/td&gt;
            &lt;td&gt;apóstrofe&lt;/td&gt;
        &lt;/tr&gt;
    &lt;/tbody&gt;
    &lt;/table&gt;

Use `?"'"` para listar todos
---
# O pacote stringr do R

No R base, temos várias funções para trabalhar com strings

As vantagens do `stringr` são:

&lt;ul&gt;
&lt;li&gt;possibiliade de trabalhar em várias línguas
&lt;li&gt;não considera NA como caracter
&lt;li&gt;possibilidade de trabalhar com expressões regulares
&lt;\ul&gt;


```r
library(stringr)
```
---

# A função `str_lenght`


```r
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```

```r
str_length(s3)
```

```
## [1] 6 5 8
```

# Combinando strings


```r
str_c("Eu", "adoro", "chocolate")
```

```
## [1] "Euadorochocolate"
```

```r
str_c("Eu", "adoro", "chocolate", sep = " ")
```

```
## [1] "Eu adoro chocolate"
```
---
# Combinando vetores e strings


```r
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```

```r
str_c(s3, collapse = ",")
```

```
## [1] "mulher,linda,poderosa"
```

```r
str_c(1:3, s3)
```

```
## [1] "1mulher"   "2linda"    "3poderosa"
```

```r
str_c(str_c(1:3, ". "), s3)
```

```
## [1] "1. mulher"   "2. linda"    "3. poderosa"
```
---
# Separando strings


```r
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```

```r
str_sub(s3, start = 1, end = 2)
```

```
## [1] "mu" "li" "po"
```

```r
str_sub(s3, -3, -2)
```

```
## [1] "he" "nd" "os"
```
---
# Caixa alta e caixa baixa


```r
str_to_lower(s1)
```

```
## [1] "hello, world"
```

```r
str_to_upper(s1)
```

```
## [1] "HELLO, WORLD"
```

```r
str_to_title(s1)
```

```
## [1] "Hello, World"
```
---
# Expressões Regulares (regex)

```r
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```

```r
str_detect(s3, "l")
```

```
## [1]  TRUE  TRUE FALSE
```

```r
str_detect(s3, "a")
```

```
## [1] FALSE  TRUE  TRUE
```
---
# Nem tudo é o que parece...

 &lt;img src="img/nutella-no-pote-de-feijão.jpg" alt="feijão no pote de nutella"&gt;
---
#Nem tudo é o que parece...

Sempre que um \ aparecer em uma expressão regular, você deve escrevê-lo como \\\

Use `writeLines()` para ver como R vê sua string de fato:

```r
writeLines("\\.")
```

```
## \.
```

```r
writeLines("\\ é uma barra invertida")
```

```
## \ é uma barra invertida
```
---
# Caracteres especiais em regex


```r
spec1 &lt;- "AnaLu." 

str_detect(spec1, "Lu.") #ponto como regex
```

```
## [1] TRUE
```

```r
str_detect(spec1, "Lu\\.") #ponto como ponto
```

```
## [1] TRUE
```

```r
spec2 &lt;- "R-ladies\\AnaLu" #queremos uma barra só

str_detect(spec2, "s\\\\A") #queremos achar uma barra entre s e A
```

```
## [1] TRUE
```
---
# 4 barras para localizar 1??

.center[
  - Estamos progurando por uma barra invertida (#4)
  - Usamos uma barra invertida para indicar que é uma barra e não um caracter special (#3)
  - Usamos duas barras para indicar a regex (#2 e #1)
]
---

# Marcadores (âncoras)

&lt;ul&gt;
&lt;li&gt; ^ indica começo do string
&lt;li&gt; $ indica fim do string



```r
s3
```

```
## [1] "mulher"   "linda"    "poderosa"
```

```r
str_detect(s3, "a$") #palavras que terminam com a
```

```
## [1] FALSE  TRUE  TRUE
```

```r
str_extract(s3, "^.u" ) #palavras com u na segunda posição
```

```
## [1] "mu" NA   NA
```
---
class: center, midle

# Obrigada!

GitHub: analuspi
    </textarea>
<script src="https://remarkjs.com/downloads/remark-latest.min.js"></script>
<script>var slideshow = remark.create({
"highlightStyle": "github",
"highlightLines": true,
"countIncrementalSlides": false
});
if (window.HTMLWidgets) slideshow.on('afterShowSlide', function (slide) {
  window.dispatchEvent(new Event('resize'));
});
(function() {
  var d = document, s = d.createElement("style"), r = d.querySelector(".remark-slide-scaler");
  if (!r) return;
  s.type = "text/css"; s.innerHTML = "@page {size: " + r.style.width + " " + r.style.height +"; }";
  d.head.appendChild(s);
})();</script>

<script>
(function() {
  var i, text, code, codes = document.getElementsByTagName('code');
  for (i = 0; i < codes.length;) {
    code = codes[i];
    if (code.parentNode.tagName !== 'PRE' && code.childElementCount === 0) {
      text = code.textContent;
      if (/^\\\((.|\s)+\\\)$/.test(text) || /^\\\[(.|\s)+\\\]$/.test(text) ||
          /^\$\$(.|\s)+\$\$$/.test(text) ||
          /^\\begin\{([^}]+)\}(.|\s)+\\end\{[^}]+\}$/.test(text)) {
        code.outerHTML = code.innerHTML;  // remove <code></code>
        continue;
      }
    }
    i++;
  }
})();
</script>
<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
(function () {
  var script = document.createElement('script');
  script.type = 'text/javascript';
  script.src  = 'https://mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML';
  if (location.protocol !== 'file:' && /^https?:/.test(script.src))
    script.src  = script.src.replace(/^https?:/, '');
  document.getElementsByTagName('head')[0].appendChild(script);
})();
</script>
  </body>
</html>
