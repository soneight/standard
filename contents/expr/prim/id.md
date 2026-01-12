### Names
###### [CXX](../../../README.md) / [expr](../../expr.md) / [expr.prim](../prim.md) / expr.prim.id

```
    id-expression:
        unqualified-id
        qualified-id
```

1. [Unqualified names](./id/unqual.md)
2. [Qualified names](./id/qual.md)

> 1.
> An id-expression is a restricted form of a primary-expression.
> [ Note: An id-expression can appear after `.` and `->` operators [expr.ref](../../expr/ref.md).
> — end note ]

> 2.
> An id-expression that denotes a non-static data member or non-static member function of a class can only be used:
> 1. — as part of a class member access [expr.ref](../../expr/ref.md) in which the object expression refers to the member’s class[⁶⁵](#65)
> or a class derived from that class, or
> 2. — to form a pointer to member [expr.unary.op](../../expr/unary/op.md), or
> 3. — if that id-expression denotes a non-static data member and it appears in an unevaluated operand.
> [ Example:
> ```cxx
>   struct S {
>       int m;
>   };
>   int i = sizeof( S::m );       // OK
>   int j = sizeof( S::m + 42 );  // OK
> ```
> — end example ]

###### 65
> This also applies when the object expression is an implicit `(*this)` [class.mfct.non-static](../../class/mfct/non-static.md).
