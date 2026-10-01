# Python String Interview Questions: 100 Answers

> Answers to every question in the supplied PDF. The PDF is a practice checklist and source material, not instructions that narrow this request. Each answer includes a concise explanation; assumptions are called out where wording is ambiguous.

## Interview response pattern

State the rule, give a clear solution, and mention relevant edge cases (empty input, spaces, punctuation, case, overlap, Unicode). Python strings are immutable: methods such as upper() and replace() return a new string.

## 1. Print a string

**Question:** Print a string.

    print('Hello, Python!')

Displays the text; quote marks are syntax, not output.

## 2. Read and print a string

**Question:** Take a string as input and print it.

    text = input('Enter text: ')
    print(text)

input() always returns text, even when the user types digits.

## 3. Length using len()

**Question:** Find the length of a string using len().

    len('Python')  # 6

Counts string elements.

## 4. Length without len()

**Question:** Find the length of a string without using len().

    n = 0
    for _ in 'Python':
        n += 1
    print(n)  # 6

A loop visits one element per iteration; use len() in real code.

## 5. First character

**Question:** Print the ﬁrst character of a string.

    text = 'Python'
    print(text[0] if text else 'empty')

Index 0 is first; check empty strings to avoid IndexError.

## 6. Last character

**Question:** Print the last character of a string.

    text = 'Python'
    print(text[-1] if text else 'empty')

Index -1 is last; check for empty input.

## 7. Print each character

**Question:** Print every character using a loop.

    for char in 'Python':
        print(char)

Strings are iterable, in order.

## 8. Characters at even indexes

**Question:** Print characters at even indexes.

    text = 'Python'
    print(text[::2])  # Pto

Even indexes are 0, 2, 4; this is not ordinal positions 2, 4, 6.

## 9. Characters at odd indexes

**Question:** Print characters at odd indexes.

    text = 'Python'
    print(text[1::2])  # yhn

Odd indexes are 1, 3, 5.

## 10. Uppercase

**Question:** Convert a string to uppercase.

    'Python strings'.upper()  # PYTHON STRINGS

Returns a new string; strings are immutable.

## 11. Lowercase

**Question:** Convert a string to lowercase.

    'Python STRINGS'.lower()  # python strings

Returns a new string.

## 12. Swap case

**Question:** Swap uppercase letters to lowercase and vice versa.

    'PyThOn 3!'.swapcase()  # pYtHoN 3!

Swaps cased letters; punctuation and digits stay the same.

## 13. Capitalize first character

**Question:** Capitalize the ﬁrst character of a string.

    'python is fun'.capitalize()  # Python is fun

Also lowercases the remaining cased characters.

## 14. Title case

**Question:** Convert every word in a sentence to title case.

    'learning python'.title()  # Learning Python

Simple title rules may not suit all names/languages.

## 15. Entirely uppercase

**Question:** Check whether a string is entirely uppercase.

    'PYTHON'.isupper()  # True

Needs at least one cased letter; uncased-only text returns False.

## 16. Entirely lowercase

**Question:** Check whether a string is entirely lowercase.

    'python'.islower()  # True

Needs at least one cased letter.

## 17. Only alphabetic

**Question:** Check whether a string contains only alphabetic characters.

    'Python'.isalpha()  # True

Unicode letters count; spaces and empty string do not.

## 18. Only digits

**Question:** Check whether a string contains only digits.

    '2026'.isdigit()  # True

Not a signed/decimal-number validator.

## 19. Alphanumeric

**Question:** Check whether a string is alphanumeric.

    'Python3'.isalnum()  # True

Letters and digits only, at least one character.

## 20. Only whitespace

**Question:** Check whether a string contains only whitespace.

    ' \t\n'.isspace()  # True

Empty string returns False.

## 21. Reverse by slicing

**Question:** Reverse a string using slicing.

    'Python'[::-1]  # nohtyP

Negative step walks backward.

## 22. Reverse using loop

