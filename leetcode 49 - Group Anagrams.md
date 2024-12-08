49. Group Anagrams, https://leetcode.com/problems/group-anagrams/description/

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = defaultdict(list)
        for word in strs:
            count = [0] * 26
            for c in word:
                count[ord(c) - ord('a')] += 1
            d[tuple(count)].append(word)
        return list(d.values())
```