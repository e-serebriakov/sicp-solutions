### Упражнение 1.22.

Большая часть реализаций Лиспа содержат элементарную процедуру `runtime`, которая возвращает целое число, показывающее, как долго работала система (например, в миллисекундах). Следующая процедура `timed-prime-test`, будучи вызвана с целым числом `n`, печатает `n` и проверяет, простое ли оно. Если `n` простое, процедура печатает три звездочки и количество времени, затраченное на проверку.

```scheme
  (define (timed-prime-test n)
    (newline)
    (display n)
    (start-prime-test n (runtime)))

  (define (start-prime-test n start-time)
    (if (prime? n)
        (report-prime (- (runtime) start-time))))
        
  (define (report-prime elapsed-time)
    (display " *** ")
    (display elapsed-time))
```

Используя эту процедуру, напишите процедуру `search-for-primes`, которая проверяет на простоту все нечетные числа в заданном диапазоне. С помощью этой процедуры найдите наименьшие три простых числа после `1000`; после `10 000`; после `100 000`; после `1 000 000`. Посмотрите, сколько времени затрачивается на каждое простое число. Поскольку алгоритм проверки имеет
порядок роста `Θ(√n)`, Вам следовало бы ожидать, что проверка на простоту чисел, близких к `10 000`, занимает в `√10` раз больше времени, чем для чисел, близких к `1000`. Подтверждают ли это Ваши замеры времени? Хорошо ли поддерживают предсказание `√n` данные для `100 000` и `1 000 000?` Совместим ли Ваш результат с предположением, что программы на Вашей машине затрачивают на выполнение задач время, пропорциональное числу шагов?

### Решение

```scheme
  (define (search-for-primes number-from prime-count) 
    (if (and (> prime-count 0) (timed-prime-test number-from))
      (search-for-primes (+ number-from 1) (- prime-count 1)) 
      (search-for-primes (+ number-from 1) prime-count)))
```

Не смог запустить (`*** ERROR: unbound variable: runtime`)

[решение из другого источника](http://sicp.sergeykhenkin.com/2007/10/10/sicp-exercise-solution-1-22/)