**Question:** Reverse a string using a loop.

    out = ''
    for c in 'Python':
        out = c + out
    print(out)  # nohtyP

Clear but repeated concatenation is inefficient for large strings.

## 23. Reverse with reversed()

**Question:** Reverse a string using reversed(). Python String Manipulation Coding Questions

    ''.join(reversed('Python'))  # nohtyP

reversed() is an iterator; join builds the string.

## 24. Palindrome exact

**Question:** Check whether a string is a palindrome.

    s = 'level'
    s == s[::-1]  # True

Case and spaces matter in this definition.

## 25. Palindrome ignoring spaces

**Question:** Check whether a sentence is a palindrome while ignoring spaces.

    s = 'Never odd or even'
    c = s.replace(' ', '').lower()
    c == c[::-1]  # True

Only ordinary spaces and case are ignored.

## 26. Palindrome ignoring punctuation/case

**Question:** Check whether a sentence is a palindrome while ignoring spaces, punctuation, and letter case.

    s = 'A man, a plan, a canal: Panama!'
    c = ''.join(ch.casefold() for ch in s if ch.isalnum())
    c == c[::-1]  # True

casefold handles caseless Unicode comparison better than lower; alphanumeric filter drops punctuation/spaces.

## 27. Reverse word order

**Question:** Reverse the order of words in a sentence. Example: I love Python becomes Python love I.

    ' '.join('I love Python'.split()[::-1])  # Python love I

split() normalizes repeated whitespace.

## 28. Reverse each word

**Question:** Reverse each word individually in a sentence. Example: I love Python becomes I evol nohtyP.

    ' '.join(w[::-1] for w in 'I love Python'.split())  # I evol nohtyP

Keeps word order, reverses characters in each word.

## 29. Reverse only vowels

**Question:** Reverse only the vowels in a string.

    def reverse_vowels(s):
        v = set('aeiouAEIOU')
        a = list(s); i, j = 0, len(a)-1
        while i < j:
            while i < j and a[i] not in v: i += 1
            while i < j and a[j] not in v: j -= 1
            a[i], a[j] = a[j], a[i]; i += 1; j -= 1
        return ''.join(a)
    print(reverse_vowels('hello'))  # holle

Two pointers swap vowels in place in a mutable list. Defines English vowels as aeiou.

## 30. Reverse without slicing

**Question:** Reverse a string without using slicing ([::-1]).

    ''.join(reversed('Python'))  # nohtyP

Avoids slicing; if reversed() is also disallowed, loop indexes from len(s)-1 down to zero.

## 31. Count vowels

**Question:** Count vowels in a string.

    sum(c.lower() in 'aeiou' for c in 'Python Interview')  # 5

Defines vowels as English aeiou; sum counts True values.

## 32. Count consonants

**Question:** Count consonants in a string.

    sum(c.isalpha() and c.lower() not in 'aeiou' for c in 'Python 3')  # 5

Only alphabetic non-vowels count.

## 33. Count digits

**Question:** Count digits in a string.

    sum(c.isdigit() for c in 'Python 3.12')  # 3

Unicode-aware; use '0' <= c <= '9' for ASCII only.

## 34. Count spaces

**Question:** Count spaces in a string.

    'Python is fun'.count(' ')  # 2

Counts ordinary spaces; use isspace() to include tabs/newlines.

## 35. Count uppercase/lowercase

**Question:** Count uppercase and lowercase characters separately.

    s='PyTHon 3!'
    (sum(c.isupper() for c in s), sum(c.islower() for c in s))  # (3, 3)

Nonletters are neither.

## 36. Count special characters

**Question:** Count special characters.

    s='Py@thon-3!'
    sum(not c.isalnum() and not c.isspace() for c in s)  # 3

Defines special as neither letter/digit nor whitespace; clarify definition.

## 37. Count words

**Question:** Count the number of words in a sentence.

    len('  Python   makes data work. '.split())  # 4

No-argument split handles runs of whitespace.

## 38. Count lines

