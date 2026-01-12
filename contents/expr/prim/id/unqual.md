#### Unqualified names
###### [CXX](../../../../README.md) / [expr](../../../expr.md) / [expr.prim](../../prim.md) / [expr.prim.id](../id.md) / expr.prim.id.unqual

```
    unqualified-id:
        identifier
        operator-function-id
        conversion-function-id
        literal-operator-id
        ~ class-name
        ~ decltype-specifier
        template-id
```

> 1.
> An identifier is an id-expression provided it has been suitably declared [dcl.dcl](../../../dcl/dcl.md).
> [ Note: For operator-function-ids, see [over.oper](../../../over/oper.md); for conversion-function-ids, see [class.conv.fct](../../../class/conv/fct.md);
> for literal-operator-ids, see [over.literal](../../../over/literal.md); for template-ids, see [temp.names](../../../temp/names.md).
> A class-name or decltype-specifier prefixed by ~ denotes a destructor; see [class.dtor](../../../class/dtor.md).
> Within the definition of a non-static member function,
> an identifier that names a non-static member is transformed to a class member access expression [class.mfct.non-static](../../../class/mfct/non-static.md).
> — end note ] The type of the expression is the type of the identifier. The result is the entity denoted by the identifier.
> The expression is an lvalue if the entity is a function, variable, or data member and a prvalue otherwise; it is a bit-field if the identifier designates a bit-field [dcl.struct.bind](../../../dcl/struct/bind.md).
