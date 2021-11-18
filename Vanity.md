# Vanity Accounts
It is possible create "vanity" public keys just like there are vanity license plates. You can be like the cool kids with a pubkey that starts with your initials. The way you create a vanity keypair is by using `safecoin-keygen grind`.

For example you might want to name your validator Wally:

```bash
safecoin-keygen grind --starts-with Wa11y:1 -o id.json
Searching with 8 threads for:
	1 pubkey that starts with 'Wa11y' and ends with ''
Searched 1000000 keypairs in 6s. 0 matches found.
Searched 2000000 keypairs in 13s. 0 matches found.
Searched 3000000 keypairs in 20s. 0 matches found.
    ...
Searched 17738000000 keypairs in 134260s. 0 matches found.
Wrote keypair to Wa11ysC4xguKmaSERxA9asHH6Bex2o3uWHFex1C27eu.json
```

Couple of points: First, yes that's "Wa11y" with two ones, because "1" and "l" because visual ambiguity is not allowed with public keys [per the bs58 "standard"](https://bitcoin.stackexchange.com/questions/75527/eli5-what-is-base58check-encoding).  Second, I really did that and it took a *while*!!! More than 37 hours on my 8 core modern linux development box.

Your read that correctly: 37 hours (to search 17,738,000,000 (almost 18 billion) keypairs)

Why can it take so long?  Note that I used the word "can" not "does."  It *can* take a while because its simply random chance: The program is literally generating ("grinding") random pubkey pairs with over and over again until the keypair's pubkey actually matches your desired string of characters.  Just to *grind* the point home: a pubkey has 128 bits of randomness, which is a very big roulette wheel to spin.

So how do you possibly speed this up?
* Use a short match.  Matching `--starts-with Wa:1` happens nearly instantly, matching `--starts-with Wa1:1` took 11 seconds and `Wa11` took almost half an hour on my three-year-old macbook pro. Beyond that length you might want to get some coffee and come back many minutes/hours later...

* Use a really fast computer with many cores.  By default the program uses 8 parallel threads to go eight times faster than a single thread if you have more than 8 cores its worth it to use the `--threads` option set to however many cores your hardware uses.

* Don't follow my example of being dern picky about what you want to match. Essentially, each acceptable match is a lottery ticket and more lottery tickets mean more chances to win baby!!!  Here follow your options for not being so picky as me.

* Use the `--ignore-case` option. With the my "Wa11y" pattern I could have gotten a hit sooner by matching "wA11Y". And my math says that I had 8 chances to win for each pubkey vs only one chance.

* use `--starts-with` (or `--ends-with`) as many times as you can!  Thats legal.  So going back to "Wally" I could have further improved my odds of a match by allowing 'L' instead of '1'.  Actually, after a little thought I came up with the following to maximally broaden my match:
```
  ❯ safecoin-keygen grind --starts-with Wa11y:1 --starts-with WaL1y:1 --starts-with Wa1Ly:1 --starts-with WaLLy:1
  Searching with 8 threads for:
	1 pubkey that starts with 'Wa11y' and ends with ''
	1 pubkey that starts with 'WaL1y' and ends with ''
	1 pubkey that starts with 'WaLLy' and ends with ''
	1 pubkey that starts with 'Wa1Ly' and ends with ''
```

## Wrapping Up

So grinding is the *only* way to get a vanity keypair.  You might want a vanity keypair for a number of reasons. In my case I thought a vanity keypair would be better for marketing my validator. But actually, having gone down the keygen rathole, it occurs to me that a vanity keypair might be a nice thing to have for my primary wallet so that I can, at a glance, see that I am using the right pubkey.  A little extra peace of mind when using crypto is valuable.

In conclusion, the moral of this article (the *key* take-away, if you will) could be:

##### With great vanity comes great cost.


If you want that cool, neato, keen five (*possibly* six) character string in your pubkey then you are looking at a program execution time that can be measured in days. That little extra time you spend optimizing your key grinding is probably worth it.

#### PS
There is no regular expression option for keygen because (I assume) there is no well-tested regular expression algorithm that runs against bs58 strings.

#### PPS
As far as I can tell using the google, there is no bs58 standard.

 

