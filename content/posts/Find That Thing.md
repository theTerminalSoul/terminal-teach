+++
date = '2026-09-12T21:11:23+05:30'
draft = false
title = 'Find That Thing'
+++

# Where the Hell Is My File? 🔎🐧

You will encounter many situations where you **know the file exists somewhere on your system**...

But where? 😕  
You have absolutely no idea.

In this case, you do:

```text
cd → ls → cd → ls → cd → ls
````

<!--more-->

And after 10 minutes...

**You're still looking for that damn file.** 😭

Well, stop doing that.

# 🔎 Linux Has Tools For This

Linux has tools that can help you find files and directories without manually wandering around your filesystem.

Today, we are going to learn one of those tools:

**`find`**

Okay Terminal, I got it.

There is a tool called `find` in Linux.

But...

**How do I actually use it?** 🤔

Why worry?

When Terminal is here... 😎

Hop onto the terminal and write it with me.

---

# 🧩 The `find` Command

The basic structure of the `find` command is:

```bash
find [path] [options] [expression]
```

Let's understand what these actually mean.

### 1. `path`

This is the location where you want `find` to search.

For example:

```bash
find .
```

The `.` means **the current directory**.

You can also give it an absolute path:

```bash
find /etc
```

Now `find` will search inside `/etc`.

### 2. `options`

Options can modify how `find` behaves.

They help you refine your search.

For example:

```bash
-type
-size
-mtime
```

### 3. `expression`

An expression tells `find` **what you're actually looking for**.

For example:

```bash
-name "log.txt"
```

So don't let this command structure scare you.

It's basically:

```text
Where should I search?
        ↓
How should I search?
        ↓
What am I looking for?
```

That's it!

This is the `find` command.

Go and enjoy life. 😎

...

Just kidding.

Let's actually learn how to use it. 😂

---

# 🔎 Finding Files by Name

Let's start with the most common use case.

Imagine you are looking for:

```text
log.txt
```

You know it exists somewhere in your current directory, but you don't know where.

You can use:

```bash
find . -name "log.txt"
```

This tells `find`:

> Search from the current directory (`.`) and find something whose name exactly matches `log.txt`.

The result might look something like:

```text
./logs/log.txt
```

### Case-sensitive vs Case-insensitive

Remember:

```bash
-name
```

performs a **case-sensitive** name match.

So:

```text
log.txt
```

and:

```text
Log.txt
```

are considered different names.

If you don't care about uppercase and lowercase, use:

```bash
find . -iname "log.txt"
```

Now:

```text
log.txt
Log.txt
LOG.TXT
LoG.TxT
```

can all match.

---

# 🧰 Useful `find` Options

Now that you understand searching by name, let's look at some useful ways to refine your search.

### `-type`

Use `-type` when you want to tell `find` what kind of filesystem object you're looking for.

For example:

```bash
find . -type f
```

This finds **files**.

And:

```bash
find . -type d
```

This finds **directories**.

Some useful types are:

```text
f → regular file
d → directory
l → symbolic link
```

So if you only want directories:

```bash
find . -type d
```

---

### `-size`

What if you know the file is huge?

For example, you want to find files larger than 100 MB:

```bash
find . -type f -size +100M
```

You can also search for files smaller than a particular size:

```bash
find . -type f -size -10M
```

The `+` and `-` can be used to search for sizes above or below the specified value.

> 💡 Be careful with the units. `find` supports units such as `k`, `M`, `G`, etc.

---

### `-mtime`

What if you want to find files based on when they were modified?

That's where `-mtime` comes in.

For example:

```bash
find . -type f -mtime -1
```

This finds files modified **within the last 24 hours**.

And:

```bash
find . -type f -mtime +7
```

finds files modified **more than 7 days ago**.

This can be really useful when you're trying to figure out:

> "Which files did I change recently?"

---

### `-empty`

What if you want to find empty files or directories?

Easy:

```bash
find . -empty
```

This finds empty files and directories inside the current directory.

You can also combine it with `-type`:

```bash
find . -type f -empty
```

This finds only empty files.

Or:

```bash
find . -type d -empty
```

This finds only empty directories.

---

### `-perm`

You can even search for files based on their permissions.

For example:

```bash
find . -type f -perm 644
```

This searches for files with the specified permission mode.

Permissions are a whole topic by themselves, so we won't go too deep into them here.

---

# 🤔 Okay Terminal...

I got it.

We can use different expressions to make our search more specific.

But what if I want to **do something with the files I find?**

For example:

* Find empty files and delete them
* Find files and change their permissions
* Find files and run another command on them

Do I really have to:

```text
find the file
        ↓
look at the result
        ↓
write another command
        ↓
