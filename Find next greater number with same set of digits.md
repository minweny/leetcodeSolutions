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

if there are negative numbers
```
def nextPermutation(num: str) -> str:
    if not num: return ""
    n = int(num)
    digits = list(num)
    flag = 1
    if n < 0:
        flag = -1
        digits = digits[1:]
    l = len(digits)
    right = l - 1
    # nextLarger: make sure it's decreasing
    # nextSmaller: make sure it's increasing
    while right - 1 >= 0 and (int(digits[right - 1]) - int(digits[right])) * flag >= 0:
        right -= 1
    if right == 0:
        if n > 0:
            return ""
        else:
            return num[1:]
    replace = l - 1
    while (int(digits[right - 1]) - int(digits[replace])) * flag >= 0:
        replace -= 1
    digits[right - 1], digits[replace] = digits[replace], digits[right - 1]
    digits[right:] = reversed(digits[right:])
    i = 0
    while i < l and digits[i] == "0":
        i += 1
    digits = digits[i:]
    if n < 0:
        digits = ["-"] + digits
    return "".join(digits)

print(nextPermutation("218765"))
# “251678”
print(nextPermutation("1234"))
# “1243”
print(nextPermutation("4321"))
# “”
print("------------------------")
print(nextPermutation("-21"))
# -12
print(nextPermutation("-200"))
# -20
print(nextPermutation("-12"))
# 12
```