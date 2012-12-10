# Autocorrect

## Language

Anything that takes stdin that I can also run easily. Ruby, JavaScript, Python, PHP (others fine too).

## Bounty

This is a hurt-me-plenty mission, so a **Little Village gyro - and beer** - awaits any Skookum challenger who manages to tackle it.
I'll even go out and **pick it up for you.** In the cold. That's how hard this is.

## Requirements

This challenge is to **build your own touch-screen-keyboard inspired autocorrect algorithm.**

It has three levels of difficulty so the Sr. devs don't get an easy beer off me.
You can check how your program is doing by running the tests from the makefile:

### Jr

- Accept strings of text via stdin.
- Separate words by whitespace (like an iPhone).
- Check each word entered against a dictionary (words.txt).
- Replace any words that aren't in the dictionary file.
- Replacements should be dictionary words with the shortest hamming distance.
- If two replacements share a hamming distance, the one with the higher frequency wins.
- Output your corrected string to stdout (don't worry about punctuation or formatting).

### Mid

- All the above, plus:
- Your output should exactly match the punctuation of the input string.
- It should also match the formatting (capitalization, white-space) of the input string.

### Sr

- All the above, plus:
- Instead of the hamming distance, you'll be using the keyboard distance like a real iPhone.
- All keys on your keyboard are separated by some shortest path (A -> Z = 1, Z -> P = 9).
- To find the distance between characters in words, you'll add +N instead of hamming +1.
- N is the keyboard distance between the desired key and the one your user fat-fingered.
- If the distance to the nearest dictionary match is > 12, use the original non-dictionary word.

## Tools at your disposal

- `fixtures/words.txt` a dictionary of the top 47.2k English words, sorted by frequency (desc).
- `fixtures/keymap.json` a map between each relevant keyboard key and its neighbors.

## Warnings

- The makefile will send 0/1/2 as a final argument to your program. Feel free to ignore it.
- `words.txt` has duplicate entries, so use the highest frequency rank for a duplicated word.

### Testing

- replace START in the makefile, then:
- `$ make quotes` - a quick test of your output
- `$ make test-{{jr/mid/sr}}` - build output.txt, test results
- `$ make time` - times your program

## Examples

### Jr

```
$ echo 'Clood, haz hig num pir reep woorn!' | node hunter.js
blood had his sum per keep woman
```

### Mid

```
echo 'Clood, haz hig num pir reep woorn!' | node hunter.js
Blood, had his sum per keep woman!
```

### Sr

```
$ echo 'Clood, haz hig num pir reep woorn!' | node hunter.js
Flood, has big bum pie deep women!
```

## Submissions

I'll post the code to these awesome solutions in a few days, so everyone has time to hack.

- @elaforc - Sr - 138 lines - 1.910s (!!!)
- @snodgrass23 - Jr Mid - 147 lines - 14.207s
- @hunterloftis - Jr Mid Sr - 160 lines - 1.477s (using the early bailout idea from @elaforc)