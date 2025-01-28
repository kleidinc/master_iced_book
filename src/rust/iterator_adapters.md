# Iterator Adapters Methods

### last

```rust
fn last(self) -> Option<Self::Item>
where
    Self: Sized,
```

Consuming the iterator, returning the last element.

This method will evaluate the iterator until it returns `None`. While doing
so, it keeps track of the current element. After None is returned, `last()`
will then return the last element it saw.

```rust
let a = [1,2,3];
assert_eq!(a.iter().last(), Some(&3))
```

### advance_by

### nth

Returns the nth element of an iterator.

Like most indexing operations, the count starts from 0, so `nth(0)` returns the first value, `nth(1)`
returns the second, and so on.

Note that all preceding elements, as well as the returned element, will be consumed from the iterator.
That means that the preceding elements will be discarded, and also that calling the `nth(0)` multiple
times on the same iterator will return different elements.

`nth()` will return `None` if the n is greater than or equal to the length of the
iterator.

### step_by

### chain

Takes two iterators and creates a new iterator over both in sequence.

### zip

'Zips up' two iterators into a single iterator of pairs.

### map

```rust
fn map<B,F>(self, f: F) -> Map<Self,F>
where
    Self: Sized,
    F: FnMut(Self::Item) -> B
```

Takes a closure and creates an iterator which calls that closure on each element.

`map()` transforms one iterator into another, by means of its argument: something that implements `FnMut`.
It produces a new iterator which calls this closure on each element of the original iterator.
