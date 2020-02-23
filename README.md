# Soil moisture meter - измеритель влажности почвы

Среди электронных способов измерения влажности почвы наиболее часто используются измерение сопротивления и измерение емкости.  Звучит парадоксально, но в большинстве случаев так назваемые «емкостные измерители влажности почвы» в реальности тоже измеряют сопротивление почвы, а не ее емкость.

Эквивалентная схема участка почвы, на котором производится измерение, состоит из параллельно включенных резистора и конденсатора. Резистор имеет сопротивление от сотен ом до сотен килоом, в зависимости от влажности почвы и ее солености/кислотности и т.п. Емкость конденсатора зависит от площади электродов, расстояния между ними, а также от влажности почвы. Конденсатор в эквивалентной схеме обычно имеет емкость единицы-десятки пикофарад, когда электроды находятся в воздухе. Если опустить их в воду, емкость увеличивается примерно в 2-3 раза. 

Чаще всего любительские «емкостные» измерители влажности сделаны примерно так, как показано на фиг.1

![Figure 1](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_1.png)

Figure 1

Датчик состоит из емкости связи Ccpl и, собственно, почвы Rsoil, Csoil. Генератор на базе микроконтроллера выдает прямоугольный сигнал возбуждения частотой несколько десятков кГц. Резистор R1 соединен с датчиком и образует делитель сигнала. Результирующий сигнал  снимается квазипиковым детектором D1,C1,R2 и  измеряется при помощи АЦП, встроенного в тот же микроконтроллер. 

Для уверенной работы такой схемы емкость связи Ccpl должна быть как можно больше. Поэтому датчик обычно выполняется в виде довольно широкой двухсторонней печатной платы, наружные поверхности которой заняты электродами. От почвы электроды отделены тонким слоем паяльной маски. Такая изоляция мало защищает от коррозии, датчики служат недолго, зато тонкая изоляция обеспечивает большую емкость связи. 

Результаты моделирования этой схемы в Spice при частоте генератора 100 кГц показаны на фиг.2. По горизонтальной оси — время, по вертикальной — напряжение на входе АЦП. Зависимость выходного сигнала от емкости почвы Csoil очень слабая, сигнал в основном зависит от сопротивления почвы Rsoil.

![Figure 2](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_2.png)

Figure 2

Как видим, такой способ измерения очень чувствителен к химическому составу почвы.

Другая схема «емкостного» измерителя представлена на фиг.3. Она использует генератор на триггере Шмидта. К сожалению, она обладает такими же недостатками, как и схема фиг.1.

![Figure 3](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_3.png)

Figure 3

Датчик и генератор собраны на 4-слойной печатной плате размерами 145х10 мм. Электроды расположены на внутренних слоях, толщина диэлектрика между наружными и внутренними слоями 0.25 мм.  Датчик подключен к терминалам W1, W2. В воздухе частота генератора равна 55 кГц, в стакане с водой — 10 кГц.

Из-за относительно большой толщины диэлектрика и малой площади электродов, емкость связи Ccpl мала. Поэтому при прямом контакте с землей зона наибольшей чувствительности датчика приходится на совсем сухую, высокоомную почву. При добавлении в сухой песчаный суглинок всего лишь 0.8% воды (по весу) частота уходит к минимуму и затем почти не меняется. 

Улучшить свойства датчика удалось после того, как на обе стороны печатной платы был наклеен синтетический войлок толщиной 4 мм. После этого передаточная характеристика получилась такой, как показано на фиг.4

![Figure 4](https://github.com/akouz/Soil_moisture/blob/master/pic/Fig_4.png)

Figure 4

Частота в воздухе уменьшилась до 51.6 кГц, примем это за 100%
  * В сухом песчаном суглинке — частота 98%
  * При добавлении 1% воды (по весу) — 89%
  * 2% воды — 81%
  * 3% воды — 69%
  * 4% воды — 54%
  * 5% воды — 42%
  * 6% воды — 36%
  * 7% воды — 31%
  * 8% воды — 28%
