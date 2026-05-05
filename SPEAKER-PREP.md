# Speaker Preparation Guide — Wawa-Uiua Talk

Read this document before your talk. It covers all concepts you present plus likely Q&A topics.

---

## 1. What is Uiua?

- **Pronunciation**: "WEE-wah" (like the first syllable of "we" + "wah")
- **Paradigm**: Tacit, stack-based, array-oriented programming language
- **Creator**: Kai Schmidt (started ~2022, actively developed)
- **Written in**: Rust
- **Status**: Pre-1.0, evolving rapidly but core is stable
- **Website**: uiua.org — has a browser-based playground (uiua.org/pad)

**Tacit** = functions don't refer to arguments by name. Data flows through implicitly.  
**Stack-based** = no variable names needed. Values pushed/popped from a stack (LIFO).  
**Array-oriented** = the primary data structure is the multi-dimensional array. Operations apply to entire arrays at once (rank-polymorphism).


## 1b. Theoretical Foundations

### Why Right-to-Left?

Uiua code executes **right to left**. This is not arbitrary — it comes from **function composition** in mathematics.

In math, `f(g(x))` means: apply g first, then f. The rightmost function runs first. Uiua simply removes the parentheses and the variable name:

```
Math:    f(g(x))     — apply g to x, then f to result
Python:  f(g(x))     — same, nested calls
Uiua:    f g x       — same order, no parens, no variable
```

This is called **prefix notation** (operator before operands). Benefits:
- No operator precedence rules needed — always unambiguous
- Function composition is implicit (just place functions next to each other)
- Reads like a pipeline flowing leftward: each glyph transforms what came before it
- The rightmost value is your "input", and you read the transformations applied to it going left

Think of it like a Unix pipeline written backwards: `⇡10` produces data, then each glyph to the left is a filter/transform — like `range 10 | mod 2 | eq 0 | filter | times 2 | sum`.

### What is Tacit Programming?

**Tacit** (also called "point-free") means writing functions **without naming their arguments**.

Compare:
```python
# Explicit (pointed) — argument x is named
def double(x):
    return x * 2

# Tacit (point-free) — no argument named
double = partial(mul, 2)    # or in functional: (2*)
```

In Uiua, ALL code is tacit. You never write `x = ...`. Data sits on the stack and functions consume it implicitly. The "point" (variable) is gone — hence "point-free."

**Why tacit?**
- Forces you to think about **data flow** rather than naming things
- Eliminates an entire class of bugs (wrong variable name, shadowing, stale references)
- Makes composition trivial — functions snap together like LEGO
- Encourages writing small, reusable transformations

**Historical note**: Tacit programming was pioneered by **John Backus** (inventor of Fortran!) in his 1977 Turing Award lecture *"Can Programming Be Liberated from the von Neumann Style?"* He argued that named variables force sequential thinking and proposed **function-level programming** — combining functions without mentioning data. APL, J, BQN, and Uiua are direct descendants of this idea.
### Why Glyphs Instead of Words?

You might ask: why not just write `reverse` instead of `⇌`? There are real reasons:

**1. Information density** — `/+×2▽=0◿2⟜∘⇡10` fits on one line. Written out as `reduce add multiply 2 keep equals 0 modulo 2 on identity range 10` it becomes a wall of text where structure disappears. Glyphs let you see the *shape* of the pipeline at a glance.

**2. Pattern recognition** — Humans process symbols faster than words once trained. Musicians read `♩` not "quarter note". Mathematicians read `∑` not "summation of". After a few hours with Uiua, `⇌` *is* reverse — you stop decoding and start perceiving.

**3. Language neutrality** — Glyphs work regardless of your native language. A Japanese developer and a Polish developer read the same `⇌`. Word-based code privileges English speakers.

**4. Visual mnemonics** — Many glyphs look like what they do:
- `⇌` (reverse) — arrows going both ways
- `↯` (reshape) — lightning bolt = restructure
- `△` (shape) — a triangle has a shape
- `♭` (flatten) — a musical flat = make flat
- `⊂` (join) — two things being cupped together
- `↻` (rotate) — a circular arrow

