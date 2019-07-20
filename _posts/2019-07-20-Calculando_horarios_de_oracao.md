---
layout: post
title:  "Calculando os Horários de Oração"
author: "Hamid Zarrabi-Zadeh"
translator: "Carlos Delfino"
date:   2019-07-20 12:00:00 -0300
tags: [App, Orações, Cálculos, Matemática, Fajr, Sunrise, Dhuhr, Asr, Sunset, Maghrib, Isha, Midnight ]
image: bismila.png
categories: ["App","Islamic App", Cálculos]
---

Muçulmanos devem orar cinco vezes ao dia. Cada oração tem um horário definido onde deve ser realizada. Este documento descreve estes horários rápidamente, e explica como ele pode ser calculado matemáticamente.

<!--more-->

## Observações do tradutor

O Texto foi traduzido livremente, tendo como objetivo compartilhar para os interessados e para muçulmanos em geral.

O texto original pode ser encontrado em [http://praytimes.org/wiki/Prayer_Times_Calculation](http://praytimes.org/wiki/Prayer_Times_Calculation)

Este algoritimo de calculo é usado em nossa aplicação, e um módulo já com a interface para NativeScript foi disponibilizado em [https://github.com/islamic-works/pray-times-module](https://github.com/islamic-works/pray-times-module).

## Definições

Para determinar o horário exato do período de cada oração (e também para acelerar), nos precisamos determinar nove horários por dia. Estes horários são definidos pela seguinte tabela:

| Horário | Definição |
| Fajr | Quando as estrelas começam a se apagarem (dawn - alvorecer). |
| Sunrise | Horário em que a primeira parte do Sol aparece no horizonte. |
| Dhuhr | Quando o Sol inicia a declinar após atingir  seu ponto mais alto no céu. |
| Asr	| Horário em que o comprimento da sombra de algum objeto atinge um fator (normalmente 1 ou 2) do comprimento do objeto em sí mais o comprimento da sombra do objeto ao meio dia |
| Sunset | O horário em que o Sol desaparece abaixo do horizonte. Por do Sol. |
| Maghrib | logo após o por do sol (sunset). |
| Isha | O Horário que a escuridão cai e não há luz espalhada no céu. |
| Midnight | O horário médio entre o por do sol (sunset) e o amanhecer (sunrise), (ou do por do sol ao Fajr, em algumas escolas de pensamento) |

A próxima seção fornece informações de como calcular os horários acima de forma matemática para alguma localização, se as coordenadas da localização são conhecidas.

## Medidas astronômicas

Há duas medidas astronômicas que são essenciais para calcular os horários de oração. Estas duas medidas são equações de tempo e o declino do Sol.

A Equação do tempo é a diferença entre o horário como lido de um horário de sol e um relógio. Ele resulta de um movimento aparamente irregular do Sol e causado pela combinação da inclinação do eixo de rotação da Terra e a excentricidade de sua orbita. P relógio de sol pode estar a frente (mais rápido) em torno de 16 minutos e 33 segundos (aproximadamente em 3 de novembro) ou atrasar em torno de 15 minutos e 6 segundos (aproximadamente em 12 de fevereiro), como apresentado no gráfico a seguir:

![Gráfico de Horários]({{site.baseurl}}/assets/images/pray-times/Equation_of_time.png)

O Gráfico acima foi originalmente obtida em: http://en.wikipedia.org/wiki/File:Equation_of_time.png

A inclinação do Sol é o angulo entre os raio do sol e o plano do equador da Terra. A inclinação  do Sol altera continuamente través do ano. Ela é uma consequência da inclinação da terra. por exemplo a diferença entre os eixos de rotação e revolução.

![Gráfico de Horários]({{site.baseurl}}/assets/images/pray-times/Declination.png)

As duas medidas astronomicas acima podem ser obtidas com precisão do Almanaque das Estrelas (The Star Almanac), ou pode ser calculado aproximadamente. O seguinte algoritmo do [Observatório Naval dos Estados Unidos Norde Americano \(U.S. Naval Observatory\)](http://aa.usno.navy.mil/faq/docs/SunApprox.php) calcula as coordenadas angulares do Sol para uma aproximação em torno de 1 arcminuto em dois séculos do ano 2000.

```  
   d = jd - 2451545.0;  // jd is the given Julian date 

   g = 357.529 + 0.98560028* d;
   q = 280.459 + 0.98564736* d;
   L = q + 1.915* sin(g) + 0.020* sin(2*g);

   R = 1.00014 - 0.01671* cos(g) - 0.00014* cos(2*g);
   e = 23.439 - 0.00000036* d;
   RA = arctan2(cos(e)* sin(L), cos(L))/ 15;

   D = arcsin(sin(e)* sin(L));  // declination of the Sun
   EqT = q/15 - RA;  // equation of time
```

## Calculando os horários de oração

Para calcular os horários de oração para uma dada localização, nos precisamos conhecer a *latitude* (L) e a *longitude* (Lng) da localidade, com o fuso horário (Time Zone) para esta localização. Nos também obtemos a equação do tempo (EqT) e a inclinação do Sol (D) para uma certa data  usando o algotimo mencionado na seção anterior


### Dhuhr

O Dhuhr pode ser calculado facilmente usando a seguinte formula:

```
Dhuhr = 12 + TimeZone - Lng/15 - EqT
```

A fórmula acima busca calcular o horário do meio do dia, quando o Sol atinge seu ponto mais alto no céu. A uma leve margem é usualmente considerada para o **Dhuhr** como explicado [na nota encontrada neste link.]({{site.baseurl}}/Observacoes_quanto_ao_calculo_do_horario_do_Dhur/)


## Sunrise/Sunset

A Diferença de tempo entre o meio dia e o horário em que o sol atinge um angulo  α acim ado horizonte pode ser calculado usando a seguinte formula:

![Fórmula do Crepúsculo]({{site.baseurl}}/assets/images/pray-times/Twilight-formula.png)

O [Nascer do Sol e o o por do sol Astronômico]({{site.baseurl}}/Nascer_e_Por_do_Sol_Astronomico/), ocorre em α=0. Porém devido a regração da luz pela atmosfera terrestre, o nascer do sol real parece ocorrer antes do nascer do sol astronômico e o pôr do sol real ocorre após o pôr do sol astronômico. O Nascer e Pôr do Sol real podem ser computados usando as seguintes formúlas:

```
Sunrise = Dhuhr - T(0.833),
Sunset = Dhuhr + T(0.833).
```

Se a localização do observador é mais alta que o entorno do terreno, nos podemos considerar esta elevação em consideração, acrescentando a constante acima 0.833 de  `0.347 x sqrt(h)`, onde `h` é a altura do observador em metros.

## Fajr e Isha

There are differing opinions on what angle to be used for calculating Fajr and Isha. The following table shows several conventions currently in use in various countries (more information is available at this page).

| Convention | Fajr Angle | Isha Angle |
| Muslim World League | 18 | 17 |
| Islamic Society of North America (ISNA) | 15 | 15 |
| Egyptian General Authority of Survey | 19.5 | 17.5 |
| Umm al-Qura University, Makkah | 18.5 | 90 min after Maghrib<br> 120 min during Ramadan | 
| University of Islamic Sciences, Karachi | 18 |18 |
| Institute of Geophysics, University of Tehran | 17.7 | 14* |
| Shia Ithna Ashari, Leva Research Institute, Qum | 16 | 14 |

* O Ángulo Isha não é explicitamente definido no método Tehran.

Por exemplo, de acordo com a convenção *Muslim World League*, Fajr = Dhuhr - T(18) e Isha = Dhuhr + T(17).

### Asr

Há duas opiniões principais sobre como calcular o horário do Asr. A maioria das escolas (incluindo Shafi'i, Maliki, Ja'fari, e Hanbali) dizem que o horário é quando o comprimento da sombra do objeto  mais o comprimento da sombra do objeto ao meio dia. A opinião dominante na escola Hanafi, diz que Asr inicia quando o comprimento da sombra de algum objeto é duas vezes o comprimento do objeto mais o comprimento da sombra deste mesmo objeto ao meio dia.

A seguinte fórmula calcula a diferença de horário entre o meio dia e o horário em que a sombra do objeto é igual a `t` vezes o comprimento do objeto em sí, mais o comprimento da sombra do objeto ao meio dia.

[Fórmula do Asr]({{site.baseurl}}/assets/images/pray-times/Asr-formula.png)

Porém, nas primeiras quatros escolas de pensamento, `Asr = Dhuhr + A(1)` e na escola Hanafi `Asr = Dhuhr + A(2).

### Maghrib

No ponto de vista Sunni, o horário para oração do Maghrib inicia uma vez o Sol tendo completamente situado abaixo do horizonte, isto é, Maghrib = Sunset (algumas calculadoras sugerem 1 a 3 minutos após o pôr do sol por precaução). No ponto de vista Shia, a opinião dominante é que assim que a vermelhidão ao leste do Céu que aparece após o por do sol não tenha passado o topo, a oração do Maghrib não deve ser feito. é usual levar em consideração assumindo um angulo crepuscular como  Maghrib = Dhuhr + T(4).

### Midnight

A meia noite é geralmente calculado como a metade do tempo entre o Pôr do Sol e o Nascer do sol, ou seja, Midnight = 1/2(Sunrise - Sunset). No ponto de vista Shia, a meia noite oficial (o fim do horário para fazer a oração do Isha) é a metade do tempo do por do sol ao Fajr, ou seja, Midnight = 1/2 (Fajr - Sunset).

## Altas Latitudes

Em localidades com altas latitudes, o crepúsculo pode persistir através da noite durante alguns meses do ano. Neste períodos anormais, a determinação do Fajr e Isha não é possível usando formulas usualmente mencionadas nas seções anteriores. Para superar este problema, várias soluções tem sido propostas, três delas são descritas abaixo.

### Meio da noite

Neste método, o periodo do por do sol até o nascer do só é dividido em duas metades. A primeira metade é considerado ser a "noite" e outra metade é chamada "aurora". Fajr e Isha são nestes métodos são assumidos ser na metade da noite durante o período anormal.

### Um sétimo da noite

Neste método, o periodo entre o pôr do sol e o nascer do sol é dividido em setes partes. Isha inicia após a primeira sétima parte, e o Fajr é então iniciado na sétima parte.

### Método baseado no Ângulo

Esta é uma solução intermediária, usada por novos calculadoras do horário de oração. Permite α ser o angulo do crepúsculo para o Isha, e permite t = α/60. O período entre o pôr do sol e o nascer do sol é dividido em `t` partes. Isha inicia após a primeira parte. Por exemplo, se o angulo crepuscular para o Isha é 15, então Isha inicia no fim do primeiro quarta parte (15/60) da noite. o Horário do Fajr é calculado de forma similar.

No caso do Maghrib não é igual ao pôr do sol, nos podemos aplicar as regras acima para o Maghrib tanto como para ter certeza que o Maghrib sempre cairá entre o pôr do sol e o Isha durante os períodos anormais.

## Implementação

As fórmulas acima descritas são implementadas completamente e podem ser obtidas em várias linguagens de programação [neste link](http://praytimes.org/wiki/Code).

>> Nota do tradutor: as formulas acima podem ser vista em funcionamento no aplicátivo que estamos desenvolvendo, para baixa-lo em sua versão de teste, [clique aqui, escolha a versão mais recente](https://github.com/islamic-works/pray-times-module/releases). Cso tenha dificuldades use o campo de comentários abaixo para suporte.

## Referências

* [The Determination of Salat Times](http://www.ummah.net/astronomy/saltime), by Dr. Monzur Ahmed.
* [Approximate Solar Coordinates](http://aa.usno.navy.mil/faq/docs/SunApprox.php), by U.S. Naval Observatory.
* [The Islamic Prayer Times](http://www.jas.org.jo/muneer/), by Professor Tariq Muneer.
* Wikipedia, the free encyclopedia.
* [Islamic Works Apps](http/islamic-works.github.io/) 