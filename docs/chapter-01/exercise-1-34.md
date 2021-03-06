### Упражнение 1.34.

Допустим, мы определили процедуру

```scheme
  (define (f g)
    (g 2))
```

```scheme
  (f square) ; => 4
```

```scheme
  (f (lambda (z) (* z (+ z 1)))) ; => 6
```


Что случится, если мы (извращенно) попросим интерпретатор вычислить комбинацию `(f f)`? Объясните.


### Решение.

Процедура `f` вызывает другую процедуру, переданную в качестве аргумента, с аргументом 2.
При вычислении `(f f)` произойдет следующий вызов `(f 2)`. Получается, что в определенный момент 
будет вызвано `(2 2)`, где первая двойка выступает в качестве оператора, что приведет к ошибке. 