run it again
```

That's boring...

And not very productive. 😭

Good question.

You can actually perform an operation on the files that `find` discovers.

And one of the most useful ways to do this is:

**`-exec`**

---

# ⚡ The `-exec` Option

`-exec` allows you to run another command on the files found by `find`.

The general structure looks like this:

```bash
find [path] [expression] -exec command {} \;
```

The important part is:

```text
{}   → represents the file currently found by find
\;   → tells find where the -exec command ends
```

For example:

```bash
find . -type f -empty -exec ls -l {} \;
```

This finds empty files and runs:

```bash
ls -l
```

on each file.

---

# 💀 Let's Delete Something

Okay...

Enough looking at files.

Let's destroy some. 💀

If you want to delete empty files:

```bash
find . -type f -empty -delete
```

This is much simpler than using `-exec`.

But if you specifically want to understand `-exec`, you could do:

```bash
find . -type f -empty -exec rm -i {} \;
```

Here:

```text
rm   → removes the file
-i   → asks for confirmation
{}   → represents the file found by find
\;   → ends the -exec command
```

So `find` finds the files, and `rm` removes them.

> ⚠️ **Be very careful when combining `find` with commands like `rm`.**
> A wrong search condition can delete many files at once.
> Always test your `find` command first without `-delete` or `rm`.

For example, first run:

```bash
find . -type f -empty
```

Check the results.

**Then** decide whether you actually want to delete them.

---

# 🧩 Finding Files Using Patterns

Okay Terminal...

What if I don't remember the exact filename?

I only remember that it ends with:

```text
.txt
```

No problem.

We can use a wildcard:

```bash
find . -type f -name "*.txt"
```

This finds all regular files ending with `.txt`.

For example:

```text
notes.txt
passwords.txt
todo.txt
linux.txt
```

The `*` means:

> "Anything can come before `.txt`."

You can make even more specific searches.

For example:

```bash
find /etc -type f -name "*.conf"
```

This searches `/etc` for regular files ending with `.conf`.

---

# 📏 Finding Files by Name AND Size

Now let's combine multiple conditions.

Suppose you want to find:

* regular files
* inside `/etc`
* ending with `.txt`
* larger than 100 MB

You can write:

```bash
find /etc -type f -name "*.txt" -size +100M
```

Now `find` has to satisfy **all of those conditions**.

This is where `find` becomes really powerful.

You can keep combining conditions to make your search more precise.

---

# 🌳 Finding the Directory Hierarchy

What if you simply want to see all the directories under your current location?

Easy:

```bash
find . -type d
```

You'll get something like:

```text
.
./Documents
./Documents/Linux
./Documents/Linux/Notes
./Downloads
./Projects
./Projects/Java
./Projects/Python
```

It gives you a view of the directory structure.

> 💡 There are other programs specifically designed for displaying directory structures, such as `tree`.

For example:

```bash
tree
```

But if your goal is **finding directories**, `find` is the tool you want.

---

# 🔍 `find` vs `locate`

Okay Terminal...

One more thing.

If you've used Linux for a while, you may have heard about another command:

```bash
locate
```

So what's the difference?

The main difference is **how they search**.

### `find`

`find` searches the filesystem when you run the command.

For example:

```bash
find /home -name "notes.txt"
```

It actually walks through the directories and checks the filesystem.

Because of this, searching a large filesystem can sometimes take a while.

### `locate`

`locate` searches a **database of filenames** instead of walking through the filesystem every time.

That's why it can be much faster.

But there's a catch. 👀

The database may not immediately contain files that were created recently.

So `locate` can sometimes miss a newly created file until its database is updated.

In short:

```text
find
 ↓
Searches the filesystem directly
 ↓
Can be slower
 ↓
Sees current filesystem contents

locate
 ↓
Searches a filename database
 ↓
Usually much faster
 ↓
Database may need to be updated
```

So if you need a current filesystem search:

**`find` is your friend.** 🤝

---

# 🎯 That's It!

Well...

Not really. 😂

`find` can do **a lot more** than what we covered here.

You can search by:

* Name
* Type
* Size
* Modification time
* Permissions
* Empty files/directories
* Patterns
* And much more

You can also combine these conditions and execute other commands on the results.
But don't try to memorize everything.
**Learn what you need, and learn more as you use it.**

---

# 🧠 The Commands You Should Remember

If you forget everything else from this blog, remember these:

```bash
# Find by name
find . -name "log.txt"

# Case-insensitive name search
find . -iname "log.txt"

# Find files
find . -type f

# Find directories
find . -type d

# Find files larger than 100 MB
find . -type f -size +100M

# Find files modified within the last 24 hours
find . -type f -mtime -1

# Find empty files
find . -type f -empty

# Find .txt files
find . -type f -name "*.txt"

# Execute a command on found files
find . -type f -exec command {} \;
```

And remember:

```text
You don't need to know every option.

You just need to know how to find the one you need.
```
So the next time you forget where you put a file...
Don't do:
```text
cd → ls → cd → ls → cd → ls
```
Just:

```bash
find
```
🔎🐧
**Now go practice.**

