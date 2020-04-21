`shasum` computes checksum for a file. `-a` sets the algorithm used (1, 225, 256, 384, 512) to create the checksum.

`shasum` has a check option `-c` that expects a list of sums to check against but I found it hard to use.

`diff` provides a quick way to be side-by-side comparisons. It expects two files as input. We use `<` to redirect the input from commands, executed with `( )`.

```
diff <(shasum -a 245 path/to/filename.txt) <(echo shasum)

< 90e83ac8762694204aa9092ccf0ad951800314c98b2e07c1d092c6805e02ba5d
---
> 90e83ac8762694204aa9092ccf0ad951800314c98b2e07c1d092c6805e02ba5d
```
