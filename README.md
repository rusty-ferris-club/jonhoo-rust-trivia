# What is this?

Once upon a time, [Jon Gjengset](https://twitter.com/jonhoo) did a [Rust trivia on Twitter](https://twitter.com/jonhoo/status/1532761983606411264). This is the thread, unrolled and cleaned up ([with permission](https://twitter.com/jonhoo/status/1537819805121511424)):

:nerd_face: You can also check out the [keywords thread](keywords.md).

## Rust Trivia

[`TcpStream`](https://twitter.com/carllerche/status/1532773523667660800)

> Did you know that in its default configuration, TcpStream uses Nagle's Algorithm to schedule packet sends (https://en.wikipedia.org/wiki/Nagle%27s_algorithm), which can introduce unfortunate latency spikes. If you're particularly latency sensitive, consider calling TcpStream::set_nodelay(true)

[`std::fmt::Debug`](https://twitter.com/byblakeorriver/status/1532929909525319681)

> Did you know that the `Formatter` argument to `Debug::fmt` makes it _really_ easy to customize debug representations for structs, enums, lists, and sets? See the `debug_*` methods on it and

[`Formatter`](https://twitter.com/ChevyRay/status/1532864527649615872)

> Did you know that std::fmt::Formatter is _super_ easy to use if you want more control over debugging for a custom type. For example, to emit a "list-like" type, just Formatter::debug_list().entries(self.0.iter()).finish()

[`Option<T>`](https://twitter.com/nomad421/status/1532764636994490369)

> Did you know that Option<T> implements IntoIterator yielding 0/1 elements, and you can then call Iterator::flatten to make that be 0/n elements if T: IntoIterator?

[`std::sync::mpsc::channel::Sender`](https://twitter.com/strangecasts/status/1532771830653755394)

> Did you know that std::sync::mpsc has had a known bug since 2017 (https://github.com/rust-lang/rust/issues/39364), and that the implementation may actually be replaced entirely with the crossbeam channel implementation? https://github.com/rust-lang/rust/pull/93563

[`type EmptyTupleList = Vec<()>:`](https://twitter.com/nevi_me/status/1532772034291310592)

> Did you know that since () is a zero-sized type, and the vector never actually has to store any data, the capacity of Vec<()> is usize::MAX!

[`Box<T>`](https://twitter.com/jafagervik/status/1532762282320617474)

> Did you know that Box<T> is a #[fundamental] type, which means that it's exempt from the normal rules that don't allow you to implement foreign traits for foreign types (assuming T is a local type)?

[`T`](https://twitter.com/bnwlfsnNYT/status/1532798173567139842)

> Did you know that T doesn't imply ownership? When we say a type is generic over T, that T can just as easily be a reference to something on the stack, and the type system will still be happy. Even T: 'static doesn't imply owned — consider &'static str for example.

[`u128`](https://twitter.com/llogiq/status/1532812061603930118)

> Did you know that even though we got u128 a long time ago now, we still don't have repr(128)? https://github.com/rust-lang/rust/issues/56071

[`std::ffi::OsString`](https://twitter.com/pfesenmeier/status/1532770956690726914)

> Did you know that there are per-platform extension traits for OsString that bake in the assumptions you can safely make on that platform? Such as strings being [u8] on Unix (https://doc.rust-lang.org/std/os/unix/ffi/trait.OsStringExt.html) and UTF-16 on Windows (https://doc.rust-lang.org/std/os/windows/ffi/trait.OsStringExt.html).

[`std::ptr::NonNull`](https://twitter.com/i_ppetkov/status/1532855639503843328)

> Did you know that one of the super neat features of NonNull is that it enables the same niche optimization that regular references and the NonZero* types get where Option<NonNull<T>> is the same size as *mut T?

[`Cow<T>`](https://twitter.com/maddymakesgames/status/1532770820262612999)

> Did you know that there used to be a special IntoCow trait, but it was deprecated before 1.0 was released!
> https://github.com/rust-lang/rust/issues/27735

[`std::process::Child`](https://twitter.com/oconnor663/status/1532964962137649152)

> Did you know that std has three different ways to spawn a child process on Linux (posix_spawn, clone3/exec, fork/exec) depending on what capabilities your kernel version has? https://github.com/rust-lang/rust/blob/master/library/std/src/sys/unix/process/process_unix.rs

[`Pin<T>`](https://twitter.com/tyrannican/status/1532763198897758209)

> Did you know that the name Pin (and the name Unpin) where both _heavily_ debated? Pin was almost called Pinned, for example. The discussion in https://github.com/rust-lang/rust/issues/55766#issuecomment-438789462 is an interesting read now after the fact.

[`CString`](https://twitter.com/maxleiko/status/1532762451065847808)

> I'm going to pretend you said CStr, and say: did you know that CStr::default creates a CStr that points to a const string "0" stored in the binary text segment, which means all default CStrs point to the same (non-null) string!

[`f32`](https://twitter.com/GolDDranks/status/1532797144310198272)

> Did you know that in Rust 1.62 we'll get a deterministic ordering function for floating point numbers? https://github.com/rust-lang/rust/pull/95431

[`Vec<T>`](https://twitter.com/DailyCatBattle/status/1532762260266962944)

> Did you know that Vec::swap_remove is _way_ faster than Vec::remove if you can tolerate changes to ordering?

[and also](https://twitter.com/Gankra_/status/1532798237161168896)

> But since it's you, here's another: did you know that the smallest non-zero capacity for a Vec<T> depends on the size of T? https://github.com/rust-lang/rust/blob/9a74608543d499bcc7dd505e195e8bfab9447315/library/alloc/src/raw_vec.rs#L106-L110

[`for<'a> SomeTrait<'a>`](https://twitter.com/jdonszelmann/status/1532786263035633667)

> Did you know that you can use for<'a> to say that a bound has to hold for _any_ lifetime 'a, not just a _specific_ lifetime you happen to have available at the time. For example, <T> for<'a>: &'a T: Read says that _any_ shared reference to a T must implement Read.

[`FnOnce`](https://twitter.com/ArthurMilchior/status/1532812759641071623)

> Did you know that until Rust 1.35, you couldn't call a Box<dyn FnOnce> and needed a special type (FnBox) for it! This was because it requires "unsized rvalues" to implement, which are still unstable today. https://github.com/rust-lang/rust/issues/28796 + https://github.com/rust-lang/rust/issues/48055

[`Rc<T>`](https://twitter.com/vasishath/status/1532773971099193344)

> Did you know that the Rc type was among the arguments for why std::mem::forget shouldn't be marked as `unsafe`? https://github.com/rust-lang/rust/issues/24456

[`std::thread::Thread`](https://twitter.com/UncannyInfinity/status/1532771680220741632)

> Did you know that the ThreadId that's available for each Thread is entirely a std construct? Creating a ThreadId simply increments a global static counter under a lock.

[`Arc<T>`](https://twitter.com/BinSlashBash/status/1532764686181093376)

> Did you know that Arc has a make_mut method that effectively gives you copy-on-write? Given a &mut Arc<T>, it will either give you &mut T if there are no other Arcs, or it will clone T, make the Arc<T> point to that new T, and then give you a &mut to it!

[`!`](https://twitter.com/panna_pudi/status/1532762409068290048)

> Did you know that std::convert::Infallible is the "original" !, and that the plan is to one day replace Infallible with a type alias for !?

[`fn`](https://twitter.com/anotherwalther/status/1532765117028483073)

> Specifically, did you know that the name of a function is _not_ an fn? It's a "FnDef", which can then be coerced to a "FnPtr": https://github.com/rust-lang/rust/issues/86654#issuecomment-869173835

[`PhantomData`](https://twitter.com/dss_gabriel/status/1532763980887883776)

> Did you know that it's actually kind of tricky to define PhantomData yourself: https://github.com/dtolnay/ghost

[`std::os::unix::net::UnixStream`](https://twitter.com/urcyanide/status/1532889075614527489)

> Did you know that (on nightly) you can pass UNIX file descriptors over UnixStreams too, and thereby give another process access to a file it may not otherwise be able to open? https://doc.rust-lang.org/std/os/unix/net/struct.SocketAncillary.html#method.add_fds

[`std::sync::Condvar`](https://twitter.com/mithridates/status/1532764893908447233) (and `Mutex`)

> Did you know that Mara is doing some _awesome_ work on making Condvar (and Mutex and RwLock) much better on a wide array on platforms? https://github.com/rust-lang/rust/issues/93740

[`bool`](https://twitter.com/pnkfelix/status/1532809057576357889)

> Did you know that bool isn't just "stored as a byte", the compiler straight up declares its representation as the same as that of u8? https://github.com/rust-lang/rust/blob/master/compiler/rustc_middle/src/ty/layout.rs#L676-L682

[`Any`](https://twitter.com/dmilith/status/1532763659281260546)

> Did you know that Any is _really_ non-magical? It just has a blanket implementation for all T that returns TypeId::of::<T>(), and to downcast it simply compares the return value of that trait method to see if it's safe to cast to downcast to a type! TypeId _is_ magic though.

[`Self`](https://twitter.com/rcjmurillo/status/1532846789199400961)

> Did you know that `fn foo(self)` is syntactic sugar for `fn foo(self: Self)`, and that one day you'll be able to use other types for `self` that involve `Self`, like `fn foo(self: Arc<Self>)`. https://github.com/rust-lang/rust/issues/44874

[`File`](https://twitter.com/4mehrJungs/status/1532803886049898499)

> Did you know that there are implementations of Read, Write, and Seek for &File as well, so multiple threads can share a single File and call those concurrently. Whether they _should_ is a different question of course.

[`u32`](https://twitter.com/Floppie7th/status/1532762373508976642)

> Did you know that u32 now has associated constants for MIN and MAX, so you no longer need to use std::u32::MIN and can use u32::MIN directly instead.

[`BTreeMap<K, V>`](https://twitter.com/lucperkins/status/1532762512512339968)

> Did you know that BTreeMap is one of the few collections that still doesn't have a drain method? https://github.com/rust-lang/rust/issues/81074

[`struct InvariantLifetime<'id>(PhantomData<*mut &'id ()>);`](https://twitter.com/Firefighterduck/status/1532778909988794370)

> Did you know that PhantomData<T> has variance like T, and *mut T is invariant over T, and so by placing a lifetime inside T you make the outer type invariant over that lifetime?

[`std::future::Ready`](https://twitter.com/brandonhgomes/status/1533004866670452737)

> Did you know that these days you can just use `async move { x }`  instead of `future::ready(x)`. The main reason to still use `future::ready(x)` is that you can name the future it returns, which is harder with `async` (without `type_alias_impl_trait` that is).

[`usize`](https://twitter.com/xTeKc/status/1532845646855692289)

> Did you know that `usize` isn't really "the size of a pointer". Instead, it's more like "the size of a pointer address difference", and the two can be fairly different! https://github.com/rust-lang/rust/issues/95228

[`RefCell`](https://twitter.com/monsieurbadia/status/1532768919332732936)

> Did you know that RefCell allows you to replace a value in-place directly (like std::mem::replace)? https://doc.rust-lang.org/std/cell/struct.RefCell.html#method.replace

[`PanicInfo`](https://twitter.com/epicevilmusic/status/1532909291916693504)

> Did you know that since PanicInfo is in `core`, its Display implementation cannot access the panic data if it's a String (since it can't name that type), so trying to print the PanicInfo after a std::panic::panic_any(format!("x y z")) won't print "x y z"? https://github.com/rust-lang/rust/blob/352e621368c31d7b4a6362e081586cdb931ba020/library/core/src/panic/panic_info.rs#L159-L162

[`core::num::Wrapping`](https://twitter.com/kaidokert/status/1532771465837174784)

> Did you know that there used to also be a trait accompanying Wrapping, WrappingOps, that was removed last minute before 1.0? https://github.com/rust-lang/rust/pull/23549

[`*const T`](https://twitter.com/13erbse/status/1532764790975864833)

> Did you know that, at least for the time being, *const T and *mut T are more or less equivalent? https://github.com/rust-lang/unsafe-code-guidelines/issues/257

[`std::task::Waker`](https://twitter.com/mx00s/status/1532792050034221056)

> Did you know that Waker is secretly just a `dyn std::task::Wake + Clone` done in a way that doesn't require a wide pointer or support for multi-trait dynamic dispatch? See https://doc.rust-lang.org/std/task/struct.RawWakerVTable.html

[`impl Trait`](https://twitter.com/moduledoc/status/1532769238921859072)

> Did you know that impl Trait in argument position and impl Trait in return position represent completely different type constructs, even though they "feel" related? https://doc.rust-lang.org/nightly/reference/types/impl-trait.html

[`std::ops::ControlFlow`](https://twitter.com/chrismhanks/status/1532767802549063681)

> Did you know that ControlFlow is really a stepping stone towards making ? work for other types than Option and Result? The full design has gone through a _lot_ of iterations, but the latest and greatest is RFC3058: https://github.com/rust-lang/rust/issues/84277

[`Result<T, E>`](https://twitter.com/jaaaarwr/status/1532765735277166598)

> Did you know that Rust originally (pre-1.0) had both Result _and_ an Either type? They decided to remove Either way back in 2013: https://github.com/rust-lang/rust/issues/9157

[`Cow<str>`](https://twitter.com/Absolucyyy/status/1532903829636886529)

> Did you know that because Cow<'a, T> is covariant in 'a, you can always assign Cow::Borrowed("some string") to one no matter what it originally held?

[`struct S` and `()`](https://twitter.com/ekuber/status/1532764579641425921)

> That's cheating, but I'll bite.
>
> Did you know that () implements FromIterator, so you can .collect::<Result<(), E>> to _just_ see if anything in an iterator erred?
>
> Did you know that struct S implicitly declares a constant called S, which is why you can make one using just S?

[`std::ffi::c_void`](https://twitter.com/ematipico/status/1532824299161239552)

> Did you know that the whole c_void type is a collection of hacks to try to work around the lack for extern types? https://github.com/rust-lang/rust/issues/43467

[`u256`](https://twitter.com/junderwood4649/status/1533014451015757824)

> Did you know that because Rust compiles through LLVM, we're sort of constrained to the primitive types LLVM supports, and LLVM itself only goes up to 128? https://llvm.org/doxygen/classllvm_1_1Type.html#pub-static-methods

[`u8`](https://twitter.com/jakevossen5/status/1532762509467299841)

> Did you know that as of Rust 1.60, you can now use u8::escape_ascii to get an iterator of the bytes needed to escape that byte character in _most_ contexts: https://doc.rust-lang.org/std/ascii/fn.escape_default.html

[`#[feature(raw_ref_op)] &raw const T`](https://twitter.com/chyyran/status/1532804582417522689)

> Definitely cheating :p But did you know that originally the intention was to have &const raw variable be just a MIR construct and let &variable as *const _ be automatically changed to &const raw? https://github.com/RalfJung/rfcs/blob/fd4b4cd769300cfde5d54865d227990b71b762d1/text/0000-raw-reference-operator.md

[`std::ops::Hash`](https://twitter.com/punkeel/status/1532890659140644865)

> Did you know that Hash is responsible for not just one, but _two_ of the issues on the "rust 2 breakage wishlist"?
> https://github.com/rust-lang/rust/issues/29263
> https://github.com/rust-lang/rust/issues/65744

[`_`](https://twitter.com/bsto0403/status/1532773696175235074)

> Did you know that whether or not let _ = x should move x is actually fairly subtle? https://github.com/rust-lang/rust/issues/10488

[`MaybeUninit`](https://twitter.com/NeubauerTroy/status/1532762670629376001)

> Did you know that MaybeUninit arose because the previous mechanism, std::mem::uninitialized, produced _immediate_ undefined behavior when invoked with _most_ types (like uninitialized::<bool>()).

[`struct T<const C: usize>`](https://twitter.com/c_o_n_s_o_l_i/status/1532804383460757505)

> Did you know that with Rust 1.59.0 you can now give C a default value? https://blog.rust-lang.org/2022/02/24/Rust-1.59.0.html#const-generics-defaults-and-interleaving

[`Weak<T>`](https://twitter.com/Seewishnew/status/1532811823338008576)

> Did you know that actual deallocation logic for Arc<T> is implemented in Weak<T>, and is invoked by considering all copies of a particular Arc<T> to _collectively_ hold a single Weak<T> between them? https://github.com/rust-lang/rust/blob/7e9b92cb43a489b34e2bcb8d21f36198e02eedbc/library/alloc/src/sync.rs#L1108-L1109

[`[T; N]`](https://twitter.com/Slctvdplcate/status/1532768315651006464)

> Did you know that while _most_ trait implementations for arrays now use const generics to impl for any length N, we can't _yet_ do the same for Default: https://github.com/rust-lang/rust/blob/e40d5e83dc133d093c22c7ff016b10daa4f40dcf/library/core/src/array/mod.rs#L371-L394

[`HashMap<K, V>`](https://twitter.com/CompilersJay/status/1532842262995927040)

> Did you know that the Rust devs are working on a "raw" entry API for HashMap that allows you to (unsafely) avoid re-hashing a key you've already hashed? https://github.com/rust-lang/rust/issues/56167

[`&mut T`](https://twitter.com/the_abhizer/status/1532766405124567040)

> Did you know that while &mut T is defined as meaning "mutable reference" in the Rust reference, you're often better off thinking of it as "mutually exclusive reference". Quoth David Tolnay: https://docs.rs/dtolnay/latest/dtolnay/macro._02__reference_types.html

[`std::ops::Range`](https://twitter.com/SheWhoCannotTan/status/1532794851900764161)

> Did you know that there's been a _lot_ of debate around whether or not the Range types should be Copy? https://github.com/rust-lang/rust/pull/21846

[`AtomicU32`](https://twitter.com/Urhengula5/status/1532767727286370305)

> Did you know that you'll often want compare_exchange_weak over compare_exchange to get more efficient code on ARM cores: https://devblogs.microsoft.com/oldnewthing/20180329-00/?p=98375

[`{integer}`](https://twitter.com/nasso4991/status/1532765663772672000)

> Did you know that fasterthanlime's most recent article does a great job at explaining `{integer}`? https://fasterthanli.me/articles/the-curse-of-strong-typing#different-kinds-of-numbers

[`Fn`](https://twitter.com/qwellter/status/1532765065086132227)

> Did you know that until Rust 1.35.0, Box<T> where T: Fn did not impl Fn, so you couldn't (easily) call boxed closures! https://github.com/rust-lang/rust/pull/55431

[`((), ())`](https://twitter.com/pnkfelix/status/1533248925397819394?t=mV9c7PNAdw03_GaMUz-F4Q&s=19)

> Did you know that ((), ()) and () have the same hash? https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=894b78e8ee2721440aa8dea5e35f9dc3

[`[T]`](https://twitter.com/NyxMC/status/1533276185748193280?t=PbXx58vxDy41PLv2CfSLxQ&s=19)

> Did you know that &[u8] implements Read and Write? So for anything that takes impl Read, you can provide &mut slice instead! Comes in handy for testing. Note that the slice itself is shortened for each read, hence &mut &[u8].

[`*`](https://twitter.com/o_uz_a/status/1532822488400416770)

> Did you know that `*` is (mostly) just syntax sugar for the std::ops::Mul trait?

[`UnsafeCell<T>`](https://twitter.com/Nilstrieb/status/1532763412370972673)

> Did you know that UnsafeCell is one of those types that the compiler needs "special magic" for because it has to instruct LLVM to _not_ assume Rust's normal aliasing rules hold once code traverses the boundary of any UnsafeCell?
