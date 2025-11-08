---
layout: post
title:  "Observações quanto ao cálculo do horário do Dhur"
author: "Hamid Zarrabi-Zadeh"
translator: "Carlos Delfino"
date:   2019-07-20 11:59:00 -0300
tags: [App, Orações, Cálculos, Nascer do Sol, Pôr do Sol, Horário, Fajr, Sunrise, Dhuhr, Asr, Sunset, Maghrib, Isha, Midnight ]
image: bismila.png
categories: ["App","Islamic App", Cálculos]
---

Dhuhr tem sido definido de diversas formas na literatura:

<!--more-->

* Quando o Sol inicia a declinar (Zawall) após atingir seu ponto mais alto no céu.
* Quando o a sombra de um indicador (uma vara vertical) atinge seu comprimento máximo e inicia a diminuir.
* Quando o disco do Sol sai da linha do zenit, que é a linha entre o observador e o centro do Sol, quando ele está no ponto mais alto.

> Nota do tradutor, este texto foi traduzido do site [Pray Times](http://praytimes.com)

A primeira e a segunda definição são equivalentes, como o comprimento da sombra tem uma correlação direta com a elevação do sol no céu via a seguinte fórmula:

```
Shadow Length = Object Height × cot(Sun Angle).
```

O angulo do Sol é uma função continua sobre o tempo e tem somente um ponto de pico (o ponto em que a tangent de sua curva tem um declive zero) que é realizado exatamente no meio dia. Assim sendo, concordando com a primeira definição, _Dhuhr_ inicia imediatamente após o meio do dia. 

A terceira definição é ligeiramente diferente da duas definições anteriores. De acordo com esta definição, o Sol deve passar a sua linha de zenith antes do _Dhuhr_ iniciar. Nos precisamos a seguinte informação para calcular este horário:

* *Sun radius (r): 695,500 km
* Sun-Earth distance (d): 147,098,074 km to 152,097,701 km

Tendo **r** e **d**, o tempo **t** necessário para o Sol passar sua linha de zenith pode ser calculado usando a seguinte fórmula:

```
t = arctan(r/d) / 2π × 24 × 60 × 60.
```

O valor máximo obtido pela fórmula acima (que corresponde à distância minima entre Sol e Terra), é 65.0 segundos. Sendo assim, ele toma um minuto até o disco do Sol sair do seu zenith que deve ser considerado em considerações para calcular o Dhuhr, se a terceira definição for usada.

## Conclusion

Há três definições para o horário do _Dhuhr_ como descrito acima. De acordo com a primeira definição, _Dhuhr_ = Meio do dia, e de acordo com a terceria definição, Dhuhr = meio do dia + 65 segundos.

## Referências

[Sun](http://en.wikipedia.org/wiki/Sun), from Wikipedia, the free encyclopedia.
[Sun-Earth Distance](http://wiki.answers.com/Q/What_is_the_distance_from_the_Sun_to_the_Earth), from Wiki Answers.
[Islamic Works](http://islamic-works.github.io)