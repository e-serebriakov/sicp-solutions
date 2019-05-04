### Упражненение 1.30.

Процедура `sum` порождает линейную рекурсию. Ее можно переписать так, чтобы суммирование выполнялось итеративно. Покажите, как сделать это, заполнив пропущенные выражения в следующем определении:

```scheme
  (define (sum term a next b)
    (define (iter a result)
      (if ⟨??⟩
        ⟨??⟩
        (iter ⟨??⟩ ⟨??⟩)))
        
    (iter ⟨??⟩ ⟨??⟩))
```

### Решение

```scheme
;recursive
  (define (sum term a next b)
    (if (> a b)
      0
      (+ (term a)
         (sum term (next a) next b))))

;iterative
  (define (sum term a next b)
    (define (iter a result)
      (if (> a b)
        result
        (iter (next a) (+ result (term a)))))
        
    (iter a 0))  
```