# Python Interview Questions and Answers: Lists, Tuples, Sets, and Dictionaries

> Self-contained revision guide: each original question is followed immediately by an answer, example, and important edge case. Questions are taken from the supplied checklist; that document is reference material, not additional instructions.

## How to use this guide

Try answering the question aloud before reading the solution. In coding interviews, state assumptions, explain the data structure choice, then discuss complexity and edge cases where useful.

## Lists (1–30)

### 1. What is a list in Python, and how is it different from an array?

A list is an ordered, mutable sequence that can hold mixed Python objects. Unlike a traditional typed array, a list can contain different types and is a general-purpose container. For numeric arrays and compact homogeneous storage, use array/numpy.

### 2. Are Python lists mutable? Show an example.

Yes. Assignment by index changes an existing element:    values = [10, 20]; values[0] = 99  # [99, 20]

### 3. How do you create an empty list and a list with initial values?

    empty = []
    also_empty = list()
    scores = [85, 92, 78]
Both [] and list() create an empty list; literals are most common.

### 4. Explain positive indexing and negative indexing in a list.

For [10, 20, 30], indexes 0,1,2 select from the left; -1,-2,-3 select from the right. Example: values[-1] is 30. Valid indexes range from -len(lst) through len(lst)-1.

### 5. What is list slicing? Explain `lst[start:stop:step]`.

A slice selects a range:    lst[start:stop:step]. Start is included, stop excluded; defaults depend on step. Example: [0,1,2,3,4][1:5:2] gives [1,3]. Negative step walks backward.

### 6. What is the difference between `append()` and `extend()`?

append(x) adds x as one item; extend(iterable) adds each item.    a=[1,2]; a.append([3,4])  # [1,2,[3,4]]    b=[1,2]; b.extend([3,4])  # [1,2,3,4]

### 7. What is the difference between `append()` and `insert()`?

append(x) adds at the end; insert(i,x) adds at position i and shifts later items.    a=[1,3]; a.append(4) -> [1,3,4]; a=[1,3]; a.insert(1,2) -> [1,2,3]

### 8. What is the difference between `remove()`, `pop()`, `del`, and `clear()`?

remove(value) deletes first matching value; pop(index) deletes and returns item (last by default); del removes by index or slice; clear empties the same list. Example: x=[1,2,2]; x.remove(2) -> [1,2]; x.pop() returns 2.

### 9. What happens if you call `remove(x)` when `x` is not in the list?

It raises ValueError and leaves the list unchanged. Check membership first if absence is expected: if x in items: items.remove(x).

### 10. What is the difference between `sort()` and `sorted()`?

list.sort() sorts the list in place and returns None; sorted(iterable) returns a new sorted list and accepts any iterable. Use key= and reverse=True as needed.

### 11. What does `reverse()` do, and how is it different from `reversed()`?

reverse() reverses a list in place and returns None. reversed() returns a reverse iterator without changing the list: list(reversed(items)).

### 12. How do you find the index of an element? What happens if it does not exist?

Use items.index(value); it returns the first matching index and raises ValueError if missing. Check with if value in items first when expected absent.

### 13. How do you count how many times an element occurs in a list?

items.count(value) returns the number of equal elements. For many different values, collections.Counter(items) gives all frequencies efficiently.

### 14. How do you copy a list? Compare `a = b`, `a[:]`, `a.copy()`, and `list(a)`.

a=b makes both names refer to the same list. a[:] / a.copy() / list(a) make shallow copies (new outer list, nested objects shared). For nested independent copies use copy.deepcopy(a).

### 15. Explain shallow copy versus deep copy with a nested list.

A shallow copy duplicates only the outer container; inner lists/objects remain shared. A deep copy recursively copies nested objects.    import copy; a=[[1],[2]]; b=copy.copy(a); b[0].append(9); a becomes [[1,9],[2]]. Deep copy avoids that sharing.

### 16. Why can `[[0] * 3] * 3` cause unexpected results?

