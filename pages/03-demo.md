---
layout: section
transition: slide-left
---

# Let's see it.

<!--
[shift energy - now we move from theory to practice]

Enough talking about it. Let's see it in action.

I've got a classic data transformation for you. Something every Pythonista does daily.
-->

---
layout: center
transition: fade
class: text-left
---

<div class="w-full max-w-2xl">
<h1 class="text-4xl mb-6">The Python way</h1>

<div class="font-mono text-xl leading-loose bg-black/60 rounded-lg p-6">
<div>numbers <span class="text-pink-400">=</span> <span class="text-pink-400">list</span>(<span class="text-pink-400">range</span>(<span class="text-cyan-400">10</span>))</div>
<div v-click>evens <span class="text-pink-400">=</span> [x <span class="text-pink-400">for</span> x <span class="text-pink-400">in</span> numbers <span class="text-pink-400">if</span> x <span class="text-pink-400">%</span> <span class="text-cyan-400">2</span> <span class="text-pink-400">==</span> <span class="text-cyan-400">0</span>]</div>
<div v-click>doubled <span class="text-pink-400">=</span> [x <span class="text-pink-400">*</span> <span class="text-cyan-400">2</span> <span class="text-pink-400">for</span> x <span class="text-pink-400">in</span> evens]</div>
<div v-click>result <span class="text-pink-400">=</span> <span class="text-pink-400">sum</span>(doubled)</div>
<div v-click class="text-green-400 op-80"><span class="text-gray-400">#</span> 40</div>
</div>

</div>

<BgEmoji emoji="🐍" :count="9" animate="drift" :opacity="0.10" :seed="21" />

<!--
Here's a classic. We start with range(10) - zero through nine. Same as Uiua's range glyph.

[click] We filter for evens - a list comprehension with a condition.

[click] Then we double each one. Another list comprehension.

[click] And sum it all up. One function call.

[click] Forty. Four lines. Very Pythonic. Very readable. We all know this.

Now let me show you the same thing in Uiua.
-->

---
transition: fade
class: text-center
clicks: 7
---

<div class="h-full w-full flex flex-col items-center justify-center">
<div class="text-2xl op-90 mb-4">The same transformation</div>
<div class="text-5xl font-mono mb-10 flex items-center justify-center gap-1">
  <span :class="$clicks === 7 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">/+</span><span :class="$clicks === 6 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">×2</span><span :class="$clicks === 5 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">▽</span><span :class="$clicks === 4 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">=0</span><span :class="$clicks === 3 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">◿2</span><span :class="$clicks === 2 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : $clicks >= 1 ? 'text-green-400 uiua-glow' : 'text-green-400 op-60'" class="transition-all duration-300">⟜∘</span><span :class="$clicks === 1 ? 'text-yellow-400 scale-125 uiua-glow-yellow' : 'text-green-400 op-60'" class="transition-all duration-300">⇡10</span>
</div>

<div class="text-2xl h-16 flex flex-col items-center justify-center">
  <div v-show="$clicks === 0" class="op-75">← read right to left</div>
  <div v-show="$clicks === 1" class="text-yellow-400"><span class="font-mono">⇡10</span> <span class="op-90 ml-2">range - gives us 0..9</span></div>
  <div v-show="$clicks === 2" class="text-yellow-400"><span class="font-mono">⟜∘</span> <span class="op-90 ml-2">duplicate - copy the array</span></div>
  <div v-show="$clicks === 3" class="text-yellow-400"><span class="font-mono">◿2</span> <span class="op-90 ml-2">modulo 2 - remainder of each</span></div>
  <div v-show="$clicks === 4" class="text-yellow-400"><span class="font-mono">=0</span> <span class="op-90 ml-2">equals 0 - mask of evens</span></div>
  <div v-show="$clicks === 5" class="text-yellow-400"><span class="font-mono">▽</span> <span class="op-90 ml-2">keep - filter by the mask</span></div>
  <div v-show="$clicks === 6" class="text-yellow-400"><span class="font-mono">×2</span> <span class="op-90 ml-2">multiply 2 - double them</span></div>
  <div v-show="$clicks === 7" class="text-yellow-400"><span class="font-mono">/+</span> <span class="op-90 ml-2">reduce add - sum to one number</span></div>
</div>

<div class="font-mono text-lg op-80 h-8 mt-2">
  <span v-show="$clicks === 1" class="text-green-300">→ [0 1 2 3 4 5 6 7 8 9]</span>
  <span v-show="$clicks === 2" class="text-green-300">→ [0..9] [0..9]</span>
  <span v-show="$clicks === 3" class="text-green-300">→ [0 1 0 1 0 1 0 1 0 1] · [0..9]</span>
  <span v-show="$clicks === 4" class="text-green-300">→ [1 0 1 0 1 0 1 0 1 0] · [0..9]</span>
  <span v-show="$clicks === 5" class="text-green-300">→ [0 2 4 6 8]</span>
  <span v-show="$clicks === 6" class="text-green-300">→ [0 4 8 12 16]</span>
  <span v-show="$clicks === 7" class="text-green-300 text-xl font-bold">→ 40</span>
</div>
</div>

<!--
[let it sit for 2 seconds]

Same transformation. One line. Watch the stack - right to left.

[click] Range of 10 - the stack now holds zero through nine.

[click] Duplicate - two copies on the stack. We'll need both.

[click] Modulo 2 - remainder of each. Top of stack becomes: 0, 1, 0, 1...

[click] Equals 0 - flips it into a boolean mask. Ones where even.

[click] Keep - uses that mask to filter. Stack shrinks to just the evens.

[click] Times 2 - doubles everything. [0 4 8 12 16].

[click] Reduce add - slash plus. The whole array collapses into a single number. Forty. Array in, number out. That's reduce.

See the data flowing? Each glyph transforms the stack. That's the whole language.
-->

---
transition: fade
class: text-center
---

<div class="h-full w-full flex flex-col items-center justify-center">
<div class="text-2xl op-90 mb-6">Change one glyph...</div>

<div class="text-5xl font-mono text-green-400 mb-8">

<span class="uiua-glow">/+</span><span>×</span><span class="text-yellow-400 uiua-glow-yellow-isolated relative z-10 px-0.5 inline-block">3</span><span>▽</span><span class="uiua-glow">=0◿2⟜∘⇡10</span>

</div>

<div v-click class="text-2xl op-90">Triple instead of double. One character.</div>
<div v-click class="font-mono text-xl text-green-300 op-80 mt-4">→ 60</div>
</div>

<!--
Now watch this.

I change ONE glyph. The 2 becomes a 3.

[click] Triple instead of double. One character.

[click] Sixty instead of forty. The whole pipeline - filter, transform, reduce - shifts with one keystroke.

In Python, you'd hunt through comprehensions to find the right variable. Here, the change is exactly where the meaning is.
-->

---
layout: statement
transition: fade
---

<div class="text-5xl font-bold leading-relaxed">
The code <span class="text-yellow-400">IS</span> the shape of the data.
</div>

<BgEmoji emoji="🚀" :count="5" animate="fly" :opacity="0.20" :seed="55" />

<!--
[pause - let this statement land]

This is the key insight. In Uiua, the code isn't describing what to do step by step. It's describing the SHAPE of the transformation.

You can literally SEE the data flowing through the glyphs. Filter here, multiply there, reshape here.

Once you get it, you can't unsee it.

And that brings us to the real question...
-->
