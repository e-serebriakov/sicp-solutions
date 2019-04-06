### Упражнение 1.12

Приведенная ниже таблица называется треугольником Паскаля (Pascal’s triangle).

```
        1
      1   1
    1   2   1 
  1   3   3   1
```

Все числа по краям треугольника равны 1, а каждое число внутри треугольника равно сумме двух чисел над ним. Напишите процедуру, вычисляющую элементы треугольника Паскаля с помощью рекурсивного процесса.

### Решение

```scheme
  (define (pascal-triangle r c)
    (cond ((or (= r 0) (= c 0)) 0)
          ((or (< r 0) (< c 0) (< r c)) 0)
          ((or (= c 1) (= r c)) 1)
          (else (+ (pascal-triangle (- r 1) (- c 1))
                   (pascal-triangle (- r 1) c)))))

```