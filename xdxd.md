- Write a program to find the word with maximum different letters in given string python
```py
def getMaxOccuringChar(str):
    # Create array to keep the count of individual characters
    # Initialize the count array to zero
    count = [0] * ASCII_SIZE

    # Utility variables
    max = -1
    c = ''

    # Traversing through the string and maintaining the count of
    # each character
    for i in str:
        count[ord(i)]+=1;

    for i in str:
        if max < count[ord(i)]:
            max = count[ord(i)]
            c = i

    return c
```
Time Complexity: O(n)
Space Complexity: O(1) — Because we are using fixed space (Hash array) irrespective of input string size.

- Write a program to change the first letter in every word of the string into uppercase.

```py
given_string = "Write a program to change the change first letter of every word of the string into uppercase"

modified_string = " ".join([w[0].upper() + w[1:] for w in given_string.split(" ")])

print(modified_string)
```