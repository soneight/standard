# Expressions
###### [CXX](../README.md) / expr

1. [Primary expressions](./expr/prim.md)
2. [Postfix expressions](./expr/post.md)
3. [Unary expressions](./expr/unary.md)
4. [Explicit type conversion (cast notation)](./expr/cast.md)
5. [Pointer-to-member operators](./expr/mptr/oper.md)
16. [Conditional operator](./expr/cond.md)
18. [Assignment and compound assignment operators](./expr/ass.md)
19. [Comma operator](./expr/comma.md)

> 1.
> [ *Note:* [expr](./expr.md) defines the syntax, order of evaluation, and meaning of expressions.[⁶²](#62)
> An expression is a sequence of operators and operands that specifies a computation.
> An expression can result in a value and can cause side effects. — *end note* ]

> 2.
> [ *Note:* Operators can be overloaded, that is,
> given meaning when applied to expressions of class type [class](./class.md) or enumeration type [dcl.enum](./dcl/enum.md).
> Uses of overloaded operators are transformed into function calls as described in [over.oper](./over/oper.md).
> Overloaded operators obey the rules for syntax and evaluation order specified in [expr](./expr.md),
> but the requirements of operand type and value category are replaced by the rules for function call.
> Relations between operators, such as `++a` meaning `a += 1`, are not guaranteed for overloaded operators [over.oper](./over/oper.md). — *end note* ]

> 3.
> [expr](./expr.md) defines the effects of operators when applied to types for which they have not been overloaded.
> Operator overloading shall not modify the rules for the built-in operators, that is,
> for operators applied to types for which they are defined by this Standard.
> However, these built-in operators participate in overload resolution,
> and as part of that process user-defined conversions will be considered where
> necessary to convert the operands to types appropriate for the built-in operator.
> If a built-in operator is selected,
> such conversions will be applied to the operands before the operation is considered further according to the rules in [expr](./expr.md);
> see [over.match.oper](./over/match/oper.md), [over.built](./over/built.md).

> 4.
> If during the evaluation of an expression, the result is not mathematically defined or not in the range of representable values for its type,
> the behavior is undefined.
> [ *Note:* Treatment of division by zero, forming a remainder using a zero divisor, and all floating-point exceptions vary among machines,
> and is sometimes adjustable by a library function.
> — *end note* ]

> 5.
> If an expression initially has the type “reference to T” [dcl.ref](./dcl/ref.md), [dcl.init.ref](./dcl/init/ref.md),
> the type is adjusted to `T` prior to any further analysis.
> The expression designates the object or function denoted by the reference, and the expression is an lvalue or an xvalue, depending on the expression.
> [ *Note:* Before the lifetime of the reference has started or after it has ended, the behavior is undefined (see 6.8).
> — *end note* ]
> 6.
> If a prvalue initially has the type “cv T”, where `T` is a cv-unqualified non-class, non-array type,
> the type of the expression is adjusted to T prior to any further analysis.

> 7.
> [ *Note:* An expression is an xvalue if it is:
> 1. — the result of calling a function, whether implicitly or explicitly, whose return type is an rvalue reference to object type,
> 2. — a cast to an rvalue reference to object type,
> 3. — a class member access expression designating a non-static data member of non-reference type in which the object expression is an xvalue, or
> 4. — a `.*` pointer-to-member expression in which the first operand is an xvalue and the second operand is a pointer to data member.
>
> In general, the effect of this rule is that named rvalue references are treated as lvalues and unnamed rvalue references to objects are treated as xvalues;
> rvalue references to functions are treated as lvalues whether named or not.
> — *end note* ]
> [ *Example:*
> ```cxx
> struct A {
>     int m;
> };
> A &&operator+( A, A );
> A &&f( );
> A a;
> A &&ar = static_cast< A && >( a );
> ```
> The expressions `f( ), f( ).m, static_cast< A&& >( a )`, and `a + a` are xvalues. The expression `ar` is an lvalue.
> — *end example* ]

> 8.
> In some contexts, unevaluated operands appear
> [expr.typeid](./expr/typeid.md), [expr.sizeof](./expr/sizeof.md), [expr.unary.noexcept](./expr/unary/noexcept.md), [dcl.type.simple](./dcl/type/simple.md).
> An unevaluated operand is not evaluated.
> [ *Note:* In an unevaluated operand, a non-static class member may be named [expr.prim](./expr/prim.md) and naming of objects or functions does not,
> by itself, require that a definition be provided [basic.def.odr](./basic/def/odr.md).
> An unevaluated operand is considered a full-expression [intro.execution](./intro/execution.md).
> — *end note* ]

> 9.
> Whenever a glvalue expression appears as an operand of an operator that expects a prvalue for that operand, the lvalue-to-rvalue [conv.lval](./conv/lval.md),
> array-to-pointer [conv.array](./conv/array.md),
> or function-to-pointer [conv.func](./conv/func.md) standard conversions are applied to convert the expression to a prvalue.
> [ *Note:* Because cv-qualifiers are removed from the type of an expression of non-class type when the expression is converted to a prvalue,
> an lvalue expression of type `int const` can, for example, be used where a prvalue expression of type `int` is required.
> — **end note** ]

> 10.
> Whenever a prvalue expression appears as an operand of an operator that expects a glvalue for that operand,
> the temporary materialization conversion [conv.rval](./conv/rval.md) is applied to convert the expression to an xvalue.

> 11.
> Many binary operators that expect operands of arithmetic or enumeration type cause conversions and yield result types in a similar way.
> The purpose is to yield a common type, which is also the type of the result.
> This pattern is called the usual arithmetic conversions, which are defined as follows:
> 1. — If either operand is of scoped enumeration type [dcl.enum](./dcl/enum.md), no conversions are performed;
> if the other operand does not have the same type, the expression is ill-formed.
> 2. — If either operand is of type long double, the other shall be converted to long double.
> 3. — Otherwise, if either operand is double, the other shall be converted to double.
> 4. — Otherwise, if either operand is float, the other shall be converted to float.
> 5. — Otherwise, the integral promotions [conv.prom](./conv/prom.md) shall be performed on both operands.[⁶³](#63)
> Then the following rules shall be applied to the promoted operands:
> - 1. — If both operands have the same type, no further conversion is needed.
> - 2. — Otherwise, if both operands have signed integer types or both have unsigned integer types,
> the operand with the type of lesser integer conversion rank shall be converted to the type of the operand with greater rank.
> - 3. — Otherwise, if the operand that has unsigned integer type has rank greater than or equal to the rank of the type of the other operand,
> the operand with signed integer type shall be converted to the type of the operand with unsigned integer type.
> - 4. — Otherwise, if the type of the operand with signed integer type can represent all of the values of the type of the operand with unsigned integer type,
> the operand with unsigned integer type shall be converted to the type of the operand with signed integer type.
> - 5. — Otherwise, both operands shall be converted to the unsigned integer type corresponding to the type of the operand with signed integer type.

> 12.
> In some contexts, an expression only appears for its side effects. Such an expression is called a discarded-value expression.
> The array-to-pointer [conv.array](./conv/array.md) and function-to-pointer [conv.func](./conv/func.md) standard conversions are not applied.
> The lvalue-to-rvalue conversion [conv.lval](./conv/lval.md) is applied
> if and only if the expression is a glvalue of volatile-qualified type and it is one of the following:
> 1. — ( expression ), where expression is one of these expressions,
> 2. — id-expression [expr.prim.id](./expr/prim/id.md),
> 3. — subscripting [expr.sub](./expr/sub.md),
> 4. — class member access [expr.ref](./expr/ref.md),
> 5. — indirection [expr.unary.op](./expr/unary/op.md),
> 6. — pointer-to-member operation [expr.mptr.oper](./expr/mptr/oper.md),
> 7. — conditional expression [expr.cond](./expr/cond.md) where both the second and the third operands are one of these expressions, or
> 8. — comma expression [expr.comma](./expr/comma.md) where the right operand is one of these expressions.
>
> [ *Note:* Using an overloaded operator causes a function call; the above covers only operators with built-in meaning.
> — *end note* ] If the expression is a prvalue after this optional conversion, the temporary materialization conversion [conv.rval](./conv/rval.md) is applied.
> [ *Note:* If the expression is an lvalue of class type,
> it must have a volatile copy constructor to initialize the temporary that is the result object of the lvalue-to-rvalue conversion.
> — *end note* ]
> The glvalue expression is evaluated and its value is discarded.

> 13.
> The values of the floating operands and the results of floating expressions may be represented in greater precision and range than that required by the type;
> the types are not changed thereby.[⁶⁴](#64)

> 14.
> The cv-combined type of two types `T1` and `T2` is a type `T3` similar to `T1` whose cv-qualification signature [conv.qual](./conv/qual.md) is:
> 1. — for every i > 0, cv<sub>i</sub><sup>3</sup> is the union of cv<sub>i</sub><sup>1</sup> and cv<sub>i</sub><sup>2</sup>;
> 2. — if the resulting cv<sub>i</sub><sup>3</sup> is different from cv<sub>i</sub><sup>1</sup> or cv<sub>i</sub><sup>2</sup>,
> then `const` is added to every cv<sub>k</sub><sup>3</sup> for 0 < k < i.
>
> [ *Note:* Given similar types `T1` and `T2`, this construction ensures that both can be converted to `T3`.
> — *end note* ]

> 15.
> The composite pointer type of two operands `p1` and `p2` having types `T1` and `T2`, respectively,
> where at least one is a pointer or pointer to member type or `std::nullptr_t`, is:
> 1. — if both `p1` and `p2` are null pointer constants, `std::nullptr_t`;
> 2. — if either `p1` or `p2` is a null pointer constant, `T2` or `T1`, respectively;
> 3. — if `T1` or `T2` is “pointer to *cv1* `void`” and the other type is “pointer to *cv2* `T`”, where `T` is an object type or `void`,
> “pointer to *cv12* `void`”, where *cv12* is the union of *cv1* and *cv2*;
> 4. — if `T1` or `T2` is “pointer to `noexcept` function” and the other type is “pointer to function”, where the function types are otherwise the same,
> “pointer to function”;
> 5. — if `T1` is “pointer to *cv1* `C1`” and `T2` is “pointer to *cv2* `C2`”,
> where `C1` is reference-related to `C2` or `C2` is reference-related to `C1` [dcl.init.ref](./dcl/init/ref.md),
> the cv-combined type of `T1` and `T2` or the cv-combined type of `T2` and `T1`, respectively;
> 6. — if `T1` is “pointer to member of `C1` of type *cv1* `U1`” and `T2` is “pointer to member of `C2` of type *cv2* `U2`”
> where `C1` is reference-related to `C2` or `C2` is reference-related to `C1` [dcl.init.ref](./dcl/init/ref.md),
> the cv-combined type of `T2` and `T1` or the cv-combined type of `T1` and `T2`, respectively;
> 7. — if `T1` and `T2` are similar types [conv.qual](./conv/qual.md), the cv-combined type of `T1` and `T2`;
> 8. — otherwise, a program that necessitates the determination of a composite pointer type is ill-formed.
>
> [ *Example:*
> ```cxx
> typedef void *p;
> typedef int const *q;
> typedef int **pi;
> typedef int const **pci;
> ```
> The composite pointer type of `p` and `q` is “pointer to `void const`”;
> the composite pointer type of `pi` and `pci` is “pointer to pointer `const` to `int const`”.
> — *end example* ]

###### 62
> The precedence of operators is not directly specified, but it can be derived from the syntax.
###### 63
> As a consequence, operands of type `bool`, `char16_t`, `char32_t`, `wchar_t`, or an enumerated type are converted to some integral type.
###### 64
> The cast and assignment operators must still perform their specific conversions as described in
> [expr.cast](./expr/cast.md), [expr.static.cast](./expr/static/cast.md) and [expr.ass](./expr/ass.md).