**Question:** Count lines in a multi-line string.

    len('Python\nPandas\nStrings'.splitlines())  # 3

splitlines handles common line breaks.

## 39. Count character

**Question:** Count occurrences of a given character.

    'programming'.count('m')  # 2

Counts matches.

## 40. Count word

**Question:** Count occurrences of a given word.

    ' '.join('Python is fun; Python is useful.'.lower().replace(';','').replace('.','').split()).split().count('python')  # 2

Normalize punctuation/case before token counting; for general text use a tokenizer.

## 41. Count substring

**Question:** Count occurrences of a substring.

    'banana'.count('ana')  # 1

Counts non-overlapping matches; overlapping count is 2.

## 42. Character frequencies

**Question:** Find the frequency of every character.

    from collections import Counter
    Counter('banana')  # a:3, n:2, b:1

Counter is a dictionary-like frequency counter.

## 43. Word frequencies

**Question:** Find the frequency of every word in a sentence.

    from collections import Counter
    Counter('Python is fun and Python is useful'.lower().split())

Whitespace tokenization; punctuation remains attached unless normalized.

## 44. Most frequent character

**Question:** Find the most frequently occurring character.

    from collections import Counter
    Counter('banana').most_common(1)  # [('a', 3)]

Define tie handling if multiple characters tie.

## 45. Least frequent character

**Question:** Find the least frequently occurring character.

    from collections import Counter
    c=Counter('banana'); m=min(c.values())
    [x for x,n in c.items() if n==m]  # ['b']

Returns all ties; handle empty input before min().

## 46. Substring exists

**Question:** Check whether a substring exists in a string.

    'gram' in 'programming'  # True

in returns a Boolean.

## 47. First substring position

**Question:** Find the position of the ﬁrst occurrence of a substring.

    'banana'.find('na')  # 2

Returns -1 when absent.

## 48. Last substring position

**Question:** Find the position of the last occurrence of a substring.

    'banana'.rfind('na')  # 4

Searches from right; index is still in original string.

## 49. All character positions

**Question:** Find all positions where a character appears.

    [i for i,c in enumerate('banana') if c=='a']  # [1,3,5]

enumerate pairs each character with its zero-based index.

## 50. Replace word

**Question:** Replace one word with another in a sentence.

    'I like Java'.replace('Java','Python')  # I like Python

Returns a new string; replaces all matches by default.

## 51. Spaces to hyphens

**Question:** Replace spaces with hyphens (-).

    'Python interview questions'.replace(' ','-')

Every ordinary space replaced.

## 52. Collapse whitespace

**Question:** Replace multiple spaces with one space.

    ' '.join('Python   strings\tare useful'.split())  # Python strings are useful

Normalizes spaces, tabs, and newlines to one space.

## 53. Replace vowels with *

**Question:** Replace all vowels with *.

    ''.join('*' if c.lower() in 'aeiou' else c for c in 'Python Interview')  # Pyth*n *nt*rv**w

Simple English vowel set.

## 54. Digits to #

**Question:** Replace digits with #.

    ''.join('#' if c.isdigit() else c for c in 'Room 204')  # Room ###

Unicode digit behavior follows isdigit().

## 55. Remove specified character

**Question:** Remove a speciﬁed character from a string.

    'programming'.replace('m','')  # prograning

Empty replacement removes all occurrences.

## 56. Remove spaces

**Question:** Remove all spaces from a string.

    'Python is fun'.replace(' ','')  # Pythonisfun

For all whitespace, use ''.join(s.split()).

## 57. Remove leading whitespace

**Question:** Remove leading whitespace.

    '   Python  '.lstrip()  # Python  

Only left edge.

## 58. Remove trailing whitespace

**Question:** Remove trailing whitespace.

    '   Python  '.rstrip()  #    Python

Only right edge.

## 59. Trim both ends

**Question:** Remove whitespace from both ends.

    '   Python  '.strip()  # Python

Does not remove internal whitespace.

## 60. Remove punctuation

