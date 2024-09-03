# KMP


The Knuth-Morris-Pratt (KMP) algorithm is an efficient string-matching algorithm that searches for occurrences of a "pattern" string P within a "text" string T. The key advantage of KMP over brute-force string matching is that it avoids redundant comparisons by preprocessing the pattern into a partial match table, known as the "Longest Prefix Suffix" (LPS) array.


Pattern Matching:
Let T be the text of length n.
Let P be the pattern of length m.
The goal is to find all starting indices in T where P occurs as a substring.

Longest Prefix Suffix (LPS) Array:
The LPS array is used to store the length of the longest proper prefix of the pattern P that is also a suffix for each substring P[0:i].
A proper prefix is a prefix that is not equal to the entire string.
For example, if P = "abab", the LPS array would be [0, 0, 1, 2].

Prefix:
A prefix of a string is any leading contiguous substring. For example, the prefixes of "abc" are "", "a", "ab", and "abc".

Suffix:
A suffix of a string is any trailing contiguous substring. For example, the suffixes of "abc" are "abc", "bc", "c", and "".


Build the LPS Array:
The LPS array helps in determining the next positions to check in the pattern if a mismatch occurs during the search.
The LPS array is constructed by iterating through the pattern P and comparing the characters of P with its own prefixes.

Pattern Matching:
Begin by comparing the pattern P with the text T starting from the first character of T.
If characters match, continue to compare the next characters of P and T.
If a mismatch occurs:
Use the LPS array to skip unnecessary comparisons by aligning the pattern with the next potential match in the text.
Repeat this process until the entire text T has been searched.
Construction of the LPS Array


Initialize:
Let lps be an array of length m initialized to 0.
Let len be the length of the previous longest prefix suffix (len = 0).
Start with i = 1.

Iterate Through the Pattern:
If P[i] == P[len], increment len and set lps[i] = len.
If P[i] != P[len]:
If len != 0, update len to lps[len - 1] and continue comparing.
If len == 0, set lps[i] = 0 and move to the next character (i++).

Example of LPS Array Construction
For the pattern P = "ababaca":
i | 0 1 2 3 4 5 6
P | a b a b a c a

lps | 0 0 1 2 3 0 1


Initialize:
Let i = 0 (index for T).
Let j = 0 (index for P).

Iterate Through the Text:
Compare P[j] with T[i].
If P[j] == T[i], increment both i and j.
If j == m (full pattern match):
Record the starting index i - j as a match.
Update j = lps[j - 1] to continue searching for the next match.
If P[j] != T[i] and j != 0:
Update j = lps[j - 1].
If P[j] != T[i] and j == 0:
Increment i and move to the next character in T.


Time Complexity
Preprocessing (LPS Array): O(m) where m is the length of the pattern.
Pattern Matching: O(n) where n is the length of the text.
The overall time complexity of the KMP algorithm is O(n + m).
