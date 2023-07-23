# Substring-Frequency-Count-using-SuffixTree

- It takes multiple strings as input and puts them into a suffix tree. Then extract frequency of all substrings for multiple strings based on the frequencies of the suffix tree nodes.

- The output is equivalent to storing the frequencies by splitting the string into substrings of length 1 up to substrings of length n(see validation part).

- It is possible to count the frequency of only one substring per packet by storing the index of the most recent string counted in the node. (It can solve some problems related with duplicated substrings in a string like 'AAAAAAAA'

You can set the length of the minimum substring to be extracted via the input parameter `k`.
```python
l = ['test1', 'test2', 'esttes']
print(SuffixTree(l).get_frequency(k=3))
```

```python
{'tes': 3, 'test': 2, 'test1': 1, 'test2': 1, 'tte': 1, 'ttes': 1, 'st1': 1, 'st2': 1, 'stt': 1, 'stte': 1, 'sttes': 1, 'est': 3, 'est1': 1, 'est2': 1, 'estt': 1, 'estte': 1, 'esttes': 1}
```
You can set the minimum frequency of substrings to extract via the input parameter `th`.
```python
l = ['test1', 'test2', 'esttes']
print(SuffixTree(l).get_frequency(k=2, th=2))
```

```python
{'te': 3, 'tes': 3, 'test': 2, 'st': 3, 'es': 3, 'est': 3}
```   
   
The result of this module exactly matches the result of the code below (when `th` is 0, `k` is 4).
```python
from collections import Counter

k = 4
c = Counter()
for s in tqdm(strings):
    temp = set()
    for n in range(k, len(s)+1):
        for i in range(len(s) - n + 1):
            temp.add(s[i:i+n])
    c.update(list(temp))
```

### validation
```python
l = ['ABCDEFG', 'ASDCS', 'BCDEF', 'VBDFA', 'ADFVAD', 'ABDVADF', 'VCBDABC', 'AAAAA']
k = 2

d = dict()
for s in l:
    temp_set = set()
    for kk in range(k, len(s)+1):
        for i in range(0, len(s)-kk+1):
            temp_set.add(s[i:i+kk])
    for sub_s in temp_set:
        if tuple(sub_s) not in d:
            d[tuple(sub_s)] = 0
        d[tuple(sub_s)] += 1
        
tree_d = SuffixTree(l).get_frequency(k=2, th=1)
sorted(tree_d.items(), key=lambda x: x[0]) == sorted(d.items(), key=lambda x: x[0])
```

```python
True
```



This code based on Manvi Saxena's ukkonen SuffixTree python code
https://favtutor.com/blogs/ukkonen-algorithm-suffix-tree
