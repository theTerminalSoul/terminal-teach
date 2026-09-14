+++
date = '2026-09-14T16:11:35+05:30'
draft = false
title = 'Regex Is Weird'
+++

# Regex: The Shit Nobody Remembers 😭

Okay...

Tell me honestly.

How many times have you learned **Regex**?

1 time?  
2 times?  
5 times?

And yet, after 3 weeks, you see something like this:

```regex
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

And you're like:

> "What the fuck is this? 😭"

What kind of gibberish-looking text is this?

Yet somehow...

It's important.

Regex has been around for decades and is still used everywhere in tech — from searching text and processing logs to validating input and working with command-line tools.

So yeah...

You can hate it as much as you want.

But if you're in tech, you can't really ignore it.

So don't avoid it.  
Just learn the damn thing.  
Simple.

---

Okay Terminal, I get it.  
Regex is unavoidable.

But it's so damn hard... 😭

Yes.

But here's the thing:

Regex feels hard mainly because you don't understand what all those symbols actually mean.

Once you understand what each symbol does and get enough practice, Regex starts becoming much more intuitive.

And I'm here to teach you Regex in a way that hopefully makes you say:

> "Ohhh... that's what that symbol means."

So you don't have to relearn the whole damn thing every few months.

---

## 🤔 What Is a Regular Expression?

A **Regular Expression (Regex)** is a sequence of characters that defines a pattern used to search or match text.

Using Regex, you can create patterns that help you:

- Search for specific text  
- Find patterns inside text  
- Validate input  
- Extract information  
- Replace or transform text (when used with a tool that supports Regex)

You can do something as simple as finding a `,` in your text...

Or something more complicated like finding a pattern inside a huge log file.

For example, this:

```regex
ERROR
```

can be used to find occurrences of `ERROR`.

And this:

```regex
\d+
```

can find one or more digits.

So Regex is basically:

> A way of describing what you're looking for in text.

Before we jump into complicated patterns, let's clear up some basics.

---

## 🧱 Basics of Regular Expressions

Let's start with the characters you're going to see everywhere.

### 1. Escape Character — `\`

The backslash `\` is called the **escape character**.

It is used when you want to treat a character literally instead of giving it its special Regex meaning.

For example, the dot:

```regex
.
```

has a special meaning in Regex.  
It doesn't mean an actual `.`.  
It means **any character**.

So if you want to match an actual dot:

```regex
\.
```

The backslash tells Regex:

> "Hey, I actually mean the dot character here. Don't treat it as a special Regex symbol."

You'll see this a lot in Regex.

---

### 2. Any Character — `.`

The dot:

```regex
.
```

matches **any single character** in many Regex implementations.

For example:

```text
cat
```

The pattern:

```regex
c.t
```

can match:

- `cat`  
- `cut`  
- `c9t`  
- `c-t`  

because the `.` can represent that middle character.

That's also why, when we want to match an actual dot, we use:

```regex
\.
```

---

### 3. Digit — `\d`

The:

```regex
\d
```

represents a **digit**.

In many common Regex flavors, this means:

- `0 1 2 3 4 5 6 7 8 9`

For example:

```regex
\d
```

can match:

- `7`

And:

```regex
\d\d
```

can match:

- `42`

You can also use a quantifier:

```regex
\d+
```

which means:

> One or more digits.

So it can match:

- `7`  
- `42`  
- `123`  
- `98765`  

---

### 4. Not a Digit — `\D`

The uppercase version:

```regex
\D
```

does the opposite of `\d`.

It matches a character that is **not a digit**.

So:

- `\d` → digit  
- `\D` → not a digit  

Think of uppercase as the opposite in these common shorthand character classes.

---

### 5. Word Character — `\w`

The:

```regex
\w
```

matches a **word character**.

In many common Regex flavors, this includes:

- `a-z`  
- `A-Z`  
- `0-9`  
- `_`  

So:

```regex
\w
```

can match:

- `a`  
- `Z`  
- `7`  
- `_`  

For example:

```regex
\w+
```

can match:

- `hello`  
- `hello123`  
- `user_name`  

> ⚠️ The exact definition of `\w` can vary between Regex implementations, especially when Unicode is involved.

---

### 6. Not a Word Character — `\W`

The uppercase version:

```regex
\W
```

matches a character that is **not a word character**.

So:

- `\w` → word character  
- `\W` → not a word character  

For example, characters such as:

- `!`  
- `@`  
- `#`  
- `$`  
- `%`  

