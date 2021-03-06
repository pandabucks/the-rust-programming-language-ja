--- a/src/doc/book/choosing-your-guarantees.md
+++ b/src/doc/book/choosing-your-guarantees.md
@@ -52,7 +52,7 @@ These pointers cannot be copied in such a way that they outlive the lifetime ass
 
 ## `*const T` and `*mut T`
 
-These are C-like raw pointers with no lifetime or ownership attached to them. They just point to
+These are C-like raw pointers with no lifetime or ownership attached to them. They point to
 some location in memory with no other restrictions. The only guarantee that these provide is that
 they cannot be dereferenced except in code marked `unsafe`.
 
@@ -204,7 +204,7 @@ borrow checker. Generally we know that such mutations won't happen in a nested f
 to check.
 
 For large, complicated programs, it becomes useful to put some things in `RefCell`s to make things
-simpler. For example, a lot of the maps in [the `ctxt` struct][ctxt] in the Rust compiler internals
+simpler. For example, a lot of the maps in the `ctxt` struct in the Rust compiler internals
 are inside this wrapper. These are only modified once (during creation, which is not right after
 initialization) or a couple of times in well-separated places. However, since this struct is
 pervasively used everywhere, juggling mutable and immutable pointers would be hard (perhaps
@@ -235,7 +235,6 @@ At runtime each borrow causes a modification/check of the refcount.
 [cell-mod]: ../std/cell/
 [cell]: ../std/cell/struct.Cell.html
 [refcell]: ../std/cell/struct.RefCell.html
-[ctxt]: ../rustc/middle/ty/struct.ctxt.html
 
 # Synchronous types
 
@@ -255,7 +254,7 @@ major ones will be covered below.
 
 ## `Arc<T>`
 
-[`Arc<T>`][arc] is just a version of `Rc<T>` that uses an atomic reference count (hence, "Arc").
+[`Arc<T>`][arc] is a version of `Rc<T>` that uses an atomic reference count (hence, "Arc").
 This can be sent freely between threads.
 
 C++'s `shared_ptr` is similar to `Arc`, however in the case of C++ the inner data is always mutable.
@@ -340,11 +339,11 @@ With the former, the `RefCell<T>` is wrapping the `Vec<T>`, so the `Vec<T>` in i
 mutable. At the same time, there can only be one mutable borrow of the whole `Vec` at a given time.
 This means that your code cannot simultaneously work on different elements of the vector from
 different `Rc` handles. However, we are able to push and pop from the `Vec<T>` at will. This is
-similar to an `&mut Vec<T>` with the borrow checking done at runtime.
+similar to a `&mut Vec<T>` with the borrow checking done at runtime.
 
 With the latter, the borrowing is of individual elements, but the overall vector is immutable. Thus,
 we can independently borrow separate elements, but we cannot push or pop from the vector. This is
-similar to an `&mut [T]`[^3], but, again, the borrow checking is at runtime.
+similar to a `&mut [T]`[^3], but, again, the borrow checking is at runtime.
 
 In concurrent programs, we have a similar situation with `Arc<Mutex<T>>`, which provides shared
 mutability and ownership.
diff --git a/src/doc/book/closures.md b/src/doc/book/closures.md
