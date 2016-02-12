# Pattern Matching on Multiple Lists

Scala has nice pattern matching syntax. I got quite excited when I realized I could match on tuples. Here's an example

`merge` is a function which combines two sorted lists of integers. It matches on a tuple contaning its two list parameters. The first two cases match on the condition that either of the lists are Nil, and if so, returns the opposite list, contained in the `zs` vals. The third case breaks each list into a head element, `x` and `y`, and the rest of the list, `xs1` and `ys1`.

```scala
def merge(xs: List[T], ys: List[T]): List[T] =
  (xs, ys) match {
    case (zs, Nil) => zs
    case (Nil, zs) => zs
    case (x :: xs1, y :: ys1) =>
      if (ord.lt(x, y)) x :: merge(xs1, ys)
      else y :: merge(xs, ys1)
  }
```