can match `\W` in common Regex flavors.

---

### 7. Whitespace — `\s`

The:

```regex
\s
```

matches **whitespace characters**.

This can include things like:

- Space  
- Tab  
- Newline  

For example:

```text
Hello World
```

There is a space between `Hello` and `World`.  
That space can be matched using:

```regex
\s
```

So:

```regex
Hello\sWorld
```

can match:

- `Hello World`  

---

### 8. Beginning of String/Line — `^`

The caret:

```regex
^
```

is commonly used as an **anchor** for the beginning of a string or line.

For example:

```regex
^Hello
```

means:

> "Hello must appear at the beginning."

So this can match:

- `Hello Terminal`  

but not:

- `Hey Hello Terminal`  

> ⚠️ The exact behavior of `^` can depend on the Regex tool and whether multiline mode is enabled.

---

### 9. End of String/Line — `$`

The dollar sign:

```regex
$
```

is commonly used as an **anchor** for the end of a string or line.

For example:

```regex
world$
```

means:

> "world must appear at the end."

So this can match:

- `Hello world`  

but not:

- `world is cool`  

Together, `^` and `$` are extremely useful when you want to match the whole string.

For example:

```regex
^Hello$
```

would only match:

- `Hello`  

---

## 🧩 Character Classes

Okay Terminal...

I got the basic characters.

But what if I want to match a character that belongs to a particular group?

No worries.

Regex has something called a **character class**.

### 1. Character Class — `[]`

Square brackets:

```regex
[]
```

are used to create a character class.

A character class tells Regex:

> "Match one character from this set."

For example:

```regex
[aeiou]
```

matches any one vowel:

- `a`  
- `e`  
- `i`  
- `o`  
- `u`  

So if you search:

```regex
c[aeiou]t
```

it can match:

- `cat`  
- `cet`  
- `cit`  
- `cot`  
- `cut`  

The important thing to remember:

```regex
[abc]
```

does **not** mean "match `abc`."

It means:

> Match one character that is either `a`, `b`, or `c`.

#### What About `.` Inside `[]`?

Remember earlier when I told you:

```regex
.
```

has a special meaning?

Inside a character class, many Regex metacharacters lose their special meaning.

So:

```regex
[.]
```

can match an actual dot.

You generally don't need:

```regex
[\.]
```

although the exact escaping rules can vary by Regex flavor.

---

### 2. Negated Character Class — `[^]`

What if we want the opposite?

Instead of:

> Match a vowel.

We want:

> Match anything except a vowel.

That's where the caret comes in:

```regex
[^aeiou]
```

This is a **negated character class**.

It means:

> Match one character that is NOT `a`, `e`, `i`, `o`, or `u`.

For example:

```regex
[^0-9]
```

means:

> Match any character that is not a digit.

Be careful:

```regex
[^aeiou]
```

is different from:

```regex
^aeiou
```

The `^` has a different meaning depending on where it appears.

- At the beginning of a character class: `[^...]` → **NOT**  
- Outside a character class: `^` → commonly an anchor for the beginning of a string/line.

---

### 3. Alternation — `|`

The pipe:

```regex
|
```

works like **OR**.

For example:

```regex
cat|dog
```

means:

> Match `cat` OR `dog`.

So it can match:

- `I have a cat.`  

or:

- `I have a dog.`  

Think of it like:

> `cat` OR `dog`

Simple.

---

## 🔢 Quantifiers

Okay Terminal...

What if I want to match more than one character?

Regex got you covered there too.

We have something called **quantifiers**.

As the name suggests, quantifiers tell Regex how many times something should be matched.

And this "something" can be a character, character class, or group.

### 1. Zero or More — `*`

The asterisk:

```regex
*
```

means:

> Match the previous character, class, or group **zero or more times**.

For example:

```regex
ab*
```

can match:

- `a`  
- `ab`  
- `abb`  
- `abbb`  
- `abbbb`  

Why?

Because the `b` can appear zero or more times.

