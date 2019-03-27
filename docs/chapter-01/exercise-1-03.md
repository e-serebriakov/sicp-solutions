### Упражнение 1.3

Определите процедуру, которая принимает в качестве аргументов три числа и возвращает сум- му квадратов двух больших из них.

### Решение

```scheme
(define (sqr a) (* a a))

(define (sumSqr a b) (+ (sqr a) (sqr b)))

(define (sumSqrOfBiggest a b c)
  (cond ((and (> a c) (> b c)) (sumSqr a b))
        ((and (> c a) (> b a)) (sumSqr b c))
        (else (sumSqr a c))))
```