The multiplication repeats references to the same inner list. One edit appears in every row: grid=[[0]*3]*3; grid[0][0]=1 changes all rows' first value. Build rows separately: [[0]*3 for _ in range(3)].

### 17. Write a program to find the largest and smallest element in a list without using `max()` or `min()`.

    values=[7, 2, 9, -1]
    smallest=largest=values[0]
    for value in values[1:]:
        if value < smallest: smallest=value
        if value > largest: largest=value
    print(smallest, largest)  # -1 9
Assumes non-empty input; otherwise handle the empty case.

### 18. Write a program to find the second-largest distinct element in a list.

    values=[4, 1, 9, 9, 7]
    distinct=sorted(set(values))
    second=distinct[-2] if len(distinct)>=2 else None
    print(second)  # 7
This clear approach is O(n log n); a one-pass O(n) solution can track the largest two distinct values.

### 19. Reverse a list without using `reverse()` or slicing.

Use an index that starts at the final position and moves left:

    def reverse_list(values):
        result = []
        for i in range(len(values) - 1, -1, -1):
            result.append(values[i])
        return result

This uses O(n) time and O(n) extra space.

### 20. Remove duplicate values from a list while preserving original order.

    result=[]; seen=set()
    for x in values:
        if x not in seen:
            result.append(x); seen.add(x)
Order is kept; elements must be hashable. O(n) average time.

### 21. Find all duplicate elements in a list.

    from collections import Counter
    counts=Counter(values)
    duplicates=[x for x,n in counts.items() if n>1]
Returns each duplicate value once, in first-seen order (modern Python).

### 22. Move all zeros in a list to the end while keeping the order of non-zero values.

    nonzero=[x for x in values if x!=0]
    result=nonzero+[0]*(len(values)-len(nonzero))
Preserves nonzero order; O(n) time and space.

### 23. Rotate a list right by `k` positions.

    if values:
        k %= len(values)
        result=values[-k:]+values[:-k] if k else values[:]
    else: result=[]
Modulo handles k larger than length; empty input is safe. O(n) time/space.

### 24. Split a list into chunks of size `n`.

    chunks=[items[i:i+n] for i in range(0,len(items),n)]
Require n>0; otherwise range step is invalid. Final chunk may be shorter.

### 25. Flatten a nested list by one level.

    flat=[item for sublist in nested for item in sublist]
This removes exactly one nesting level; it does not recursively flatten deeper lists.

### 26. Flatten a deeply nested list using recursion.

    def flatten(items):
        out=[]
        for item in items:
            if isinstance(item,list): out.extend(flatten(item))
            else: out.append(item)
        return out
Example flatten([1,[2,[3]],4]) -> [1,2,3,4]. Recursion depth is limited; use an explicit stack for very deep input.

### 27. Find the common elements between two lists.

Use a set for membership, filter the first list to keep its order:    second=set(b); common=list(dict.fromkeys(x for x in a if x in second)). This returns unique common values in a's order.

### 28. Merge two sorted lists into one sorted list.

Two pointers compare the next unused value from each already-sorted list:

    def merge_sorted(a, b):
        i = j = 0
        result = []
        while i < len(a) and j < len(b):
            if a[i] <= b[j]:
                result.append(a[i]); i += 1
            else:
                result.append(b[j]); j += 1
        result.extend(a[i:])
        result.extend(b[j:])
        return result

    print(merge_sorted([1, 4, 8], [2, 3, 9]))  # [1, 2, 3, 4, 8, 9]

Runs in O(len(a) + len(b)) time.

### 29. Find the missing number from a list containing numbers from 1 to `n`.

If numbers are distinct and exactly one number in 1..n is absent:    missing=n*(n+1)//2-sum(values). For duplicates or malformed input, use a set/count check; XOR is another overflow-safe approach in fixed-width languages.

### 30. Find two numbers in a list whose sum equals a target value.

Store earlier values and look for each value's complement:

    def pair_with_sum(values, target):
        seen = set()
        for value in values:
            needed = target - value
            if needed in seen:
                return needed, value
            seen.add(value)
        return None

    print(pair_with_sum([4, 6, 1, 9], 10))  # (4, 6)