- `a` + zero `b`s → `a`  
- `a` + one `b` → `ab`  
- `a` + two `b`s → `abb`  

---

### 2. One or More — `+`

The plus:

```regex
+
```

means:

> Match the previous character, class, or group **one or more times**.

For example:

```regex
ab+
```

can match:

- `ab`  
- `abb`  
- `abbb`  
- `abbbb`  

But it **won't** match:

- `a`  

because at least one `b` is required.

So remember:

- `*` → 0 or more  
- `+` → 1 or more  

---

### 3. Zero or One — `?`

The question mark:

```regex
?
```

means:

> Match the previous character, class, or group **zero or one time**.

For example:

```regex
colou?r
```

can match:

- `color`  
- `colour`  

The `u` is optional.

So:

- `?` → optional  

That's a pretty useful one.

---

### 4. Exact Number — `{n}`

Curly brackets let us specify exactly how many times something should appear.

For example:

```regex
a{4}
```

means:

> Match exactly 4 `a` characters.

So it can match:

- `aaaa`  

but not:

- `aaa`  
- `aaaaa`  

Remember:

- `{4}` → exactly 4  

---

### 5. Range — `{min,max}`

You can also specify a range.

For example:

```regex
a{1,3}
```

means:

> Match between 1 and 3 `a` characters.

So it can match:

- `a`  
- `aa`  
- `aaa`  

But not:

- `aaaa`  

You can also leave out the maximum:

```regex
a{2,}
```

This means:

> Match 2 or more `a` characters.

So:

- `aa`  
- `aaa`  
- `aaaa`  
- `aaaaa`  
- ...  

can all match.

---

## 🧠 Let's Put Everything Together

Okay Terminal...

We've learned a lot of symbols.

Let's go back to the Regex we saw at the beginning:

```regex
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

Before reading this blog, this probably looked like:

> Gibberish. 👽

Now let's break it down.

- `^`  
  Start of the string.

- `[a-zA-Z0-9._%+-]+`  
  One or more characters from this character class.

- `@`  
  An actual `@` character.

- `[a-zA-Z0-9.-]+`  
  One or more characters from this character class.

- `\.`  
  An actual dot.

- `[a-zA-Z]{2,}`  
  Two or more letters.

- `$`  
  End of the string.

So now this:

```regex
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

doesn't look quite as scary anymore.

Right? 😎

> ⚠️ This is a simplified email pattern for learning Regex. Real-world email validation is more complicated, so don't treat this as a complete RFC-compliant email validator.

---

## 🎯 That's Regex... For Now

Well...

That's not everything Regex can do.  
Not even close. 😂

But you've learned the building blocks.

You now know:

```text
\       → Escape
.       → Any character
\d      → Digit
\D      → Not a digit
\w      → Word character
\W      → Not a word character
\s      → Whitespace
^       → Beginning
$       → End

[]      → Character class
[^]     → Negated character class
|       → OR

*       → 0 or more
+       → 1 or more
?       → 0 or 1
{n}     → Exactly n
{n,m}   → Between n and m
```

And that's already enough to start understanding a lot of Regex patterns.

---

## 🧠 Don't Memorize Regex

Here's the most important thing I want you to take away from this blog:

> **Don't memorize Regex. Understand how to build the pattern.**

You are going to forget these symbols.  
I guarantee it. 😂

You'll see a Regex six months from now and still think:

> "What the fuck is this?"

And that's okay.

Because now you know how to break it down.

You can look at:

```regex
\d+
```

and think:

- `\d` → digit  
- `+` → one or more  

Therefore:

> one or more digits

That's the real skill.

---

## 🏁 Now Go Practice

Reading Regex once isn't going to make you good at Regex.

You need to actually write patterns.

Try creating Regex patterns for things like:

- Find all numbers in a text  
- Find words starting with `A`  
- Find `.txt` files  
- Find phone numbers  
- Find IP addresses  
- Find dates  
- Find email-like patterns  

The more you practice, the more intuitive it becomes.

And when you eventually forget Regex...

Don't panic.

You now know exactly where to find the notes. 😎

And yes...

AI is also there. 😂

But don't just copy a Regex from AI.

Ask:

> "Explain this Regex to me."

Because the goal isn't to memorize the pattern.

The goal is to understand **why** the pattern works.

Now go practice.
