

## Методы создания графиков

В предыдущих главах было описано, как пользоваться мощными возможностями создания визуальных сценариев в Dynamo. Понимание этих возможностей является основой и первым шагом к созданию надежных визуальных программ. При работе с визуальными программами в полевых условиях, обмене ими с коллегами, устранении неполадок или проверке ограничений приходится сталкиваться и с другими проблемами. Если программа рассчитана на другого пользователя или предполагается открыть ее только через полгода, она должна обладать абсолютно понятной графикой и логикой. В Dynamo есть множество инструментов для работы со сложными программами. В этой главе приводятся рекомендации по их своевременному использованию.

![группы](images/13-2/cad-chart-visual.jpg)

### Упрощение

По мере разработки графика Dynamo и проверки различных идей он увеличивается в размере и становится сложнее. Несомненно, очень важно создать работающую программу, однако столь же важно сделать ее максимально простой. Благодаря этому работа графика будет более быстрой и предсказуемой, а пользователи вместе с разработчиком смогут понять его логику по прошествии времени. Ниже представлены варианты того, как можно упорядочить логику графиков.

#### Модульная организация за счет групп

* Благодаря группам можно **создавать функционально автономные части** при разработке программы.
* Группы позволяют **перемещать крупные части программы**, соблюдая при этом модульность и выравнивание.
* Можно менять **цвета групп, чтобы различать** их предназначение (входные данные или функции).
* С помощью групп можно **структурировать график таким образом, чтобы упростить создание пользовательских узлов**.

![группы](images/13-2/groups.png)

> Цвета в этой программе обозначают назначение каждой группы. Этот метод может использоваться для создания иерархии в любых разрабатываемых графических стандартах или шаблонах.

> 1. Группа функций (синий)
2. Группа входных данных (оранжевый)
3. Группа сценариев (зеленый)
> Сведения об использовании групп см. в разделе [Управление программой](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html).

#### Эффективная разработка с помощью блоков кода

* Иногда с помощью блока кода можно **быстрее ввести число или метод узла, чем при поиске** (Point.ByCoordinates, Number, String, Formula).

* Блоки кода можно использовать **для настройки пользовательских функций в DesignScript, уменьшающих количество узлов в графике**.

![блок кода](images/13-2/codeblock.png)

> Примеры 1 и 2 выполняют одну и ту же функцию. Получилось значительно быстрее написать несколько строк кода, чем прибегать к функции поиска и добавлять каждый узел по отдельности. Кроме того, блок кода значительно меньше по объему.

