## Предисловие

Данный текст - перевод статьи Madhavan Nagarajan "An Introduction to CSS Pre-Processors: SASS, LESS and Stylus".

Оригинал доступен по [ссылке](https://medium.com/@itIsMadhavan/an-introduction-to-css-pre-processors-sass-less-and-stylus-1f45178ff5ba "An Introduction to CSS Pre-Processors: SASS, LESS and Stylus"). 
Прочитавших, просьба поддержать [автора](https://medium.com/@itIsMadhavan "Madhavan Nagarajan
"). Также рекомендую прочитать его другие статьи (уже на английском языке).

# Введение в препроцессоры CSS: SASS, LESS and Stylus.

Препроцессоры CSS уже годы помогают нам в разработке. Когда они только появились, у них было всего несколько дополнительных возможностей.
Но сейчас они занимают ключевое место в разработке и имеют массу очень полезных инструментов для работы с CSS.
Препроцессоры расширяют возможности CSS благодаря переменным, операторам, интерполяции, функциям, миксинам и множеству других полезных полезных функций.
Одни из наиболее известных препроцессоров: SASS, LESS и Stylus.
На момент публикации статьи, актуальная версия SASS - 3.3.5, LESS - 1.7.0, Stylus - 0.43.1.

## Для чего использовать препроцессоры CSS?

CSS очень примитивен и даёт мало возможностей.
Создание функции, переиспользование значений свойств или наследование достигается нелёгким путём.
Из-за этого поддержка и обслуживание больших проектов или сложных систем - большая проблема.
С другой стороны, WEB эволюционирует. Новые спецификации создаются как для HTML, так и для CSS.
Но каждый браузер понимает эти спецификации только со специальным вендорным префиксом.
В некоторых случаях (например, установка градиента на задний фон) написание всех вендорных префиксов превращается в пытку.
Вам необходимо написать все вендорные префиксы, чтобы их поддерживали разные браузеры, всего лишь чтобы добиться одного результата.

Для того, чтобы было удобнее писать код CSS, применялись различные практики, такие как разделение определений на маленькие файлы и импортирование их в один главный файл.
Этот подход помогал с разделением кода на компоненты, но это не решало проблем повторения правил и возможности поддержки такого кода.
Другой подход заключался в введении объектно-ориентированного CSS.
В данном случае применяли два или более класса к одному элементу.
Каждый класс добавляет один типовой стиль для элемента.
Использование нескольких классов увеличило возможность их повторного использования, но снизило удобство обслуживания.

Препроцессоры с их дополнительными возможностями помогают написать переиспользуемый, легко-поддерживаемый и расширяемый код CSS. 
Используя препроцессор, вы можете легко повысить свою производительность и уменьшить объем кода, который вы пишете в проекте.

## Узнаём особенности

Как и любые другие языки программирования, препроцессоры имеют разный синтаксис, но к счастью, схожий друг на друга.
Каждый из них поддерживает классическое написание CSS и их синтаксис очень похож на обычный CSS. SASS и Stylus имеют дополнительные стили.
В SASS вы можете избегать круглых скобок и точек с запятой, в то время как в Stylus вы можете не использовать ещё и двоеточие.
Они необязательны как в SASS, так и Stylus.

В примерах ниже вы встретите написание на SASS, LESS и Stylus и как они это преобразуют в CSS.
Это лишь примеры использования их функций.
Для более детальных примеров смотрите официальную документацию каждого препроцессора.

## Переменные

Переменные - одна из самых желанных функций в CSS за всё время.
Каждый разработчик хочет определить основной цвет и использовать его во всём файле CSS, не писав каждый раз HEX-код в значении свойства.
Точно так же, как переменные нужны для цветов, они необходимы и для задание значений “width”, “font-size”, “font-family”, “borders” и тому подобного.

Переменные в SASS объявляются знаком $, в LESS - знаком @, а в Stylus префикс не нужен.
В SASS и LESS значения следуют после двоеточия (:), а в Stylus - после знака равно (=).

*SASS:*

    $font-size: 16px;

    div {
      font-size: $font-size;
    }


*LESS:*

    @font-size: 16px;

    div {
      font-size: @font-size;
    }

*Stylus:*

    font-size = 16px

    div
      font-size font-size

*Вывод в CSS:*

```css
div {
  font-size: 16px;
}
```

## Вложенность

В CSS отсутствует визуальная иерархия при работе с дочерними селекторами. Вы должны задавать стили селекторам и их комбинациям отдельно.
Вложенность помогает видеть иерархию (прямо как в HTML) и это заметно повышает читаемость кода. В некоторых случаях вложенность перегружает селекторы и получается что-то вроде "поезда селекторов", поэтому пользуйтесь ей с умом.

*SASS:*

    $link-color: #999;
    $link-hover: #229ed3;
    
    ul {
      margin: 0;
      
      li {
        float: left;
      }
      
      a {
        color: $link-color;
        
        &:hover {
            color: $link-hover;
        }
      }
    }


*LESS:*

    @link-color: #999;
    @link-hover: #229ed3;
    
    ul {
      margin: 0;
      
      li {
        float: left;
      }
      
      a {
        color: @link-color;
        
        &:hover {
            color: @link-hover;
        }
      }
    }

*Stylus:*

    link-color = #999
    link-hover = #229ed3
    
    ul
      margin 0
      
      li
        float left
        
      a
        color link-color
        
        &:hover
          color link-hover

*Вывод в CSS:*

```css
ul { margin: 0; }
ul li { float: left; }
ul a { color: #999; }
ul a:hover { color: #229ed3; }
```

## Миксины

Миксины - это набор свойств, которые компилируется в соответствии с переданными им параметрами или статическими правилами. С помощью них можно с лёгкостью создавать кроссбраузерные градиенты для заднего фона, стрелки-CSS и т.п.


*SASS:*

    @mixin bordered($width) {
      border: $width solid #ddd;
        
      &:hover {
        border-color: #999;
      }
    }
    
    h1 {
      @include bordered(5px);
    }

*LESS:*

    .bordered (@width) {
      border: @width solid #ddd;
        
      &:hover {
        border-color: #999;
      }
    }
    
    h1 {
      .bordered(5px);
    }

*Stylus:*

    bordered(w)
      border: n solid #ddd
      
      &:hover
        border-color: #999
            
    h1
      bordered(5px)

*Вывод в CSS:*

```css
h1 { border: 5px solid #ddd; }
h1:hover { border-color: #999; }
```

## Расширения

Расширения применяются для объединения общих правил для селекторов, вместо того, чтобы копировать их всем. Все селекторы с расширениями сгруппированы в скомпилированном CSS-файле. SASS расширяет каждый экземпляр расширенного селектора, который включает его дочерние селекторы и унаследованные свойства. Однако в LESS можно выбрать каждый экземпляр расширяемого селектора, добавив атрибут «all» для метода расширения, или же можно выбрать только основной экземпляр.

*SASS:*

    .block { margin: 10px 5px; }
    
    p {
      @extend .block;
      border: 1px solid #eee;
    }
    
    ul, ol {
      @extend .block;
      color: #333;
      text-transform: uppercase;
    }

*LESS:*

    .block { margin: 10px 5px; }
    
    p {
      &:extend(.block);
      border: 1px solid #eee;
    }
    
    ul, ol {
      &:extend(.block);
      color: #333;
      text-transform: uppercase;
    }

*Stylus:*

    .block
      margin 10px 5px
        
    p
      @extend .block
      border 1px solid #eee
        
    ul
    ol
      @extend .block
      color #333
      text-transform uppercase
        
*Вывод в CSS:*

```css        
.block, p, ul, ol { margin: 10px 5px; }
p { border: 1px solid #eee; }
ul, ol { color: #333; text-transform: uppercase; }
```


## Операции с цветами

Все три препроцессора имеют функции для работы с цветами. Вы можете изменить яркость или насыщенность исходного цвета, вы даже можете смешивать 2 и более разных цвета. Эта особенность не такая существенная, но неплохо иметь её ввиду.

*SASS:*

    saturate($color, $amount)
    desaturate($color, $amount)
    lighten($color, $amount)
    darken($color, $amount)
    adjust-hue($color, $amount)
    opacify($color, $amount)
    transparentize($color, $amount)
    mix($color1, $color2[, $amount])
    grayscale($color)
    complement($color)

*LESS:*

    saturate(@color, @amount)
    desaturate(@color, @amount)
    lighten(@color, @amount)
    darken(@color, @amount)
    fadein(@color, @amount)
    fadeout(@color, @amount)
    fade(@color, @amount)
    spin(@color, @amount)
    mix(@color1, @color2, @weight)
    grayscale(@color)
    contrast(@color)

*Stylus:*

    red(color)
    green(color)
    blue(color)
    alpha(color)
    dark(color)
    light(color)
    hue(color)
    saturation(color)
    lightness(color)


## Выражения if/else

Управляющие директивы и выражения помогают создавать аналогичные определения стиля в соответствии с согласованными условиями или переменными. SASS и Stylus поддерживают обычные условные выражения if / else. В LESS это достигается с помощью CSS Guards.

*SASS:*

    @if lightness($color) > 30% {
        background-color: black;
    }
    @else {
        background-color: white;
    }
    
*LESS:*
    
    .mixin (@color) when (lightness(@color) > 30%) {
        background-color: black;
    }
    .mixin (@color) when (lightness(@color) =<; 30%) {
        background-color: white;
    }
    
*Stylus:*
    
    if lightness(color) > 30%
        background-color black
    else
        background-color white
        
## Циклы

Циклы полезны, когда мы делаем проход по массиву или создаём серию повторяющихся стилей (например, задание ширины у гридов). Как и в случае с выражением if/else, LESS использует CSS Guard и рекурсивные миксины для циклов.

*SASS:*

    @for $i from 1px to 3px {
        .border-#{i} {
            border: $i solid blue;
        }
    }

*LESS:*

    .loop(@counter) when (@counter > 0){
        .loop((@counter - 1));
        .border-@{counter} {
            border: 1px * @counter solid blue;
        }
    }

*Stylus:*

    for num in (1..3)
        .border-{num}
            border 1px * num solid blue

## Математические операции

Математические операции могут быть использованы для обычных арифметических операций или конверции единиц измерений. SASS и Stylus поддерживают арифметические операции между разными единицами измерения. В дополнении к простым математическим операциям, препроцессоры поддерживают и сложные, такие как округление, нахождение максимального и минимального значений и т.п.

*SASS:*

    1cm * 1em => 1 cm * em
    2in * 3in => 6 in * in
    (1cm / 1em) * 4em => 4cm
    2in + 3cm + 2pc => 3.514in
    3in / 2in => 1.5

*LESS:*

    1cm * 1em => 1cm * 1em
    2in * 3in => 6in
    (1cm / 1em) * 4em => 4cm
    2in + 3cm + 2pc => 3.514in
    3in / 2in => 1.5in

*Stylus:*

    1cm * 1em => 1 cm * em
    2in * 3in => 6in
    (1cm / 1em) * 4em => 4cm
    2in + 3cm + 2pc => 5.181in
    3in / 2in => 1.5in

## Импорт

Вместо того, чтобы использовать один большой файл, разделение своего кода на небольшие части повышает удобство обслуживания и контроль всей кодовой базы. Вы можете группировать похожие части кода в общие папки и импортировать их в главный CSS файл. Также с помощью импорта могут быть добавлены фреймворки.

*SASS:*

    @import "library";
    @import "mixins/mixin.scss";
    @import "reset.css";

*LESS:*

    @import "library"
    @import "mixins/mixin.less"
    @import "reset.css"

*Stylus:*

    @import "library"
    @import "mixins/mixin.styl"
    @import "reset.css

## Заключение

Все три препроцессора, описанные здесь, имеют более-менее похожий функционал. Просто выберите для себя тот, который больше всего подходит вашему стилю кода и используйте его уже в вашем следующем проекте.