Average O(n) time and O(n) space. A repeated number can pair with itself only if it occurs twice.

## Tuples (31–45)

### 31. What is a tuple in Python?

A tuple is an ordered, immutable sequence. It can contain mixed types and supports indexing/slicing, but its element slots cannot be reassigned.

### 32. What are the major differences between a list and a tuple?

Lists are mutable, written with []; tuples are immutable, usually written with (). Both are ordered sequences, allow duplicates, indexing, and iteration. Tuple immutability is shallow if it contains mutable objects.

### 33. Why would you use a tuple instead of a list?

Use a tuple for a fixed record or value that should not be structurally changed, and when hashability is useful. Lists suit changing collections. Do not choose tuple solely on vague speed claims.

### 34. How do you create an empty tuple and a single-element tuple?

    empty=()
    one=(5,)
The comma makes a one-item tuple; tuple() also creates an empty tuple.

### 35. Why is `(5)` an integer but `(5,)` a tuple?

Parentheses group an expression; the comma creates a tuple. So (5) is integer 5, while (5,) is a one-element tuple.

### 36. Are tuples immutable? Can a tuple contain mutable objects?

A tuple's item bindings cannot be reassigned. It can contain a mutable list, and that list can still be changed; the tuple continues to refer to that same list.

### 37. Can you modify a list stored inside a tuple? Explain with an example.

Yes, the nested list can mutate:    t=([1,2], 'x'); t[0].append(3); print(t)  # ([1,2,3], 'x'). You cannot assign t[0]=... because tuple slots are immutable.

### 38. How do tuple packing and unpacking work?

Packing:    point=3, 4 creates tuple (3,4). Unpacking:    x,y=point assigns values by position; counts must match unless starred unpacking is used.

### 39. What does extended unpacking mean in `a, *middle, b = values`?

The starred target collects zero or more middle items into a list:    a,*middle,b=[1,2,3,4]; # a=1, middle=[2,3], b=4. Exactly one starred target is allowed on the left.

### 40. How do you swap two variables using tuple unpacking?

    a,b=10,20
    a,b=b,a
Assignment evaluates the right side first, then binds both names.

### 41. How do you convert a list to a tuple and a tuple to a list?

    t=tuple([1,2,3])
    values=list(t)
The conversions create new containers; nested objects are still shared.

### 42. How do `count()` and `index()` work on tuples?

t.count(x) counts matches; t.index(x) returns the first position and raises ValueError when absent. Use x in t when absence needs checking first.

### 43. Can a tuple be used as a dictionary key? Under what condition?

A tuple is a valid key if it is hashable: every element must be hashable (and remain equality/hash stable). A tuple containing a list is not hashable.

### 44. Why are tuples often used for fixed records, coordinates, or database-like rows?

Tuples can represent fixed-position fields such as (latitude, longitude) or database rows. Their fixed structure communicates record-like data; namedtuple/dataclass may be clearer when field names matter.

### 45. Given a list of tuples, sort it by the second value and then by the first value.

    records=[('A',2),('B',1),('C',2)]
    result=sorted(records, key=lambda row:(row[1],row[0]))
Sort key is second value then first; output [('B',1),('A',2),('C',2)].

## Sets (46–65)

### 46. What is a set in Python?

A set is a mutable collection of distinct hashable elements. It supports fast average-case membership and mathematical set operations; it has no positional indexing.

### 47. Why are sets unordered, and why do they not allow duplicates?

Sets enforce uniqueness using equality and hashing; their iteration order is not a sequence contract. Do not rely on display order for logic.

### 48. What is the difference between `{}` and `set()`?

{} creates an empty dictionary. set() creates an empty set. A nonempty set literal looks like {1,2}.

### 49. How do you create a set from a list?

    unique=set([1,2,2,3])  # {1,2,3}
Set order is not guaranteed.

### 50. What is the difference between `add()` and `update()`?

add(x) inserts one element; update(iterable) inserts each element from one or more iterables.    s={1}; s.add([2]) is invalid because list is unhashable; s.update([2,3]) works.