**5. Uniform width** — Every function is one character. This means code has a predictable visual rhythm. You can count operations by counting glyphs. In `/+×2▽=0◿2⟜∘⇡10` there are exactly 7 operations — you can see that immediately.

**The tradeoff**: Higher initial learning curve. But Uiua mitigates this with the formatter — you never need to memorize how to *type* glyphs, only how to *read* them. You type `reverse` and get `⇌`.


### Computer Science Foundations

Concepts Uiua builds on that you should be able to explain:

**1. Stack (LIFO data structure)**
- Last In, First Out. Like a stack of plates — you can only touch the top.
- Push = add to top. Pop = remove from top.
- Classic CS structure used in: function call frames, expression evaluation, undo systems, parsing.
- In Uiua: the entire program state is a stack of arrays. Functions pop inputs, push outputs.

**2. Array / Tensor**
- Contiguous block of memory holding elements of the same type.
- Dimensions described by "shape": `[3, 4]` = 3 rows × 4 columns.
- CPU-friendly: elements sit next to each other in RAM → cache-efficient, vectorizable (SIMD).
- This is why NumPy is fast despite Python being slow — the array operations run in C on contiguous memory.
- Uiua's runtime (Rust) does the same: array ops are tight loops over contiguous memory.

**3. Rank Polymorphism**
- A function written for scalars automatically works on arrays of any rank.
- `+1` works on a number, a vector, a matrix, a 5D tensor — same code.
- No need to write loops or special cases for different dimensions.
- Equivalent to NumPy broadcasting but more general and built into every operation.

**4. Reduction (Fold)**
- Collapsing an array into a single value by repeatedly applying a binary function.
- `/+ [1 2 3 4]` = `1+2+3+4` = 10
- Mathematically: `reduce(f, [a,b,c,d])` = `f(f(f(a,b),c),d)`
- This is `functools.reduce()` in Python, `.reduce()` in JS, `fold` in Haskell.

**5. Higher-Order Functions (Modifiers)**
- Functions that take other functions as arguments.
- `/` (reduce), `≡` (rows/map), `⊞` (table/outer product) are all higher-order.
- Same concept as Python's `map()`, `filter()`, `functools.reduce()`.
- In Uiua they're called "modifiers" — they modify how a function is applied.

**6. Boolean Masking**
- A boolean array (0s and 1s) used to select elements from another array.
- `[1 0 1 0 1]` applied to `[a b c d e]` → `[a c e]`
- Replaces if-statements: the condition IS the data, not control flow.
- Exact same concept as NumPy: `arr[arr > 5]` creates a mask then filters.

**7. Function Composition**
- Combining simple functions into complex ones: `h = f ∘ g` means `h(x) = f(g(x))`.
- In Uiua, composition is implicit — just write functions next to each other.
- This is the backbone of tacit programming: build complex behavior by composing primitives.

---

## 2. Core Concepts You Must Know

### The Stack
- Values are pushed onto a stack. Functions consume values from the top.
- `3 5 +` → pushes 3, pushes 5, `+` pops both, pushes 8.
- Code reads **right to left** (rightmost executes first).
- No variables needed for most programs — data threads through the stack.

### Arrays
- Everything is an array. A number is a 0D array (scalar). A list is 1D. A matrix is 2D.
- Arrays must be rectangular (uniform shape per axis).
- **Shape** (`△`): dimensions of an array. `△[1 2 3]` → `[3]`.
- **Rank**: number of axes. Scalar=0, vector=1, matrix=2.

### Pervasive Operations
- Math functions automatically apply element-wise to arrays:
  - `×2 [1 2 3]` → `[2 4 6]` (no loop needed)
  - `+ [1 2 3] [4 5 6]` → `[5 7 9]`
- This is like NumPy broadcasting but built into the language at every level.

### Key Glyphs (the ~20 you mention)

