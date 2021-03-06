### Item23 : Don't use raw types in new code

----------

Each generic type defines a set of *parameterized types*, which consist of the class or interface name followed by an angle-bracketed list of *actual type parameters* corresponding to the generic type's formal type parameters. For example, `List<String>` is a parameterized type representing a list whose elements are of type `String`. Each generic type defines a *raw type*, which is the name of the generic type used without any accompanying actual parameters. For example, the raw type corresponding to `List<E>` is `List`. Raw types behave as if all the generic type information were erased the type delcaration.

While you shouldn't use raw types such as `List` in new code, it is fine to use types that are parameterized to allow insertion of arbitrary objects, such as `List<Object>`. Just what is the difference between the raw type `List` and the parameterized type `List<Object>` ? Loosely speaking, the former has opted out of generic type checking, whie the latter has explicity told the compiler that it is capable of hoding objects of any type. While you can pass a `List<String>` to a parameter of type `List`, you can't pass it to a parameter of type `List<Object>`. There are subtyping rules for generics, and `List<String>` is a subtype of the raw type `List`, but not of the parameterized type `List<Object>`. As a consequence, **you lose type sefety if you use a raw type like `List`, but not if you use a parameterized type like `List<Object>`**.

If you want to use a generic type but you don't know or care what the actual type parameter is, you can use a question mark instead. For example, the unbounded wildcard type for the generic type `Set<E>` is `Set<?>`.

What is the difference between the unbounded wilecard type `Set<?>` and the raw type `Set`? You can put any element into a collection with a raw type, easily corrupting the collection's type invariant; **you can't put any element (other than null) into a Collection<?>**. 

#### Summary

In summary, using raw types can lead to exceptions at runtime, so don't use them in new code. They are provide only for compatibility and interoperability with legacy code that predates the introduction of generics. As a quick review, `Set<Object>` is a parameterized type representing a set that can contain objects of any type, `Set<?>` is a wildcard type representing a set that can contain only objects of some unknown type, and `Set` is a raw type, which opts out of the generic type system. The first two are safe and the last is not.