---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе 2"
subtitle: "дисциплина: Математическое моделирование"
author: "Фогилева Ксения Михайловна, НПИбд-02-18"

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

Решить задачу о погоне, построить графики с помощью Python.

# Задание

**Вариант 43**
На море в тумане катер береговой охраны преследует лодку браконьеров.
Через определенный промежуток времени туман рассеивается, и лодка обнаруживается 
на расстоянии 16.2 км от катера. Затем лодка снова скрывается в тумане и уходит 
прямолинейно в неизвестном направлении. Известно, что скорость катера в 4 раза 
больше скорости браконьерской лодки.

1. Вывести дифференциальное уравнение, описывающее движение катера, с начальными условиями.
2. Построить траектории движения катера и лодки для двух случаев.
3. Определить точку пересечения катера и лодки.


# Выполнение лабораторной работы

**1. Вывод дифференциального уравнения**

1.1. Принимаем за $t_{0} = 0$, $x_{Л0} = 0$ -- место нахождения лодки браконьеров 
в момент обнаружения, $x_{К0} = 16.2$ км -- место нахождения катера береговой охраны 
относительно лодки браконьеров в момент обнаружения лодки.

1.2. Вводим полярные координаты. Полюс – это точка обнаружения лодки 
браконьеров $x_{Л0} (θ = x_{Л0} = 0)$, а полярная ось $r$ проходит через точку нахождения 
катера береговой охраны. (см. рис. -@fig:001)

![Положение катера и лодки в начальный момент времени](image/1.png){ #fig:001 width=70% }

1.3. Траектория катера такая, что и катер, и лодка все время 
на одном расстоянии от полюса $θ$, только в этом случае траектория катера пересечется с 
траекторией лодки. Поэтому в начале катер береговой охраны должен двигаться некоторое 
время прямолинейно, пока не окажется на том же расстоянии от полюса, что и лодка браконьеров. 
После этого катер береговой охраны должен двигаться вокруг полюса удаляясь от него с той же 
скоростью, что и лодка браконьеров.

1.4. Для того, чтобы найти расстояние x (расстояние, после которого катер начнет двигаться 
вокруг полюса), нужно составить простое уравнение. Через время $t$ катер и лодка 
окажутся на одном расстоянии x от полюса. За это время лодка пройдет $x$, а катер $16,2 - x$ (или 
$16,2 + x$, в зависимости от начального положения катера относительно полюса). Время, за которое 
они пройдут это расстояние, можно вычислить как $x \over v$ или $16.2 - x \over 4v$ (во втором 
случае $16,2 + x \over 4v$). Так как время одинаковое, то эти величины одинаковы. Значит
неизвестное расстояние $x$ находится из следующего уравнения:
$$ \frac{x}{v} = \frac{16,2-x}{4v}\ или\ \frac{x}{v} = \frac{16,2+x}{4v}\ $$ 

Тогда $x_{1} = \frac{1}{5}k = 3,24$ (км), а $x_{2} = \frac{1}{3}k = 3,2$ (км), задачу решаем для двух случаев.

1.5. Когда катер береговой охраны окажется на одном расстоянии от полюса, что и лодка, он 
должен сменить прямолинейную траекторию и начать двигаться вокруг полюса удаляясь от него со скоростью 
лодки $v$. Для этого скорость катера раскладывается на две составляющие: $v_{r}$ – радиальная скорость и 
$v_{τ}$ – тангенциальная скорость. (см. рис. -@fig:002)

![Разложение скорости катера на тангенциальную и радиальную составляющие](image/2.png){ #fig:002 width=70% }

Радиальная скорость – скорость, с которой катер удаляется от полюса, $v_{r} = \frac{\partial r}{\partial t}$. Требуется, 
чтобы эта скорость была равна скорости лодки, поэтому $v_{r} = \frac{\partial r}{\partial t} = v$.
                                        
Тангенциальная скорость – линейная скорость вращения катера относительно полюса. Она равна 
произведению угловой скорости на радиус, $v_{τ} = r\frac{\partial θ}{\partial t}$.

Из рис. -@fig:002 по теореме Пифагора: $v_{τ} = \sqrt{16v^2 - v^2} = \sqrt{15}v = \frac{\sqrt{15}}v$, 
тогда $r\frac{\partial θ}{\partial t} = \frac{\sqrt{15}}v$.
1.6. Решение исходной задачи сводится к решению системы из двух дифференциальных уравнений:
\begin{equation*} 
  \begin{cases} 
    \frac{\partial r}{\partial t} = v 
    \\
    r\frac{\partial θ}{\partial t} = \frac{\sqrt{5}}v 
  \end{cases}
\end{equation*} 

Если исключить из полученной системы производную по t, можно перейти к уравнению ниже:
$$ \frac{\partial r}{\partial θ} = \frac{r}{\sqrt{15}} $$

Решив это уравнение, получим траекторию движения катера в полярных координатах. Начальные условия:
\begin{equation*}
  \begin{cases}
    θ_{0} = 0 
    \\ 
    r_{0} = x_{1} = \frac{1}{5}k
  \end{cases}
\end{equation*}

\begin{equation*}
  \begin{cases}
    θ_{0} = 0 
    \\ 
    r_{0} = x_{2} = \frac{1}{3}k
  \end{cases}
\end{equation*} 

**2. Построение траекторий движения катера и лодки**

2.1. Была написана программа на Python:
```
import math
import numpy as np
from scipy.integrate import odeint
import matplotlib.pyplot as plt

k = 16.2
fi = 3*math.pi/4

#функция, которая описывает движение катера береговой охраны
def dr(r, tetha): 
    dr = r/math.sqrt(15)
    return dr

r01 = 1/5*k #1 случай
r02 = 1/3*k #2 случай

te = np.arange(0, 2*math.pi, 0.01)

r1 = odeint(dr, r01, te)
r2 = odeint(dr, r02, te)

#функция, которая описывает движение лодки браконьеров
def xt(t): 
    xt = math.tan(fi)*t
    return xt

t = np.arange(0, 20, 1)

#Перевод в полярные координаты
tete = (np.tan(xt(t)/t))**-1
rr = np.sqrt(t*t + xt(t)*xt(t))

#построение траектории движения катера в полярных координатах. Случай 1
plt.polar(te, r1, 'g')
#построение траектории движения лодки в полярных координатах
plt.polar(tete, rr, 'b') 

#построение траектории движения катера в полярных координатах. Случай 2
plt.polar(te, r2, 'g')
#построение траектории движения лодки в полярных координатах
plt.polar(tete, rr, 'b')
```

2.2. Получились следующие графики:(см. рис. -@fig:003 и -@fig:004)

![Траектории движения катера и лодки. 1 случай](image/3.jpg){ #fig:003 width=70% }

![Траектории движения катера и лодки. 2 случай](image/4.jpg){ #fig:004 width=70% }

**3. Точка пересечения**

3.1. Для определения точки пересечения добавим следующие строки:
```
#Случай 1
idx = np.argwhere(np.diff(np.sign(rr - r1))).flatten()
print (tete[-1])
print (rr[idx[-1]])

#Случай 2
idd = np.argwhere(np.diff(np.sign(rr - r2))).flatten()
print (tete[-1])
print (rr[idd[-1]])
```

3.2. В итоге получили, что в случае 1 точка пересечения: $θ = -0.6420926159343304, r = 15.556349186104047$,
а в случае 2: $θ = -0.6420926159343304, r = 25.455844122715714$.

# Выводы

Решила задачу о погоне, построила графики с помощью Python.
