---
layout: section
transition: fade
---

# Backup: Fibonacci

<!--
[only use these slides if there's time left or during Q&A]

Remember that alien-looking expression from the very beginning? Let's prove it works.
-->

---
layout: center
class: text-center
transition: fade
clicks: 10
---

<div class="font-mono text-center">
<div class="text-3xl text-green-400 op-80 mb-6 uiua-glow">⧻⇡10↯⊃(⊂⊙(↻1))⊃(⊂⊙(↻¯1))</div>

<div class="text-xl op-90 tracking-widest uppercase mb-8">fibonacci on the stack</div>

<div class="text-3xl mb-4 h-14 flex items-center justify-center text-yellow-400">
  <span v-show="$clicks === 0">[0 1]</span>
  <span v-show="$clicks === 1">[0 1 1]</span>
  <span v-show="$clicks === 2">[0 1 1 2]</span>
  <span v-show="$clicks === 3">[0 1 1 2 3]</span>
  <span v-show="$clicks === 4">[0 1 1 2 3 5]</span>
  <span v-show="$clicks === 5">[0 1 1 2 3 5 8]</span>
  <span v-show="$clicks === 6">[0 1 1 2 3 5 8 13]</span>
  <span v-show="$clicks === 7">[0 1 1 2 3 5 8 13 21]</span>
  <span v-show="$clicks === 8">[0 1 1 2 3 5 8 13 21 34]</span>
  <span v-show="$clicks >= 9" class="text-green-400 font-bold">[0 1 1 2 3 5 8 13 21 34]</span>
</div>

<div class="text-2xl op-90 h-10">
  <span v-show="$clicks === 0">start with [0 1]</span>
  <span v-show="$clicks === 1">0 + 1 = 1</span>
  <span v-show="$clicks === 2">1 + 1 = 2</span>
  <span v-show="$clicks === 3">1 + 2 = 3</span>
  <span v-show="$clicks === 4">2 + 3 = 5</span>
  <span v-show="$clicks === 5">3 + 5 = 8</span>
  <span v-show="$clicks === 6">5 + 8 = 13</span>
  <span v-show="$clicks === 7">8 + 13 = 21</span>
  <span v-show="$clicks === 8">13 + 21 = 34</span>
  <span v-show="$clicks >= 9">10 Fibonacci numbers. One line.</span>
</div>
</div>

<!--
[backup - only if asked or time allows]

Remember that "alien" expression from slide one? Let's prove it's not magic.

We start with zero and one.

[rapid-fire the clicks]

0 + 1 = 1. 1 + 1 = 2. 1 + 2 = 3. 2 + 3 = 5. 3 + 5 = 8...

[keep going] 5 + 8 = 13. 8 + 13 = 21. 13 + 21 = 34.

[click] Ten Fibonacci numbers. One line of code. Take the last two, add them, append. That's ALL this expression does.

The "alien" code from the beginning? Just this - repeated addition on a stack.
-->
