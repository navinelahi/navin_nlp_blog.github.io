+++
date = '2024-12-28T15:37:40-08:00'
draft = true
title = 'Regex'
+++
### Regular Expressions Cheatsheet and Exercises

#### **Basic Regular Expressions**

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/[wW]oodchuck/`     | `woodchuck` or `Woodchuck`                                              |
| `/[abc]/`            | `a` or `b` or `c`                                                      |
| `/[1234567890]/`     | Any digit                                                              |
| `/[A-Z]/`            | One uppercase letter                                                   |
| `/[a-z]/`            | One lowercase letter                                                   |
| `/[0-9]/`            | One digit                                                              |
| `/[^A-Z]/`           | No uppercase letters                                                   |
| `/[^a-z]/`           | No lowercase letters                                                   |
| `/[^Aa]/`            | Not `A` or `a`                                                        |
| `/[^.]/`             | Not a dot                                                              |
| `/[A^]/`             | `A` or `^`                                                             |
| `/[a^b]/`            | `a`, `^`, or `b`                                                      |
| `/a^b/`              | The pattern `a^b`                                                     |
| `/woodchucks?/`      | `woodchuck` or `woodchucks`                                            |
| `/colou?r/`          | `color` or `colour`                                                   |

#### **Quantifiers**

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/baa*/`             | `ba`, `baa`, `baaaa`, etc.                                             |
| `/ba+/`              | `ba`, `baa`, `baaaa`, etc.                                             |
| `/[ba]*/`            | Zero or more `b` or `a` (e.g., `aaaaa`, `abab`, `bbbbb`)               |
| `/a*/`               | Zero or more `a`s                                                     |
| `/[0-9][0-9]*/`      | An integer with at least one digit                                      |
| `/[0-9]+/`           | An integer with at least one digit                                      |
| `/beg.n/`            | Any character between `beg` and `n` (e.g., `begin`, `beg'n`)           |
| `/love.*love/`       | Any number of characters between two occurrences of `love`            |

#### **Anchors**

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `^`                  | Start of line                                                         |
| `$`                  | End of line                                                           |
| `/^The dog\.$/`     | Only the sentence `The dog.` (backslash escapes the `.`)               |
| `/^The/`             | Matches `The` at the start of a line                                   |
| `/hmm\.$/`          | Matches `hmm.` at the end of a line                                    |
| `\b`                | Word boundary                                                          |
| `/\bthe\b/`         | Matches `the` but not `other`                                         |
| `/\b99\b/`          | Matches `99` but not `299`                                            |
| `\B`                | Non-word boundary                                                     |

#### **Pipe Symbol (OR)**

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/cat|dog/`          | `cat` or `dog`                                                        |
| `/pupp(y|ies)/`      | `puppy` or `puppies`                                                  |
| `/Column [0-9]+ */`  | Matches `Column 1`, `Column 2`, etc.                                  |

#### **Examples of Ambiguity**

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/the*/`             | Matches `theeeee` but not `thethe`                                    |
| `/the|any/`          | Matches `the` or `any` but not `thany`                                |
| `/[a-z]*/`           | Matches any string with zero or more characters, returns the longest   |

#### **Complex Example**
Suppose our goal is to find expressions like `6 GHz`, `500 GB`, and `$999.99`:

| Pattern               | Matches                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/$[0-9]+/`          | Matches integers starting with `$`                                     |
| `/$[0-9]+\.[0-9][0-9]/` | Matches decimals with two decimal places                             |
| `/\b[0-9]+ *(GB|[Gg]igabytes?)\b/` | Matches `500 GB` or `500 Gigabytes`                    |

#### **Exercises**

**2.1 Write regular expressions for the following languages:**

1. The set of all alphabetic strings:
   ```regex
   /^[a-zA-Z]+$/
   ```

2. The set of all lowercase alphabetic strings ending in `b`:
   ```regex
   /^[a-z]*b$/
   ```

3. The set of all strings from the alphabet `a,b` such that each `a` is immediately preceded and followed by a `b`:
   ```regex
   /^(b(ab)*b|b*)$/
   ```

**2.2 Write regular expressions for the following languages:**

1. The set of all strings with two consecutive repeated words:
   ```regex
   /\b(\w+) \1\b/
   ```

2. All strings that start at the beginning of the line with an integer and end at the end of the line with a word:
   ```regex
   /^\d+ \w+$/
   ```

3. All strings that have both the word `grotto` and the word `raven`:
   ```regex
   /\b(grotto).*\b(raven)\b|\b(raven).*\b(grotto)\b/
   ```

4. Write a pattern that places the first word of an English sentence in a register:
   ```regex
   /^([A-Z][a-z]*)/g
   ```

**2.3 Implement an ELIZA-like program:**
Use substitutions to create conversational responses. For example:

```regex
s/I feel (.*)/Why do you feel \1?/
s/I am (.*)/How long have you been \1?/
```

**2.4 Compute the edit distance of `leda` to `deal` using insertion, deletion, and substitution costs of 1:**

|    |    | d  | e  | a  | l  |
|----|----|----|----|----|----|
|    |  0 |  1 |  2 |  3 |  4 |
| l  |  1 |  1 |  2 |  3 |  3 |
| e  |  2 |  2 |  1 |  2 |  3 |
| d  |  3 |  2 |  2 |  2 |  3 |
| a  |  4 |  3 |  3 |  2 |  3 |

**Edit Distance = 3**

**2.5 Compute whether `drive` is closer to `brief` or `divers` and calculate the edit distance.**

**2.6 Implement a minimum edit distance algorithm.**

**2.7 Augment the minimum edit distance algorithm to output an alignment.**