> 1. Сценарий DesignScript, написанный с помощью блока кода
2. Аналогичная программа с использованием узлов
> Сведения об использовании блоков кода см. в разделе [Определение блока кода](http://primer.dynamobim.org/en/07_Code-Block/7-1_what-is-a-code-block.html).

#### Сжатие узла в код

* **Сложность графика можно уменьшить с помощью преобразования узла в код (Node to Code)**. При этом для набора простых узлов будет создан соответствующий сценарий DesignScript, состоящий из одного блока кода.
* Функция Node to Code позволяет **сжать код, не усложнив восприятие программы**.
* Далее перечислены **преимущества** использования функции Node to Code.
* Простое сжатие кода в один редактируемый компонент.
* Упрощение значительной части графика.
* Удобство применения к мини-программам, которые редко редактируются.
* Возможность встраивания других типов блоков кода, таких как функции.

* Ниже представлены **недостатки** использования функции Node to Code.
* Типовые имена ухудшают удобочитаемость.
* Сложность восприятия для других пользователей.
* Нет простого способа вернуться к визуальной версии программы.

![nodetocode](images/13-2/nodetocode.png)

> 1. Существующая программа
2. Блок кода, созданный с помощью функции Node to Code
> Сведения об использовании функции Node to Code см. в разделе [Синтаксис DesignScript](http://primer.dynamobim.org/en/07_Code-Block/7-2_Design-Script-syntax.html).

#### Гибкий доступ к данным с помощью функции List@Level

* С помощью функции List@Level можно **упростить график, заменив узлы List.Map и List.Combine**, которые могут занимать значительное место рабочей области.
* При построении логики узла List@Level работает **быстрее, чем List.Map/List.Combine**, так как предоставляет доступ к данным любого уровня в списке непосредственно с входного порта узла.

![listatlevel](images/13-2/listatlevel.png)

> Активировав функцию List@Level для входных данных списка CountTrue, можно проверить, сколько истинных значений и в каких списках возвращает функция BoundingBox.Contains. List@Level позволяет определить, с какого уровня данные будут подаваться на ввод. Работа с List@Level отличается гибкостью, эффективностью и более предпочтительна по сравнению с другими методами, где используются функции List.Map и List.Combine.

> 1. Подсчет истинных значений на 2 уровне списка.
2. Подсчет истинных значений на 3 уровне списка.
> Сведения о работе с функцией List@Level см. в разделе [Списки списков](http://primer.dynamobim.org/en/06_Designing-with-Lists/6-3_lists-of-lists.html#list@level).

### Обеспечение наглядности

Помимо простоты и эффективности графиков, необходимо позаботится об их максимальной наглядности. Несмотря на все усилия по созданию интуитивного графика за счет логических группировок, взаимосвязи могут быть видны недостаточно хорошо. Лишних поисков и неопределенности можно избежать благодаря простому примечанию внутри группы или переименованному регулятору. Описанные ниже способы помогут обеспечить визуальное единообразие в одном или нескольких графиках.

#### Достижение визуальной целостности посредством выравнивания узлов

* Чтобы уменьшить количество доработок после построения графика, попытайтесь сделать компоновку узлов удобочитаемой, **периодически выравнивая их**.
* Если с графиком будут работать другие пользователи, **убедитесь, что компоновка проводов и узлов имеет четкую логику**.
* Для упрощения выравнивания **используйте функцию «Очистить компоновку узла», чтобы автоматически выровнять** график (однако в таком случае точность будет меньше, чем при выравнивании вручную).

![выравнивание](images/13-2/alignment.png)

> 1. Неупорядоченный график
2. Выровненный график
> Сведения об использовании функции выравнивания узлов см. в разделе [Управление программой](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html).

#### Использование описательных меток при переименовании

* Переименование входных данных сделает график более понятным другим пользователям, **особенно если требуется подсоединиться к узлу, который не будет виден на экране**.
* **При переименовании любых узлов, кроме узлов входных данных, будьте максимально осторожны.** Можно также создать пользовательский узел из кластера узлов и переименовать его: при этом будет понятно, что в нем содержится нечто другое.

![входные данные](images/13-2/inputs.png)

> 1. Входные данные для управления поверхностью
2. Входные данные архитектурных параметров
3. Входные данные в сценарии моделирования водоспуска
> Чтобы переименовать узел, щелкните его имя правой кнопкой мыши и выберите «Переименовать узел...».

#### Разъяснения в примечаниях

* Примечание добавляется, если для какой-либо части **графика требуется пояснение на простом языке**, которое не может быть выражено с помощью узла.
* Примечание добавляется, если набор **узлов или группа имеют слишком большой размер, сложную структуру или логику**.

![примечания](images/13-2/notes.png)

> 1. Примечание, описывающее часть программы, которая возвращает примерные расстояния переноса.
2. Примечание, описывающее код, который сопоставляет эти значения с синусоидальной волной.
> Сведения о том, как добавить примечание, см. в разделе [Управление программой](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html).

### Зондирование на всех этапах работы

При создании визуального сценария важно убедиться в том, что возвращаемые результаты соответствуют ожидаемым. Не все ошибки или проблемы ведут к немедленному сбою в работе программы. Особенно это касается нулевых значений, которые могут повлиять на работу значительно позже. Этот метод также применяется к текстовым сценариям. См. раздел [Методы создания сценариев](http://primer.dynamobim.org/en/12_Best-Practice/13-2_Scripting-Strategies.html). Следующие рекомендации помогут получить ожидаемые результаты.

#### Мониторинг данных с помощью марок наблюдения (Watch) и предварительного просмотра (Preview)

* При создании программы используйте марки Watch и Preview, чтобы **убедиться в правильности ключевых выходных данных**.

![watch](images/13-2/watch.png)

> Узлы Watch используются для сравнения следующих данных:

> 1. примерные расстояния переноса;
2. значения, проходящие через уравнение синусоиды.
> Инструкции по использованию узла Watch см. в разделе [Библиотека](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-2_dynamo_libraries.html).

### Повторное использование

Весьма вероятно, что рано или поздно вашу программу откроет другой пользователь, даже если вы работаете самостоятельно. На основе входных и выходных данных этому пользователю нужно будет быстро понять, что требуется для работы программы и каковы результаты этой работы. Это особенно важно при разработке пользовательских узлов, которые будут применяться сообществом Dynamo и добавляться в программы других разработчиков. Следующие рекомендации помогут создавать надежные, многократно используемые программы и узлы.

#### Управление вводом/выводом

* Чтобы обеспечить удобочитаемость и масштабируемость, попробуйте **минимизировать входные и выходные данные**.
* Перед тем, как добавить первый узел в рабочую область, необходимо **определить метод построения логики, создав примерный план** ее действия. При создании примерного плана отслеживайте, какие входные и выходные данные войдут в сценарии.

#### Использование наборов параметров при добавлении входных значений

* При наличии **определенных вариантов или условий, которые требуется включить в график**, для быстрого доступа к ним следует использовать наборы параметров.
* Наборы параметров можно также использовать для **уменьшения сложности путем кэширования определенных значений регулятора** на графике с длительным временем выполнения.

> Сведения об использовании наборов параметров см. в разделе [Управление данными с помощью наборов параметров](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-5_presets.html).

#### Упаковка программ с пользовательскими узлами в контейнеры

* Пользовательский узел применяется, если **можно объединить программу в одном контейнере**.
* Еще пользовательский узел применяется, если **часть графика будет повторно использоваться ** в других программах.
* И, наконец, пользовательский узел применяется, если **необходимо сделать функцию доступной сообществу Dynamo**.

![пользовательский узел](images/13-2/customnode.png)

> Если собрать программу преобразования точек в пользовательский узел, получится более надежная и оригинальная переносная программа, в которой легко разобраться. Правильно обозначенные порты ввода помогут другим пользователям понять, как применять узел. Не забудьте добавить описания и требуемые типы данных для каждого входного элемента.

> 1. Существующая программа точки притяжения
2. Пользовательский узел для размещения программы, PointGrid
> Сведения о работе с пользовательскими узлами см. в разделе [Введение в пользовательские узлы](http://primer.dynamobim.org/en/09_Custom-Nodes/9-1_Introduction.html).

#### Создание шаблонов

* Шаблоны используются в качестве **визуальных стандартов, чтобы обеспечить общий подход к построению графиков среди пользователей, осуществляющих совместную работу**.
* При создании шаблона можно стандартизировать **цвета и размеры шрифтов группы**, чтобы отнести типы рабочих процессов или операции с данными к определенным категориям.
* При создании шаблона можно даже стандартизировать **метки, цвета или стили для обозначения различий между внешними и внутренними рабочими процессами** на графике.

![](images/13-2/templating.jpg)

> 1. Пользовательский интерфейс (внешняя часть программы). Включает в себя имя проекта, регуляторы ввода и импортируемую геометрию.
2. Внутренняя часть программы.
3. Цветовые категории групп (проект в целом, входные данные, сценарии на языке Python, импортированная геометрия).

### Упражнение «Архитектурная крыша»

> Скачайте файл примера, прилагаемый к этому упражнению (щелкните правой кнопкой мыши и выберите «Сохранить ссылку как...»). Полный список файлов примеров можно найти в приложении. [RoofDrainageSim.zip](datasets/13-2/RoofDrainageSim.zip)

Ознакомившись с некоторыми практическими советами, попробуйте применить их к быстро составленной программе. Несмотря на то, что программа успешно создает крышу, график отражает «поток сознания» автора. Отсутствует какая-либо структура и руководство по использованию. Применив практические советы по организации, описанию и анализу программы, мы поможем понять другим пользователям, как ее использовать.

![поток сознания](images/13-2/1.jpg)

> Программа работает, но график не структурирован.

Начните с определения данных и геометрии, возвращаемых программой.

![данные](images/13-2/1-1.JPG)

> Чтобы создать логические разделы или модули, очень важно понимать, когда данные подвергаются наибольшим изменениям. Перед переходом к следующему шагу попробуйте проверить остальную часть программы с помощью узлов Watch, чтобы убедиться в возможности определить группы.

> 1. Этот блок кода с математическим уравнением выглядит как ключевая часть программы. Узел Watch указывает, что он возвращает списки расстояний переноса.
2. Назначение этой области не очевидно. Расположение истинных значений на уровне списка L2 из BoundingBox.Contains и наличие List.FilterByBoolMask говорит о том, что это выборка части из сетки точек.

Разобравшись в компонентах программы, разделите их на группы.

![группы](images/13-2/1-2.jpg)

> Группы позволяют визуально дифференцировать компоненты программы.

> 1. Импорт 3D-модели площадки
2. Преобразование сетки точек на основе уравнения синусоиды
3. Выборка части из сетки точек
4. Создание поверхности архитектурной крыши
5. Создание стеклянного витража

После определения групп выровняйте узлы, чтобы обеспечить визуальную целостность графика.

![выравнивание](images/13-2/2.jpg)

> Визуальная целостность позволяет видеть ход выполнения программы и скрытые взаимосвязи между узлами.

Сделайте программу более понятной, добавив еще один слой улучшений графического интерфейса. Добавьте примечания, чтобы пояснить, как работает та или иная часть программы, укажите пользовательские имена входных данных и назначьте цвета различным типам групп.

![примечания, переименование](images/13-2/2-2.jpg)

> Благодаря этим улучшениям графического интерфейса пользователи лучше поймут назначение этой программы. Различные цвета групп позволяют отличать входные данные от функций.

> 1. Примечания
2. Входные данные с описательными именами

Перед тем как приступить к сжатию программы, определим предполагаемое место вставки сценария Python для моделирования водоспуска. Разместите выходные данные первой масштабированной поверхности крыши в соответствующих входных данных сценария.

![интеграция сценариев](images/13-2/3.jpg)

> Сценарий встраивается в эту часть программы, чтобы можно было запустить моделирование водоспуска на одной исходной поверхности крыши. Данная поверхность не отображается в области предварительного просмотра, но при этом не нужно выбирать верхнюю поверхность на сложной поверхности с фаской.

> 1. Исходная геометрия для входных данных сценария
2. Узел Python
3. Регуляторы ввода
4. Переключатель вкл./откл.

Упростите график, чтобы расставить все по местам.

![пользовательский узел, Node to Code](images/13-2/3-2.jpg)

> Сжатие программы с помощью функций Node to Code и Custom Node привело к значительному уменьшению размера графика. Группы, отвечающие за создание поверхности крыши и стен, преобразованы в код, так как характерны только для данной программы. Группа преобразования точек содержится в пользовательском узле, так как ее можно использовать в другой программе. Создайте в файле примера собственный пользовательский узел из группы преобразования точек.

> 1. Пользовательский узел для размещения группы «преобразование сетки точек»
2. Функция Node to Code для сжатия групп «Создание поверхности архитектурной крыши и виража»

В завершение создайте наборы параметров для образцов формы крыши.

![наборы параметров](images/13-2/3-3.jpg)

> Эти входные данные в существенной мере определяют форму крыши и помогут пользователям увидеть возможности программы.

Программа, где видны два набора параметров.

![наборы параметров](images/13-2/3-4.jpg)

![наборы параметров](images/13-2/3-5.jpg)

> Аналитический вид наборов параметров, соответствующих образцам водостока крыши.
