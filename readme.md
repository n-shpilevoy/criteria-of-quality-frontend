# Критерии хорошей верстки

Обязательные и необязательные критерии оценки вёрстки.


## 1. Разметка


### 1.1. Соблюден код-гайд

TODO: Добавить ссылку на код-гайд.


### 1.2. Разметка проходит валидацию на [validator.w3.org/nu](https://validator.w3.org/nu/)

Проверяются все сверстанные страницы.

Проверке подвергается и логическая структура документа (флаг `Show Outline` при проверке). Допустим «безымянный» блок для `<nav>`.


### 1.3. Отсутствуют грубые ошибки

Примеры грубых ошибок: ссылки не являются ссылками, `<br><br>` вместо параграфов.

Примеры негрубых (условно-допустимых) ошибок: `<div>` вместо `<section>`, `<header>` или `<article>`, отсутствие списка в одноуровневой навигации.


### 1.4. Страница работоспособна без картинок, стилей и скриптов

Страница без стилей и скриптов, будучи открыта в браузере, выглядит логично и работает, а именно:

- видна чёткая иерархия блоков (заголовки),
- важные для восприятия контента страницы изображения вставлены тегом `img`,
- оформительские картинки вставлены через CSS (SVG-иконки можно вставлять c помощью `<svg>`),
- ссылки, представленные в дизайне иконками, имеют человекопонятные текстовые узлы (текст скрывается стилями),
- не видны элементы, ненужные или не работающие без стилей и скриптов (пример: бургер главного меню),
- интерактивные элементы (ссылки, в т.ч. якорные, формы) видны и работоспособны,
- «кнопки», клики на которых открывают поп-апы, являются ссылками, ведущими к блокам с поп-апами (якоря) или ссылками на другие страницы,
- интерактивная карта при отключенном JS показывается в виде статической картинки.

**Исключение:** страницы, работоспособность которых невозможна без стилей/скриптов.


### 1.5. Использована методология БЭМ, отсутствуют типовые ошибки

