---
date: 20220704
keyword: rust
---

# Iterate by window

Use standard library to implement window iterate:

```rust
let x = &[1, 2, 3, 4, 5, 6];
let expect = vec![(&1, &2), (&2, &3), (&3, &4), (&4, &5), (&5, &6)];

let iter = zip(x.iter(), x.iter().skip(1));
assert_eq!(expect, iter.collect::<Vec<(&i32, &i32)>>());

// before 1.59.0
let iter_not_support_iter_zip = x.iter().zip(x.iter().skip(1));
assert_eq!(
    expect,
    iter_not_support_iter_zip.collect::<Vec<(&i32, &i32)>>(),
);
```
