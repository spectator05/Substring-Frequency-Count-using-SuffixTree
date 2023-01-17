# Substring-Frequency-Count-using-SuffixTree

- It takes multiple strings as input and puts them into the suffix tree. Then extract frequency of all substrings for multiple strings based on the frequencies of the suffix tree nodes.

- The output of this is equivalent to storing the frequencies by splitting the string into substrings of length 1 up to substrings of length n.

- It is possible to count the frequency of only one substring per packet by storing the index of the most recent packet counted in the node.

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
            temp.add(p[i:i+n])
    c.update(list(temp))
```

This code based on Manvi Saxena's ukkonen SuffixTree python code
https://favtutor.com/blogs/ukkonen-algorithm-suffix-tree
