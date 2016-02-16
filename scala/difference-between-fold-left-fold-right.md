# Difference Between Fold Left and Fold Right

My understanding of the differences between fold left and fold right has always been murky. This is an attempt to better understand those differences.

The Fold operations in scala operate on a list, taking a initial value of type `U` and a `(U, T) => U` function. In this example, `0` and `((sum: Int, x: Int) => sum + x)`. 

`List(1,2,3).foldLeft(0)((sum, x) => sum + x)` conceptually reduces to:
```scala
(((0 + 1) + 2) + 3)
```

For Fold Right, `List(1,2,3).foldLeft(0)(_ + _)`, reduces to:
```scala
(1 + (2 + (3 + 0)))
```

Because addition is associative and commutative, the two examples produce the same result. However, there is an important implmentation difference between the two. `foldLeft` is implemented with a while loop. `foldRight` use non-tail recursion, and thus requires extra memory and risks stack overflow.

Okay. So when to reach for fold right? When you have a right associative operation. For example, any operations begining in `:`.

```scala
scala> (0.to(3).foldRight(List[Int]())((x, xs) => x :: xs))
res1: List[Int] = List(0, 1, 2, 3)
```
Reduces to `(0 :: (1 :: (2 :: (3 :: List()))))`.

So, in general, unless you have a right associative operation, use foldLeft.
