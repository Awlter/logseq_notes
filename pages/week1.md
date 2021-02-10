---
title: week1
---

## pre-class
### understanding the problem
#### Tho this is a pretty easy question to understand, at first glance I missed the phrase, "at least".
#### To restate the problem: Given a series of letters, check if every letter appears at least once. If it's true, it's called a pangram.
#### What is the unknown, or what I am asked to do is --- whether a phrase is a pangram
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
## Post-class work
### understanding the problem
#### restate the problem
- Given an array of arrays representing guests info, each array represents the check-in and check-out day in which integers represent Xth day of the year (let's assume it true), e.g. [4, 32] represents a guest checks in at 4th and 32nd.
- Another array of integers is also given as queries, each integer presents a particular day
- Based on the guests' info and queries, it is expected to return an array of integers that each integer represents how many guests are staying on that particular day
#### the unknown are always the expected output, here is an array of integers that represent guest numbers of that day
#### the data are the guests info array and the queries array
#### the condition is that whether a guest stays at the hotel on that day
### Eliminate uncertainties
#### since this is more of a practice for Polya's process, let's assume (since right now I cannot confirm with Elliot) guests info arrays are always an array with two integers.
#### Let's also assume the inputs are well-formed --- no empty array, no empty or invalid elements in the array ( 's', nil, '', '1', or integer larger than 365 and less than 1), no repeated data, for guests info array, the first integer is always smaller than the second.
### Devise a plan
#### Some helpful heuristic questions (let's pretend this problem is quite difficult)
##### Could you imagine a more accessible problem
###### yes, whether the specific day is in between the range of each guest info.
##### Could you imagine a similar or general problem
###### yes, given an array of integers, check
