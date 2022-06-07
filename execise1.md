


#### 1.9 

first is recursive, second is iterative.

http://community.schemewiki.org/?sicp-ex-1.9

#### 1.11

```
#lang sicp


(define (recur n)
  (cond
    ((< n 3) n)
    (else (+
            (recur (- n 1))
            (* 2 (recur (- n 2)))
            (* 3 (recur (- n 3)))
          )
    )
  )
)

```