### 51. What is the difference between `remove()`, `discard()`, and `pop()` for sets?

remove(x) deletes a known element or raises KeyError; discard(x) silently does nothing if absent; pop() removes and returns an arbitrary element (or raises KeyError if empty).

### 52. What happens when you call `remove()` for an element that is absent?

KeyError is raised and no element is removed. Use discard when missing is acceptable or check x in s first.

### 53. How do you remove all duplicates from a list using a set?

    unique=list(set(items))
This removes duplicates but does not preserve original order. To preserve order, use dict.fromkeys(items) (hashable values required).

### 54. Why may converting a list to a set change its order?

A set is unordered, so converting back to a list does not promise the original sequence order. Set iteration order may appear stable during one run but must not be relied on.

### 55. What are union, intersection, difference, and symmetric difference?

For A,B: union=A|B (either); intersection=A&B (both); difference=A-B (in A only); symmetric difference=A^B (in exactly one).

### 56. Explain the difference between `|`, `&`, `-`, `^` and their method versions.

Operators work with set operands; methods such as union(), intersection(), difference(), symmetric_difference() accept iterables. Methods can be easier when operands are lists or other iterables.

### 57. What is the difference between `issubset()`, `issuperset()`, and `isdisjoint()`?

A.issubset(B): every A member is in B. A.issuperset(B): every B member is in A. A.isdisjoint(B): no shared elements.

### 58. What is a `frozenset`, and when would you use it?

frozenset is an immutable set. Use it when set contents must not change, or as a dictionary key / member of another set; all elements still must be hashable.

### 59. Why can a list not be a set element?

Set elements must be hashable so Python can compute stable hash values for membership and uniqueness. Lists are mutable and unhashable; tuples of hashable values can be elements.

### 60. Find common values among three lists using sets.

    common=set(a) & set(b) & set(c)
Intersection gives distinct common values; order is unspecified.

### 61. Find values present in the first list but not in the second.

    result=set(first)-set(second)
Returns unique values only; use a list comprehension if duplicates/order from first list must be preserved.

### 62. Determine whether two lists contain exactly the same unique elements.

    set(a)==set(b)
This tests equality of unique elements, ignoring order and multiplicity. If multiplicity matters, compare Counter(a)==Counter(b).

### 63. Find the first repeated element in a list.

    seen=set()
    for x in values:
        if x in seen: return x
        seen.add(x)
    return None
Returns the earliest value whose second occurrence is encountered; hashable values required.

### 64. Check whether a string contains all unique characters.

    len(text)==len(set(text))
This compares exact code points and is case-sensitive. For case-insensitive uniqueness, casefold first.

### 65. Given two sentences, find the unique words common to both, ignoring case.

    a={w.casefold() for w in s1.split()}
    b={w.casefold() for w in s2.split()}
    common=a & b
Punctuation remains attached to tokens unless normalized.

## Dictionaries (66–90)

### 66. What is a dictionary in Python?

A dictionary maps unique hashable keys to values. It is mutable and preserves insertion order in modern Python.

### 67. What makes a dictionary key valid?

A key must be hashable and have stable equality/hash behavior. Typical keys: strings, numbers, and tuples of hashable values; lists and dictionaries cannot be keys.

### 68. Why must dictionary keys be hashable?

Hashing lets dict quickly choose where to look up a key. Keys must retain a stable hash while stored; mutating a key in a way that changes its hash would break lookup.

### 69. Are dictionaries ordered in modern Python? What does that mean in practice?

Yes, insertion order is guaranteed in Python 3.7+. Updating an existing key does not move its position; deleting and reinserting places it at the end.

### 70. Can dictionary values be duplicated?

Yes. Values need not be unique or hashable:    {'a': 1, 'b': 1} is valid.

### 71. What happens when you assign a value to an existing dictionary key?

The existing value is replaced; the key keeps its insertion position.    d={'x':1}; d['x']=2 -> {'x':2}.

