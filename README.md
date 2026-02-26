# LibString

A lightweight C++ string utility library designed for embedded or performance-critical applications. `LibString` provides a minimal subset of `std::string` functionality with a focus on efficiency, predictable memory usage, and a small code footprint.

---

## 🔧 Purpose & Use Cases

`LibString` was created to offer a simple replacement for the STL `std::string` in environments where the standard library is unavailable, too heavy, or where deterministic behavior is required. The class uses a 22‑byte small‑string buffer by default; heap allocations are only introduced when data outgrows that buffer or when UTF‑32 storage is needed. Typical scenarios include:

- Embedded systems with limited RAM/ROM
- Game engines or real-time applications needing fast, inline operations
- Educational projects demonstrating string manipulation internals
- Codebases avoiding dynamic allocations or exceptions

---

## ✅ Features

- Basic string operations: concatenation, comparison, length queries
- Null‑terminated C-style access when needed
- Header‑only implementation (see `String.hpp` and `CharUtils.hpp`)
- Unit tests included (`StringTest.cpp`) to verify correctness

---

## ⚖️ Advantages

1. **Small Footprint** – no dependency on the full C++ standard library
2. **Deterministic behavior for small strings** – uses small‑string optimization (SSO) to keep short, pure‑ASCII content entirely on the object itself. Heap allocations only occur when a string grows beyond the SSO buffer or when non‑ASCII (UTF‑32) data is required.
3. **Easy to read and extend** – source code is intentionally minimal and commented
4. **Header-only** – drop‑in; just include the headers in your project

---

## ⚠️ Limitations

- Not a drop‑in replacement for all `std::string` APIs
- Lacks locale/encoding support and advanced algorithms
- Manual bounds checking; users must take care with capacities
- Intended for simple use cases; not optimized for large or complex text processing
- Will allocate on the heap once strings exceed the small‑buffer limit or require UTF‑32 encoding

---

## 📦 Getting Started

1. Copy `String.hpp` and `CharUtils.hpp` into your project
2. Include the header where you need string functionality:

   ```cpp
   #include "String.hpp"
   ```

3. Run the provided test (`StringTest.cpp`) with your preferred C++ compiler to ensure everything works.

---

## 🧠 Design Notes

The implementation favors clarity over cleverness; functions are implemented with simple loops. A small‑string buffer (22 bytes) lives inside the `String` object; when only ASCII data fits, everything stays on the stack. The code switches to `std::vector`‑backed "HEP" modes for larger strings or when decoding UTF‑8, which is where heap allocations occur.

Happy coding! 🚀
