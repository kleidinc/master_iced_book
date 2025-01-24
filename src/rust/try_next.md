# Trait Stream

## Trait Stream

```rust
pub trait Stream  {
    type Item;

    // Required method
    fn poll_next(
        self: Pin<&mut Self>,
        cx: &mut Context<'_>a,
    ) -> Poll<Option<Self::Item>>;

    // Provided method
    fn size_hint(&self) -> (usize, Option<usize>) {...}
}
```

A stream of values produced asynchronously.

If Future`<Output = T>` is an asynchronously version of `T`, then `Stream<Item = T>` is an asynchronously version of
`Iterator<Item = T>`. A stream represents a sequence of value-producing events that occur asynchronously to the
caller.

The trait is modeled after `Future`, but allows `poll_next` to be called even after a value has been produced,
yielding None once the stream is fully exhausted.

### Required Associated Types

```rust
type Item
```

Values yielded by a stream.

### Required methods

```rust
fn poll_next(
    self: Pin<&mut Self>,
    cx: &mut Context<'_>,
) -> Poll<Option<Self::Item>>
```

Attempt to pull out the next value of this stream, registering the current task for wakeup if the value is not yet
available, and returning None if the stream is exhausted.

_Return Value_
There are several possible return values, each indicating a distinct stream state:

- `Poll::Pending` means that this stream's next value is not yet ready. Implementations will ensure that the current
  task will be notified when the next value may be ready.
- `Poll::Ready(Some(val))` means that the stream has successfully produced a value, val, and may produce further values
  on subsequent `poll_next` calls.
- `Poll::Ready(None)` means that the stream has terminated, and `poll_next` should not be invoked again.

## Pin

```rust
#[repr(transparent)]
pub struct Pin<Ptr> { /* private fields */}
```

A pointer which it its pointee in place.

`Pin` is a wrapper around some kind of pointer `Ptr` which makes that pointer `pin` its pointee value in place ,thus
preventing the value referenced by that pointer from being moved or otherwise invalidated at that place in memory
unless it implements `Unpin`.

### What is the use case of `Pin`

The most common set of types which require pinning related guarantees for soundness are the compiler-generated
state machines that implement `Future` for the return value of `async fns`. These compiler-generated `Futures`
may contain self-referential pointers, one of the most common use-cases for `Pin`.

This requirement for the implementation of `async fns` means that the `Future` trait requires all calls to `poll`
to use a `self::Pin<&mut Self>` parameter instead of the usual `&mut Self`. Therefore, when manually polling a
future, you will need to pin it first.

When `Unpin` is implemented, then you can access the value being a Pin pointer, `Pin<&mut Self>` just like you
would access a `&mut Self`, without caring about the `Pin`. Only types that don't implement `Unpin` are
restricted.

### Pinning a value that implements `Unpin`

```rust
use std::pin::Pin;
// Create a value of a type that implements `Unpin`
let mut unpin_future = std::future::ready(5);

// Pin it by creating a pinning mutable reference to it (ready to be polled)
let my_pinned_unpin_future: Pin<&mut _> = Pin::new(&mut unpin_future);
```

### Pinning a value inside a Box

```rust
use std::pin::Pin;

async fn add_one(u: u32) -> u32 {
    x + 1
}

// the async function to get a future back
let fut = add_one(42);

// Pin the future inside a pinning box
let pinned_fut: Pin<Box<_>> = Bon::pin(fut);
```

If you have a value that is already boxed, for example a `Box<dyn Future>`, you can pin that value in-place
at its current memory address using `Box::into_pin`

```rust
use std::pin::Pin;
use std::future::Future;

async fn add_one(x: u32) -> u32 {
    x + 1
}

fn boxed_add_one(u: 32) -> Box<dyn Future<Output = u32>> {
    Box::new(add_one(x))
}

let boxed_fut = boxed_add_one(42);

// Pin the future inside the existing box
let pinned_fut: Pin<Box<_>> = Box::into_pin(boxed_fut);
```