| Glyph | Name | What it does |
|-------|------|-------------|
| `⇡` | range | Generate 0..n-1 |
| `⇌` | reverse | Reverse an array |
| `♭` | deshape/flatten | Flatten to 1D |
| `↯` | reshape | Change shape |
| `⊂` | join | Concatenate arrays |
| `△` | shape | Get dimensions |
| `⧻` | length | Number of rows |
| `▽` | keep | Filter by mask |
| `⊃` | fork | Apply two functions to same args |
| `◿` | modulo | Remainder |
| `/` | reduce | Fold function over array |
| `↻` | rotate | Circular shift |
| `⟜` | on | Keep first arg in front of outputs |
| `∘` | identity | Pass-through (no-op) |
| `⊙` | dip | Skip top, apply to rest |
| `≡` | rows | Apply function to each row |
| `×` | multiply | Multiply |
| `+` | add | Add |
| `-` | subtract | Subtract |
| `□` | box | Box a value (for mixed arrays) |

### The Formatter
- You type ASCII names: `reverse`, `range`, `reduce`, etc.
- The editor/formatter auto-converts to glyphs: `⇌`, `⇡`, `/`
- No special keyboard needed — this is Uiua's killer UX feature vs APL/BQN.
- You can even type partial names (just enough to disambiguate).

### Modifiers (Higher-Order Functions)
- **Reduce** (`/`): fold a function between elements. `/+ [1 2 3 4 5]` → 15
- **Rows** (`≡`): apply function to each row.
- **Table** (`⊞`): apply function to all combinations.
- **Fork** (`⊃`): apply two functions to the same arguments.

### No Control Flow
- No if/else, no for/while loops.
- Conditions become boolean masks (arrays of 0s and 1s).
- Filtering = multiplying by a mask (`▽` keep).
- Repetition = reduce, scan, or recursion via modifiers.

---

## 3. The Demo Breakdown (memorize this)

**Task**: Take 0-9, keep evens, double them, sum.

```
/+×2▽=0◿2⟜∘⇡10
```

Reading right to left:
1. `⇡10` — range → `[0 1 2 3 4 5 6 7 8 9]`
2. `⟜∘` — duplicate the array (keep a copy)
3. `◿2` — modulo 2 each element → `[0 1 0 1 0 1 0 1 0 1]`
4. `=0` — equals 0 → boolean mask `[1 0 1 0 1 0 1 0 1 0]`
5. `▽` — keep (filter by mask) → `[0 2 4 6 8]`
6. `×2` — double each → `[0 4 8 12 16]`
7. `/+` — reduce with add → `40`

**Python equivalent**:
```python
numbers = list(range(10))
evens = [x for x in numbers if x % 2 == 0]
doubled = [x * 2 for x in evens]
result = sum(doubled)  # 40
```

**NumPy equivalent**:
```python
import numpy as np
numbers = np.arange(10)
result = (numbers[numbers % 2 == 0] * 2).sum()  # 40
```

The Uiua version and the NumPy version share the same mental model: boolean masking + vectorized ops.

---

## 4. The Fibonacci Expression

```
⧻⇡10↯⊃(⊂⊙(↻1))⊃(⊂⊙(↻¯1))
```

- Starts with `[0 1]`, repeatedly takes the last two elements, sums them, appends.
- Uses rotate (`↻`) to shift arrays and join (`⊂`) to append.
- Produces: `[0 1 1 2 3 5 8 13 21 34]`
- The expression is dense but does exactly what you'd write in any language — just without naming anything.

---

## 5. The Language Family (for Q&A)

| Language | Year | Key Trait | Still Used? |
|----------|------|-----------|-------------|
| **APL** | 1966 | Original array language (Ken Iverson). Special keyboard. | Yes — finance, insurance |
| **J** | 1990 | APL successor by Iverson. ASCII digraphs instead of glyphs. | Yes — niche |
| **K/Q** | 1993 | Finance branch. Powers kdb+ at every major bank. Extremely fast time-series. | Yes — heavily in finance |
| **BQN** | 2020 | Modern APL redesign. Cleaner semantics, Unicode glyphs. Active community. | Growing |
| **Uiua** | 2022 | Stack-based (no variables at all). Auto-formatter. Lowest barrier to entry. | Growing |

