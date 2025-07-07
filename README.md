# LeakDay
Offset Farming Simulator 2025

## Acknowledgements
 Special thanks to:
 
 - [risporce](https://github.com/risporce/)
 - [S.B](https://github.com/PeterHackz)
 - [Shei](https://github.com/Shei-Bi)

 [exportTrie structure](https://github.com/qyang-nj/llios/blob/main/exported_symbol/README.md)
  


## Authors

- [@DarKDevz](https://www.github.com/DarKDevz)
- [@itstermohh](https://github.com/itstermoh)
- [@rldv1](https://github.com/rldv1/)



## Introduction

In the late 24, June 2025
an update was pushed to Hay-Day,
and this started the great 3 weeks of leaks!

#### Leak Day
You are probably wondering what i mean by leak day, im guessing you already know what debug symbols are, but if you dont lemme summarize them:


A debug symbol is a special marker or label programmers add to their software programs to help them understand and troubleshoot the code. Debug symbols are not human-readable, but programmers use debugging tools to interpret them and get meaningful insights.

we will talk more about the format and why not many people noticed the issue, i wont get into the technicalities and why only certain games managed to go through with this
but basically only games built with a later version of promon, and for ios 12+ ONLY


## The great __LINKEDIT

at first the issue was brought up by risporce, but nobody paid attention 

(i asked without pinging and never got a reply)

Then 5 June 2025, coolboy and kubune brought it up again

Because i was already familiar with Mach-O formats because of other reversing i had done prior, i decided to look into it

Coolboy sent the full __LINKEDIT segment, but i knew this wasnt accurate
as that holds not only debug symbols but also imported symbols

While __LINKEDIT does hold all of this info, it mainly is just a command specifying the size of all groups inside of it

<p align="center">
  <img src="https://raw.githubusercontent.com/DarKDevz/LeakDay/refs/heads/main/image.png?token=GHSAT0AAAAAADF2NTBXV5RHDXFTOANSOI7M2DLVSSQ" width="100%" />
</p>


the one we are intersted in is exportTrie, as that one contains the debug information we need to extract

My first try was just looping through the export trie by remaking the code in [here](https://github.com/qyang-nj/llios/blob/main/exported_symbol/README.md)

This gave some very small results, as the rest of the trie is "corrupted", i did not go into why and how the table was corrupted.


## The bruteforcing

Rldv1 then made a simple script which ignored the actual structure and just tried extracting symbols in a quick and dirty way, this gave some results but the names were incorrect as they didnt follow the actual table structure 

Meanwhile in the server we were talking about this in, coolboy said he "bruteforced" the nodes of the table to be able to extract the info

I sent all of this info to itstermoh, he made a script which bruteforced every table's node and returned once the "best" result was returned (AKA the biggest amount of functions), this would also return class names which are stored in the entry node

With this we bruteforced all games affected by this:

## Affected builds

| Game Name| Version|
| ----------------- | ------------------------------------------------------------------ |
| Brawl Stars | v62.x |
| Hay Day | v1.66 |
| Clash of Clans | v17.x |
| Squad Busters | v11-v12.x |
| Boom Beach | TBD|
| Clash Royale | None |
| Mo.co | None |


## Why?

While we aren't supercell developers but instead are reverse engineers, we dont have a 100% accurate reasoning for this, as it could be a mixture of things

But because we saw that this leak only happened on binaries which had iOS 12+ compatible binaries, as games like Clash Royale and Mo.co which target iOS 14+ dont have this

It could be either:

Their protection which had been updated very recently, which actually works very close to the symbols, i reverse this protection (i wont talk about it at all though) i noticed that some "imported" symbols were being kept and not extracted to be later protected

So their protection which only acts like this on iOS 12+ binaries could be the cause of this,
They also advertise "Debug symbol stripping" which could've broke once they changed the logic sligthly

### Or/And

Their compiler settings for iOS 12+ binaries

But this makes less sense, as it didnt affect just one game but all of them (meaning the settings would've had to be wrong for all of them)


## Final words

This is the biggest leak of supercell binaries, so we wont give any further details on scripts/symbols (also because it took a lot of processing time to extract them)

Supercell was informed by a third party about this issue, and fixed it

The release time of this write-up was done once all games affected were updated, to prevent anyone from modding them in this insecure state

## Legal Notice

This is just for educational purposes, please dont sue us supercell



