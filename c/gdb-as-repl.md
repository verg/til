The feeback loop of compiling-then-runing C programs can make learning C seem more painful than higher-level languages with powerful REPLs.

Here's a way to use gdb as a psudo C repl.

Start by writing a tiny program, gdbrepl.c:
```
int main()
{
  int i = 1;
  return 0;
}
```

Compile with -g flag so gdb has debugging information:
`gcc -g gdbrepl.c -o gdbrepl`

Run gdb:
`gdb dgbrepl`

You can now evaluate expressions with gdb's print command:
```
(gdb) print 1 + 1
$1 = 2
(gdb) print -2147483647-1U < 2147483647
$2 = 0
```