### 72. Compare `d[key]`, `d.get(key)`, and `d.setdefault(key, default)`.

d[key] raises KeyError if missing. d.get(key, default) returns default without inserting. d.setdefault(key, default) returns existing value or inserts the default if absent.

### 73. What is the difference between `keys()`, `values()`, and `items()`?

keys() gives a dynamic view of keys; values() a view of values; items() a view of (key,value) pairs. Views reflect later dictionary changes; wrap in list() for a snapshot.

### 74. How do you safely delete a key from a dictionary?

Use d.pop(key, default) to avoid KeyError, or if key in d: del d[key]. Choose whether a missing key is expected.

### 75. Compare `pop()`, `popitem()`, `del`, and `clear()`.

pop(key[, default]) removes/returns named value; popitem() removes/returns last inserted pair (LIFO); del removes named entry; clear() removes all entries in place.

### 76. What is the difference between `update()` and the `|` dictionary merge operator?

update(other) changes the dictionary in place; duplicates from other overwrite existing values. d1 | d2 creates a new dict with right-side values winning; d1 |= d2 updates in place.

### 77. How do dictionary comprehensions work?

A comprehension builds a dictionary from an iterable:    {key: value for item in iterable if condition}. Example: {x:x*x for x in range(1,4)} -> {1:1,2:4,3:9}.

### 78. Create a dictionary where numbers 1 to 10 are keys and their squares are values.

    squares={n:n*n for n in range(1,11)}
Keys 1..10 map to their squares.

### 79. Reverse the keys and values of a dictionary. What if values are repeated?

    reverse={value:key for key,value in d.items()}
This only works without losing information when values are unique. If repeated, collect keys into lists:    reverse.setdefault(value,[]).append(key).

### 80. Count the frequency of each element in a list.

    from collections import Counter
    Counter(items)
Returns a dict-like mapping from each hashable item to its frequency.

### 81. Count the frequency of each character in a string.

    from collections import Counter
    Counter(text)
Counts each character, including spaces and punctuation.

### 82. Find the key with the maximum value in a dictionary.

    key=max(scores, key=scores.get)
Raises ValueError on an empty dict. Ties return the first encountered key among tied maxima.

### 83. Sort a dictionary by key.

    sorted_dict=dict(sorted(d.items()))
Sorts by key; values do not determine ordering.

### 84. Sort a dictionary by value in descending order.

    sorted_dict=dict(sorted(d.items(), key=lambda pair:pair[1], reverse=True))
Equal values retain stable relative order from the input iteration.

### 85. Merge two dictionaries. What should happen if they have the same key?

    merged=d1 | d2
Right-hand values win for duplicate keys. update() is the in-place alternative.

### 86. Group a list of words by their first character.

    from collections import defaultdict
    groups=defaultdict(list)
    for word in words:
        if word:
            groups[word[0]].append(word)
    print(dict(groups))  # {'a': ['apple', 'ant'], 'b': ['banana']}

Guarding empty words avoids indexing errors. dict(groups) converts to a regular dict.

### 87. Group anagrams together using a dictionary.

    from collections import defaultdict
    groups=defaultdict(list)
    for word in words: groups[''.join(sorted(word.casefold()))].append(word)
Words with same normalized sorted letters share a key; casefold policy combines case variants.

### 88. Given a list of records, create a dictionary indexed by `id`.

    by_id={record['id']:record for record in records}
Duplicate IDs overwrite earlier records; decide whether to reject or collect them.

### 89. Find the first non-repeating character in a string.

    from collections import Counter
    counts=Counter(text)
    next((c for c in text if counts[c]==1), None)
Counter supports one frequency pass, then scan preserves original order. Returns None if none.

### 90. Check whether two strings are anagrams using a dictionary or `Counter`.

    from collections import Counter
    Counter(a.casefold())==Counter(b.casefold())
This preserves multiplicity. Normalize spaces/punctuation first only if they should be ignored.

## Mixed Questions (91–100)

### 91. When would you choose a list instead of a set?

