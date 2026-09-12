+++
date = '2026-09-08T23:42:51+05:30'
draft = false
title = 'Compress and Archive That Thing.'
+++

# Wait… What the Hell Is `.tar.gz`? 📦🗜️

Today we are going to learn about **compressing and archiving files** in Linux.

But wait, Terminal… 🤔

**What exactly are Compression and Archiving?**

<!--more-->

## 📦 Archiving

Let's say you have 10 files:

```text
file1.txt
file2.txt
file3.txt
...
file10.txt
````

And you want to bundle all of them together into **one file**.

That's where **archiving** comes in.

Archiving means taking multiple files and directories and putting them together into a **single archive file**.

> ⚠️ One important thing: an archive is not the same thing as a folder.
> An archive is a file that contains other files and directories.

Archiving **does not necessarily reduce the size** of your files. It mainly **bundles them together**.

For example:

You have 10 files, each 10 MB in size:

```text
10 files × 10 MB = 100 MB
```

After archiving them, you might get:

```text
files.tar → ~100 MB
```

The exact size can be slightly different because of metadata and how the archive is created, but **tar itself is not being used to compress the data**.

Think of it like putting 10 books into **one box** 📦.

The books didn't become smaller.

You just put them together.

---

## 🗜️ Compression

Now let's talk about **compression**.

Compression is the process of reducing the amount of space required to store data.

For example, imagine you have a 100 MB file and you want to send it somewhere, but the service has a much smaller file-size limit.

If the data is highly compressible, compression might reduce it significantly.

For example:

```text
Original:    100 MB
Compressed:   25 MB
```

The receiver can then **decompress** the file and get the original data back.

> ⚠️ Compression does not always reduce a file to a specific size.
> You can't simply tell gzip "make this 100 MB file exactly 15 MB."
> The result depends on the data.

And yes, there are different types of compression and different compression algorithms.

> How does compression actually work internally?
> That's a topic for another blog. 😎

---

# 🤔 So What's the Difference?

At this point, you might be thinking:

**"Terminal, just tell me the difference!"**

Easy.

| Archiving 📦                                | Compression 🗜️                         |
| ------------------------------------------- | --------------------------------------- |
| Combines files/directories into one archive | Reduces the size of data                |
| Does not primarily focus on reducing size   | Specifically focuses on reducing size   |
| Example: `tar`                              | Example: `gzip`                         |
| Think: putting books in one box             | Think: making the books take less space |

And here's the important part:

**We can combine both!**

That's exactly what we commonly do in Linux.

---

# 🐧 How Do We Do This in Linux?

Okay Terminal, now I understand what compression and archiving are.

But...

**How do I actually do this in Linux?** 🤔

Don't worry. It's pretty easy.

There are several programs available for this, but today we'll focus on:

1. `tar` → Archiving 📦
2. `gzip` → Compression 🗜️

---

# 📦 What is `tar`?

`tar` is a Linux utility used to **create and extract archives**.

An archive created with `tar` is commonly called a **tarball**.

A basic `tar` command looks like this:

```bash
tar [options] archive-name files/directories
```

For example:

```bash
tar -cvf files.tar file1.txt file2.txt file3.txt
```

Let's break it down:

```text
-c  → create a new archive
-v  → verbose (show what is happening)
-f  → specify the archive filename
```

So:

```bash
tar -cvf files.tar file1.txt file2.txt file3.txt
```

means:

> "Hey tar, create (`-c`) an archive, show me what you're doing (`-v`), and save it as `files.tar` (`-f`)."

You can also archive an entire directory:

```bash
tar -cvf my_files.tar my_folder/
```

Now `my_files.tar` contains everything inside `my_folder`.

---

# 🗜️ What is `gzip`?

Now we have our archive.

But Terminal...

**It's still the same size! 😭**

Exactly.

Remember, `tar` is primarily for **archiving**, not compression.

This is where `gzip` comes in.

`gzip` is a compression utility that compresses files and reduces their size when the data is compressible.

The basic command is:

```bash
gzip [options] filename
```

For example:

```bash
gzip file.txt
```

This will create:

```text
file.txt.gz
```

By default, `gzip` removes the original uncompressed file after successful compression.

If you want to keep the original file, use:

```bash
gzip -k file.txt
```

Here are some useful options:

```text
-k  → keep the original file
-d  → decompress
-r  → recursively process files in directories
-l  → display compression information
```

To decompress a `.gz` file:

```bash
gzip -d file.txt.gz
```

---

# ⚠️ One Important Thing About `gzip`

Here's something you should remember:

> **gzip works on files, not on directories as a single compressed object.**

So if you try to directly gzip a directory, that's not the normal workflow.

Instead, we first **archive the directory with `tar`**, and then compress the resulting archive.

And this brings us to the really useful part. 👇

---

# 📦 + 🗜️ Archiving AND Compression

What if I want to archive an entire directory **and** compress it?

Simple.

We combine `tar` and `gzip`.

```bash
tar -czvf files.tar.gz my_folder/
```

Look at the options:

```text
-c  → create archive
-z  → use gzip compression
-v  → verbose
-f  → specify filename
```

So:

```bash
tar -czvf files.tar.gz my_folder/
```

means:

> "Create a tar archive, compress it using gzip, and save it as `files.tar.gz`."

🔥 Now we're doing both:

```text
my_folder/
     ↓
   tar
     ↓
  archive
     ↓
  gzip
     ↓
files.tar.gz
```

To extract it again:

```bash
tar -xzvf files.tar.gz
```

Here:

```text
-x  → extract
-z  → gzip
-v  → verbose
-f  → archive filename
```

---

# 🤔 What About `-j`?

You might also see this:

```bash
tar -cjvf files.tar.bz2 my_folder/
```

The `-j` option tells `tar` to use **bzip2** compression.

You may also come across:

```bash
tar -cJvf files.tar.xz my_folder/
```

Here `-J` tells `tar` to use **xz** compression.

So you can remember it like this:

```text
.tar       → tar archive
.tar.gz    → tar + gzip
.tar.bz2   → tar + bzip2
.tar.xz    → tar + xz
```

---

# 📊 What is Compression Ratio?

Okay Terminal...

**What does "compression ratio" actually mean?** 🤔

The compression ratio tells us how much smaller the compressed data is compared with the original.

For example:

```text
Original size:   100 MB
Compressed size: 25 MB
```

That's a:

```text
4:1 compression ratio
```

Why?

Because:

```text
100 ÷ 25 = 4
```

So the original data is **4 times the size** of the compressed data.

A simple way to think about it:

```text
Original
████████████████████ 100 MB

Compressed
█████                 25 MB
```

However, don't expect every file to achieve a 4:1 ratio.

A text file might compress very well, while an already-compressed file such as a JPEG or MP4 may barely get smaller.

---

# 🎯 That's It!

So now you know the difference between **archiving** and **compression**.

Remember:

```text
Archiving   → Put multiple files together 📦
Compression → Make data take less space 🗜️
```

And Linux lets us combine both:

```bash
tar -czvf archive.tar.gz folder/
```

So next time you see something like:

```text
backup.tar.gz
```

you'll know what's happening.

It's basically:

**`tar` + `gzip` = archive + compression** 😎

And that's the basic idea behind compressing and archiving files in Linux.