**Question:** Remove punctuation from a sentence.

    import string
    ''.join(c for c in "Hello, Python!" if c not in string.punctuation)  # Hello Python

string.punctuation is ASCII; Unicode punctuation needs extra handling.

## 61. Split sentence

**Question:** Split a sentence into a list of words.

    'I love Python'.split()  # ['I','love','Python']

Whitespace split.

## 62. Join sentence

**Question:** Join a list of words into a sentence.

    ' '.join(['I','love','Python'])  # I love Python

All list elements must be strings.

## 63. Join with hyphen

**Question:** Join words using a hyphen.

    '-'.join(['python','interview','questions'])

Separator is the string before join().

## 64. Split comma list

**Question:** Split a comma-separated string into a list. Example: Python,Java,C++ becomes ['Python', 'Java', 'C++'].

    'Python,Java,C++'.split(',')

Exact delimiter; strip fields if spaces around commas are possible.

## 65. Comma to spaces

**Question:** Convert a comma-separated string to a space-separated string.

    ' '.join(x.strip() for x in 'Python, Java,C++'.split(','))

Split, trim each field, then join.

## 66. Email username and domain

**Question:** Extract a username and domain from an email address.

    user, domain = 'learner@example.com'.split('@', 1)

Assumes a well-formed address and one @ separator.

## 67. Filename and extension

**Question:** Extract the ﬁlename and extension from report.pdf.

    from pathlib import PurePath
    p=PurePath('report.pdf'); (p.stem, p.suffix)  # ('report','.pdf')

suffix includes dot; pathlib handles path naming.

## 68. File extension

**Question:** Extract the ﬁle extension from a ﬁlename.

    from pathlib import PurePath
    print(PurePath('report.pdf').suffix)  # .pdf

For multiple suffixes use .suffixes.

## 69. Date hyphens to slashes

**Question:** Convert a date from 27-09-2026 to 27/09/2026.

    '27-09-2026'.replace('-', '/')  # 27/09/2026

Replacement changes formatting only; use datetime for validation.

## 70. Split first/last name

**Question:** Split a full name into ﬁrst name and last name.

    first, last = 'Rahul Kumar'.split()

Assumes exactly two parts; real names can contain more.

## 71. Underscore to space

**Question:** Convert ﬁ rst_name to ﬁ rst name.

    'first_name'.replace('_',' ')  # first name

Simple replacement.

## 72. Space to underscore

**Question:** Convert ﬁ rst name to ﬁ rst_name.

    'first name'.replace(' ','_')  # first_name

Simple replacement.

## 73. Sentence to characters

**Question:** Convert a sentence into a list of individual characters.

    list('Python')  # ['P','y','t','h','o','n']

Spaces/punctuation are included.

## 74. Join characters with hyphen

**Question:** Join characters using -. Example: Python becomes P-y-t-h-o-n.

    '-'.join('Python')  # P-y-t-h-o-n

Strings are iterable.

## 75. Separate camelCase words

**Question:** Separate words from a camelCase string. Example: pythonInterviewQuestions becomes python Interview Questions.

    import re
    s='pythonInterviewQuestions'
    r=re.sub(r'([a-z0-9])([A-Z])', r'\1 \2', s)
    r[0].upper()+r[1:]  # Python Interview Questions

Regex inserts boundary; acronyms such as HTTPServer need a stated rule.

## 76. Remove duplicate characters

**Question:** Remove duplicate characters from a string.

    ''.join(dict.fromkeys('programming'))  # progamin

Dict preserves insertion order in modern Python.

## 77. Remove duplicate words

**Question:** Remove duplicate words from a sentence.

    ' '.join(dict.fromkeys('Python is fun and Python is useful'.split()))  # Python is fun and useful

Case-sensitive; casefold tokens for case-insensitive uniqueness.

## 78. Remove vowels

**Question:** Remove all vowels from a string.

    ''.join(c for c in 'Python Interview' if c.lower() not in 'aeiou')  # Pythn ntrvw