CSS-классы, использованные в разметке, написаны по БЭМ ([Описание методологии](https://ru.bem.info/methodology/quick-start/)). Предпочтительным является использование [диалекта Two Dashes](https://ru.bem.info/methodology/naming-convention/#Стиль-two-dashes) (`__` как разделитель для элемента и `--` как разделитель для модификатора).

Типовые ошибки:

- повторение разделителя более одного раза в одном классе: `block__element__element` или `block--modifier--modifier`,
- класс-модификатор без класса, который он модифицирует: `<div class="block--modifier">` или `<div class="btn  toggler--red">`,
- упоминание внешнего вида блока или элемента в классах, не являющихся модификаторами,
- избыточные сокращения в именах классов (допустимые: `img`, `descr`, `btn`, `wrap`, `xs`, `sm`, `md`, `lg`, `xl`),
- наличие классов-хелперов, наподобие `right`, `text-center`.


### 1.6. Использован правильный вьюпорт-тег

Для адаптивных сайтов: `<meta name="viewport" content="width=device-width,initial-scale=1">`

Для неадаптивных сайтов: `<meta name="viewport" content="width=1000">` (число — контентная ширина макета).


### 1.7. Отсутствуют закомментированные блоки

**Исключения:** особые состояния блоков (пример: блок авторизации для авторизованного посетителя).


### 1.8. Для контентных изображений прописаны атрибуты размеров


### 1.9. Для ссылок прописаны правильные протоколы

Для ссылок на адрес электропочты — `mailto:`, для телефонов — `tel:`, для skype — `skype:`.


### 1.10. Для `<input>` использованы правильные типы

`email`, `tel`, `date` и подобные.


### 1.11. Если у `<input>` есть текстовое название, оно указано в привязанном `<label>`

```
<label class="field-text">
  <span class="field-text__name">Название поля </span>
  <input class="field-text__input" type="text" value="" placeholder="Образец заполнения">
</label>
<!-- или -->
<div class="field-text">
  <label for="input-id" class="field-text__name">Название поля </label>
  <input id="input-id" class="field-text__input" type="text" value="" placeholder="Образец заполнения">
</div>
```


### 1.12. Табличные данные представлены в `<table>`

**Исключение:** некоторые адаптивные таблицы.


## 2. Стилизация


### 2.1. Соблюден код-гайд

TODO: Добавить ссылку на код-гайд.


### 2.2. Отклонения от макета минимальны

На прорисованных ширинах вертикальные отклонения не должны превышать 10px (но не более 5%). Горизонтальные отклонения не должны превышать 5px.

**Исключение:** ширины блоков, формирующих раскладку блоков на странице должны точно совпадать с макетом.

Недопустимы отклонения по параметрам текста, цветам, контентным изображениям.

### 2.3. Шрифты заданы правильно

При указании названия шрифта в `font-family` должны быть указаны альтернативные семейства и тип семейства.


### 2.4. Отсутствуют «CSS-заплатки»

В стилях не должно быть `!important` (как быстрая правка проблемы вместо устранения причины проблемы).

**Исключение:** сокрытие или показ блоков с `!important` не являются «CSS-заплатками».

На `<body>` или иных общих обёртках страницы не должно быть `overflow[-x||-y]: hidden;` (как быстрая правка проблемы с горизонтальным скроллом страницы).


### 2.5. Фрагменты страницы выдерживают переполнение и недополнение

Простые фрагменты верстки должны выдерживать переполнение текстом (увеличение габаритов и/или сокрытие части длинного текста). При этом внутри кнопок или ячеек таблицы текст не должен начинать касаться краёв.

Фрагменты, содержащие потоковые блоки (пример: блок каталога товаров, содержащий поток вложенных блоков с товарами), должны выдерживать переполнение и недополнение потоковыми блоками.

Вставка в разметку контентных изображений с размерами, отличающимися от представленных в макете, не должно ломать страницу.


### 2.6. Использован подход mobile-first

При стилизации компонентов страницы, сначала написана стилизация под мобильные устройства, затем дописаны стили для широких вьюпортов. **Исключение:** фрагменты страницы, имеющие сильные отличия на широких вьюпортах.


### 2.7. Для стилизации не использованы `id`


### 2.8. Для фрагментов с изображением в фоне явно прописан фоновый цвет


### 2.9. Отступы между блоками сделаны свойствами соседствующих блоков, а не выступающими `margin`-ами вложенных блоков


### 2.10. Для раскладки блоков на странице не использованы стилизованный `<table>` и `position: absolute;`

**Исключение:** `position: absolute;` можно использовать для отдельных непереполняемых блоков (пример: бургер меню в мобильной версии).


### 2.11. Изменение размеров textarea не ломает вёрстку


### 2.12. Контентные изображения не должны работать как «распорки»

```
img {
  max-width:100%;
  height:auto;
}
```


### 2.13. У отдельных блоков не фиксированы размеры

Для любых блоков (кроме блоков, служащих для раскладки на странице) не должно быть жесткой фиксации ширины и высоты (могут быть заданы минимальные размеры).


### 2.14. В коде отсутствуют неиспользуемые в разметке селекторы

**Исключение:** стилизация фрагментов страницы, видимых не сразу или не всем (пример: стили для авторизованного посетителя).


## 3. CSS-процессинг


### 3.1. Стилевые файлы разделены поблочно

Один бэм-блок = один препроцессорный файл. Пример: внутри файла `promo.less` должна быть только стилизация бэм-блока `promo`.

Допустимы несколько глобальных стилевых файлов: диспетчер подключений, переменные, глобальные стили.


### 3.2. При вложении селекторов нет вложений глубже 3-го уровня

Псевдоселекторы и `@media` не считаются увеличивающими уровень вложенности.

```
.promo {
  display: block;

  &__link {         // первый уровень вложенности

    &:hover {       // не увеличивает уровень вложенности

      span {...}    // второй уровень вложенности
    }

    strong {...}   // второй уровень вложенности
  }

  @media (min-width: 600px) { // не увеличивает уровень вложенности
    display: none;
  }
}
```


### 3.3. `@media` написаны в контексте селекторов

`@media` не считаются увеличивающими вложенность.

```
// файл promo.scss
.promo {
  display: block;

  @media (min-width: $screen-md) {...} // правильно, написано в контексте
}

@media (min-width: $screen-md) {       // неправильно, написано вне контекста
  .promo {...}
}
```


### 3.4. Все переменные описаны в одном файле. В переменные вынесены, как минимум: breakpoints, главные размеры текста, главные шрифтовые группы

```
$font-size:                   1.6rem;
$font-size--h1:               3rem;
$font-size--h2:               2.4rem;

$line-height:                 1.375;

$font-family:                 Roboto, 'Helvetica Neue', Arial, sans-serif;
$font-family--headings:       Georgia, 'Times New Roman', Times, serif;

$screen-sm:                   600px;
$screen-md:                   900px;
$screen-lg:                   1200px;
$screen-xl:                   1800px;
```


### 3.5. Амперсанд использован правильно

Амперсанд допустимо использовать перед:

- разделителем БЭМ-элемента,
- разделителем БЭМ-модификатора,
- псевдоэлементом или псевдоселектором.

```
.promo {

  // Правильно: амперсанд перед псевдоклассом
  &:hover { ... }

  // Правильно: амперсанд перед разделителем элемента
  &__item {

    // НЕПРАВИЛЬНО: амперсанд в месте разделения словосочетания в названии элемента
    &-link { ... }
  }

  // НЕПРАВИЛЬНО: амперсанд в месте разделения словосочетания в названии блока
  &-shover { ... }

  // Правильно: модификаторы нужно писать под элементами
  &--large { ... }

}
```


### 3.6. Использован простпроцессинг

Стили должны обрабатываться, как минимум, Autoprefixer-ом и конкатенатором медиа-выражений.


### 3.7. Примеси не используются для генерации правил с вендорными префиксами


### 3.8. Не используются `extend`


## 4. Дополнительные файлы


### 4.1. Выбраны подходящие форматы для изображений

Если возможно использовать векторную графику — SVG (см. критерий про векторную графику). Нужно изображение с полупрозрачными пикселами — PNG. Нужно фото и допустимы небольшие искажения в угоду малому «весу» — JPEG.


### 4.2. Шрифты подключены в нужных форматах

Необходимые форматы: `woff`, `woff2`.


### 4.3. Растровые изображения оптимизированы

Растровые изображения должны быть оптимизированы, но не иметь видимых отличий от макета.


### 4.4. Векторные изображения не содержат растра

Внутри используемых SVG не должно встречаться растровых изображений.

**Исключение:** использование SVG для каких-либо сложных эффектов на растровых изображениях.


## 5. Оптимизация


### 5.1. Минимум подключенных файлов

К странице должны быть подключены 1 CSS-файл и не более 3 синхронно подгружаемых JS-файлов.

CSS-файл должен быть подключен в секции `<head>`. JS-файлы должны быть подключены перед `</body>`.


### 5.2. Мелкие растровые иконки и декоративные изображения сшиты в компактный спрайт

Отдельные изображения должны быть представлены в папке с исходниками.


## 6. Автоматизация


### 6.1. Все зависимости проекта устанавливаются командой `npm i` или `yarn install` и не хранятся в репозитории проекта

Зависимости прописаны, как минимум, в `package.json`, папки зависимостей (`node_modules`, `bower_components`) добавлены в `.gitignore`.


### 6.2. В репозитории есть `readme.md` с описанием того, как стартовать проект локально и описанием дополнительных команд (если есть)

Выполнение инструкции должно позволять вести разработку проекта вне зависимости от операционной системы и установленных в системе пакетов.

Должен быть представлен список доступных команд. Пример: команда `npm run deploy` — выгрузка содержимого папки `build` на GH-pages.


### 6.3. При старте автоматизации отсутствуют необязательные ресурсоёмкие задачи

Пример: оптимизация растровых изображений должна происходить по отдельной команде, а не при любом старте локального сервера.


### 6.4. Результат сборки проекта не хранится в репозитории

Результат компиляции/транспиляции не должен присутствовать в репозитории проекта. **Исключение:** использование GH-pages, наличие собранного проекта в ветке `gh-pages`.


## 7. Разное


### 7.1. В именах файлов нет пробелов, транслита, все символы строчные, использован английский язык


### 7.2. Главное меню должно быть видимо при выключенном JS

При выключенном JS главные навигационные элементы (меню, поиск) должны быть видимы, а элементы для их сокрытия (бургер, крестик) должны быть скрыты.


### 7.3. Верстка имеет минимальные отличия в IE11 и последних 2-х версиях Chrome, Firefox, Opera и Safari

Допустимы отличия, связанные с рендером шрифтов и использованием нативных элементов форм (флажки, радиокнопки и т.п.).

Допустимы различия в вертикальных размерах до 10px, но не более 5%.


### 7.4. В именах классов нет транслита, использован английский язык


### 7.5. Использованные фреймворки для верстки (Bootstrap и подобные) установлены как зависимости проекта

NPM- или yarn-зависимости. Ошибкой считается копирование всех файлов фреймворка в папку исходников и хранение их в репозитории.


### 7.6. Сделано базовое типографическое оформление

- Заданы общие стиль для контентного текста.
- Прописаны стили для тегов всех заголовков, для параграфов, списков, цитат.


### 7.7. Логотип — ссылка на главную страницу

На главной странице — `<div>`. Должен выдерживать смену тега на `<h1>`.


### 7.8. Главное содержимое страницы должно идти в разметке до второстепенного

См. критерий про логичность страницы в состоянии без стилей, картинок и скриптов.



## Необязательные критерии


### Контроль включенного JS (если нужно)

В разметке страниц использовано что-то вроде:

```
<html lang="ru" class="no-js">
...
<script>
  // Маркер работающего javascript
  document.documentElement.className = document.documentElement.className.replace('no-js', 'js');
</script>
```


### Спорные текстовые элементы могут быть представлены любым тегом

Если в отношении фрагмента страницы сложно определить является ли он заголовком (или сложно понять уровень заголовка), у этого фрагмента должен быть класс со стилизацией, позволяющей использовать любой подходящий блочный тег (`<div>`, `<h[1-6]>`).


### Текстовые фрагменты, выводимые из CMS, не должны иметь классов на тегах

Текстовой фрагмент, предположительно появляющийся из CMS целиком, не должен иметь CSS-классов на тегах, но должен иметь обертку с CSS-классом.

Пример: текст записи в блоге.

Антипример: главная навигация (из CMS выводится текстовые узлы пунктов, но не разметка целиком).


### Контроль загрузки шрифтов

При первой загрузке страницы сознательно выбран FOIT/FOUT/FOFT, при второй и далее минимизирована заметность выбранного подхода.


### В автоматизации предусмотрена команда «чистовой» сборки проекта

Выполнение команды приводит к сборке бьютифицированной разметки, минимизированных стилей/скриптов без карт кода.


### Минимум тегов без текста

Допустим пустой тег для добавления бургера/крестика сокрытия главного меню в мобильной версии, пустые теги для добавления иконок.


### Ретинизация растровой графики

Если представленные в макете слои позволяют, растровая графика должны быть адаптирована для retina-экранов.


### Отступы между блоками сделаны однообратно: «вниз по потоку»

Стоит выбирать отступ в сторону условного окончания потока: если блоки располагаются сверху вниз, слева направо, то внешние отступы следует делать вниз и вправо.


### Интерлиньяж указан в относительных единицах


### Векторные изображения, использованные в иконках, собраны в спрайт по принципу `symbol > use`
