### Упражнение 1.31.

а. Процедура `sum` — всего лишь простейшая из обширного множества подобных абстракций, которые можно выразить через процедуры высших порядков. Напишите аналогичную процедуру под названием `product`, которая вычисляет произведение значений функции в точках на указанном интервале. Покажите, как с помощью этой процедуры определить `factorial`. Кроме того, при помощи `product` вычислите приближенное значение π по формуле

```
  (π/4) = (2/3) * (4/3) * (4/5) * (6/5) * (6/7) * (8/7) * (8/9) * ...
```

б. Если Ваша процедура `product` порождает рекурсивный процесс, перепишите ее так, чтобы она порождала итеративный. Если она порождает итеративный процесс, перепишите ее так, чтобы она порождала рекурсивный.

### Решение

а.

Реализация через рекурсивный процесс

```scheme
  (define (product term a next b)
    (if (> a b)
      1
      (* (term a)
          (product term (next a) next b))))
```

```scheme
  (define (factorial n)
    (define (identity x) x)
    (define (inc x) (+ x 1))

    (product identity 1 inc b))
```

```scheme
  (define (pi-product n)
    (define (inc x) (+ x 1))

    (define (term n)
      (* (/ (* 2 n)
            (- (* 2 n) 1))
        (/ (* 2 n)
            (+ (* 2 n) 1))))

    (4 * (product term 1 inc n)))
```

б. Реализации `product` через рекурсивный и итеративный процессы

Реализация через рекурсивный процесс
```scheme
  (define (product term a next b)
    (if (> a b)
      1
      (* (term a)
          (product term (next a) next b))))
```

Реализация через итеративный процесс
```scheme
  (define (product term a next b)
    (define (iter a result)
      (if (> a b)
        result
        (iter (next a) (* result (term a)))))
        
    (iter a 1))  
```