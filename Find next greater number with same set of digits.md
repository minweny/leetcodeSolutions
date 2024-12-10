https://www.geeksforgeeks.org/find-next-greater-number-set-digits/

O(n)
```
def nextPermutation(num: str) -> str:
    if not num: return ""
    digits = list(num)
    l = len(digits)
    right = l - 1
    while right - 1 >= 0 and digits[right - 1] >= digits[right]:
        right -= 1
    if right == 0:
        return ""
    replace = l - 1
    while digits[right - 1] >= digits[replace]:
        replace -= 1
    digits[right - 1], digits[replace] = digits[replace], digits[right - 1]
    digits[right:] = reversed(digits[right:])
    return "".join(digits)

print(nextPermutation("218765"))
# “251678”
print(nextPermutation("1234"))
# “1243”
print(nextPermutation("4321"))
# “”
```