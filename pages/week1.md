---
title: week1
---

#### Tho this is a pretty easy question to understand, at first glance I missed the phrase, "at least".
#### To restate the problem: Given a series of letters, check if every l
#### What are the data? Besides the pangram, I also need to know the alphabet
#### Conditions: every letter in the alphabet appears once
### Devise a plan
#### First plan
##### A more general problem could be --- count the number of times for the appearance of each letter in the give phase.
##### Then, the result can be used.
##### if all letters appear at least once, it's a pangram
#### Second plan
##### A related problem could be --- the uniq letters of the phrase
##### if the number of uniq letters happen to be 26, it's a pangram
#### Third plan
##### Based on the alphabet, check each letter if it's in the phrase.
##### If there is one letter that is not in the phrase, it's not a pangram
