# Библиотека орнаментов

> Готовые SVG-фрагменты. Использовать инлайн, цвет подставлять через `currentColor` или CSS-переменную.  
> Все мотивы — только `stroke`, без `fill` (кроме особо оговорённых).

---

## Орнамент 1 — Розетка-подсолнух

Применение: **разделитель между именами в Hero** (вариант A).  
Принцип: 8 ромбовидных лепестков, построенных через `<use transform="rotate()">` вокруг центра. Центральный круг — двойной контур.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 80 80" width="80" height="80"
     fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round">
  <!-- центральные круги -->
  <circle cx="40" cy="40" r="6"/>
  <circle cx="40" cy="40" r="10"/>
  <!-- 8 лепестков: вытянутый ромб, повёрнутый на 0°, 45°, 90° ... -->
  <g id="petal">
    <polygon points="40,14 43,40 40,30 37,40"/>
  </g>
  <use href="#petal" transform="rotate(45 40 40)"/>
  <use href="#petal" transform="rotate(90 40 40)"/>
  <use href="#petal" transform="rotate(135 40 40)"/>
  <use href="#petal" transform="rotate(180 40 40)"/>
  <use href="#petal" transform="rotate(225 40 40)"/>
  <use href="#petal" transform="rotate(270 40 40)"/>
  <use href="#petal" transform="rotate(315 40 40)"/>
  <!-- внешний ободок -->
  <circle cx="40" cy="40" r="34" stroke-dasharray="3 4"/>
</svg>
```

**Анимация stroke-dashoffset для Hero:**
```css
.sunflower-svg path, .sunflower-svg polygon, .sunflower-svg circle {
  stroke-dasharray: 300;
  stroke-dashoffset: 300;
  animation: draw 1.4s ease-out forwards;
}
.sunflower-svg *:nth-child(2) { animation-delay: 0.1s; }
.sunflower-svg *:nth-child(3) { animation-delay: 0.2s; }
/* и т.д. для каждого дочернего элемента */

@keyframes draw {
  to { stroke-dashoffset: 0; }
}
```

---

## Орнамент 2 — Бегущий бордюр «ромб + крест»

Применение: **горизонтальные разделители** между секциями (оба варианта).  
Принцип: паттерн из чередующихся ромбов `◇` и крестов `+` в `<pattern>`, растянутый на всю ширину.

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="20"
     fill="none" stroke="currentColor" stroke-width="1">
  <defs>
    <pattern id="border-pattern" x="0" y="0" width="40" height="20" patternUnits="userSpaceOnUse">
      <!-- ромб -->
      <polygon points="10,2 18,10 10,18 2,10"/>
      <!-- крест -->
      <line x1="30" y1="4" x2="30" y2="16"/>
      <line x1="24" y1="10" x2="36" y2="10"/>
    </pattern>
  </defs>
  <rect width="100%" height="20" fill="url(#border-pattern)"/>
</svg>
```

Для варианта A: `stroke="var(--rule)"` (#D4C9B0).  
Для варианта B: `stroke="var(--gold-dim)"` (#8A6E30).

---

## Орнамент 3 — Казачья звезда (двойной контур)

Применение: **разделитель между именами в Hero** (вариант B), медленное вращение.  
Принцип: два вложенных квадрата, повёрнутых на 45° друг к другу, образуют восьмиконечную звезду. Внешний квадрат скруглён через `rx`.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64" width="64" height="64"
     fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round">
  <!-- внешний квадрат -->
  <rect x="8" y="8" width="48" height="48" rx="3"/>
  <!-- повёрнутый на 45° — образует звезду при наложении -->
  <rect x="8" y="8" width="48" height="48" rx="3" transform="rotate(45 32 32)"/>
  <!-- центральный круг -->
  <circle cx="32" cy="32" r="5"/>
</svg>
```

**CSS-вращение:**
```css
.star-svg {
  animation: spin 20s linear infinite;
  transform-origin: center;
}
@keyframes spin {
  to { transform: rotate(360deg); }
}
```

---

## Орнамент 4 — Солярный крест

Применение: **иконка в карточке «Церемония»** или декоративный акцент.  
Принцип: круг + 4 диагональных штриха внутри каждого квадранта, имитирующих зерно / солнечные лучи.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48" width="48" height="48"
     fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round">
  <!-- основной круг -->
  <circle cx="24" cy="24" r="20"/>
  <!-- крест-делитель -->
  <line x1="24" y1="4"  x2="24" y2="44"/>
  <line x1="4"  y1="24" x2="44" y2="24"/>
  <!-- штрихи в квадрантах — лучи -->
  <line x1="10" y1="10" x2="16" y2="16"/>
  <line x1="38" y1="10" x2="32" y2="16"/>
  <line x1="10" y1="38" x2="16" y2="32"/>
  <line x1="38" y1="38" x2="32" y2="32"/>
  <!-- малый центральный круг -->
  <circle cx="24" cy="24" r="4"/>
</svg>
```

---

## Орнамент 5 — Плетёный бордюр (тесьма черкески)

Применение: **альтернативный горизонтальный разделитель**, более декоративный, чем орнамент 2.  
Принцип: волнистая линия (синусоида через `<path>`) с ромбами в точках перегиба.

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="24"
     fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round">
  <defs>
    <pattern id="braid" x="0" y="0" width="60" height="24" patternUnits="userSpaceOnUse">
      <!-- волна: одна полуволна 30px → следующая -->
      <path d="M0,12 Q15,2 30,12 Q45,22 60,12"/>
      <!-- ромб в пике волны -->
      <polygon points="30,4 33,12 30,20 27,12"/>
    </pattern>
  </defs>
  <rect width="100%" height="24" fill="url(#braid)"/>
</svg>
```

---