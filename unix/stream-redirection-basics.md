A stream is something that can transfer data. In the case of these streams, the data is text.

`stdin` - Input stream

`stdout` & `stderr` - Output streams

`<` redirects `stdin` (default is likely the terminal input)

```
# parens execute the ls command and pass the output the cat
cat <(ls)
filename.txt

# note, realisitically you'd normally pipe here instead

ls | cat
```

`>` redirects `stdout` (default is likely the terminal)

```
echo hello world > filename.txt
cat filename.txt
hello world
```

`>>` appends to an existing file

```
echo one more hello >> filename.txt
cat filename.txt
hello world
one more hello
```

There are numeric descriptors for each stream you can use when redirecting:

```
# stdin
0>

# stdout
1>

# stderr
2>
```

Because error messages and normal output each have their own conduit to carry them to the terminal window, they can be handled independently of one another.

These allow the different output streams to be redirected to different files

```
echo hello world 1> filename.txt 2> error.txt
```
