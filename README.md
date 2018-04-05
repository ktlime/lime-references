# Lime Language References

📘 Language definition for the little incomplete macro language

## The Syntax

+ Lisp-style sexpression-based syntax

```lisp
(-> a 1) ; a comment
; comments starts from ';', ends at '\n'
(@ a)
((() () 'a) 1 2 3)
```

+ Syntax sugar

```
(-> 世界 'world)
(@ 'Hello,_world!)
(@ "Hello, #{世界}!")
```

From-text types

+ Sexpr `() (() a b c) (b 'a)`
+ String `"a" 'a 'a' <<-ENDaEND`
+ Symbol(Reference) `a b :'a :"b"`
+ Char `'a 'b`
+ Number(byte/short/int/long/float/double) `1 0x2 0b3dec 32big 2.2`
+ Boolean `#t #f`
+ Hash `#h`
+ List `#i`

### Syntax rules

#### Sexpr

```
'(' sexp_or_atom* ')'
```

```lisp
(puts 'a)
(->" :"a symbol")
(puts (->" :"a symbol") () (r 1))
((? (> (rand) 0.5) puts exit) 0)
```

#### String

> single-quote string

starts from: '
ends at: ), ,',\n

> _ is seen as ' ' in single-quote string

```
'a_string "a string"
'dog "dog"
'' ""
'abc_defg'
```

> double-quote string

starts from: "
ends at: " (but not \")

> double-quoted strings has #{} syntax sugar

```
"Hello" "Hello"
"H
e
llo" "H\ne\nllo"
"Are U #{okay}" (+ "Are U " (->" okay))
```

> heredoc

`<<-terminator\ncontent\nterminator`

```
(eval <<-END
(puts 'emmmm "Hello")
END) (eval "(puts 'emmm \"Hello\")")
```

#### Symbol

```
a b c
10.times
:"with space"
:'with_space
:"#{won't process sugar}"
```

#### Char

```
'a
'b
'🐭
```

#### Number

starts: -,0-9
ends: ), ,\n

```
032
434
23.2
0x1
0b1
0o1
0x123i32
0x32f64
```

types:
i8 -> byte
i16 -> short
i32 -> int
i64 -> long
f32 -> float
f64 -> double
big -> math.BigInteger
dec -> math.BigDecimal

#### Fragment

```
#t true
#f false
#n nil
#g 1
#e 0
#l -1
#p 0.5
#h new a Hash
#i new a List
```
