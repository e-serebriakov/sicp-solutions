### Упражнение 1.33.

Можно получить еще более общую версию `accumulate` (упражнение 1.32), если ввести понятие фильтра (`filter`) на комбинируемые термы. То есть комбинировать только те термы, порожденные из значений диапазона, которые удовлетворяют указанному условию. Получающаяся абстракция `filtered-accumulate` получает те же аргументы, что и `accumulate`, плюс дополнительный одноаргументный предикат, который определяет фильтр. Запишите `filtered-accumulate` в виде процедуры. Покажите, как с помощью `filtered-accumulate` выразить следующее:
а. сумму квадратов простых чисел в интервале от `a` до `b` (в предположении, что процедура `prime?` уже написана);
б. произведение всех положительных целых чисел меньше n, которые просты по отношению к `n` (то есть всех таких положительных целых чисел `i < n`, что НОД(`i`, `n`) = 1).


### Решение

```scheme
  (define (filtered-accumulate redicate? combiner null-value term a next b)
    (if (> a b)
      null-value
      (combiner
       (if (predicate? a) (term a) null-value)
       (filtered-accumulate predicate? combiner null-value term (next a) next b))))
```

a.

```scheme
  (define (inc n) (+ n 1))

  (define (sum-of-squares-prime a b)
    (filtered-accumulate prime? + 0 square a inc b))
```

б.

```scheme
  (define (identity x) x)

  (define (mult-n-prime n)
    (define (n-prime? i n)
      (= (gcd i n) 1))
 
    (filtered-accumulate n-prime? * 1 identity 1 inc n))
```