**What makes Uiua unique in this family**:
- Stack-based (others use explicit argument syntax or variable assignment)
- The formatter — type English, get glyphs (others need keyboard layouts or memorization)
- Built-in multimedia (images, audio, GIFs)
- Designed from scratch for tacit-only programming

---

## 6. Likely Q&A and Answers

### "Is this practical / production-ready?"
No, and that's not the point. It's a thinking tool. Like learning Latin to understand English grammar better. It sharpens your array-thinking, which directly improves your NumPy/Pandas code.

### "How fast is it?"
Surprisingly fast for an interpreted language. Array operations are vectorized in the Rust runtime. For numeric work on arrays it can compete with Python+NumPy because it avoids Python's per-element overhead entirely.

### "How many people use it?"
Small community (~1000-2000 on Discord). The creator Kai Schmidt is very active. It's a passion project, not a corporate product. Think of it like a language workshop where the design evolves rapidly.

### "Can you do real programs in it?"
Yes — file I/O, HTTP, images, audio, GIFs, FFI. People have made games, image processors, Advent of Code solutions, even web servers. But it's best for data transformation tasks.

### "How is this different from APL?"
1. Stack-based (APL uses named variables and infix notation)
2. Auto-formatter (APL needs a special keyboard layout)
3. Simpler syntax (no operator precedence rules — always right-to-left)
4. Modern tooling (LSP, package manager, built-in formatter)

### "Why not just use NumPy?"
You should! The point isn't to replace NumPy. It's that practicing in Uiua makes you *think* in arrays instinctively. You start reaching for boolean masks and vectorized ops instead of for-loops. Cross-training.

### "What's the learning curve like?"
~20 glyphs to be productive. The tutorial on uiua.org/tutorial takes about 2 hours. The playground (uiua.org/pad) gives instant feedback. Most people get comfortable in a weekend.

### "What about readability?"
- The "unfamiliar ≠ unreadable" argument from your talk.
- Once you know the glyphs, Uiua code is extremely information-dense but readable — like sheet music.
- The code literally shows the shape of data transformation.
- Compare: a musician reads notes, not letter-by-letter descriptions of notes.

### "What's the mascot?"
Kala — a cute crab-like creature. Appears in tutorials and documentation.

---

## 7. Technical Details (if deep questions arise)

- **Array model**: Flat (like J). Arrays must be rectangular. Use `□` (box) for mixed types/shapes.
- **Type system**: Numbers (f64), characters, bytes, boxes. No strings — strings are character arrays.
- **Error handling**: `⍣` (try) modifier — like try/catch but functional.
- **Inverses**: `°` (un) modifier reverses a function. `°⊟` unsplits a coupled array. Very powerful.
- **Under** (`⍜`): Apply a function, transform, then undo the first function. (e.g., modify a specific element then put it back)
- **Fill** (`⬚`): Provide a default value for operations that would fail with mismatched shapes.
- **Modules**: Import system exists. Can split code into files.
- **Testing**: Built-in test assertions.

---

## 8. Key Talking Points Cheat Sheet

1. "Unfamiliar is not unreadable" — the central thesis
2. Sheet music analogy — dots on lines vs. hearing melody
3. The formatter removes the keyboard barrier
4. Same mental model as NumPy — cross-training for Python devs
5. No control flow — conditions become data (masks)
6. One line = one transformation pipeline = visible data flow
7. It's a weird side quest, not a conversion sermon

---

## 9. Quick Reference — Try These Live

If someone asks you to demo something live at uiua.org/pad:

```uiua
# Hello world
"Hello, Python Pizza!"

# Reverse a string
⇌ "Warsaw"

# Range and sum
/+ ⇡100        # sum of 0-99 = 4950

# Matrix
↯3_3 ⇡9        # 3x3 matrix of 0-8

# Sort an array
⊏⍏ [3 1 4 1 5 9 2 6]

# Fibonacci (your slide)
⧻⇡10↯⊃(⊂⊙(↻1))⊃(⊂⊙(↻¯1))

# Your demo: filter evens, double, sum
/+×2▽=0◿2⟜∘⇡10
```

---

*Good luck! Remember: confidence, pacing, and the Borat voice. 🎬*
