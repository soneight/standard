### This
###### [CXX](../../../README.md) / [expr](../../expr.md) / [expr.prim](../prim.md) / expr.prim.this

> 1.
> The keyword `this` names a pointer to the object for which a non-static member function [class.this](../../class/this.md) is invoked
> or a non-static data member’s initializer [class.mem](../../class/mem.md) is evaluated.

> 2.
> If a declaration declares a member function or member function template of a `class X`,
> the expression `this` is a prvalue of type “pointer to cv-qualifier-seq X” between the optional cv-qualifier-seq and the end of the function-definition,
> member-declarator, or declarator.
> It shall not appear before the optional cv-qualifier-seq and it shall not appear within the declaration of a static member function
> (although its type and value category are defined within a static member function as they are within a non-static member function).
> [ Note: This is because declaration matching does not occur until the complete declarator is known.
> — end note ]
> Unlike the object expression in other contexts,
> `*this` is not required to be of complete type for purposes of class member access [expr.ref](../ref.md) outside the member function body.
> [ Note: Only class members declared prior to the declaration are visible.
> — end note ] [ Example:
> ```cxx
>   struct A {
>       char g( );
>       template< class T > auto f( T t ) -> decltype( t + g( ) )
>       { return t + g( ); }
>   };
>   template auto A::f( int t ) -> decltype( t + g( ) );
> ```
> — end example ]

> 3.
> Otherwise, if a member-declarator declares a non-static data member [class.mem](../../class/mem.md) of a `class X`,
> the expression `this` is a prvalue of type “pointer to X” within the optional default member initializer [class.mem](../../class/mem.md).
> It shall not appear elsewhere in the member-declarator.

> 4.
> The expression `this` shall not appear in any other context.
> [ Example:
> ```cxx
>   class Outer {
>       int a[sizeof(*this)];               // error: not inside a member function
>       unsigned int sz = sizeof(*this);    // OK: in default member initializer
>       void f() {
>           int b[sizeof(*this)];           // OK
>           struct Inner {
>               int c[sizeof(*this)];       // error: not inside a member function of Inner
>           };
>       }
>   };
> ```
> — end example ]
