### Упражнение 1.26.

У Хьюго Дума большие трудности в упражнении 1.24. Процедура `fast-prime?` у него работает медленнее, чем `prime?`. Хьюго просит помощи у своей знакомой Евы Лу Атор. Вместе изучая код Хьюго, они обнаруживают, что тот переписал процедуру `expmod` с явным использованием умножения вместо того, чтобы вызывать `square`:

```scheme
  (define (expmod base exp m)
    (cond ((= exp 0) 1)
          ((even? exp)
           (remainder (* (expmod base (/ exp 2) m)
                         (expmod base (/ exp 2) m))
                      m))
          (else
           (remainder (* base (expmod base (- exp 1) m))
                      m))))
```

Хьюго говорит: «Я не вижу здесь никакой разницы». «Зато я вижу, — отвечает Ева. — Переписав процедуру таким образом, ты превратил процесс порядка `Θ(log n)` в процесс порядка `Θ(n)`». Объясните.

### Решение

*Для оригинального алгоритма*

```scheme
  (define (expmod base exp m)
      (cond ((= exp 0) 1)
            ((even? exp)
              (remainder (square (expmod base (/ exp 2) m))
                         m))
            (else
              (remainder (* base (expmod base (- exp 1) m))
                         m))))    
```

```scheme
  (expmod 3 2 4)
```

```scheme
  (remainder (square (expmod 3 (/ 2 2) 4))
             4)
```

```scheme
  (remainder (square (expmod 3 1 4))
             4)
```

```scheme
  (remainder (square (remainder (* 3 (expmod 3 (- 1 1) 4))
                                4))
             4)
```

```scheme
  (remainder (square (remainder (* 3 (expmod 3 0 4))
                                4))
             4)
```

```scheme
  (remainder (square (remainder (* 3 1)
                                4))
             4)
```

```scheme
  (remainder (square 3)
             4)
```

```scheme
  (remainder 9 4)
```

```scheme
  1
```

*Для алгоритма Хьюго*

```scheme
  (define (expmod base exp m)
    (cond ((= exp 0) 1)
          ((even? exp)
           (remainder (* (expmod base (/ exp 2) m)
                         (expmod base (/ exp 2) m))
                      m))
          (else
           (remainder (* base (expmod base (- exp 1) m))
                      m))))
```

```scheme
  (expmod 3 2 4)
```

```scheme
  (remainder (* (expmod 3 (/ 2 2) 4)
                (expmod 3 (/ 2 2) 4))
             4)
```

```scheme
  (remainder (* (expmod 3 1 4)
                (expmod 3 1 4))
             4)
```

```scheme
  (remainder (* (remainder (* 3 (expmod 3 (- 1 1) 4))
                           4)
                (remainder (* 3 (expmod 3 (- 1 1) 4))
                           4))
             4)
```

```scheme
  (remainder (* (remainder (* 3 (expmod 3 0 4))
                           4)
                (remainder (* 3 (expmod 3 0 4))
                           4))
             4)
```

```scheme
  (remainder (* (remainder (* 3 1)
                           4)
                (remainder (* 3 1)
                           4))
             4)
```

```scheme
  (remainder (* (remainder 3 4)
                (remainder 3 4))
             4)
```

```scheme
  (remainder (* 3 3)
             4)
```

```scheme
  (remainder 9 4)
```

```scheme
  1
```

Для версии алгоритма, предложенной Хьюго, в случае четного показателя степени функция `expmod` рекурсивно вызывает себя дважды на каждом шаге понижения степени, а не единожды. 
`Θ(log(2^n) => Θ(nlog2) => Θ(n)`
