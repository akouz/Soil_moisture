# Измеритель влажности почвы - Soil moisture meter

**Среди электронных способов измерения влажности почвы наиболее часто используются измерение сопротивления и измерение емкости.  Звучит парадоксально, но в большинстве случаев так назваемые «емкостные измерители влажности почвы» в реальности тоже измеряют сопротивление почвы, а не ее емкость.** _Among electronic methods for measuring soil moisture, resistance measurements and capacitance measurements are most commonly used. It sounds like a paradox, but in most cases so-called "capacitive soil moisture meters" measure soil resistance rather than soil capacitance._

**Эквивалентная схема участка почвы, на котором производится измерение, состоит из параллельно включенных резистора Rsoil и конденсатора Csoil. Резистор Rsoil имеет сопротивление от сотен ом до сотен килоом, в зависимости от влажности почвы и ее солености/кислотности и т.п. Емкость конденсатора Csoil зависит от площади электродов, расстояния между ними, а также от влажности почвы. Конденсатор Csoil в эквивалентной схеме обычно имеет емкость единицы-десятки пикофарад, когда электроды находятся в воздухе. Если опустить их в воду, емкость увеличивается в несколько раз, так как диэлектрическая проницаемость воды в 80 раз больше, чем диэлектрическая проницаемость воздуха.** _Soil can be represented by a resistor Rsoil and a capacitor Csoil connected in parallel. Resistance Rsoil is in the range from hundreds Оhms to hundreds kОhms, depending on soil moisture and its salinity / acidity, etc. Capacitance Csoil depends on electrodes area, the distance between them, as well as on amount of water in soil. Usually capacitance Csoil is few pF when the electrodes are in air. In water capacitance increases few times, since the dielectric constant of water is 80 times greater than the dielectric constant of air._

Чаще всего любительские «емкостные» измерители влажности сделаны примерно так, как показано на Fig.1

![Figure 1](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_1.png)

Figure 1

Эквивалентная схема датчика состоит из емкости связи Ccpl и, собственно, почвы Rsoil, Csoil. Генератор на базе микроконтроллера выдает прямоугольный сигнал возбуждения частотой несколько десятков или сотен kHz. Резистор R1 соединен с датчиком и образует с ним делитель сигнала. Результирующий сигнал  снимается квазипиковым детектором D1,C1,R2 и  измеряется при помощи ADC, встроенного в тот же микроконтроллер. 

Для уверенной работы такой схемы емкость связи Ccpl должна быть как можно больше,  а частота генератора - как можно выше. Датчик обычно выполняется в виде довольно широкой двухсторонней печатной платы, наружные поверхности которой заняты электродами. Электроды  отделены от почвы  тонким слоем паяльной маски. Такая изоляция мало защищает от коррозии, поэтому датчики служат недолго, зато тонкая изоляция обеспечивает большую емкость связи Ccpl. 

Результаты моделирования этой схемы в Spice при частоте генератора 100 kHz показаны на Fig.2. По горизонтальной оси — время, по вертикальной — напряжение на входе АЦП. Зависимость выходного сигнала от емкости почвы Csoil очень слабая, сигнал в основном зависит от сопротивления почвы Rsoil. То есть, такой способ измерения чувствителен к химическому составу почвы. Кроме того, схема с детектором на обычном кремниевом диоде чувствительна к изменениям температуры.

![Figure 2](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_2.png)

Figure 2

Другая схема «емкостного» измерителя представлена на Fig.3. Она использует генератор на триггере Шмидта. К сожалению, за исключением меньшей чувствительности к изменениям температуры, она обладает такими же недостатками, как и схема Fig.1.

![Figure 3](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_3.png)

Figure 3

Устройство по схеме Fig.3 было собрано на 4-слойной печатной плате размерами 145х10 mm. Электроды расположены на внутренних слоях, толщина диэлектрика между наружными и внутренними слоями 0.25 mm.  Датчик подключен к терминалам W1, W2. В воздухе частота генератора равна 55 kHz, в стакане с водой — 10 kHz.

Из-за относительно большой толщины диэлектрика и малой площади электродов, емкость связи Ccpl мала. Поэтому при прямом контакте с землей зона наибольшей чувствительности датчика приходится на совсем сухую, высокоомную почву. При добавлении в сухой песчаный суглинок всего лишь 0.8% воды (по весу) частота уходит к минимуму и затем почти не меняется. 

Сдвинуть чувствительность датчика в сторону более влажной (и более низкоомной) почвы можно, если уменьшить R1 до 1...10 kOhm. Соответственно, частота на выходе увеличится, а влияние емкости связи уменьшится.

Не меняя R1 улучшить свойства такого датчика удалось после того, как на обе стороны печатной платы был наклеен синтетический войлок толщиной 4 mm. После этого передаточная характеристика получилась такой, как показано на Fig.4

![Figure 4](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_4.png)

Figure 4

С войлоком частота в воздухе уменьшилась до 51.6 kHz, примем это за 100%. Результаты измерений:
  * В сухом песчаном суглинке — частота 98%
  * При добавлении 1% воды (по весу) — 89%
  * 2% воды — 81%
  * 3% воды — 69%
  * 4% воды — 54%
  * 5% воды — 42%
  * 6% воды — 36%
  * 7% воды — 31%
  * 8% воды — 28%

На Fig.5 показаны датчики без войлока и с войлоком. Электроника залита нейтральным силиконом Dow Corning 3140 и защищена прозрачной термоусадочной трубкой поверх заливки. 

![Figure 5](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_5.png)

Figure 5

Для того, чтобы датчик влажности почвы действительно мерял влажность, он должен мерять емкость почвы Csoil невзирая на изменения сопротивления почвы. Очевидно измерения надо производить на таких частотах,  где импеданс Csoil будет существенно меньше, чем  Rsoil. Например,  на частоте 100 MHz импеданс конденсатора 10 pF составляет всего 159 Ohm, поэтому изменения сопротивления почвы от 1 kOhm и выше не будут сильно влиять на результат. 

Такой высокочастотный датчик был проверен, результаты [описаны здесь.](https://github.com/akouz/Soil_moisture/tree/master/Sensor)
