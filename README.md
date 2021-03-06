# Требования к psd-макетам

*Сверстать можно почти всё. "Накостылить" - вообще всё. Но всегда нужно помнить о таких вещах как бюджет и сроки. И никогда не забывать о том, что верстка будет интегрироваться в какую-то систему на этапе программирования. Данные требования ни в коем случае не несут цели подавить фантазию дизайнера, но предлагают некоторые рамки, работа в которых позволит сделать верстку максимально быстрой и качественной. И положительно скажутся на дальнейшей разработке и развитии проекта. Всегда есть место компромису, всегда можно чуть-чуть подвинуться, "стерпеть" отход от общей сетки в отдельном блоке. Но все компромисы должны быть оправданы, а не являться следствием лени или некомпетентности.*

### Содержание:

1. [Общие требования](#Общие-требования)
2. [Модульность](#Модульность)
3. [Модульня сетка](#Модульня-сетка)
4. [Адаптивный дизайн](#Адаптивный-дизайн)
5. [Retina, графика, иконки и иконочные шрифты](#retina-графика-иконки-и-иконочные-шрифты)
6. [Шрифты](#Шрифты)
7. [Контент](#Контент)
8. [Статьи и видео по теме](#Статьи-и-видео-по-теме)


### Общие требования

Название файлов и слоёв писать по-английски или транслитом. К названиям файлов добавлять приставки, позволяющие легко определить актуальную версию. Например, `file-1.psd` или `file-final.psd`.

Макет должен иметь тот размер, в котором его нужно сверстать.

Цветовой профиль - `sRGB`. Обязательно и критично. Иначе цвета в вёрстке могут отличаться от макетных.

Единицы измерения - пиксели (в том числе и для текста).

Между объектами (например иконка и карта) допустим только режим наложения `normal`. Внутри объектов, которые предполагается экспортировать целиком (например баннер) - все что угодно.

Не использовать корректирующие слои. Любые «пост-модификации» могут всерьёз осложнить работу верстальщика.

Соблюдать порядок в слоях и папках в макете. Обозначать скрытые слои (например цветом слоя), писать комментарии ко всем неочевидным моментам, описывать анимации.

Все отдельные элементы должны быть на разных слоях. Если макетов несколько, в любом из них должен быть полный набор всех элементов. например, header не должен быть вставленным картинкой или смарт-объектом.

При передаче макетов в архиве использовать `.zip` формат.


### Модульность

На каждом из этапов (дизайн, верстка, программирование) сайт должен собираться из типовых элементов. Именно модульный дизайн обеспечивает легкость дальнейшей разработки и облегчает поддержку и развитие сайта.

Необходимо сделать отдельный макет с набором типовых элементов и стилей (цветовая палитра, стили текста, кнопки, ссылки, отступы, типовые блоки и т.д.) и все остальные макеты собирать из этих элементов.

Не следует плодить лишние сущности (цвета, стили текста, блоки), когда можно обойтись теми, что уже есть.


### Модульня сетка

Обязательно использовать модульную сетку для расположения элементов.
Идеальный вариант сетки 12 колонок (делится на 2, 3, 4 и 6). Так же иногда используются 16 и 24.
Отход от стандартной сетки допустим, например, на сложных промо-страницах или для отдельных элементов, но в целом это скорее исключение.

Важно понимать, как работает сетка для верстальщика.

Самый популярный подход к сетке на сегодняшний день предлагает [Bootstrap](http://getbootstrap.com/css/#grid).
Его суть заключается в том, что задается общее количество колонок, а размеры элементов, указываются в колонках.

Например, если мы используем 12-колоночный вариант и хотим задать ширину элемента в 50% ширины сайта, то зададим ему ширину 6 колонок.

Колонки можно вкладывать в другие колонки, но здесь кроется важная деталь - вложенная сетка имеет столько же колонок.
Например, на странице есть элемент шириной 6 колонок (половина страницы если используем 12).
Внутри него - 2 элемента, визуально и в соответствие с направляющими, шириной в 3 колонки каждый.
На самом же деле, внутри у нас так же 12 колонок, соответственно вложенные элементы должны иметь ширину 6 колонок каждый, что и будет соответствовать 3 колонкам.

![Grid](https://raw.githubusercontent.com/andrey-hohlov/psd-templates-requirements/master/assets/grid.png)

Проблема возникает с элементами, шириной например 7 колонок, внутри которых 2 элемента - 3 и 4 колонки шириной. Нельзя, используя сетку, если у нас адаптивный / резиновый макет, разделить этот блок, чтобы получить элементы такой ширины.

![Grid problem](https://raw.githubusercontent.com/andrey-hohlov/psd-templates-requirements/master/assets/grid-problem.png)

Это не является серьезной проблемой, и может быть решено несколькоими способами. Однако, если изначально стоит задача сделать дизайн под конкретную модульную сетку ("дизайн под bootstrap") - следует быть внимательными с такими моментами.


Старайтесь изначально определить количество колонок и расстояние между колонками (gutter) и использовать их для всех размеров экрана. Если верстальщик пользуется не готовыми сетками, а использует инструменты для их генерации (scss-исходники bootstrap 4, susy и т.д. ), становится возможным задавать разное количество колонок и расстояние между ними для разных размеров экрана.
Однако, это усложняет как процесс верстки так и дальнейшую поддержку такого кода и является потенциальным источником ошибок.

Будет очень хорошо, если сетка представлена не направляющими, а отдельным полу-прозрачным слоем, [например](https://raw.githubusercontent.com/hagatorn/bootstrap3-grid-template/master/bootstrap%20md%20970px.png). Направляющие могут использоваться дизайнером не только для построения основной сетки, но и для каких-то отдельных элементов, что иногда путает при верстке.

[Полное руководство по сеткам в веб дизайне](http://deadsign.ru/design/grids_in_web_design/)

### Адаптивный дизайн :iphone::computer:

При создании макетов, особенно адаптивных, следует понимать процесс верстки и технические ограничения. Пройдите базовый курс верстки или посоветуйтесь с верстальщиком при создании макета.

В идеале использовать подход `mobile first`.

На сегодняшний день актуальные разрешения экранов для адаптивного сайта:

* 320px (смартфон, в том числе iPhone до 6 включительно)
* 768px (планшет в портретной ориентации)
* 1024 (планшет в альбомной ориентации, ноутбук)

[Почему iPhone указан с шириной 320px при разрешении экрана 750 × 1334 у iPhone 6](http://www.paintcodeapp.com/news/ultimate-guide-to-iphone-resolutions)

[Настоящие размеры viewport у разных мобильных устройств](http://viewportsizes.com/)

Поддержка остальных разрешений зависит от проекта. Так, например, нет смысла делать блог, в котором преобладает текстовый контент, шириной больше чем 1024. А вот интернет-магазин вполне можно сделать под бОльшие размеры экрана.

Основные разрешения экранов: 1280, 1366, 1440, 1680, 1920. Очевидно что не имеет смысла делать разные макеты для 1280 и 1366.

Важно понимать, что при разрешении экрана 1024px по ширине контент должен быть меньше (~960-980px), так как из ширины придется вычесть полосу прокрутки (17px в среднем) и, возможно, рамки окна.

Как правило, не обязательно делать макеты всех страниц под все разрешения, в некоторых случаях достаточно будет описания, например: *"На экранах 1200px+ добавляется ещё один столбец товаров в каталоге"*


### Retina, графика, иконки и иконочные шрифты

Все что можно сделать векторным (в том числе и иллюстрации) - должно быть векторным. Векторные элементы лучше передать отдельными файлами.

Все иконки без сложных эффектов (градиенты, тени) должны быть векторными и без проблем эскпортироваться в svg. Такие иконки следует рисовать шейпами в Photoshop или в Illustrator, вставляя в макет так же шейпами (shape). Вставленные смарт-объектами иконки приходится по отдельности открывать в Illustrator и сохранять оттуда, что замедляет работу.

Выравнивайте точки в кривых по пиксельной сетке если возможно. Тогда иконки не будут мыльными на экранах с низким разрешением, к тому же будут лучше сжиматься. В редакторах настройка обычно называется «snap to pixel».

Артборд должен быть подогнан по габаритам фигуры. Для нескольких иконок одинакового размера допустимо, чтобы атрборды были одинаковых размеров (больше габарита фигур).

Всё, что может быть слито в единую форму, должно быть слито.

Избегайте наложения эффектов и трансформаций.

Избегайте градиентов и теней. В некоторых случаях это может наложить ограничения на использование векторной графики.

Не комбинируйте в макете слои со вставленной векторной графикой с элементами, нарисованными в макете. Если Вы вставили в макет векторную картинку и потом «дополнили» её какими-то слоями макета, использовать такую картинку без растеризации в вёрстке не получится

Если ипользуются иконки с [icomoon.io](http://icomoon.io), [flaticon.com](http://flaticon.com) и подобных сервисов и вы скачиваете их оттуда в виде архива с SVG-файлами, приложите используемые к макету.

Не накладывайте на векторные изображения в PSD-макетах корректирующие слои, маски, эффекты. Это приведёт к невозможности использования такой векторной графики.

Все элементы интерфейса со сложными эффектами, которые будут экспортироваться в растре, должны быть в 2-кратном размере (тогда весь макет рисуется в 2-кратном размере) либо без потери качества ресайзиться.

Контентные элементы (фото, баннеры и т.д.) готовятся под ретину по согласованию с заказчиком и разработчиком. При поддержке retina-экранов и для контента весь макет рисуется в 2-кратном размере.

Не стоит использовать иконочные шрифты из-за проблем с кросс-платформенностью и возможных дефектов отрисовки. Статьи по теме:

1. https://css-tricks.com/svg-sprites-use-better-icon-fonts/
2. https://css-tricks.com/svg-symbol-good-choice-icons/


### Шрифты

Приоритет использования:

1. [Системные шрифты](http://www.cssfontstack.com/)
2. Шрифты с [Google Fonts](https://www.google.com/fonts/)
3. Бесплатные шрифты, имеющие web-версию
4. Платные приобретенные шрифты, имеющие web-версию
4. Бесплатные шрифты, не имеющие web-версии
5. Платные приобретенные шрифты, не имеющие web-версии
6. Платные не приобретенные

Веб-версия шрифта включает в себя форматы `.eot`, `woff`, `woff2` (опционально), `ttf`, `svg` (опционально).

Существует множество конвертеров шрифтов для использования на сайте, однако ни один из них не дает 100% качества: разная высота символов, несоответствие высоты строки в браузере, "рваные" символы, отдельные символы не отображаются.

Не стоит использовать шрифты, имеющие лицензионные ограничения (т.е. которые для использования следует купить), не покупая их.
Если заказчик настаивает - следует предупредить о нарушении лицензии. Вероятность привлечения к ответственности очень мала, но это как минимум не этично. И именно с такими шрифтами больше проблем при их конвертации.

Не рекомендуется использовать на сайте более 2 шрифтов и 3 начертаний (`regular`, `semibold`, `bold`) в каждом. Каждое начертание каждого семейства увеличивает время загрузки страницы.

Используемые шрифты приложить к макету (файлы, или ссылки).

В макете кегль шрифта задавать целым числом.

В Photoshop можно деформировать текстовый блок, например - вытянуть по вертикали, сжать по горизонтали. В верстке скорее всего это будет невозможно.

В web нет кроссбраузерных переносов. Лучше не использовать переносы слов вообще. Расстановка символов мягкого переноса в тексте возможна, но делать это вручную никто не будет.

### Контент

Для всех активных элементов (ссылки, кнопки, инпуты) помимо обычного, должны быть нарисованы состояния:

* Для ссылок: `hover` и `active`, иногда требуется `visited`
* Для кнопок `hover`, `active`, `disabled`
* Для текстовых инпутов: `focus` и `disabled`
* Для чекбоксов и радио-кнопок: `checked` и `disabled`

Если предполагаются текстовые страницы, должен быть макет со всеми типовыми элементами:

* Заголовки H1-H6
* Параграфы
* Нумерованные и маркированные списки
* Таблицы
* Медиа (изображения, галереи, файлы для скачивания) в зависимости от задач
* Цитата (blockquote) опционально
* и т.д.

Если предполагаются формы, должны быть нарисованы основные элементы:

* Input Text
* Textarea
* Checkbox
* Radiobutton
* Select

А также сама форма и лейблы к полям.

По возможности следует избегать стилизации нестандартных элементов. Например, `select` стилизовать средствами css нельзя, приходится подключать скрипт, который заменяет его другой конструкцией. Если на сайте select используется только в 1 месте и для выбора пола пользователя, разумнее будет заменить его на 2 радио.

Текст-рыбу использовать на языке сайта. [Генератор для русского языка](http://fishtext.ru/index.php).

Не помещать в 1 текстовый блок 2 разных стиля, если это возможно. Например, если идет заголовок (красный, 60px), а за ним текст (черный, 18px) - это должны быть 2 разных блока, нажав на каждый из которых верстальщик сможет сразу увидеть используемый стиль.

Не набирать текстовые блоки КАПСОМ, использовать «All Caps».

Не использовать прозрачность, чтобы добиться цвета (например прозрачность для черного текста, чтобы он выглядел серым).

Ели используется фон из бесшовной текстуры - нужно приложить её отдельно.

Все элементы должны быть подготовлены и обрезаны таким образом, чтобы исключить ситуации, когда, например, при экспорте треугольника из макета получается ромб (потому, что верхнюю его половину просто прикрывал другой слой.


### Статьи и видео по теме:
* [Правила хорошего тона в «Фотошопе»](http://i-love-psd.ru/)
* [Памятка дизайнеру сайтов](http://habrahabr.ru/post/50497/)
* [8 простых способов улучшить типографику в вашем дизайне](http://habrahabr.ru/post/56625/)
* [Designing for web](https://github.com/KyreenaH/Designing-for-Web)
* [О чём должен помнить веб-дизайнер](https://github.com/nicothin/web-design)
* [О чём смеются верстальщики | Вадим Макеев | Дизайн-форум Prosmotr](https://www.youtube.com/watch?v=lW4uzJp6uIg)
* [Дизайнь как верстальщик](https://habrahabr.ru/post/311800/)

