---
layout: default
nav: Days with prices
title: "Days with prices"
description: ""
parent: Examples
nav_order: 5
permalink: /examples/days-with-prices
---

# Days with prices
{: .no_toc }

### Demo

<input id="eg-days-prices" class="form-control demo-wrapper" data-cfg="egdaysprices" style="width: 250px;"/>

### Quick example

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>easepick</title>
    <script src="https://cdn.jsdelivr.net/npm/@easepick/bundle@1.0.0-beta.5/dist/index.umd.min.js"></script>
  </head>
  <body>
    <input id="datepicker"/>
    <script>
      const picker = new easepick.create({
        element: document.getElementById('datepicker'),
        css: [
          'https://cdn.jsdelivr.net/npm/@easepick/bundle@1.0.0-beta.5/dist/index.css',
          'https://easepick.com/assets/css/demo_prices.css',
        ],
        setup(picker) {
          // generate random prices
          const randomInt = (min, max) => {
            return Math.floor(Math.random() * (max - min + 1) + min)
          }
          const prices = {};
          allowedDates.forEach(x => {
            prices[x] = randomInt(50, 200);
          });
          
          // add price to day element
          picker.on('view', (evt) => {
            const { view, date, target } = evt.detail;
            const d = date ? date.format('YYYY-MM-DD') : null;

            if (view === 'CalendarDay' && prices[d]) {
              const span = target.querySelector('.day-price') || document.createElement('span');
              span.className = 'day-price';
              span.innerHTML = `$ ${prices[d]}`;
              target.append(span);
            }
          });
        }
      });
    </script>
  </body>
</html>
```