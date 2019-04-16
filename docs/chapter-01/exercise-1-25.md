### Упражнение 1.25.

Лиза П. Хакер жалуется, что при написании `expmod` мы делаем много лишней работы. В конце концов, говорит она, раз мы уже знаем, как вычислять степени, можно просто написать

```scheme
  (define (expmod base exp m)
    (remainder (fast-expt base exp) m))
```

Права ли она? Стала бы эта процедура столь же хорошо работать при проверке простых чисел? Объясните.

### Решение

```scheme
  (define (fast-exp b n)
    (fast-expt-iter 1 b n))
  
  (define (fast-expt-iter product base exp) 
    (if (= exp 0) 
        product 
        (if (even? exp) 
          (fast-expt-iter product (square base) (/ exp 2)) 
          (fast-expt-iter (* product base) base (- exp 1)))))

  (define (even? n)
    (= (remainder n 2) 0))      

  (define (square n) (* n n))
```

Сравним выполнение `(expmod 3 2 4)`

*Без `fast-exp`*

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

*C `fast-exp`*

```scheme
  (expmod 3 2 4)
```

```scheme
  (remainder (fast-expt 3 2) 4)
```

```scheme
  (remainder (fast-expt-iter 1 3 2) 4)
```

```scheme
  (remainder (fast-expt-iter 1 3 2) 4)
```

```scheme
  (remainder (fast-expt-iter 1 (square 3) (/ 2 2)) 4)
```

```scheme
  (remainder (fast-expt-iter 1 9 1) 4)
```

```scheme
  (remainder (fast-expt-iter (* 1 9) 9 (- 1 1)) 4)
```

```scheme
  (remainder (fast-expt-iter 9 9 0) 4)
```

```scheme
  (remainder 9 4)
```

```scheme
  1
```

Операции, производимые процедурой `expmod` через `fast-exp` будут происходить над числами порядка base<sup>exp</sup>, в то время как процедура `expmod` из упражнения 1.24 оперирует с числами порядка `exp`.