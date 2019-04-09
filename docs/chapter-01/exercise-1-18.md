### Упражнение 1.18.

Используя результаты упражнений 1.16 и 1.17, разработайте процедуру, которая порождает итеративный процесс для умножения двух чисел с помощью сложения, удвоения и деления пополам, и затрачивает логарифмическое число шагов

### Решение

```scheme
  (define (fast-mult k l)
    (define (even? n)
      (= (remainder n 2) 0))      

    (define (double n) (* n 2)) 
    (define (halve n) (/ n 2)) 

    (define (mult-iter a b product)
      (cond ((= b 0) product)
            ((even? b) (mult-iter (double a) (halve b) product)) 
            (else (mult-iter a (- b 1) (+ product a)))))
    
    (mult-iter k l 0)) 

  (fast-mult 2 3)
  ; (mult-iter 2 3 0)
  ; (mult-iter 2 (- 3 1) (+ 0 2))
  ; (mult-iter 2 2 2)
  ; (mult-iter (double 2) (halve 2) 2)
  ; (mult-iter 4 1 2)
  ; (mult-iter 4 (- 1 1) (+ 2 4))
  ; (mult-iter 4 0 6)
  ; 6
```