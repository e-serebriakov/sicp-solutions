### Упражнения 1.32.

а. Покажите, что `sum` и `product` (упражнение 1.31) являются частными случаями еще более общего понятия, называемого накопление (accumulation), которое комбинирует множество термов с помощью некоторой общей функции накопления

```scheme
    (accumulate combiner null-value term a next b)
```

`Accumulate` принимает в качестве аргументов те же описания термов и диапазона, что и `sum` с `product`, а еще процедуру `combiner` (двух аргументов), которая указывает, как нужно присоединить текущий терм к результату накопления предыдущих, и `null-value`, базовое значение, которое нужно использовать, когда термы закончатся. Напишите `accumulate` и покажите, как и `sum`, и `product` можно определить в виде простых вызовов `accumulate`.

б. Если Ваша процедура `accumulate` порождает рекурсивный процесс, перепишите ее так, чтобы она порождала итеративный. Если она порождает итеративный процесс, перепишите ее так, чтобы она порождала рекурсивный.

### Решение

а. 

```scheme
  (define (accumulate combiner null-value term a next b)
    (if (> a b)
      null-value
      (combiner (term a)
                (accumulate combiner null-value (next a) next b))))
```

б. 

```scheme
  (define (accumulate combiner null-value term a next b)
    (define (iter a result)
      (if (> a b)
        result
        (iter (next a) (combiner result (term a)))))

    (iter a null-value))    
```