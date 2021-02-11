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
###### yes, given an array A of strings and an array (B) of arrays, in which each element is a char. Output an array of integers. In the array, each in integer represents how many strings in the array B include a char in array B.
#### The plan
##### the most intuitive approach would be iterating the guests info array based on a query integer
### Carry out the plan
####
```ruby
guest_infos = [[4, 20], [1, 3], [2, 27], [3, 19]]
query_dates = [1, 5, 20]

def hotel_guests(guest_infos, query_dates)
  query_dates.map do |date|
    guest_infos.sum { |(in_date, out_date)| (in_date..out_date).include?(date) ? 1 : 0 }
  end
end

hotel_guests(guest_infos, query_dates)
```
#### should have written tests and carry out the plan step by step but I guess it is not the main focus here?
### Looking back
#### programming wise
##### should use less syntactic sugar to make it more general
##### should consider more on the performance side, time and memory.
#### Can you derive the result differently?
##### yes, but why? because it not time efficient, O(n * m)
##### I think I would do something like trading space for time by pre calculating how many guests for each day of a year
##### Or to slightly reduce the time complexity, by sorting the guests' info arrays based firstly on the check-in date and then the check-out date, so that when iterating the query dates, we can skip some info arrays
#### Can you check the result and arguments
##### these have already been done during previous steps with assumption and tests (which I have not written [awkward face])
#### Can you use the procedure or result
##### yes, I guess so, the procedure and result is pretty straight-forward. Not sure how to well illustrate this point.
## Looking back version 2
### sales count (optimized)
#### sales count O(n) space O(Max(n, m)) time, n for sales, m for queries
sales = [5, 10, 23, 1, 25, 22, 17]
queries = [[1, 3], [0, 2], [2, 5], [3, 6]]

expected_result = [34, 38, 71, 65]

def sales_count(sales, queries)
	total = 0
	accumulated_sales = sales.map { |sale| total += sale }
	accumulated_sales.prepend(0)

	queries.map do |(start_day, end_day)|
		accumulated_sales[end_day + 1] - accumulated_sales[start_day]
	end
end

p sales_count(sales, queries) == expected_result

### hotel guests

guest_infos = [[4, 20], [1, 3], [2, 27], [3, 19]]
query_dates = [1, 5, 20]

def hotel_guests(guest_infos, query_dates)
  guests_count = Array.new(31, 0)

	guest_infos.each do |(in_day, out_day)|
		(in_day..out_day).each { |index| guests_count[index] += 1 }
	end

	query_dates.map { |day| guests_count[day] }
end

p hotel_guests(guest_infos, query_dates)

#### the above strategy was in my looking back procedure, but it looks the time complexity is still O(n**2)

#### now trying a new strategy

def hotel_guests(guest_infos, query_dates)
  guests_count = Array.new(31, 0)

	guest_infos.each do |(in_day, out_day)|
		guests_count[in_day] += 1
		guests_count[out_day] -= 1
	end

	total = 0

	guests_count = guests_count.map { |marker| total += marker }

	query_dates.map { |day| guests_count[day] }
end

p hotel_guests(guest_infos, query_dates)

#### now we can see that there are similarities between the two problems
-
####
```ruby
  guests_count = Array.new(31, 0)

  guest_infos.each do |(in_day, out_day)|
    guests_count[in_day] += 1
    guests_count[out_day] -= 1
  end
  ```
- what this part does is actually generating the sales count (how many people checked in or out on a specific day)
- ```ruby
  total = 0

	guests_count = guests_count.map { |marker| total += marker }
  ```
- what this part does is actually calculating the how many rooms are providing service on a specific day, which is the same as calculating the accumulated sales
- now the difference between the two is that the Sales problem asked for the result with the ranges of days, in between which how many t-shirts have been sold, but the Hotel problem just ask for the sales on a specific day
### Can you use the result for some other problem?
#### yes, for the hotel problem, the queries could be an array of arrays, which might be asking how many rooms have been occupied during that period of time
