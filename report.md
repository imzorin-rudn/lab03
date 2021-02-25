---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №3"
subtitle: "дисциплина: Математическое моделирование"
author: "Зорин Илья Михайлович"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Построить графики модели боевых действий.

# Задание

**Вариант 47**  
  Задача: Между страной Х и страной У идет война. Численность состава войск
исчисляется от начала войны, и являются временными функциями
x(t) и y(t). В начальный момент времени страна Х имеет армию численностью 55 000 человек, а
в распоряжении страны У армия численностью в 45 000 человек. Для упрощения
модели считаем, что коэффициенты a, b, c, h постоянны. Также считаем
P(t) и Q(t) непрерывные функции.  
  Постройте графики изменения численности войск армии Х и армии У для
следующих случаев:

1. Модель боевых действий между регулярными войсками  
  $\frac{\partial x}{\partial t} = -0,41x(t)-0,821y(t)+5sin(t)+1$  
  $\frac{\partial y}{\partial t} = -0,541x(t)-0,57y(t)+cos(6t)+1$

2. Модель ведение боевых действий с участием регулярных войск и
партизанских отрядов  
  $\frac{\partial x}{\partial t} = -0,31x(t)-0,87y(t)+|sin(4t)|$  
  $\frac{\partial y}{\partial t} = -0,43x(t)y(t)-0,51y(t)+|cos(3t)|$

# Выполнение лабораторной работы

**1. Рассмотрим подробнее уравнения**

1.1. В первом случае потери, не связанные с боевыми действиями, описывают члены -0,41x(t) и -0,57y(t), а
-0,821y(t) и -0,541x(t) отражают потери на поле боя. Также 5sin(t)+1 и cos(6t)+1 учитывают 
возможность подхода подкрепления к войскам Х и У в течение одного дня.

1.2. Во втором случае в борьбу добавляются партизанские отряды и потери, не связанные с боевыми действиями, описывают члены -0,31x(t) и -0,51y(t), а
-0,87y(t) и -0,43x(t)y(t) отражают потери на поле боя. Также 5sin(t)+1 и cos(6t)+1 учитывают 
возможность подхода подкрепления к войскам Х и У в течение одного дня.  
  
1.3. Начальные условия для обоих случаев будут равно $x_{0}=55.000$, $y_{0}=45.000$

**2. Построение графиков численности войск**

2.1. Написал программу на Modelica для 1 случая:
```
model lab03
  parameter Real a=-0.41;
  parameter Real b=-0.821;  
  parameter Real c=-0.541;
  parameter Real h=-0.57;
  parameter Real x0=55000;
  parameter Real y0=45000;
  Real x(start=x0);
  Real y(start=y0);
  Real t;
equation
  der(x)=a*x+b*y+5*sin(t)+1;
  der(y)=c*x+h*y+cos(6*t)+1;
  t=0;
end lab03;

```
Получил следующий график (см. рис. -@fig:001).

![Рис. 1. График для 1 случая](image/1.png){ #fig:001 width=70% }

2.2. Написал программу на Modelica для 2 случая:
```
model lab0302
  parameter Real a=-0.31;
  parameter Real b=-0.87;  
  parameter Real c=-0.43;
  parameter Real h=-0.51;
  parameter Real x0=55000;
  parameter Real y0=45000;
  Real x(start=x0);
  Real y(start=y0);
  Real t;
equation
  der(x)=a*x+b*y+abs(sin(4*t));
  der(y)=c*x*y+h*y+abs(cos(3*t));
  t=0;
end lab0302;
```
Получил следующий график (см. рис. -@fig:002).

![Рис. 2. График для 2 случая](image/2.png){ #fig:002 width=70% }

# Выводы

Построил графики модели боевых действий.
