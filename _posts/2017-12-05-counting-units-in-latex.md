---
layout: 	post
title:  	"Counting Units Directly in LaTeX"
date:   	2017-12-05
published:	true
tags:		LaTeX
comments:   true
---

Ever wondered how to deal with requests like these, when writing your assignments in LaTeX?

>You have a maximum of two pages to do it. One page equals 2400 units (incl. letters, digits and spaces). 

Like many others, I've been in that situation, and as far as I know there doesn't exist a LaTeX package for inserting the unit count directly in the document. <a href="http://app.uio.no/ifi/texcount/">TeXcount</a> does exist, but it will require you to manually determine and write the character count, and doesn't count spaces as a part of the character count. So what to do?
  
Got a computer running macOS or Linux with a LaTeX installation? Say no more, here's what to do:

1. Make sure TeXcount works (i.e. does `texcount` work in the command line?). If not, install it.
2. Insert the following code in your preamble 

    ```latex
% Run texcount to get word and character count
\immediate\write18{texcount text.tex -template="{1}" -out=words.sum}
\immediate\write18{texcount text.tex -template="{1}" -char -out=chars.sum}
% Run bash commands to get the sum (i.e. unit count)
\immediate\write18{\unexpanded{paste -d+ words.sum chars.sum | bc > sum.sum}}
% Define macro \unitcount for including the unit count
\newcommand\unitcount{\input{sum.sum}}
```
3. Change `text.tex` to the relevant .tex file you want to count units in. Add more files if your document is split up.
4. Use `\unitcount` wherever you want it in your LaTeX document to get the unit count.

So, here's the caveat: it might slightly overestimate the character count. While TeXcount counts characters (abc etc.) and punctuation (,.), it doesn't count spaces. So here I'm using the amount of words as a proxy for spaces. Also, it will require your LaTeX-editor to allow shell escaping.

I'd like to one day make this work independently of the shell commands (which is why it doesn't just run as one combined shell command), but alas – if it works, it works.