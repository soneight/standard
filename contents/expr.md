# 8. Expressions
###### [Programming languages – C++](../README.md) / expr
- [8.1 Primary expressions](./expr/prim.md)
- [8.2 Postfix expressions](./expr/post.md)
- [8.3 Unary expressions](./expr/unary.md)
1.
> [ Note: [expr](./expr.md) defines the syntax, order of evaluation, and meaning of expressions.[62](#62)
> An expression is a sequence of operators and operands that specifies a computation.
> An expression can result in a value and can cause side effects. — end note ]
2.
> [ Note: Operators can be overloaded, that is,
> given meaning when applied to expressions of class type [class](./class.md) or enumeration type [dcl.enum](./dcl/enum.md).
> Uses of overloaded operators are transformed into function calls as described in [over.oper](./over/oper.md).
> Overloaded operators obey the rules for syntax and evaluation order specified in [expr](./expr.md),
> but the requirements of operand type and value category are replaced by the rules for function call.
> Relations between operators, such as `++a` meaning `a += 1`, are not guaranteed for overloaded operators [over.oper](./over/oper.md). — end note ]
3.
> [expr](./expr.md) defines the effects of operators when applied to types for which they have not been overloaded.
> Operator overloading shall not modify the rules for the built-in operators, that is,
> for operators applied to types for which they are defined by this Standard.
> However, these built-in operators participate in overload resolution,
> and as part of that process user-defined conversions will be considered where
> necessary to convert the operands to types appropriate for the built-in operator.
> If a built-in operator is selected,
> such conversions will be applied to the operands before the operation is considered further according to the rules in [expr](./expr.md);
> see [over.match.oper](./over/match/oper.md), [over.built](./over/built.md).
4.
> If during the evaluation of an expression, the result is not mathematically defined or not in the range of representable values for its type,
> the behavior is undefined.
> [ Note: Treatment of division by zero, forming a remainder using a zero divisor, and all floating-point exceptions vary among machines,
> and is sometimes adjustable by a library function.
> — end note ]
5.
> If an expression initially has the type “reference to T” ([dcl.ref](./dcl/ref.md), [dcl.init.ref](./dcl/init/ref.md)),
> the type is adjusted to T prior to any further analysis.
> The expression designates the object or function denoted by the reference, and the expression is an lvalue or an xvalue, depending on the expression.
> [ Note: Before the lifetime of the reference has started or after it has ended, the behavior is undefined (see 6.8).
> — end note ]
6.
> If a prvalue initially has the type “cv T”, where T is a cv-unqualified non-class, non-array type,
> the type of the expression is adjusted to T prior to any further analysis.
7.
> [ Note: An expression is an xvalue if it is:
> 1. — the result of calling a function, whether implicitly or explicitly, whose return type is an rvalue reference to object type,
> 2. — a cast to an rvalue reference to object type,
> 3. — a class member access expression designating a non-static data member of non-reference type in which the object expression is an xvalue, or
> 4. — a .* pointer-to-member expression in which the first operand is an xvalue and the second operand is a pointer to data member.
>
> In general, the effect of this rule is that named rvalue references are treated as lvalues and unnamed rvalue references to objects are treated as xvalues;
> rvalue references to functions are treated as lvalues whether named or not.
> — end note ]
> [ Example:
```cxx
struct A {
    int m;
};
A &&operator+( A, A );
A &&f( );
A a;
A &&ar = static_cast< A && >( a );
```
> The expressions `f( ), f( ).m, static_cast< A&& >( a )`, and `a + a` are xvalues. The expression `ar` is an lvalue.
> — end example ]
8.
> In some contexts, unevaluated operands appear
> [expr.typeid](./expr/typeid.md), [expr.sizeof](./expr/sizeof.md), [expr.unary.noexcept](./expr/unary/noexcept.md), [dcl.type.simple](./dcl/type/simple.md).
> An unevaluated operand is not evaluated.
> [ Note: In an unevaluated operand, a non-static class member may be named [expr.prim](./expr/prim.md) and naming of objects or functions does not, by itself,
> require that a definition be provided [basic.def.odr](./basic/def/odr.md).
> An unevaluated operand is considered a full-expression [intro.execution](./intro/execution.md).
> — end note ]
##### 62
> The precedence of operators is not directly specified, but it can be derived from the syntax.

