
# Pseudocode conventions
Source : ISBN 978-0-262-03384-8 

Author : Adrien LAMIT

### 1. Indentation

Indentation indicates block structure, we will use double spaces for indentation, and not tabulations. 
Indentation applies to :

- Loops (`for`, `while`, `do while (eq. repeat-until)`)
- Conditions (`if`, `else`, `else if`)

**! We don't use any `begin` or `end` statements for clarity enhancement. !**

#### Example : 
***
`ALGORITHM ( INPUT : None , OUTPUT : None )`
***
```scala
for i from 1 to n
  if i > 0
    // do stuff here is in the for and if block
    while i < 3
      // do stuff here is in the for, if and while block
    i = i + 1 // this statement is not in the while block.
  i = 0 // this statement is only in the for block
x = 10 // this statement is not in any block 
return
```
***

### 2. Looping constructs

The loooping constructs `while`, `for`, `do while (eq. repeat-until)` and the `if`, `else` conditional constructs are similar to the ones in most programming languages (C++, Java, Scala, Python, R, ...).

We will consider that for loop counters retain their values after exiting the loop :
***
`LOOP-EXAMPLE-1 ( INPUT : NIL , OUTPUT : NIL )`
***
```scala
for i from 1 to n
  // Do stuff in the for loop
return
```
***
In the example above, `i` will increment by 1 just before the beginning of each iteration.

We will use the keyword `to` when a `for` loop increments its counter, and `downto` when it decrements its counter. If the amount incremented(decremented) is greater than 1, we will use the keyword `by` to specify the amount incremented(decremented) :
***
`LOOP-EXAMPLE-2 ( INPUT : NIL , OUTPUT : NIL )`
***
```scala
for i from n downto 0 by 2
  // Do stuff in the for loop
return
```
***

### 3. Comments

- **`//`** specifies that the rest of the line is a comment.
- **`/* Lorem ipsum ..... */`** specifies that every text between **`/*`** and **`*/`** is a comment.

### 4. Multiple assignments

A multiple assignment of the for `i = j = k` assgigns both variables `i` and `j` the value of expression `e`. This is equivalent to : 
```
j = e
i = j
```

### 5. Variables range.

Variable are local to their procedure (i.e. portion of pseudo code), global variables should not be used without explicit indication. (f.e. you can say that a global variable exist in a sentence, or mention that you use a variable from another procedure).

### 6. Arrays

We will use UpperCase letters for array variable names.

We access array elements by specifying the array name followed by the index in square brackets : `A[index]`, and we will use the notation `..` to indicate a range of values, therfore the subarray of `A` from index `a` to index `b` will be specified as `A[a..b]` :
***
`ARRAY-ACCESS-EXAMPLE ( INPUT : A, an array of length n , OUTPUT : NIL )`
***
```scala
x = A[0] // access the element of A at index 0.
B = A[0..m] // B is subarray of A from index 0 to m.
```
***

Arrays are treated like objects, with an attribute length, to get the number of elements in an array A, use `A.length`.

### 7. Objects

Object variables will be UpperCase letters, as arrays. (Arrays are objects)

For complex procedures, we might need to organize data into **objects**, which will have **attributes**. We will use the "`.`" to access a particular attribute from an object.

We treat a variable representing an object as a **pointer** (like in C language) to the data representing the object.
For all attribute `f` of an object `x`, setting `y = x` causes `y.f` to equal `x.f`. Moreover if we modify `x.f`, we also modify `y.f` at the same time. 

This means that `x` and `y` points to the same object after assignment `y = x`. (`x` and `y` are pointers and therefore assigning one to the other, is like copying the adress of our object to the assigned one). For more information on pointer you can refer to [this article](http://karwin.blogspot.ch/2012/11/c-pointers-explained-really.html).

Sometime a pointer will refer to no object at all. In this case, we give it the special value `NIL`.

### 8. Procedure parameters

Parameters are passed to procedures **by value** : this means that procedures receive their own copy of the parameters. Therefore the value passed to the procedure by the calling procedure will not be modified in the calling procedure if it is in the called procedure : 

***
`PASS-BY-VALUE ( INPUT : NIL , OUTPUT : (x,y) two integers )`
***
```scala
x = 1
y = decrement(x) // decrement is a procedure that decrements x and returns it.
return (x,y) // Here x equals 1, y equals 0, x has not been affected by decrementation in the called procedure.
```
***

But be careful, objects (and arrays) are pointers which means they contains an address. Therefore the address only is copied in the procedure, so it if you modify its attributes in the procedure, the calling procedure will be affected by changes : 

***
`MODIFY-ATTRIBUTE ( INPUT : O, an object with attribute x, OUTPUT : NIL )`
***
```scala
O.x = 0
```
***

***
`EXAMPLE ( INPUT : NIL , OUTPUT : A boolean value )`
***
```scala
O.x = 10
MODIFY-ATTRIBUTE(O)
return O.x == 10 // Will return false
```
***

If you have any experience with programming languages, **passing a pointer by value is equivalent to passing a variable by reference**. Indeed, that's what happens behind the scenes ;) .


### 9. Return statements

We will use `return` statements for every procedure, if the procedure does not have to return anything we will only use `return` keyword without anything following on the line (eq. `return NIL`).

When `return` keyword line is executed, it **immediately stops the procedure** and continues executing the calling procedure. If the procedure is our main procedure, the procedure terminates.

**! `return` statement must always correspond to what you mentionned in the headline of your procedure. !**

### 10. Boolean operators

Booleans operators will be specified by keyword : "`and`" and "`or`".

They are **short-circuiting**, which means that they are evaluated from left to right, and if at some point the boolean can be evaluated, it won't evaluate following statements : 

***
`SHORT-CIRCUIT-EXAMPLE ( INPUT : NIL , OUTPUT : NIL )`
***
```scala
FALSE AND TRUE // FALSE will be evaluated first, so TRUE won't be evaluated
TRUE OR FALSE // TRUE will be evaluated first, so FALSE won't be evaluated
TRUE AND FALSE // TRUE is evaluated, but we can't conclude, so FALSE is evaluated
```
***

### 11. Errors

The keyword `error` indicates that an error occured because conditions were wrong for the procedure to have been called. The calling procedure is responsible for handling the error, so we don't specify what action to take.
`error` has the same effect as `return` and the execution goes back to the caller. 

If you are familiar with some programming languages, this is quite similar to [Exceptions design patterns](http://wiki.c2.com/?ExceptionPatterns). 

A message in a form of a string can be attached to an error by using this syntax : `error "message"`.

***
`ERROR-EXAMPLE ( INPUT : O, an object , OUTPUT : NIL )`
***
```scala
if O.x = NIL
  error
return O.x + 1
```
***

The caller will then have to handle cases where an error is thrown.


