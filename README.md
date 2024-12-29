# QUERYNOMICON

## Введение в SQL для осторожных и утомленных <!-- {docsify-ignore} -->

> Всем привет!
> Предлагаем вашему вниманию адаптацию на русский язык учебного материала по SQL, созданного Грегом Уилсоном (Greg Wilson), автором книг [Software Design by Example in Python](https://third-bit.com/sdxpy/), [Software Design by Example in JavaScript](https://third-bit.com/sdxjs/) и других замечательных книг.
> Сейчас Грег работает над проектом [Dash](https://dash.plotly.com/dash-core-components/graph) - визуализация данных в Python. Мы, в свою очередь, в рамках [лицензии](https://lessonomicon.github.io/querynomicon/license.html), представляем эту работу русскоязычной аудитории.
> Надеемся, что этот учебный материал поможет вам изучить SQL в кратчайшие сроки.

### От автора

Впервые столкнувшись с SQL после двух десятилетий использования Fortran, C, Java и Python, я подумал, что попал в ад. Я быстро понял, что это был оптимистичный настрой: в конце концов, в аду есть правила.

С тех пор я понял, что SQL тоже, и что они не более запутаны и противоречивы, чем языки большинства других языков программирования. Они кажутся таковыми только потому, что опираются на традицию, незнакомую тем из нас, кто вырос на производных от C. Цитируя Терри Пратчетта, это не безумие, просто по-другому разумное.

Итак, добро пожаловать в мир, в котором странное станет знакомым, а знакомое — странным. Добро пожаловать, трижды добро пожаловать в SQL.

- Пожалуйста, посетите [сайт](https://lessonomicon.github.io/querynomicon/), чтобы просмотреть оригинальную версию этого руководства.

- [Загрузите базы данных SQLite, используемые в этих примерах.](https://github.com/lessonomicon/querynomicon/raw/main/querynomicon.zip)

- Мы будем рады любому вашему вкладу! Пожалуйста, ознакомьтесь с [руководством для участников](https://lessonomicon.github.io/querynomicon/contributing.html) для получения общей информации, также просим вас ознакомиться с нашей [лицензией](https://lessonomicon.github.io/querynomicon/license.html), определяющей условия использования, и принять во внимание, что все участники обязаны соблюдать наш [Кодекс поведения](https://lessonomicon.github.io/querynomicon/code_of_conduct.html).

#### Благодарности

Этот учебник не был бы возможен без:
- Модуля sqlparse Энди Альбрехта
- "The Art of PostgreSQL" Димитрия Фонтена
- "The Essence of SQL" Давида Розенштейна (сейчас, к сожалению, не издается)

Я также хотел бы поблагодарить следующих людей за обнаружение проблем, предложения или внесение изменений:

Янина Беллини Сайбене, Филлип Клауд, Зои Дэниелс, Конор Флинн, Энди Голдберг, Джей Грейвс, Сэм Хеймс, Адам Хокс, Роберт Керн, Константинос Китсиос, Оливье Лерой, Кевин Маршалл, Рой Парди, Манос Питсидианакис, Даниэль Поссенриде, Адам Розиен, Томас Зандманн, Саймон Уиллисон

### От авторов перевода

Мы также будем вашему посильному вкладу в перевод этого проекта! Пожалуйста, ознакомьтесь с нашим [руководством для участников](/resources/contributors.md) для получения общей информации и с [этими задачами](https://github.com/vndv/querynomicon/issues), где ваша помощь будет особенно ценна. Также просим принять во внимание, что все участники обязаны соблюдать [Кодекс поведения](/resources/code_of_conduit.md).

---

В этом руководстве приводятся заметки и рабочие примеры, которые инструкторы могут использовать в качестве отправной точки. Мы не ожидаем, что новички, не имеющие опыта работы с SQL, смогут научиться этому самостоятельно. Если провести музыкальную аналогию, эти ноты представляют собой смену аккордов и мелодию; мы ожидаем, что преподаватели создадут аранжировку и/или импровизируют над материалом при его доставке. Дополнительную информацию смотри на сайте [Teaching Tech Together](https://teachtogether.tech/).      

---

<center>Начните там, где вы находитесь.</center>
<center>Используйте то, что у вас есть.</center>
<center>Делайте то, что можете.</center>