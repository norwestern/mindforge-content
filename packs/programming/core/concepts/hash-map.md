---
title: Hash Map
tier: 2
prerequisites:
  - arrays
backstory: "Before hash maps, finding a value in a collection meant scanning every element — O(n). As datasets grew, that linear scan became the bottleneck. The hash map trades a little memory and a hash function for average O(1) lookup, insert, and delete. It exists to answer one question fast: have I seen this before, and what is it mapped to?"
---

# Hash Map

A **hash map** stores key/value pairs and gives you average **O(1)** lookup.

## The problem it solves

Searching an unsorted array for a key is **O(n)** — you may touch every element. When you do many lookups, that cost dominates.

## The idea

A *hash function* turns a key into an array index. You store the value at that index, so finding it later is direct — no scan.

## The catch: collisions

Two keys can hash to the same index. Real hash maps resolve this (chaining or open addressing). Worst case degrades to O(n), but with a good hash function the average stays O(1).

## When to reach for it

- Counting frequencies
- De-duplicating
- 'Have I seen this value?' lookups
- Caching computed results
