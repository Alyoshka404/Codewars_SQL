# Python Coding Challenges (5 Kyu) <img align="right" src="https://media.tenor.com/4_5IAe-TSAQAAAAi/capoo-bugcat.gif" height="100"/>
<br>

## Find the unique string

**DESCRIPTION:**

There is an array of strings. All strings contains similar letters except one. Try to find it!

```python
find_uniq([ 'Aa', 'aaa', 'aaaaa', 'BbBb', 'Aaaa', 'AaAaAa', 'a' ]) # => 'BbBb'
find_uniq([ 'abc', 'acb', 'bac', 'foo', 'bca', 'cab', 'cba' ]) # => 'foo'
```
Strings may contain spaces. Spaces are not significant, only non-spaces symbols matters. E.g. string that contains only spaces is like empty string.

It’s guaranteed that array contains more than 2 strings.<br>
<br>
<details><summary>My Solution</summary> <br>
  
>```python
>def find_uniq(arr):
>    sett = set(arr[0].lower())
>    l = [1 if (set(i.lower())==sett) else 0  for i in arr ]
>    return arr[l.index(1)] if l.count(1)==1 else arr[l.index(0)]
>```
</details>

---
<br>

## Moving Zeros To The End

**DESCRIPTION:**

Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.

```python
move_zeros([1, 0, 1, 2, 0, 1, 3]) # returns [1, 1, 2, 1, 3, 0, 0]
```
<br>
<details><summary>My Solution</summary> <br>
  
>```python
>def move_zeros(lst):
>    i=0
>    while(i<len(lst)):
>        if(lst[i]==0):
>            lst.remove(0)
>            lst.append(0)
>        i+=1         
>    return lst
>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```python
>  def move_zeros(array):
>    return [x for x in array if x] + [0]*array.count(0)
>```

></details>

---
<br>


  ## <title of the challenge>

**DESCRIPTION:**

  
```python

```

  
```python

``` 

  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```python

>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```python

>```

></details>

---
<br>



