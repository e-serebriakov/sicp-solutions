### Упражнение 1.7.

Проверка `good-enough?`, которую мы использовали для вычисления квадратных корней, будет довольно неэффективна для поиска квадратных корней от очень маленьких чисел. Кроме того, в настоящих компьютерах арифметические операции почти всегда вычисляются с ограниченной точностью. Поэтому наш тест оказывается неадекватным и для очень больших чисел. Альтернативный подход к реализации `good-enough?` состоит в том, чтобы следить, как от одной итерации к другой изменяется `guess`, и остановиться, когда изменение оказывается небольшой долей значения приближения. Разработайте процедуру вычисления квадратного корня, которая использует такой вариант проверки на завершение. Верно ли, что на больших и маленьких числах она работает лучше?

### Решение

```
  (define (sqrt-iter guess x)
    (if (good-enough? guess x)
        guess
        (sqrt-iter (improve guess x)
                   x)))

  (define (good-enough? guess x)
    (< (abs (- (improve guess x) guess))
       (abs (* guess 0.0001))))

  (define (average x y)
    (/ (+ x y) 2))

  (define (improve guess x)
    (average guess (/ x guess)))

  (define (square x)
    (* x x))

  (define (sqrt x)
    (sqrt-iter 1.0 x))
```