# ania

Fast and simple external memory reading library for Linux

## Features
- `process_vm_readv` based reading (best method on Linux)
- Optional configurable random delay
- Clean C-like API
- Easy process and module finding

## Example

```rust
use ania_memory::*;

fn main() {
    let cs2 = find_process_from_name("cs2".to_string());
    let client = find_module_from_name("libclient.so".to_string(), &cs2);

    let local_pawn = read_u64(&cs2, client.base + 0x206A9E0);
    let health = read_u32(&cs2, local_pawn + 0x354);

    println!("Health: {}", health);
}
