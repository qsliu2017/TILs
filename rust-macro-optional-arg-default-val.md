---
date: 20220711
keyword: rust macro
---

# Give optional argument of macro a default value

Use [variadic interface](https://doc.rust-lang.org/rust-by-example/macros/variadics.html). Pattern like

```rust
macro_rules! variadic_macro {
  ($fixed_arg:ident, $optional_arg:ty) => { /* def */ };
  ($fixed_arg:ident) => { variadic_macro!($fixed_arg, usize /* default type */); };
}
```

## Example

Use macro to generate Risc-V CSR read function, where the default type of register value is `u64`.

```rust
macro_rules! csrr {
    ($reg:ident) => { csrr!($reg, u64); };
    ($reg:ident, $ty:ty) => {
        #[inline]
        pub fn read() -> $ty {
            let mut x: $ty;
            unsafe {
                core::arch::asm!(concat!("csrr {}, ", stringify!($reg)), out(reg) x);
            }
            x
        }
    };
}
```

`csrr!(mstatus);` will generate:

```rust
#[inline]
pub fn read() -> u64 {
    let mut x: u64;
    unsafe {
        core::arch::asm!("csrr {}, mstatus"), out(reg) x);
    }
    x
}
```

`csrw!(satp, *const usize);` will generate:

```rust
#[inline]
pub fn read() -> *const usize {
    let mut x: *const usize;
    unsafe {
        core::arch::asm!("csrr {}, satp"), out(reg) x);
    }
    x
}
```
