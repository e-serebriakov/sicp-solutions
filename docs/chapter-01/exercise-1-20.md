### Упражнение 1.20.

Процесс, порождаемый процедурой, разумеется, зависит от того, по каким правилам работает интерпретатор. В качестве примера рассмотрим итеративную процедуру `gcd`, приведенную выше. Предположим, что мы вычисляем эту процедуру с помощью нормального порядка, описанного в разделе 1.1.5. (Правило нормального порядка вычислений для `if` описано в упражнении 1.5.) Используя подстановочную модель для нормального порядка, проиллюстрируйте процесс, порождаемый при вычислении `(gcd 206 40)` и укажите, какие операции вычисления остатка действительно выполняются. Сколько операций `remainder` выполняется на самом деле при вычислении `(gcd 206 40)` в нормальном порядке? При вычислении в аппликативном порядке?

```scheme
  (define (gcd a b)
    (if (= b 0)
        a
        (gcd b (remainder a b))))
```

### Решение

*Нормальный порядок*:

Пусть k - количество выполнении операции `remainder`

k = 0

```scheme
  (gcd 206 40)
```  

```scheme
  (if (= 40 0) 
    206 
    (gcd 40 (remainder 206 40)))
```

```scheme
  (gcd 40 (remainder 206 40))
```

```scheme
  (if (= (remainder 206 40) 0)
    40 
    (gcd (remainder 206 40) (remainder 40 (remainder 206 40))))
```

k = 1

```scheme
  (if (= 6 0)
    206 
    (gcd (remainder 206 40)
         (remainder 40
                    (remainder 206 40))))
```

```scheme
  gcd (remainder 206 40)
      (remainder 40
                 (remainder 206 40))
```

```scheme
  (if (= (remainder 40 (remainder 206 40)) 0)
    (remainder 206 40)
    (gcd (remainder 40 (remainder 206 40))
         (remainder (remainder 206 40)
                    (remainder 40
                               (remainder 206 40)))))
```

k = 3

```scheme
  (if (= 4 0)
    (remainder 206 40)
    (gcd (remainder 40 (remainder 206 40))
         (remainder (remainder 206 40)
                    (remainder 40
                               (remainder 206 40)))))
```

```scheme
  (gcd (remainder 40 (remainder 206 40))
       (remainder (remainder 206 40)
                  (remainder 40
                             (remainder 206 40))))
```

```scheme
  (if (= (remainder (remainder 206 40)
                    (remainder 40
                              (remainder 206 40)))
          0)
    (remainder 40
               (remainder 206 40))
    (gcd (remainder (remainder 206 40)
                    (remainder 40
                               (remainder 206 40)))
         (remainder (remainder 40
                               (remainder 206 40))
                     (remainder (remainder 206 40)
                                (remainder 40
                                           (remainder 206 40))))))
```

k = 7

```scheme
  (if (= 2 0)
    (remainder 40
               (remainder 206 40))
    (gcd (remainder (remainder 206 40)
                    (remainder 40
                               (remainder 206 40)))
         (remainder (remainder 40
                               (remainder 206 40))
                    (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40))))))
```

```scheme
  (gcd (remainder (remainder 206 40)
                  (remainder 40
                             (remainder 206 40)))
       (remainder (remainder 40
                             (remainder 206 40))
                  (remainder (remainder 206 40)
                             (remainder 40
                                        (remainder 206 40)))))
```

```scheme
  (if (= (remainder (remainder 40
                               (remainder 206 40))
                    (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40))))
         0)
    (remainder (remainder 206 40)
               (remainder 40
                          (remainder 206 40)))
    (gcd (remainder (remainder 40
                               (remainder 206 40))
                    (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40))))
         (remainder (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40)))
                    (remainder (remainder 40
                                          (remainder 206 40))
                               (remainder (remainder 206 40)
                                          (remainder 40
                                                     (remainder 206 40)))))))
```

k = 14

```scheme
  (if (= 0 0)
    (remainder (remainder 206 40)
               (remainder 40
                          (remainder 206 40)))
    (gcd (remainder (remainder 40
                               (remainder 206 40))
                    (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40))))
         (remainder (remainder (remainder 206 40)
                               (remainder 40
                                          (remainder 206 40)))
                    (remainder (remainder 40
                                          (remainder 206 40))
                               (remainder (remainder 206 40)
                                          (remainder 40
                                                     (remainder 206 40)))))))
```

```scheme
  (remainder (remainder 206 40)
             (remainder 40
                        (remainder 206 40)))
```

k = 18

```scheme
  2
```

Ответ: процедура `remainder` будет вызвана 18 раз.

*Аппликативный порядок*:

Пусть k - количество выполнении операции `remainder`

k = 0

```scheme
  (gcd 206 40)
```

```scheme
  (if (= 40 0)
    206
    (gcd 40 (remainder 206 40)))
```

```scheme
  (gcd 40 (remainder 206 40))
```

k = 1

```scheme
  (gcd 40 6)
```

```scheme
  (if (= 6 0)
    40
    (gcd 6 (remainder 40 6)))
```

```
  (gcd 6 (remainder 40 6))
```

k = 2

```scheme
  (gcd 6 4)
```

```scheme
  (if (= 4 0)
    6
    (gcd 4 (remainder 6 4)))
```

```scheme
  (gcd 4 (remainder 6 4))
```

k = 3

```scheme
  (gcd 4 2)
```

```scheme
  (if (= 2 0)
    4
    (gcd 2 (remainder 4 2)))
```

```scheme
  (gcd 2 (remainder 4 2))
```

k = 4

```scheme
  (gcd 2 0)
```

```scheme
  (if (= 0 0)
    2
    (gcd 0 (remainder 2 0)))
```

```scheme
  2
```

Ответ: процедура `remainder` будет вызвана 4 раза.
