---
layout: distill
title: 'ILP Methods: FOIL and FOCL'
description: Preprint Papers
gradient: linear-gradient(135deg, #0064e1 0%, #5bd3ff 100%)
hover-gradient: linear-gradient(135deg, #00c6fb 0%, #005bea 100%)
date: 2025-07-14
background_color: rgb(255, 255, 255)
---


## FOIL 



```
        john
       /    \
    mary     tom
     |         |
   alice     lucy

```

The given predicates: 


```prolog
parent(john, mary).
parent(mary, alice).
parent(john, tom).
parent(tom, lucy).


% Positive Examples 
grandfather(john, alice).   % John -> Mary -> Alice
grandfather(john, lucy).    % John -> Tom -> Lucy


% Negative Examples
grandfather(mary, lucy).    % Mary is not Lucy’s grandfather
grandfather(john, tom).     % John is Tom’s father, not grandfather
```

## Algorithm 
```
grandfather(X, Y) :-   % empty body
```

We can construct 
```prolog
parent(X, Z)
parent(Z, Y)
```

```prolog
grandfather(X, Y) :- parent(X, Z)
```