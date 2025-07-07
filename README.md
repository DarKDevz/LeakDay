# LeakDay
Offset Farming Simulator 2025

## Acknowledgements
 Special thanks to:
 
 - [risporce](https://github.com/risporce/)
 - [S.B](https://github.com/PeterHackz)
 - [Shei](https://github.com/Shei-Bi)

 [exportTrie structure](https://github.com/qyang-nj/llios/blob/main/exported_symbol/README.md])
  


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
  <img src="https://raw.githubusercontent.com/Kilo-Org/kilocode/refs/heads/main/kilo.gif" width="100%" />
</p>
