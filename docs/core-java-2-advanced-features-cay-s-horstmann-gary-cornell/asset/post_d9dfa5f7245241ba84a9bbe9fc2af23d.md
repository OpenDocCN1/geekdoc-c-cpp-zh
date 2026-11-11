
### java.nio.Buffer 1.4

- `Buffer clear()` prepares this buffer for writing by setting the position to 0 and the limit to the capacity; returns this.
- `Buffer flip()` prepares this buffer for reading after writing, by setting the limit to the position and the position to 0; returns this.
- `Buffer rewind()` prepares this buffer for rereading the same values by setting the position to 0 and leaving the limit unchanged; returns this.
- `Buffer mark()` sets the mark of this buffer to the position; returns this.
- `Buffer reset()` sets the position of this buffer to the mark, thus allowing the marked position to be read or written again; returns this.
- `int remaining()` returns the remaining number of readable or writable values—that is, the difference between the limit and position.
- `int position()`
- `void position(int newValue)` gets and sets the position of this buffer.
- `int capacity()` returns the capacity of this buffer.

### 2.6.3 File Locking

When multiple simultaneously executing programs need to modify the same file, they need to communicate in some way, or the file can easily become damaged. File locks can solve this problem. A file lock controls access to a file or a range of bytes within a file.

Suppose your application saves a configuration file with user preferences. If a user invokes two instances of the application, it could happen that both of them want to write the configuration file at the same time. In that situation, the first instance should lock the file. When the second instance finds the file locked, it can decide to wait until the file is unlocked or simply skip the writing process.

To lock a file, call either the lock or tryLock methods of the FileChannel class.

```java
FileChannel channel = FileChannel.open(path);
FileLock lock = channel.lock();
```

or

```java
FileLock lock = channel.tryLock();
```

The first call blocks until the lock becomes available. The second call returns immediately, either with the lock or with `null` if the lock is not available. The file remains locked until the channel is closed or the `release` method is invoked on the lock.

You can also lock a portion of the file with the call

```java
FileLock lock(long start, long size, boolean shared)
```

or

```java
FileLock tryLock(long start, long size, boolean shared)
```

The `shared` flag is `false` to lock the file for both reading and writing. It is `true` for a *shared* lock, which allows multiple processes to read from the file, while preventing any process from acquiring an exclusive lock. Not all operating systems support shared locks. You may get an exclusive lock even if you just asked for a shared one. Call the `isShared` method of the `FileLock` class to find out which kind you have.

> **NOTE:** If you lock the tail portion of a file and the file subsequently grows beyond the locked portion, the additional area is not locked. To lock all bytes, use a size of `Long.MAX_VALUE`.

Be sure to unlock the lock when you are done. As always, this is best done with a try-with-resources statement:

```java
try (FileLock lock = channel.lock())
{
    access the locked file or segment
}
```

Keep in mind that file locking is system-dependent. Here are some points to watch for:

- On some systems, file locking is merely *advisory*. If an application fails to get a lock, it may still write to a file that another application has currently locked.
- On some systems, you cannot simultaneously lock a file and map it into memory.
- File locks are held by the entire Java virtual machine. If two programs are launched by the same virtual machine (such as an applet or application

## Table 2.6 *(Continued)*

| Expression | Description | Example |
|---|---|---|
| `\\d, \\D` | Digits (`[0-9]`, or `\\p{Digit}` when the `UNICODE_CHARACTER_CLASS` flag is set); the complement | `\\d+` is a sequence of digits |
| `\\w, \\W` | Word characters (`[a-zA-Z0-9_]`, or Unicode word characters when the `UNICODE_CHARACTER_CLASS` flag is set); the complement |  |
| `\\s, \\S` | Spaces (`[\\n\\r\\t\\f\\x0B]`, or `\\p{IsWhite_Space}` when the `UNICODE_CHARACTER_CLASS` flag is set); the complement | `\\s*,\\s*` is a comma surrounded by optional white space |
| `\\h, \\v, \\H, \\V` | Horizontal whitespace, vertical whitespace, their complements |  |
| **Sequences and Alternatives** |  |  |
| `XY` | Any string from X, followed by any string from Y | `[1-9][0-9]*` is a positive number without leading zero |
| `X\|Y` | Any string from X or Y | `http\|ftp` |
| **Grouping** |  |  |
| `(X)` | Captures the match of X | `(".*")` captures the quoted text |
| `\\n` | The nth group | `(["']).*\\1` matches `"Fred"` or `'Fred'` but not `"Fred'` |
| `(?<name>X)` | Captures the match of X with the given name | `(?<id>[a-zA-Z0-9]+)` captures the match with name `id` |
| `\\k<name>` | The group with the given name | `\\k<id>` matches the group with name `id` |
| `(?:X)` | Use parentheses without capturing X | In `(?:http\|ftp)://(.*)`, the match after `://` is `\\1` |

## II. Aging*

In the human body, aging is the progressive deterioration of structure and function over time. The causes of aging are manifold, but they include the following:

- 1. Genetic mutations that accumulate over the course of a person's life (somatic mutations);
- 2. The shortening of telomeres—the protective caps at the end of chromosomes—each time a cell divides;
- 3. The gradual build-up of misfolded proteins, which can interfere with normal cellular functions; and
- 4. A decline in the function of mitochondria, the organelles responsible for generating cellular energy.

Each of these mechanisms is an active area of research, and discoveries about them can point the way to treatments for age-related diseases such as cancer, Alzheimer's disease, and heart disease.

In the realm of modern medicine, the question of how to slow the aging process has gained significant attention. Scientists are exploring various interventions, from caloric restriction to pharmacological agents that mimic the effects of exercise.

One promising area of study involves the use of stem cells to regenerate damaged tissues. Researchers hope that, by replenishing the body's pool of stem cells, it may be possible to restore function to aging organs and extend healthy lifespan.

Classes use a syntax that is similar to, but not quite the same as, the one used in the Perl language. Table 2.6 shows all constructs of the Java syntax. For more information on the regular expression syntax, consult the API documentation for the Pattern class or the book *Mastering Regular Expressions* by Jeffrey E. F. Friedl (O’Reilly and Associates, 2006).

The simplest use for a regular expression is to test whether a particular string matches it. Here is how you program that test in Java. First, construct a Pattern object from a string containing the regular expression. Then, get a Matcher object from the pattern and call its matches method:

```java
Pattern pattern = Pattern.compile(patternString);
Matcher matcher = pattern.matcher(input);
if (matcher.matches()) . . .
```

The input of the matcher is an object of any class that implements the CharSequence interface, such as a String, StringBuilder, or CharBuffer.

When compiling the pattern, you can set one or more flags, for example:

```java
Pattern pattern = Pattern.compile(expression,
    Pattern.CASE_INSENSITIVE + Pattern.UNICODE_CASE);
```

Or you can specify them inside the pattern:

```java
String regex = "(?iU:expression)";
```

Here are the flags:

- `Pattern.CASE_INSENSITIVE` or `i`: Match characters independently of the letter case. By default, this flag takes only US ASCII characters into account.
- `Pattern.UNICODE_CASE` or `u`: When used in combination with `CASE_INSENSITIVE`, use Unicode letter case for matching.
- `Pattern.UNICODE_CHARACTER_CLASS` or `U`: Select Unicode character classes instead of POSIX. Implies `UNICODE_CASE`.
- `Pattern.MULTILINE` or `m`: Make `^` and `$` match the beginning and end of a line, not the entire input.
- `Pattern.UNIX_LINES` or `d`: Only `'\n'` is a line terminator when matching `^` and `$` in multiline mode.
- `Pattern.DOTALL` or `s`: Make the `.` symbol match all characters, including line terminators.
- `Pattern.COMMENTS` or `x`: Whitespace and comments (from `#` to the end of a line) are ignored.
- `Pattern.LITERAL`: The pattern is taken literally and must be matched exactly, except possibly for letter case.
