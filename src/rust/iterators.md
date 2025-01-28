# Iterators

```rust
trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item> ;
}
```

### 3 Forms of Iteration

1. iter() - which iterates over &T.
2. iter_mut() - which iterates over &mut T.
3. into_iter() - which iterates over T.

### Iterating by Reference

```rust
let mut values = vec![41];
for x in values.iter_mut() {
    *x +=1;
}
for x in value.iter() {
    assert_eq!(*x,42);
}
assert_eq!(values.len(),1);
```

If a collection type C provider iter(), it usually also implements
IntoIterator for &C, with an implementation that just calls iter().

Likewise, a collection C that provides iter_mut() generally implements
IntoIterator for &mut C by delegating to iter_mut(). This enables a
convenient shorthand.

```rust
let mut values = vec![41];
for x in &mut values {  // same as iter_mut()
    *x += 1;
}
for x in &values {  // same as iter()
    assert_eq!(*x, 42);
}
assert_eq!(values.len(), 1);
```

While many collections offer iter(), not all offer iter_mut(). For
example, mutating the keys of a `HashSet<T>` could put the collection
into an inconsistent state if the key hashes change, so this collection
only offers iter().

### Adapters

Functions which take an Iterator and return another Iterator are
often called `iterator adapters`, as they're a form of the
`adapter pattern`.

Common iterator adapters are `map`, `take`, and `filter`.

If an iterator adapter panics, the iterator will be in a unspecified
(but memory safe) state. This state is not guaranteed to stay the
same across versions of Rust, so you should avoid relying on the
exact values returned by an iterator which panicked.

### Laziness

Iterators (and iterator adapters) are lazy. This means that just creating
an iterator doesn't do a whole lot. Nothing really happens until you call
`next`. This is sometimes a source of confusion when creating an iterator
solely for its side effects. For example, the `map` method calls a closure
on each element it iterates over:

```rust
let v = vec![1,2,3,4,5];
v.iter().map(|x| println!("{x}"));
```

This will not print any values, as we only created an iterator, rather
than using it.

### Idiomatic way to write a `map` for its side effects is to use

a `for loop` or call the `for_each` method:

```rust
let v = vec![1,2,3,4,5];
v.iter().for_each(|x| println!("{x}"));
// or
for x in &v {
    println!("{x}");
}
```

Another common way to evaluate an iterator is to use the `collect`
method to produce a new collection.

### Infinity

Iterators don't have to be finite. As an example, an open-ended range is
an `infinite iterator`:

```rust
let numbers = 0..;
```

It is common to use the `take` iterator adapter to turn an infinite
iterator into a finite one:

```rust
let numbers = 0..;
let five_numbers = numbers.take(5);

for number in five_numbers {
    println!("{number}");
}
```

Bear in mind that methods on infinite iterators, even those for which
a result can be determined mathematically in finite time, might not
terminate. Specifically, methods such as min, which in the general case
require traversing every element in the iterator, are likely not to
return successfully for any infinite iterators.

```rust
let ones = std::iter::repeat(1);
let least = ones.min().unwrap(); // infinite loop
```
