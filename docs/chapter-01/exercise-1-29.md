### Упражненение 1.29.

Правило Симпсона — более точный метод численного интегрирования, чем представленный выше. С помощью правила Симпсона интеграл функции f между a и b приближенно вычисляется в виде

  h/3[y0 +4y1 +2y2 +4y3 +2y4 +...+2yn−2 +4yn−1 +yn]

где `h = (b − a)/n`, для какого-то четного целого числа n, а y<sub>k</sub> = f(a + kh). (Увеличение n повышает точность приближенного вычисления.) Определите процедуру, которая принимает в качестве аргументов `f`, `a`, `b` и `n`, и возвращает значение интеграла, вычисленное по правилу Симпсона. С помощью этой процедуры проинтегрируйте `cube` между `0` и `1` (с n = 100 и n = 1000) и сравните результаты с процедурой integral, приведенной выше.

### Решение

```scheme
  (define (cube x) (* x x x))

  (define (sum term a next b)
    (if (> a b)
      0
      (+ (term a)
         (sum term (next a) next b))))

  (define (integral f a b dx)
    (define (add-dx x) (+ x dx))

    (* (sum f (+ a (/ dx 2.0)) add-dx b)
       dx))

  (define (integral-simpson f a b n)
    (define h (/ (- b a) n))
    (define (add-2h x) (+ x h h))
 
    (* (+ (f a)
          (* 2 (sum f a       add-2h b))
          (* 4 (sum f (+ a h) add-2h b))
          (f b))
       (/ h 3)))    
```