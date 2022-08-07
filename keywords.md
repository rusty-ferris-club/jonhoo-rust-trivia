
# Nuggets about each and every (strict)

https://doc.rust-lang.org/stable/reference/keywords.html

_Original thread: https://twitter.com/jonhoo/status/1539661689880137728_


<hr/>

`as`: `x as T` can do lossy conversion, so prefer `T::try_from(x).expect("…")` if you want it to fail loudly (e.g., if a u64 doesn't fit in a u32). 


> https://rust-lang.github.io/rust-clippy/master/index.html#as_conversions


<hr/>

`async`: in `async` blocks, `return` and `?` only bubble to the result of the future, whereas `break` and `continue` would affect the outer context and so re disallowed. 


> https://doc.rust-lang.org/stable/reference/expressions/block-expr.html#control-flow-operators


<hr/>

`await`: `await` is nothing but syntactic sugar for a `loop` that calls `Future::poll` and calls `yield` on `Poll::Pending`. 


> https://github.com/rust-lang/rust/blob/10f4ce324baf7cfb7ce2b2096662b82b79204944/compiler/rustc_ast_lowering/src/expr.rs#L635-L650


<hr/>

`break`: You can pass a value to break in a `loop` to make the `loop` evaluate to that value. 


> https://doc.rust-lang.org/stable/reference/expressions/loop-expr.html#break-and-loop-values


<hr/>

`const`: There are a _lot_ more constifications planned, including allowing `async {}` in `const fn`! 


> https://github.com/rust-lang/rust/issues/57563


<hr/>

`continue`: `continue` effectively evaluates to `!`, which allows it to masquerade as any type. 


> https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=8cc6050f46ba1de14afd2a8b8ab53bc2


<hr/>

`crate`: These days, the two primary uses of `crate` as a standalone keyword have mostly gone away: `extern crate` is rarely used, and `crate` as a visibility modifer won't happen (just use `pub(crate)` instead). 


> https://github.com/rust-lang/rust/issues/53120#issuecomment-1124065083


<hr/>

`dyn`: `dyn` trait objects come with a default lifetime bound inherited from the containing wide pointer type. 


> https://doc.rust-lang.org/stable/reference/lifetime-elision.html#default-trait-object-lifetimes


<hr/>

`else`: `else` is about to get another meaning with let-else expressions, which are like `.unwrap_or` for pattern matches! 


> https://github.com/rust-lang/rust/pull/93628


<hr/>

`enum`: For data-less enums ("C-style enums"), you can assign a value to only a _subset_ of the variants, and the remaining ones get inferred automatically. 


> https://doc.rust-lang.org/stable/reference/items/enumerations.html#custom-discriminant-values-for-fieldless-enumerations


<hr/>

`extern`: `extern` on its own is an alias for `extern "C"` — the two are interchangeable. 


> https://doc.rust-lang.org/stable/reference/items/external-blocks.html#abi


<hr/>

`false`: `false < true`. 


> https://doc.rust-lang.org/stable/reference/types/boolean.html#comparisons


<hr/>

`fn`: You can write `#![attr]` immediately _inside_ a function to add attributes to the function itself (though it's not very idiomatic). 


> https://doc.rust-lang.org/stable/reference/items/functions.html#attributes-on-functions


<hr/>

`for`: `for` loops are really just syntax sugar for a `loop` that calls `IntoIterator::into_iter` and then matches on `Iterator::next`. 


> https://github.com/rust-lang/rust/blob/10f4ce324baf7cfb7ce2b2096662b82b79204944/compiler/rustc_ast_lowering/src/expr.rs#L1390-L1406


<hr/>

`if`: 🤔🤷 


> undefined


<hr/>

`impl`: You can put `const`s directly in `impl` blocks to make "associated constants" for a type. 


> https://doc.rust-lang.org/stable/reference/items/associated-items.html#associated-constants


<hr/>

`in`: Not specifically about `in`, but any `..` expression is actually just a convenient constructor for a `Range` type. 


> https://doc.rust-lang.org/stable/reference/expressions/range-expr.html


<hr/>

`let`: The interaction between `let _ ` and dropping are subtle and interesting. 


> https://github.com/rust-lang/rust/issues/10488


<hr/>

`loop`: There used to be a mode in the Rust compiler that turned every function body into `loop {}`, which was used (among other things) to make `rustdoc` faster. It was called "everybody loops" 😆. 


> https://github.com/rust-lang/rust/pull/73566


<hr/>

`match`: The expression that a match matches on is called a "scrutinee". 


> https://doc.rust-lang.org/stable/reference/glossary.html#scrutinee


<hr/>

`mod`: You can make `mod` load files from non-standard locations using the `#[path]` attribute. Though use it sparingly, as it can be very confusing for other developers trying to sort through your code base. 


> https://doc.rust-lang.org/stable/reference/items/modules.html#the-path-attribute


<hr/>

`move`: The "opposite" capture behavior of `move` (that is, if `move` _isn't_ passed), is far from straightforward. 


> https://doc.rust-lang.org/stable/reference/types/closure.html#capture-modes


<hr/>

`mut`: While `mut` is *techically* short for "mutable", you're generally better off thinking about it as "MUTually exclusive". 


> https://docs.rs/dtolnay/latest/dtolnay/macro._02__reference_types.html


<hr/>

`pub`: There are a lot of visibility modifiers between non-`pub` and `pub`. `pub(crate)` and `pub(super)` are both useful, but you can even specify `pub(in crate::some_mod)` to get really specific. 


> https://doc.rust-lang.org/stable/reference/visibility-and-privacy.html


<hr/>

`ref`: You can use `ref` to match something as a reference in a pattern, instead of capturing it as a value. That's not a secret of `ref`, it's just what it means, but it's so commonly confused that it's worth repeating. 


> https://doc.rust-lang.org/stable/reference/patterns.html#identifier-patterns


<hr/>

`return`: `return` has a secret, long-unimplemented sibling, `become`, which is intended to one day maybe be used for functions that require guaranteed tail-call optimization. 


> https://rust-lang.github.io/rfcs/0601-replace-be-with-become.html


<hr/>

`self`: `self` is special when it comes to automatic inference of the lifetime of return values. Specifically, the lifetime of a `&self` or `&mut self` argument will always be inferred to be the lifetime of the return value (if lifetimes are elided). 


> https://doc.rust-lang.org/stable/reference/lifetime-elision.html


<hr/>

`Self`: 


> undefined


<hr/>

`static`: You can declare `static` items inside function bodies to get a `static` that only that function has access to (unless it gives out references). This can be handy for implementing singleton-like patterns. 


> https://doc.rust-lang.org/stable/reference/items/static-items.html#statics--generics


<hr/>

`struct`: A tuple-like struct implicitly defines a free-standing function by the same name that acts as the type's constructor. And a unit-like struct implicitly defines a constant by that name! 


> https://doc.rust-lang.org/stable/reference/items/structs.html


<hr/>

`super`: `super` is only permitted to follow either another `super` or an initial `self` in paths, and if it follows a `self` then the `self` is effectively ignored. 


> https://doc.rust-lang.org/stable/reference/paths.html#super


<hr/>

`trait`: Traits can have associated constants, both with and without default values. 


> https://doc.rust-lang.org/stable/reference/items/traits.html


<hr/>

`true`: Even though bools in Rust are generally `u8`s internally, it is illegal for `true` to be represented by anything but `0x01`. This is to enable optimizations that use other bitpatterns to compress state (like Option<bool>::None == 0x02). 


> https://github.com/rust-lang/rfcs/issues/1230


<hr/>

`type`: You cannot construct a type through its type alias name. 


> https://doc.rust-lang.org/stable/reference/items/type-aliases.html


<hr/>

`unsafe`: You don't currently have to use `unsafe {}` to perform unsafe operations inside an `unsafe fn`, though that's likely to get a lint in the future to encourage fine-grained safety tracking (and thinking). 


> https://github.com/rust-lang/rust/issues/71668


<hr/>

`use`: You can use the syntax `use path::to::Trait as _` to bring a trait into scope (so you can call its methods) without also bringing the name into scope. Handy in cases where two traits have the same name for example. 


> https://doc.rust-lang.org/stable/reference/items/use-declarations.html#underscore-imports


<hr/>

`where`: `where` clauses do not _need_ to reference the generic type parameters of the thing they're attached to. You can write, for example: `where String: Clone` if you want to. 


> https://doc.rust-lang.org/stable/reference/items/generics.html#where-clauses


<hr/>

`while`: While loops are particularly handy for cases where the iterator type is useful beyond iteration. For example, if you're iterating over a `Path` (with `Path::iter`), you can call `.as_path()` on the iterator to get the _remaining_ `Path`. 


> https://doc.rust-lang.org/std/path/struct.Iter.html


<hr/>

Okay, learning time! Name a


> undefined


<hr/>

I'm guessing this will be a learning experience as much for me too, as I'm sure there are some I'll have to dig a bit to get at something new and interesting for 😅


> undefined


<hr/>

Also, RIP my mentions


> undefined


<hr/>

I had a conversation about how to get signals about the health of and love for open-source projects recently, and had this (potentially erroneous) thought: bug reports are positive signals, while feature requests are negative.


> undefined


<hr/>

A bug report means that a) someone is using your project, b) they care enough to file an issue, and c) they didn't just immediately switch to another project instead.


> undefined


<hr/>

A feature request _also_ means that someone is using your project and care enough to file, but is additionally an indicator that their needs aren't currently (completely) served by the project. That's not the be-all and end-all, but it _is_ an indication of pain.


> undefined


<hr/>

Big announcement time 📢 For a while now, I've been working on a book that covers the next steps of


> https://nostarch.com/rust-rustaceans


<hr/>

The book is, as its name implies, written for people who are already familiar with Rust. The idea is that you read The Rust Programming Language first, play around with Rust for a bit on your own, maybe start using it "for real", and then pick this up to hone your skills.


> undefined


<hr/>

It's written so that each chapter is more or less standalone, so you can read up on the subjects you want to know more about, rather than having to read through the whole thing start-to-finish. Though of course you can do that too if you want!


> undefined


