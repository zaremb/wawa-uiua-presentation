---
layout: section
transition: slide-left
---

# What is Uiua?

<BgEmoji emoji="🚀" :count="5" animate="fly" :opacity="0.20" :seed="33" />

<!--
[transition - shift energy from playful to curious]

Okay. So what IS this thing?

Let me give you the two-word version first.
-->

---
layout: statement
transition: fade
---

# Stack-based. Array-oriented.

<!--
Stack-based. Array-oriented.

That's it. That's the whole paradigm.

Stack-based means: there are no variable names. You push values onto a stack, and functions consume them. Like a calculator - last in, first out.

Array-oriented means: EVERYTHING is an array. A single number? That's a zero-dimensional array. A list? One-dimensional array. There are no scalars. Operations apply to entire arrays at once, automatically.

If you've ever used NumPy broadcasting... you've already tasted this idea. Uiua just takes it to the extreme.
-->

---
layout: center
class: text-center
transition: fade
clicks: 4
---

<div class="font-mono">
<div class="text-xl op-90 tracking-widest uppercase mb-10">the stack</div>

<div class="text-5xl mb-8 h-20 flex items-center justify-center">
  <span v-show="$clicks === 0" class="op-70">[ ]</span>
  <span v-show="$clicks === 1" class="text-green-400">[ 3 ]</span>
  <span v-show="$clicks === 2" class="text-green-400">[ 3 &ensp; 5 ]</span>
  <span v-show="$clicks === 3" class="text-green-400">[ 8 ]</span>
  <span v-show="$clicks === 4" class="text-yellow-400">[ 16 ]</span>
</div>

<div class="text-2xl op-90 h-10">
  <span v-show="$clicks === 1">push <span class="font-mono text-green-400">3</span></span>
  <span v-show="$clicks === 2">push <span class="font-mono text-green-400">5</span></span>
  <span v-show="$clicks === 3"><span class="font-mono text-green-400">+</span> add</span>
  <span v-show="$clicks === 4"><span class="font-mono text-yellow-400">×2</span> multiply</span>
</div>
</div>

<!--
[quick demo - 20 seconds max]

Here's how the stack works. Super simple.

[click] Push 3.

[click] Push 5. Two values sitting there, waiting.

[click] "Add" - eats the top two, pushes back their sum. Eight.

[click] Multiply by two - sixteen. Each operation transforms what's on the stack.

No variables. No names. Just data flowing through.
-->

---
layout: center
class: text-center
transition: fade
clicks: 4
---

<div class="font-mono text-center">
<div class="text-xl op-90 tracking-widest uppercase mb-10">now with arrays</div>

<div class="text-4xl mb-4 text-green-400 uiua-glow">
  <span v-show="$clicks === 0">⇡5</span>
  <span v-show="$clicks === 1">+1⇡5</span>
  <span v-show="$clicks === 2">⇌+1⇡5</span>
  <span v-show="$clicks >= 3">/+⇌+1⇡5</span>
</div>

<div class="text-3xl mb-6 h-14 flex items-center justify-center text-yellow-400">
  <span v-show="$clicks === 0">[0 1 2 3 4]</span>
  <span v-show="$clicks === 1">[1 2 3 4 5]</span>
  <span v-show="$clicks === 2">[5 4 3 2 1]</span>
  <span v-show="$clicks === 3">15</span>
  <span v-show="$clicks === 4" class="text-2xl">Four glyphs. One line. Array to number.</span>
</div>

<div class="text-2xl op-90 h-10">
  <span v-show="$clicks === 0"><span class="text-yellow-400 font-mono">⇡5</span> - range of 5</span>
  <span v-show="$clicks === 1"><span class="text-yellow-400 font-mono">+1</span> - add 1 to every element</span>
  <span v-show="$clicks === 2"><span class="text-yellow-400 font-mono">⇌</span> - reverse</span>
  <span v-show="$clicks === 3"><span class="text-yellow-400 font-mono">/+</span> - reduce add - sum the whole array</span>
</div>
</div>

<!--
Now the same idea - but with arrays. In Uiua, everything is an array.

Range of 5 - one glyph creates a whole array on the stack.

[click] Plus one - adds to EVERY element. No loop. The whole array transforms at once.

[click] Reverse - flips it. Three glyphs, three transformations.

[click] Reduce add - slash-plus. The whole array collapses into a single number. Fifteen.

[click] Four glyphs. One line. We went from nothing to an array, transformed it, and reduced it to a single value. No variables, no loops.

Now - I know what some of you are thinking...
-->

---
layout: center
class: text-center
transition: fade
---

<div class="text-3xl font-mono text-green-400 op-80 mb-12 uiua-glow">⧻⇡10↯⊃(⊂⊙(↻1))⊃(⊂⊙(↻¯1))</div>

<div v-click class="text-5xl font-bold">"Unreadable!"</div>

<!--
[show the Fibonacci expression - let it sit for 3 seconds in silence]

Remember this from the beginning?

[pause - let the audience squint at it]

[click] Yeah. "Unreadable." That's what everyone says.

But here's the thing...
-->

---
layout: center
transition: fade
---

<div class="text-4xl font-bold leading-relaxed text-center">
Unfamiliar
<div v-click class="text-3xl mt-2 font-normal text-yellow-400">is not the same as</div>
<div v-click class="text-4xl mt-2">unreadable.</div>
</div>

<!--
Unfamiliar... [click] is not the same as... [click] unreadable.

This is a crucial distinction. In the world of array programming, there's a famous saying exactly like this.

Think about it - when you first saw Python list comprehensions, they looked weird too. Now you read them fluently.

The symbols in Uiua are the same. Once you know that ⇌ means "reverse" and ♭ means "flatten," you stop seeing weird squiggles and start seeing the architecture of your data.

It's exactly like...
-->

---
layout: center
class: text-center
transition: fade
---

<div class="text-7xl mb-8">🎵</div>

<div class="text-3xl font-bold">Sheet music.</div>

<div v-click class="text-2xl op-90 mt-6 max-w-lg mx-auto leading-relaxed">
Dots and lines to a beginner.<br>
A melody to a musician.
</div>

<!--
Sheet music.

To someone who's never learned it, sheet music is just... dots on lines. Meaningless.

[click] But to a musician? It's a melody. They HEAR it when they look at it.

Uiua is the same. Once you learn about twenty symbols - and that's the whole language - you don't "decode" the code anymore. You just... read the shape of the data.
-->

---
layout: center
class: text-center
transition: fade
---

<div class="text-3xl leading-relaxed">
You type <span class="font-mono text-blue-400">reverse</span>
<div v-click class="mt-4 text-5xl font-mono text-green-400 uiua-glow uiua-glow-boost">⇌</div>
<div v-click class="text-2xl op-90 mt-6">The editor does the rest.</div>
</div>

<!--
And here's the best part - you don't need a special keyboard.

You type the word "reverse"... [click] and the editor turns it into this glyph. Automatically.

[click] The editor does the rest. You type English words, and it translates them into the compact symbols.

So there's no barrier to entry. If you can type, you can write Uiua.
-->
