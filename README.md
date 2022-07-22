# Intro to File IO

## Learning Goals

- Reading from a file
- Writing to a file

***

## Key Vocab

- **File**: A file is some information or data which stays in the computer
storage devices.
- **Directory**: A directory is a location for storing files on your computer.

***

## Introduction

When we work with computers, our code needs to be able to
store data and access data created by other programs and computers.
The way we do that is file input/output (File IO). In this lesson we will talk
 about how to read data from files, how to write data, and how to work with
that data.

## Opening a file

```py
text_file = open('file_directory/file_name.txt')
```

The only required argument to pass into the open function is a combination of
file path and file name.

Now we can use the `text_file` variable to do operations on the file.

What operations can do? 
It depends on the mode we have opened the file in. 
The default mode is read when we open a file but we can specify different modes
using a second argument into the open function.

We can also define the encoding of the file using the `encoding`
attribute

```py
text_file = open('file_directory/file_name.txt', encoding='utf-8')
```

If you do not specify the encoding python will use a default
encoding. The default is platform dependent
(whatever `locale.getpreferredencoding()` returns)

It is considered good practice to always define the encoding.

## Closing a file

A file should be closed as soon as we are done using it. An open file can block
other programs from using the file depending on the mode we open it in.

```py
text_file = open('file_name.txt', encoding='utf-8')
test_file.close()
```

Nobody is perfect. What if we forget to close a file?
We can prevent problems like this by using the `with` statement

```py
with open('file_name.txt', encoding='utf-8') as text_file:
    text_file.read()
```

Inside the `with` statement code block we can use the variable `text_file`.
When the block ends, python will automatically call `test_file.close()`.
The `with` statement guarantees the file will be closed even in the case of an
exception.

## Modes

The `mode` attribute of a file can tell you which mode the file had been opened in.

```py
text_file = open('file_directory/file_name.txt')

print (text_file.mode)
#r
```

The default mode is read but we can pass a second argument which
allows us to open the file in many different modes that serve different
use cases. These modes will allow us to do things like write to a file,
open a file in binary and, append to a file. We will look into these in more
detail later on in this lesson.

Here are some example of how we can define a mode.

```py

#append mode 
text_file = open('file_directory/file_name.txt', mode='a', encoding='utf-8')

#write mode
text_file = open('file_directory/file_name.txt', mode='w' encoding='utf-8')

```

## Reading from a file

When we want to read from a file we have to open it first.
We can read from a file using the `read()` method

```py
# Lets say the file contains the following sentence
# The door swung open to reveal pink giraffes and red elephants.

text_file = open('text_file.txt', encoding='utf-8')
print(text_file.read())
# The door swung open to reveal pink giraffes and red elephants.

```

What if we want to read from a really long file?

It is inefficient to hold the entire file in memory.

We can process one line at a time instead of using the `read()`
method which gives us the entire file content.

```py
with open('big_file.txt', encoding='utf-8') as text_file:
    for line in text_file:
        print(line)
```

## Writing to a File

Writing a file is similar to reading from a file.
The only difference is that we have to open the file in
either the write or append mode.

- The write mode can be defined using the argument `mode='w'`
- The append mode can be defined using `mode='a'`

What if the file does not exist?

The write and append modes will create a new file if it does not
already exist.

```py
#Writing to a file
with open('log_file.txt', mode='w', encoding='utf-8') as log_file:
    log_file.write('Log 1')

with open('log_file.txt', mode='a', encoding='utf-8') as log_file:
    log_file.write('Log 2')

```

If a file already exists and we use the `mode='w'` the file will be overwritten.

If we use `mode='a'` we will append what we write to the existing file.

## Conclusion

Now that we have a better understanding of how to interact with files
in python. We can apply this knowledge to many use cases like storing data,
 writing logs and interacting with other programs.
***

## Resources

- [Python 3 Documentation](https://docs.python.org/3/)
- [Python File IO](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
