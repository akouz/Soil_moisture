# Soil moisture meter - измеритель влажности почвы

Среди электронных способов измерения влажности почвы наиболее часто используются измерение сопротивления и измерение емкости.  Звучит парадоксально, но в большинстве случаев так назваемые «емкостные измерители влажности почвы» в реальности тоже измеряют сопротивление почвы, а не ее емкость.

Эквивалентная схема участка почвы, на котором производится измерение, состоит из параллельно включенных резистора и конденсатора. Резистор имеет сопротивление от сотен ом до сотен килоом, в зависимости от влажности почвы и ее солености/кислотности и т.п. Емкость конденсатора зависит от площади электродов, расстояния между ними, а также от влажности почвы. Конденсатор в эквивалентной схеме обычно имеет емкость единицы-десятки пикофарад, когда электроды находятся в воздухе. Если опустить их в воду, емкость увеличивается примерно в 2-3 раза, так как дэлектрическая проницаемость воды в 80 раз больше, чем диэлетрическая проницаемость воздуха. 

Чаще всего любительские «емкостные» измерители влажности сделаны примерно так, как показано на фиг.1

![Figure 1](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_1.png)

Figure 1

Датчик состоит из емкости связи Ccpl и, собственно, почвы Rsoil, Csoil. Генератор на базе микроконтроллера выдает прямоугольный сигнал возбуждения частотой несколько десятков или сотен кГц. Резистор R1 соединен с датчиком и образует делитель сигнала. Результирующий сигнал  снимается квазипиковым детектором D1,C1,R2 и  измеряется при помощи АЦП, встроенного в тот же микроконтроллер. 

Для уверенной работы такой схемы емкость связи Ccpl должна быть как можно больше,  а частота генератора - как можно выше. Датчик обычно выполняется в виде довольно широкой двухсторонней печатной платы, наружные поверхности которой заняты электродами. Электроды  отделены от почвы  тонким слоем паяльной маски. Такая изоляция мало защищает от коррозии, поэтому датчики служат недолго, зато тонкая изоляция обеспечивает большую емкость связи Ccpl. 

Результаты моделирования этой схемы в Spice при частоте генератора 100 кГц показаны на фиг.2. По горизонтальной оси — время, по вертикальной — напряжение на входе АЦП. Зависимость выходного сигнала от емкости почвы Csoil очень слабая, сигнал в основном зависит от сопротивления почвы Rsoil.

![Figure 2](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_2.png)

Figure 2

Tакой способ измерения чувствителен к химическому составу почвы. Кроме того, схема с детектором на обычном кремниевом диоде чувствительна к изменениям температуры.

Другая схема «емкостного» измерителя представлена на фиг.3. Она использует генератор на триггере Шмидта. К сожалению, за исключением меньшей чувствительности к изменениям температуры, она обладает такими же недостатками, как и схема фиг.1.

![Figure 3](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_3.png)

Figure 3

Пртотип схемы фиг.3 был собран на 4-слойной печатной плате размерами 145х10 мм. Электроды расположены на внутренних слоях, толщина диэлектрика между наружными и внутренними слоями 0.25 мм.  Датчик подключен к терминалам W1, W2. В воздухе частота генератора равна 55 кГц, в стакане с водой — 10 кГц.

Из-за относительно большой толщины диэлектрика и малой площади электродов, емкость связи Ccpl мала. Поэтому при прямом контакте с землей зона наибольшей чувствительности датчика приходится на совсем сухую, высокоомную почву. При добавлении в сухой песчаный суглинок всего лишь 0.8% воды (по весу) частота уходит к минимуму и затем почти не меняется. 

Сдвинуть чувствительность датчика в сторону более влажной (и более низкоомной) почвы можно, если уменьшить R1 до 10...100 кОм. Соответственно, частота на выходе увеличится, а влияние емкости связи уменьшится.

Улучшить свойства такого датчика не меняя R1 удалось после того, как на обе стороны печатной платы был наклеен синтетический войлок толщиной 4 мм. После этого передаточная характеристика получилась такой, как показано на фиг.4

![Figure 4](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_4.png)

Figure 4

С войлоком частота в воздухе уменьшилась до 51.6 кГц, примем это за 100%. Результаты измерений:
  * В сухом песчаном суглинке — частота 98%
  * При добавлении 1% воды (по весу) — 89%
  * 2% воды — 81%
  * 3% воды — 69%
  * 4% воды — 54%
  * 5% воды — 42%
  * 6% воды — 36%
  * 7% воды — 31%
  * 8% воды — 28%

На фиг.5 показаны датчики без войлока и с войлоком. Электроника залита нейтральным силиконом Dow Corning 3140 и защищена прозрачной термоусадочной трубкой поверх заливки. 

![Figure 5](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_5.png)

Figure 5

Для того, чтобы датчик влажности почвы действительно мерял влажность, он должен мерять емкость почвы Csoil невзирая на изменения сопротивления почвы. Очевидно измерения надо производить на таких частотах,  где импеданс Csoil будет существенно меньше, чем  Rsoil. Например,  на частоте 100 МГц импеданс конденсатора 10 пФ составляет всего 159 Ом, поэтому изменения сопротивления почвы от 1 кОм и выше не будут сильно влиять на результат. 

Видоизмененная схема емкостного датчика на базе триггера Шмидта представлена на фиг.6. Резистор в обратной связи заменен на катушку индуктивности 330 нГ. 

![Figure 6](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_6.png)

Figure 6


При той же кофигурации электродов, когда электроды находятся в воздухе, частота на выходе датчика равна 71 МГц, двойная амплитуда 2.3В. С электродами в стакане с водой частота падает до 41 МГц. В песчаном суглинке с водой 10% по весу частота равна 64 МГц. Такому датчику обклеивание войлоком не требуется. 
