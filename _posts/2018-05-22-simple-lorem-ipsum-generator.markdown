---
layout: post
title:  "Exercise in Simplicity: Lorem Ipsum Generator in go"
date:   2018-05-22 20:29:38 +0300
categories: [software, programming, go, minimalism]
---

As I was considering my options for setting up my blog, very early on I decided I would use a static site generator for the multitude of benefits it gives me:
  * As a developer I am used to using `git` and working with simple text files.
  * Markdown is quite pleasant to write in and is familiar from `README` files etc.
  * Static websites can be hosted basically anywhere.
  * Quite secure since there is no server to run code on or database to inject.

While I did eventually settle on [jekyll](https://jekyllrb.com), I spent some time evaluating the options found on [staticgen.com](https://www.staticgen.com).

While evaluating I wanted to get a feel for how different lengths of text would look like on different templates. For this I looked for a lorem ipsum generator that I could run on the command line and easily pipe into some dummy `.markdown` files.

To my moderate surprise, I couldn't find a program that would let me simply generate a paragraph of lorem ipsum. Perhaps most people just copy and paste from a website and go on with their day. Perhaps I should have as well, but I decided to use this as an excuse to try out some [go](https://golang.org). 

I started with the default hello world:
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello")
}
```

And pretty quickly typed out a first attempt:
```go
package main

import (
	"bufio"
	"flag"
	"fmt"
	"os"
	"strings"
)

func main() {
	loremWords := strings.Fields("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.")
	loremWordsCount := len(loremWords)
	wordCountPtr := flag.Int("words", loremWordsCount, "number of words")
	flag.Parse()

	if *wordCountPtr > loremWordsCount {
		w := bufio.NewWriter(os.Stdout)
		for i := 0; i < *wordCountPtr; i++ {
			index := i % loremWordsCount
			w.WriteString(loremWords[index])
			if i != *wordCountPtr-1 {
				w.WriteString(" ")
			} else {
				w.WriteString("\n")
			}
		}

		w.Flush()
	} else {
		fmt.Println(strings.Join(loremWords[:*wordCountPtr], " "))
	}

}
```

Now, this worked and was able to generate as much lorem ipsum as I wanted:

```bash
$ ./lorem -words 2
Lorem ipsum
```
Job well done, right?

Well, _no_. As someone coming in and seeing the usage for the generator, I would have been surprised that I needed to give a named argument for the number of words. I would have expected to able to type:
```bash
$ ./lorem 2
```
to get two words. Not to mention a useless `if` statements, over-engineering with the `flag` package.. Point being, it took quite a few iterations to be satisfied with this basically trivial program. Getting it right the first time is a skill I am still working on (and will probably continue working on forever, *sigh*). 

After a few more tries I finally landed on this:
```go
package main

import (
	"bufio"
	"os"
	"strconv"
	"strings"
)

func main() {
	var wordCount int
	if len(os.Args) > 1 {
		wordCount, _ = strconv.Atoi(os.Args[1])
	}

	loremWords := strings.Fields("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.")
	loremWordsCount := len(loremWords)
	if wordCount <= 0 {
		wordCount = loremWordsCount
	}
	w := bufio.NewWriter(os.Stdout)
	for i := 0; i < wordCount; i++ {
		index := i % loremWordsCount
		w.WriteString(loremWords[index])
		if i != wordCount-1 {
			w.WriteString(" ")
		} else {
			w.WriteString("\n")
		}
	}
	w.Flush()
}
```

Now I'm not claiming it to be the best example of go code ever but it does what I would expect it to do as a user. Call it without arguments, get the default Lorem ipsum.. paragraph, call it with a number and you get that many words.

Perhaps next time when someone is looking for a lorem ipsum generator, they can find an unsurprising one faster than I could. The final version can be found on [GitHub](https://github.com/spkerkela/lorem).

Thanks for reading!