Choose a list for order, duplicates, indexing, or frequent edits. Choose a set for uniqueness and membership testing when order/duplicates do not matter.

### 92. When would you choose a tuple instead of a list?

Choose a tuple for a fixed, record-like sequence or when immutable/hashable structure is useful. Choose a list when elements/length need changing.

### 93. When would you choose a dictionary instead of a list of key-value pairs?

Use a dict when each record has a unique key and you need direct lookup by that key. A list of pairs is suitable when duplicate keys or pair order/multiplicity is meaningful.

### 94. Explain the average-case lookup complexity of list, set, and dictionary membership checks.

Average case: list membership O(n) scan; set/dict membership O(1). Worst case for hash structures can degrade to O(n), though hash collisions are managed by Python.

### 95. Why is `x in my_list` usually slower than `x in my_set`?

A list checks elements one by one; a set hashes the query and checks a bucket. So average lookup avoids scanning all n items, at the cost of memory and hashable elements.

### 96. Write a function that removes duplicates from a list but preserves order using a `set` and a `list`.

    def unique_in_order(items):
        seen=set(); result=[]
        for item in items:
            if item not in seen:
                seen.add(item); result.append(item)
        return result
Average O(n); elements must be hashable.

### 97. Given student names and marks, create a dictionary and return the student with the highest mark.

    def top_student(marks):
        if not marks: return None
        return max(marks, key=marks.get)
    marks={'Asha':88,'Bilal':95,'Chen':91}
    print(top_student(marks))  # Bilal
Tie returns first inserted maximum key.

### 98. Given a sentence, return words sorted by descending frequency; preserve alphabetical order when frequencies tie.

    from collections import Counter
    counts=Counter(word.casefold() for word in sentence.split())
    result=sorted(counts, key=lambda w:(-counts[w],w))
Lowercasing/casefold combines case variants; punctuation remains attached unless tokenized away.

### 99. Given transaction records as tuples such as `("Bengaluru", "food", 250)`, calculate the total expense for each category using a dictionary.

    transactions = [("Bengaluru", "food", 250), ("Mysuru", "travel", 100), ("Bengaluru", "food", 75)]
    totals = {}
    for city, category, amount in transactions:
        totals[category] = totals.get(category, 0) + amount
    print(totals)  # {'food': 325, 'travel': 100}

City is ignored because the requested totals are by category.

### 100. Given two lists, return a dictionary showing each item’s frequency difference: count in first list minus count in second list.

    from collections import Counter

    def frequency_difference(first, second):
        count_a, count_b = Counter(first), Counter(second)
        keys = count_a.keys() | count_b.keys()
        return {item: count_a[item] - count_b[item] for item in keys}

    print(frequency_difference(["a", "b", "a"], ["a", "c"]))
    # {'a': 1, 'b': 1, 'c': -1}

This includes negative differences; filter out zero values if only nonzero changes are useful.

## Complexity quick reference

| Operation | Typical complexity | Why |
|---|---:|---|
| List indexing | O(1) | Direct position access |
| List membership | O(n) | May scan every item |
| Set/dict membership | O(1) average | Hash-based lookup; worst case can be slower |
| Sorting | O(n log n) | Comparison sorting |
| One-pass scan | O(n) | Visits each item a constant number of times |

## Key distinctions to remember

- Assignment aliases a list; shallow copies duplicate only the outer container; deep copies recursively duplicate nested objects.
- Mutating list methods such as append(), sort(), reverse(), extend(), and clear() act in place (sort/reverse return None).
- set.remove() raises KeyError when absent; discard() does not. Set order is not a sequence guarantee.
- Tuples cannot reassign their slots, but mutable objects stored inside a tuple can still mutate.
- Dictionary keys and set members must be hashable; dictionary values can be any object.
- Counter counts hashable values; defaultdict can create a value automatically when a key is first accessed.

## References

Checked against the [Python data structures tutorial](https://docs.python.org/3/tutorial/datastructures.html), [built-in types documentation](https://docs.python.org/3/library/stdtypes.html), and [collections documentation](https://docs.python.org/3/library/collections.html).
