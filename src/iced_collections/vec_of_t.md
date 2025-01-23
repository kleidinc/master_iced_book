# Showing a Vec

### 1. First check is there is actually a Some(T) or a None

If None you can just show nothing or a place-holder.

### 2. Now iterate over Vec<T> and ...

What you need to do for each item in the Vec<T>, is to create an Element,
which you can collate, in the end, into a column of elements, where each
element represents each item.

You can't change the data in the Vec<T> in place, because that could change
the types, so you have to either create a new vector of elements, or push it
out immediately?
