### Упражнение 1.8.

Метод Ньютона для кубических корней основан на том, что если y является приближением к кубическому корню из x, то мы можем получить лучшее приближение по формуле

```
  ( x / (y ^ y) + 2 * y) / 3
```

С помощью этой формулы напишите процедуру вычисления кубического корня, подобную про- цедуре для квадратного корня. (В разделе 1.3.4 мы увидим, что можно реализовать общий метод Ньютона как абстракцию этих процедур для квадратного и кубического корня.)

### Решение 

```scheme
  (define (cube-root-iter guess x)
    (if (good-enough? guess x)
        guess
        (cube-root-iter (improve guess x)
                  x)))

  (define (good-enough? guess x)
    (< (abs (- (improve guess x) guess))
       (abs (* guess 0.0001))))

  (define (average x y)
    (/ (+ x y) 2))

  (define (improve guess x)
    (average guess (/ (+ (/ x (square guess)) (* 2 guess)) 3)))

  (define (square x)
    (* x x))

  (define (cube-root x)
    (cube-root-iter 1.0 x))
```