Uses English aeiou.

## 79. Remove digits

**Question:** Remove all digits from a string.

    ''.join(c for c in 'Room 204' if not c.isdigit())  # Room 

Filters digit characters.

## 80. Extract digits

**Question:** Extract only digits from a string.

    ''.join(c for c in 'Room 204, floor 3' if c.isdigit())  # 2043

Concatenates digits; separators between numbers are lost.

## 81. Extract alphabets

**Question:** Extract only alphabets from a string.

    ''.join(c for c in 'Py3-thon!' if c.isalpha())  # Python

Unicode alphabetic characters accepted.

## 82. Extract uppercase letters

**Question:** Extract only uppercase letters.

    ''.join(c for c in 'PyTHon 3!' if c.isupper())  # PTH

Filters uppercase cased letters.

## 83. Extract lowercase letters

**Question:** Extract only lowercase letters.

    ''.join(c for c in 'PyTHon 3!' if c.islower())  # yon

Filters lowercase cased letters.

## 84. Collapse multiple spaces

**Question:** Convert multiple spaces to a single space.

    ' '.join('Python   strings'.split())  # Python strings

Also normalizes tabs and line breaks.

## 85. Remove newline and tab

**Question:** Remove newline (\n) and tab (\t) characters.

    'Python\tstrings\n'.replace('\t','').replace('\n','')  # Pythonstrings

If separators should remain, replace with spaces and normalize.

## 86. Format name

**Question:** Format a name: rAhUl kumAr becomes Rahul Kumar.

    ' '.join(part.capitalize() for part in 'rAhUl kumAr'.split())  # Rahul Kumar

Simple casing rule, not universal name convention.

## 87. Mask email

**Question:** Mask an email address. Example: rahul@gmail.com becomes r***l@gmail.com.

    def mask_email(email):
        user, domain = email.split('@',1)
        masked = user[0] + '*'*max(0,len(user)-2) + (user[-1] if len(user)>1 else '')
        return masked+'@'+domain
    mask_email('rahul@gmail.com')  # r***l@gmail.com

Assumes one @ and nonempty username; display masking is not a security guarantee.

## 88. Mask phone except last four

**Question:** Mask a phone number except for the last four digits.

    digits=''.join(c for c in '+1 (415) 555-2678' if c.isdigit())
    '*' * max(0,len(digits)-4) + digits[-4:]  # **********2678

Example returns digits-only masking; preserve separators if required.

## 89. Basic email check

**Question:** Check whether an email has a basic valid format: one @ and a domain part.

    email='learner@example.com'
    email.count('@') == 1 and bool(email.split('@')[1])

Only the stated basic rule; not full email validation.

## 90. Password categories

**Question:** Check whether a password contains uppercase, lowercase, digit, and special characters.

    s='Python3!'
    any(c.isupper() for c in s) and any(c.islower() for c in s) and any(c.isdigit() for c in s) and any(not c.isalnum() and not c.isspace() for c in s)

Checks categories only, not length or strength.

## 91. Case-insensitive equality

**Question:** Check whether two strings are equal without considering case.

    'Python'.casefold() == 'PYTHON'.casefold()  # True

casefold is suited to Unicode caseless matching.

## 92. Starts with prefix

**Question:** Check whether a string starts with a given preﬁx.

    'python_file.py'.startswith('python')  # True

Can pass tuple of possible prefixes.

## 93. Ends with suffix

**Question:** Check whether a string ends with a given suﬃx.

    'report.pdf'.endswith('.pdf')  # True

Use pathlib for actual file path handling.

## 94. Whole word search

**Question:** Check whether a word is present as a whole word in a sentence.

    import re
    re.search(r'\bPython\b', 'Pythonista and Python') is not None  # True

Avoids matching Python inside Pythonista; language token rules can vary.

## 95. Same characters ignoring case

**Question:** Check whether two strings contain the same characters, ignoring case.

    from collections import Counter
    Counter('Listen'.casefold()) == Counter('Silent'.casefold())  # True

