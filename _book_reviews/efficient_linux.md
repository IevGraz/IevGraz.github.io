---
title: 'Efficient Linux at the Command Line'
author:  Daniel J. Barrett
rating: 4
date: 2023-08-16
goodreads_link: https://www.goodreads.com/book/show/59841860-efficient-linux-at-the-command-line
---

**Why I read this book:** I bought this book a while ago, because I felt that my command line skills and understanding of Unix systems is weaker than most of the other senior backenders I’ve worked with. The final push to reading it was moving to the platform backend team. There I encountered more tasks related to writing bash scripts and colleagues sighing deeply at me moving to the beginning of a terminal line by tapping arrow keys multiple times.

**How I read this book:**  My initial idea was to read it while sitting at the computer and trying every single example given in the book. But my partner read the book first and his advice was to just read it and add sticky notes to the places that I actually want to explore in practice later. I tried this approach and it helped me to get through the book faster and enjoy it more. I did come back to some of the pages I marked, but I have to admit I lacked the willpower to go through everything I’ve intended. 

**What I liked about it:**

My initial feeling when I started reading the book was “Where have you been all my life?!” as it explained a lot of the things I picked up from colleagues and google searches over the years, but never fully understood. 

For example, occasionally I have to find a PID of a certain process and use it to kill it. But I never gave much thought to what the PIDs are. Some quotes from the book I found useful on this topic:

> When you run a linux command, it launches one or more processes, each with a numeric process ID called PID. <...> Even when you run a simple command like `ls`, that command runs inside a new child process with its own (copied) environment. Any changes you make to a child, affect only the child and are lost when the child exists. Likewise, any changes to the parent won’t affect its children that are already running. 

I also remember copy-pasting some snippets of a bash script and seeing `$(..)` syntax in them. I remember being curious what that means and when I should use it. But I never got to googling it. Yet thanks to this book I now know:

> The syntax `$(any command here)` is called command substitution. It executes the command inside parentheses and replaces the command by its output.

Another good thing about this book is that it promotes the idea of being as efficient with your work as possible. From key combinations to navigate the terminal faster to an entire chapter on being more efficient at the keyboard and minimizing how much you use the mouse. I’d like to pick up more of these habits. For now I got comfortable with jumping between the beginning and the end of the terminal line.


**What I disliked:**
This is not a specific thing I disliked about the book, but I read the first half eagerly and then I couldn’t force myself to pick it up again for a good month. It is only 200 pages, but it took me 2.5 months to read it cover to cover. It might be due to the fact that I put a bit too much pressure on what I can get out of this book - I planned to consider it finished only after I have read it, practiced all the things I highlighted and gone through an `awk` or a `sed` tutorial online. I got back to it once I agreed with myself that just reading it is good enough for now.

Despite that, I would recommend this book for any developer who doesn’t feel too comfortable at the command line. It is easy to read and really helps to fill the gaps in the basics. 
