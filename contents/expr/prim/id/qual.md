#### Qualified names
###### [CXX](../../../../README.md) / [expr](../../../expr.md) / [expr.prim](../../prim.md) / [expr.prim.id](../id.md) / expr.prim.id.qual

```
    qualified-id:
        nested-name-specifier [`template`] unqualified-id
    nested-name-specifier:
        ::
        type-name ::
        namespace-name ::
        decltype-specifier ::
        nested-name-specifier identifier ::
        nested-name-specifier [`template`] simple-template-id ::
```

> 1.
> The type denoted by a decltype-specifier in a nested-name-specifier shall be a class or enumeration type.

> 2.
> A nested-name-specifier that denotes a class, optionally followed by the keyword `template` [temp.names](../../../temp/names.md),
> and then followed by the name of a member of either
> that class [class.mem](../../../class/mem.md) or one of its base classes [class.derived](../../../class/derived.md), is a qualified-id;
> [class.qual](../../../class/qual.md) describes name lookup for class members that appear in qualified-ids.
> The result is the member.
> The type of the result is the type of the member.
> The result is an lvalue if the member is a static member function or a data member and a prvalue otherwise.
> [ Note: A class member can be referred to using a qualified-id at any point in its potential scope [basic.scope.class](../../../basic/class/scope.md).
> — end note ]
> Where class-name ::~ class-name is used, the two class-names shall refer to the same class;
> this notation names the destructor [class.dtor](../../../class/dtor.md).
> The form ~ decltype-specifier also denotes the destructor, but it shall not be used as the unqualified-id in a qualified-id.
> [ Note: A typedef-name that names a class is a class-name [class.name](../../../class/name.md).
> — end note ]

> 3.
> The nested-name-specifier :: names the global namespace.
> A nested-name-specifier that names a namespace [basic.namespace](../../../basic/namespace.md), optionally followed by the keyword `template` [temp.names](../../../temp/names.md),
> and then followed by the name of a member of that namespace (or the name of a member of a namespace made visible by a using-directive), is a qualified-id;
> [namespace.qual](../../../namespace/qual.md) describes name lookup for namespace members that appear in qualified-ids.
> The result is the member.
> The type of the result is the type of the member.
> The result is an lvalue if the member is a function or a variable and a prvalue otherwise.

> 4.
> A nested-name-specifier that denotes an enumeration [dcl.enum](../../../dcl/enum.md), followed by the name of an enumerator of that
enumeration, is a qualified-id that refers to the enumerator. The result is the enumerator. The type of the
result is the type of the enumeration. The result is a prvalue.

> 5.
> In a qualified-id, if the unqualified-id is a conversion-function-id, its conversion-type-id shall denote the same
type in both the context in which the entire qualified-id occurs and in the context of the class denoted by the
nested-name-specifier.
