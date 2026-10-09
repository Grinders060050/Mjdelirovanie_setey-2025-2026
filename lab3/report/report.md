---
## Front matter
title: "Лабораторная работа № 3"
subtitle: "Шифрование гаммированием"
author: "Шуваев Сергей Александрович"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить и реализовать шифр гаммированием.

# Задание

Реализовать с помощью языка программирования Julia алгоритм шифрования гаммированием конечной гаммой.

# Теоретическое введение

Julia -- высокоуровневый свободный язык программирования с динамической типизацией, созданный для математических вычислений [@julialang]. Эффективен также и для написания программ общего назначения. Синтаксис языка схож с синтаксисом других математических языков, однако имеет некоторые существенные отличия.

Для выполнения заданий была использована официальная документация Julia [@juliadoc].

# Выполнение лабораторной работы

Шифрование гаммированием -- это симметричный метод шифрования, при котором к открытым данным (тексту) применяется операция наложения (обычно XOR) с последовательностью случайных чисел, называемой гаммой. 
Эта гамма должна быть не короче сообщения и обеспечивает обратимость операции, позволяя расшифровать данные при наличии той же гаммы. 
Такой метод обеспечивает высокую стойкость при условии использования случайной и одноразовой гаммы.

Реализуем этот алгоритм на Julia:

```Julia
function gamma_encryption(word, key)
    encrypted = ""
    word_chars = collect(word)
    key_chars = collect(key)
    for (i,j) in enumerate(word)
        c = (Int(j) - Int('А') + \\
          Int(key_chars[(i - 1) % length(key) + 1]) \\
            - Int('А') + 1) % 32 + Int('А')
        encrypted *= Char(c)
    end
    return encrypted
end

word = "ПРИКАЗ"
key = "ГАММА"
res = gamma_encryption(word,key)
print(res)
```

Проверим работу программы, выполнив пример из лабораторной работы ([рис. @fig-001]):

![Результат работы шифра гаммированием](image/1.png){#fig-001 width=70%}

# Выводы

В результате выполнения данной лабораторной работы был изучен и реализован алгоритм шифрования гаммированием конечной гаммой.

# Список литературы{.unnumbered}

::: {#refs}
:::
