### Упражнение 1.21.

С помощью процедуры `smallest-divisor` найдите наименьший делитель следующих чисел: 199, 1999, 19999.

```scheme
  (define (smallest-divisor n)
    (find-divisor n 2))

  (define (find-divisor n test-divisor)
    (cond ((> (square test-divisor) n) n)
          ((divides? test-divisor n) test-divisor)
          (else (find-divisor n (+ test-divisor 1)))))

  (define (divides? a b)
    (= (remainder b a)
       0))
```

### Решение

```scheme
  (smallest-divisor 199) ; => 199
```

```scheme
  (smallest-divisor 199) ; => 1999
```

```scheme
  (smallest-divisor 199) ; => 7
```