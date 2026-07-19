---
title: Two Pointers
tier: 2
prerequisites:
  - arrays
backstory: "Before two pointers, finding a pair in a sorted collection meant checking every pair against every other — O(n^2) nested loops. Once you know the data is sorted, you don't need to recheck: if the current pair sums too high, the only way down is moving the high pointer left; too low, the only way up is moving the low pointer right. Two pointers trades the brute-force search for a single O(n) sweep — the first lesson in using what you already know about the data to throw away work."
---

# Two Pointers

The **two-pointer technique** scans a sorted collection from both ends inward, using one comparison to decide which pointer moves.

## The problem it solves

Checking every pair in a collection for a property (like "do any two values sum to X?") costs O(n^2) — every element compared against every other.

## The idea

If the collection is sorted, the current pair's sum tells you everything: too high means the high pointer must come down, too low means the low pointer must go up. No comparison is ever redone — one O(n) sweep replaces nested loops.

## The catch: it needs sorted input

Two pointers only works because sorted order lets you trust "moving this pointer can only increase/decrease the sum." On unsorted data the technique breaks silently — it requires either pre-sorted input or sorting first (O(n log n)).

## When to reach for it

- Pair-sum / pair-difference problems on a sorted array
- Removing duplicates in place
- Merging two sorted sequences
