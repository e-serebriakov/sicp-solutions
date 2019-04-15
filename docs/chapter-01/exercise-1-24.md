### Упражнение 1.24.

Модифицируйте процедуру `timed-prime-test` из упражнения 1.22 так, чтобы она использовала `fast-prime`? (метод Ферма) и проверьте каждое из `12` простых чисел, найденных в этом упражнении. Исходя из того, что у теста Ферма порядок роста `Θ(log n)`, то какого соотношения времени Вы бы ожидали между проверкой на простоту поблизости от `1 000 000` и поблизости от `1000`? Подтверждают ли это Ваши данные? Можете ли Вы объяснить наблюдаемое несоот- ветствие, если оно есть?

### Решение

```scheme
  (define (fermat-test n)
    (define (expmod base exp m)
      (cond ((= exp 0) 1)
            ((even? exp)
              (remainder (square (expmod base (/ exp 2) m))
                         m))
            (else
              (remainder (* base (expmod base (- exp 1) m))
                         m))))    

    (define (try-it a)
      (= (expmod a n n) a))

    (try-it (+ 1 (random (- n 1)))))  

  (define (fast-prime? n times)
    (cond ((= times 0) true)
          ((fermat-test n) (fast-prime? n (- times 1)))
          (else false)))     

  (define (timed-prime-test n)
    (newline)
    (display n)
    (start-prime-test n (runtime)))

  (define (start-prime-test n start-time)
    (if (fast-prime? n 1000)
        (report-prime (- (runtime) start-time))))
        
  (define (report-prime elapsed-time)
    (display " *** ")
    (display elapsed-time))   
```

Не смог запустить (`*** ERROR: unbound variable: runtime`) 

[решение из другого источника](http://sicp.sergeykhenkin.com/2007/10/10/sicp-exercise-solution-1-24/)