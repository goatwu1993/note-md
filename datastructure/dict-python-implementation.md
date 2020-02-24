---
title: "Python 實作 Dictionary"
date: 2019-12-26T19:17:18+08:00
draft: false
tags: [python, datastructure]
slug: dict-python-implementation
math: true
toc: true
weight: 40
summary: A python implemented dictionary.
---

## Dictionary

Python Dictionary 的好用大家都知道，反過來，我覺得用 Python 實作一個 Dictionary 是個複習資料結構的好方法。

## 瞄一下

瞄一下[cpython](https://github.com/python/cpython/blob/master/Objects/dictobject.c)怎麼寫，[這邊](https://www.data-structures-in-practice.com/hash-tables/?fbclid=IwAR351NVEsa5779Ph_8wG7Pi5U40bQlafRDuXAZxAtJO-WOpCCjEMqv7g5HY)有詳細解釋。

## Hash table 優點

- O(1) insertion
- O(1) get
- O(1) delete

但是要在 laod factor 在一定範圍內才能給出時間複雜度 O(1)的但書。

## Load Factor & dynamic resizing

<https://en.wikipedia.org/wiki/Hash_table#Resizing_by_copying_all_entries>

$$Load Factor = n/k $$

$$ k : bucket 數目，也叫 table size$$
$$ n : 資料筆數，k 通常略大於 n，留下(k-n)筆空白欄位。$$

實務上控制 Load factor 介於 0.3 至 0.7 ，時間 O(1)的同時 k 還小。

## Dictionary Node

```python
class DictionaryNode():
    """
    Node of a DictionaryLinkedList.
    """

    def __init__(self, key, value, me_hash):
        self.key = key
        self.value = value
        self.me_hash = me_hash
        self.collided = False

    def __repr__(self):
        return (self.key.__repr__() + ": " + self.value.__repr__())
```

### me_hash

key 的 hash 值，cpython get 的時候比對會用到

```c
(ep->me_key == key ||
(ep->me_hash == hash && unicode_eq(ep->me_key, key)))
```

詳細原因可能要對編碼比較熟才看得懂，我存著 resize 就不需要重算一次。

### collided

判斷是否 collide 過的 flag，若 delete 時 collided 為 True，告訴大家這 node 沒有值但需要往後尋找，若沒有 collide 過則代表沒有 collide 過，返回 indexError。

## Dictionary Class

```python
class Dictionary():
    """
    Dictionary are implemented by HashTable
    Using open addressing method.
    Hash using siphash. I can not find siphash
    """

    def __init__(self):
        self.used_entry = 0
        self.buckets = [None for x in range(0, 8)]
```

初始大小為 8 ，python 沒有辦法 override {} 的讀取， KVP 只能慢慢塞。

另外存取 used_entry 以免 len()需要跑 O(n)的 loop，insert/del 要記得 maintain。

## Hash

仿照 cpython 用 siphash，據作者所述是一個快速的 hash ，用過 md5 也是可以的。

```bash
pip install siphash
```

```python
from siphash import siphash24
```

### Dictionary 的 me_hash()

```python
    def me_hash(self, key):
        """
        hash of key
        """
        return siphash24(b'0123456789ABCDEF',(str(key).encode('utf-8'))).hash()
```

## Dynamic Resizing

### bitmask (&) 運算

當 k (table size) 是 2 的 m 次方，則 hash(n) mod k 可以用 hash(n) & bitmask 取代，其中 bitmask 為 m 個 1 組成。

### bitmask (&) in Python terminal

```python
>>> def hash(key): return siphash24(b'0123456789ABCDEF',(str(key).encode('utf-8'))).hash()
...
>>> n = 'key_string'
>>>
>>> # m = 3, k = 8
...
>>> hash(n) & 0b111 == hash(n) & 7
True
>>> hash(n) & 0b111 == hash(n) % 8
True
>>>
>>> # m = 4, k = 16
...
>>> hash(n) & 0b1111 == hash(n) & 15
True
>>> hash(n) & 0b1111 == hash(n) % 16
True
>>>
```

### Resizing 程式碼

```python
    def resize(self):
        """
        Should change the size if load_factor > 2/3 or load_factor < 2/3
        Should do nothing if load_factor between 1/3 and 2/3
        """
        def proper_size(n, k):
            pro_size = 8 if n <= 2 else 2**(int(n * 1.5)).bit_length()
            return pro_size

        used = self.used_entry
        old_size = len(self.buckets)
        new_size = proper_size(used, old_size)
        if old_size == new_size:
            return
        new_buckets = [None for x in range(0, new_size)]
        for i in range(old_size):
            if self.buckets[i] and (self.buckets[i].key is not None):
                key_me_hash = self.buckets[i].me_hash
                # & for bitwise operation (bitmask)
                entry = key_me_hash & (new_size-1)
                while new_buckets[entry]:
                    new_buckets[entry].collided = True
                    entry = entry+1 if entry < (new_size-2) else 0
                new_buckets[entry] = self.buckets[i]
                new_buckets[entry].collided = False
        self.buckets = new_buckets
```

## Magic Methods

### 實作 python 內建的 Magic Methods

```python
# __setitem__
a[b] = c
# __getitem__
a[b]
# __len__
len(a)
# __delitem__
del a[b]
```

### Open Addressing

這裡用的是最簡單的 open addressing，entry 被佔據就找下一個，比較簡單，但容易有連續一整攤都被 occupied 的情形發生，如果有興趣可以實作其他的 open addressing 算法。

### Magic Methods 程式碼

```python
    def __repr__(self):
        s = ''
        for i in range(len(self.buckets)):
            if self.buckets[i]:
                s = s + self.buckets[i].__repr__() + ', '
        return {} if not s else "{{{0}}}".format(s[:-3])

    def __getitem__(self, key):
        key_me_hash = self.me_hash(key)
        l = len(self.buckets)
        entry = key_me_hash & (l-1)
        while self.buckets[entry]:
            if self.buckets[entry].key == key:
                return self.buckets[entry].value
            if not self.buckets[entry].collided:
                raise KeyError(key)
            entry = entry+1 if entry < (l-2) else 0
        raise KeyError(key)

    def __setitem__(self, key, value):
        self.used_entry += 1
        self.resize()

        l = len(self.buckets)
        key_me_hash = self.me_hash(key)
        entry = key_me_hash & (l-1)
        while self.buckets[entry]:
            self.buckets[entry].collided = True
            entry = entry+1 if entry < (l-2) else 0
        self.buckets[entry] = DictionaryNode(key=key,
                                             value=value,
                                             me_hash=key_me_hash)

    def __delitem__(self, key):
        key_me_hash = self.me_hash(key)
        l = len(self.buckets)
        entry = key_me_hash & (l-1)
        while self.buckets[entry]:
            if self.buckets[entry].key == key:
                self.buckets[entry].key = None
                self.buckets[entry].value = None
                self.buckets[entry].me_hash = None
                return
            if not self.buckets[entry].collided:
                raise KeyError(key)
            entry = entry+1 if entry < (l-2) else 0
        raise KeyError(key)

    def __len__(self):
        counter = 0
        for i in range(len(self.buckets)):
            if self.buckets[i]:
                counter += 1
        return counter
```

## 完整程式碼

[Github](https://github.com/goatwu1993/data_structure/blob/master/hash_table.py)

## 結論

Python 自己內建的資料結構，很多都是直接用 c 寫的，速度上快很多，如果沒必要，還是直接用就好了...

## References

- [大神解說](https://www.data-structures-in-practice.com/hash-tables/?fbclid=IwAR351NVEsa5779Ph_8wG7Pi5U40bQlafRDuXAZxAtJO-WOpCCjEMqv7g5HY)
- [wiki](https://en.wikipedia.org/wiki/Hash_table#Resizing_by_copying_all_entries)
- [cpython](https://github.com/python/cpython/blob/master/Objects/dictobject.c)
- [Magic Method](https://blog.csdn.net/yuan_j_y/article/details/9317817)

$$
$$
