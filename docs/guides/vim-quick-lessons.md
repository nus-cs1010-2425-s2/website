# Quick `vim` Lessons

Here is a quick walkthrough to get a taste of `vim.`

## Lesson 1: Navigation

Download the following file for practice using `vim` in this session.
```
$ wget https://raw.githubusercontent.com/nus-unix-workshop/2021-s1/master/jfk.txt
```

The file named `jfk.txt` should be downloaded.  Now let's start your first `vim` session.

```
$ vim jfk.txt
```

When you start, you will be in `NORMAL` mode.  For now, just move around the cursor with ++h++ ++j++ ++k++ ++l++.  Get comfortable using the keys.

Next, try ++parenthesis-left++ and ++parenthesis-right++ to move forward and backward, sentence-by-sentence.

Next, try ++brace-left++ and ++brace-right++ to move forward and backward, paragraph-by-paragraph.

Now, try ++control+f++ and ++control+b++ to move forward and backward, page-by-page.

Use ++0++ to jump to the beginning of the line, and ++shift+4++ (++dollar++) to jump to the end of the line.

Use ++g+g++ to jump to the beginning of the file, and ++shift+g++ (`G`) to jump to the last line of the file.

Now try ++slash++, type in any word (or prefix of a word) and ++enter++.  This should move the cursor to the beginning of the word.  You can use ++n++ and ++shift+n++ to move to the next match and the previous match.

When you are comfortable moving around, you can ++shift+z+z++ to exit.

Congratulations, you have just completed your first session in `vim`!

## Lesson 2: Manipulating Text

Now, we are going to open up the same file again and try to manipulate the text.  We are going to stay in the `NORMAL` mode still.

```
$ vim jfk.txt
```

### Deletion

Try ++0++ ++d++ ++3++ ++w++ to move the cursor to the beginning of the line and delete three words.

Press ++u++ to undo.  This is another lifesaver that you should remember.

In `vim`, repeating the same command twice usually means applying it to the whole line.  So ++d++ ++d++ deletes the current line.  Try that.

Pairing a command with ++shift++ (or the capital letter version) usually means applying the action until the end of the line.  So ++shift+d++ deletes from the current cursor until the end of the line.

### Copy-Pasting

Hit ++p++ to paste back what you just deleted.  Try moving the cursor to somewhere else and paste.

To copy (or yank) the current line, hit ++y++ ++y++.

Remember that all these commands can be composed using the movement-action-movement pattern.  For instance, ++shift+9++ ++y++ ++shift+0++, which corresponds to: move to the beginning of the sentence, yank, and until the end of the sentence, basically copy the current sentence.

As you have seen in the ++d++ ++2++ ++w++ example, you can precede an action with a number to repeat an action multiple times.

Try ++y++ ++y++ ++9++ ++p++.  You should be able to understand what just happened!

### Deleting a Character

The ++x++ command deletes the current character.

Try this exercise: At the end of the file `jfk.txt`, there are some typos:
```
libertyi. liberty.
```
Change `libertyi. liberty.` to `libtery.` by positioning the cursor on the second `i` and deleting it.  Then use ++shift+d++ to delete the extra `liberty.` at the end of the sentence.

### Visual Mode

In addition to the `INSERT` and `NORMAL` modes, `vim` has the third mode, the `VISUAL` mode.  You can enter the `VISUAL` mode by hitting ++v++.  Once in visual mode, you can move your cursor to select the text and perform some actions on it (e.g., ++d++ or ++x++ to delete, ++y++ to yank).

Hitting ++shift+v++ will allow you to select line-by-line.

The `VISUAL` mode allows us to pipe the selected text to another Unix command, and replace it with the result of that command.

Go ahead and try to select a paragraph in `jfk.txt`, and hit ++colon++.  You will see that
```
:'<,'>
```

appears in the last line of the terminal.  At this point, you can type in actions that you want to perform on the selected text.  For instance,
```
:'<,'>w john.txt
```

will write it to a file named `john.txt`.

But, let's try the following:
```
:'<,'>!fmt
```

`!fmt` tells `vim` to invoke the shell and run `fmt`.  `fmt` is another simple small Unix utility that takes in a text (from standard input) and spews out formatted text in the standard output.  You will see that the width of the text has changed to the default of 65.

You can try something that we have seen before.  Select the text again, and hit
```
:'<,'>!wc
```

The selected text will be replaced with the output from `wc`.

### The `:` command

You have seen examples of `:` commands for writing to a file or piping selected text to an external command.

The `:` command also enables many actions that you can do in `vim`.  Here are a few essential yet simple commands.

- To jump to a line, hit ++colon++ followed by the line number.
- To open another file, hit ++colon++ and then type in `e <filename>`
- To find help on a topic, hit ++colon++ and then type in `help <keyword>`

Other advanced features such as search-and-replace, changing preferences, splitting windows, and opening new tabs, are also accessible from the `:` command.

The `:` command prompt supports ++control+p++ and ++control+n++ for navigating back and forth your command history, just like `bash`.  It also supports ++tab++ for auto-completion.

## Lesson 3: Insert mode!

Finally, we are going to try inserting some text.  Remember, to use `INSERT` mode, we always start with a command ++i++ ++a++ ++o++ or ++s++ (may pair with ++shift++) followed by the text that
you want to insert, followed by ++esc++.

Let's try ++i++ (insert).  Place your cursor anywhere, hit ++i++, and start typing, when you are done.  Hit ++esc++.

You just added some text to the file.

Place your cursor anywhere, hit ++a++ (append), and start typing, when you are done.  Hit ++esc++.  ++a++ appends the text to the end of the current line.

Hit ++o++ (open) and start typing, when you are done.  Hit ++esc++.  ++o++ opens up a new line for your text.

Hit ++s++ (substitute) and start typing, when you are done.  Hit ++esc++.  ++s++ substitute the current character with your text.

Now try it with ++shift++ and see the difference in behavior.

## Learning More

You can run `vimtutor` to learn more about `vim`.  Check out [the tips that we have collected for CS1010](vim-operations.md), or watch the various tutorials online.  Here are some interesting ones are:

- [Vim Genius](http://vimgenius.com/): A game that goes together with `vimtutor`
- [Learn vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/).
- [Vim: Precision Editing at the Speed of Thought](https://vimeo.com/53144573): A talk by Drew Neil
- [Vim Adventure](https://www.vim-adventures.com): An adventure game for learning `vim`
- [Vim Casts](http://vimcasts.org/episodes/archive/): Videos and articles for teaching `vim`
- [Vim Video Tutorials](http://derekwyatt.org/vim/tutorials/) by Derek Wyatt
- [Vim Awesome](https://vimawesome.com/): Directory of plugins.

You can search the Web for "best vim tutorials" to find many other resources to get you started with the editor.