Anagram check; duplicates matter. Normalize punctuation/spaces only if requested.

## 96. Contains character

**Question:** Check whether a string contains a given character.

    't' in 'Python'  # True

Validate len(target)==1 if exactly one character is required.

## 97. Is empty

**Question:** Check whether a string is empty.

    text=''
    text == ''  # True; idiom: not text

Empty string is falsey.

## 98. Only ordinary spaces

**Question:** Check whether a string contains only spaces.

    bool('   ') and all(c==' ' for c in '   ')  # True

Use isspace() for tabs/newlines too; bool avoids treating empty as spaces.

## 99. Can convert to integer

**Question:** Check whether a string can be converted to an integer.

    def can_int(s):
        try: int(s); return True
        except ValueError: return False
    can_int('-42')  # True

Try the actual conversion; isdigit rejects signs and surrounding whitespace.

## 100. Valid Python identifier

**Question:** Check whether a string is a valid Python identiﬁer using isidentiﬁ er().

    'student_name'.isidentifier()  # True

Syntax only; also reject reserved words with keyword.iskeyword().

## Corrections and clarifications worth remembering

- str.count(substring) counts non-overlapping matches. In banana, count('ana') is 1 although there are two overlapping starting positions.
- isdigit() is not an integer parser: it rejects signs and decimal notation. Try int(text) and catch ValueError when checking convertibility.
- isidentifier() checks syntax, not reserved words; class is an identifier-shaped string but a Python keyword.
- A whole-word match is different from substring membership: Python appears inside Pythonista.
- Basic email/password checks in this list are intentionally limited to the stated requirements, not full validators or security policies.
- The source PDF's count sample labels whitespace as spaces; isspace() counts tabs/newlines too. Be precise about the requested category.

## Five composite sample solutions

### Count vowels, consonants, digits, and whitespace

    def count_characters(text):
        vowels = consonants = digits = whitespace = 0
        for char in text:
            if char.lower() in 'aeiou':
                vowels += 1
            elif char.isalpha():
                consonants += 1
            elif char.isdigit():
                digits += 1
            elif char.isspace():
                whitespace += 1
        return vowels, consonants, digits, whitespace
    print(count_characters('Python 3 is Fun'))  # (3, 8, 1, 3)

Consonants mean alphabetic characters outside the five English vowels. Punctuation is not counted.

### Palindrome ignoring spaces and case

    text = 'Never odd or even'
    cleaned = text.replace(' ', '').lower()
    print(cleaned == cleaned[::-1])  # True

To ignore punctuation too, filter with isalnum() and normalize with casefold(), as in Question 26.

### Character frequency

    from collections import Counter
    text = 'python programming'
    frequency = Counter(char for char in text if char != ' ')
    print(dict(frequency))

Counter handles the bookkeeping. Filtering the ordinary space is an explicit choice; preserve it if spaces should count.

### Reverse word order

    sentence = 'I am learning Python'
    print(' '.join(sentence.split()[::-1]))  # Python learning am I

### Remove duplicate characters while preserving order

    print(''.join(dict.fromkeys('programming')))  # progamin

Modern Python dictionaries preserve insertion order, so the first occurrence of every character remains.

## Complexity notes

Most scans over a string take O(n) time. Building a result usually takes O(n) extra space. Mention these when asked; prioritize explaining the rule and edge cases first.

## Core string-method reminder

- Case: lower(), upper(), casefold(), swapcase(), capitalize(), title().
- Search: find(), rfind(), index(), count(), in, startswith(), endswith(). find() returns -1; index() raises ValueError when absent.
- Editing: replace(), strip(), lstrip(), rstrip(). Strip methods work at the ends, not in the middle.
- Split/join: split(), rsplit(), splitlines(), join(). join() requires string elements.
- Character checks: isalpha(), isdigit(), isalnum(), isspace(), isupper(), islower(), isidentifier().

Prefer the simplest correct answer, and state the input assumptions aloud.
