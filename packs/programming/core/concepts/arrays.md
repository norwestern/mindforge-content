---
title: Arrays
tier: 1
prerequisites: []
backstory: "Before arrays, every value needed its own named variable — there was no way to ask for 'the 47th item' without writing 47 separate variables, and looping over 'all of them' was impossible. The array invented contiguous, indexed memory: one block, one base address, and index arithmetic (base + i × size) makes any element reachable in O(1). It exists to answer one question fast: given a position, what's the value there — and let you loop over many same-typed values as a single unit."
---

# Arrays

An **array** stores values of the same type in contiguous memory, reachable instantly by index.

## The problem it solves

Without an indexed structure, finding "the nth thing" or looping over many values means juggling separate variables — it doesn't scale past a handful of items.

## The idea

Because every element is the same size and laid out back-to-back, the address of element `i` is just `base + i * size` — no searching required, O(1) access.

## The catch: resizing and shifting

Arrays have a fixed underlying block. Inserting or removing in the middle (or at the front) means shifting every element after it — O(n). Growing past capacity means allocating a new, bigger block and copying everything over.

## When to reach for it

- You need fast access by position
- You know the size up front, or appends are mostly at the end
- You want to iterate over a fixed collection in order
