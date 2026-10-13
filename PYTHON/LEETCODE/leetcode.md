## 1768. Merge Strings Alternately

### условие : 
<details>
<summary><b>развернуть</b></summary>

[Задача 1768](https://leetcode.com/problems/merge-strings-alternately/description/)
</details>



**Example 1**:
Input: word1 = "abc", word2 = "pqr"
Output: "apbqcr"
Explanation: The merged string will be merged as so:

word1:  a   b   c

word2:    p   q   r

merged: a p b q c r

### решение 1(кастыльное)

```python
class Solution(object):
    def mergeAlternately(self, word1, word2):
        string = ""
        cnt1 = 0
        cnt2 = 0
        for i in range(len(word1)+len(word2)):
            if (cnt1 < len(word1)) and (cnt2 >= len(word2) or i%2 == 0):
                string+=word1[cnt1]
                cnt1+=1
                continue
            string += word2[cnt2]
            cnt2+=1
        return string
```
### решение 2(через zip)

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        lst = []
        for char1,char2 in zip(word1,word2):
            lst.append(char1+char2) 
        lst.append(word1[len(word2):])
        lst.append(word2[len(word1):])
        return "".join(lst) 
```
### новые функции\методы
```python
zip(word1,word2) #склеиввает поочередно 2 объекта с разных объектов(в примере строки word1,word2) и возвращает некий zip объект
```
```python
"".join(lst) #склеивает все элементы lst и раздеяет символом в кавычках(в примере пустота)
```

## 1071. Greatest Common Divisor of Strings

### условие:
<details>
<summary><b>развернуть</b></summary>

[Задача 1071](https://leetcode.com/problems/greatest-common-divisor-of-strings/description/)
</details>


**Example 1**:
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"

**Example 2**:
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"

### решение 1(кастыльное,на новом питоне вообще не сработает)

```python
class Solution(object):
    def gcdOfStrings(self, str1, str2):
        """
        :type str1: str
        :type str2: str
        :rtype: str
        """
        i = 0
        string = ""
        string_zap = ""
        while str1[i] == str2[i]:
            string_zap+=str1[i]
            i+=1
            if (string_zap * (len(str1)/len(string_zap)) == str1) and (string_zap * (len(str2)/len(string_zap))==str2):
                string = string_zap
            if(i >= len(str1) or i >= len(str2)):
                break
        return string
```
### 2 решение(через gcd)
```python
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        if str1 + str2 != str2 + str1:
            return ""
        gcd_lenght = gcd(len(str1),len(str2))
        return str1[:gcd_lenght]
```
### новые функции\методы

```python
gcd(num,num2) #возврашает Наибольший Общий Делитель двух чисел 
```
## 344. Reverse String

### условие:
<details>
<summary><b>развернуть</b></summary>

[Задача 344](https://leetcode.com/problems/reverse-string/description/)
</details>

**Example 1**:
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

### 1 решение
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        s[:] = s[::-1]
        return s
```

### 2 решение
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        return s.reverse()
```
### новые методы\функции

```python
s.reverse() #переворачивает массив
s[:] = s[::-1] #аналог
```

## 1. Two Sum

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 1](https://leetcode.com/problems/two-sum/description/)
</details>

**Example 1**:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
**Example 2**:
Input: nums = [3,2,4], target = 6
Output: [1,2]

### решение полукастыльное
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        lst = []
        ln = len(nums)
        for i in range(ln):
            sm = target - nums[i]
            if sm not in nums[i+1::]: continue
            j = 1
            while j+i < ln:
                if nums[j+i] != sm: 
                    j+=1
                else:
                    lst.append(i)
                    lst.append(i+j)
                    break
            if len(lst) != 0 :break
        return lst
```

### хорошее решение
```python
from typing import List

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_map = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in num_map:
                return [num_map[complement], i]
            num_map[num] = i
# кладем в множество индекс по индексу числа,а потом если число ровно цели,то обращаемся по числу к индексу
```
### новые методы
```python
enumerate(lst) #разбитие на индекс и значение, пример:
for i, num in enumerate(nums):
    print(f"index:{i},value:{num}")
```

## 9. Palindrome Number

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 9](https://leetcode.com/problems/palindrome-number/description/)
</details>

**Example 1**:
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.

### решение
```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        string = str(x)
        return (string == string[::-1])
```

## 13. Roman to Integer

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 13](https://leetcode.com/problems/roman-to-integer/description/)
</details>

**Example 1**:
Input: s = "III"
Output: 3
Explanation: III = 3.

### решение
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        cnt = 0
        dic = {
            'I':1,
            'V':5,
            'X':10,
            'L':50,
            'C':100,
            'D':500,
            'M':1000
        }
        for i in range(len(s)):
            if i < len(s)-1 and dic[s[i]] < dic[s[i+1]]:
                cnt-= dic[s[i]]
            else:
                cnt+= dic[s[i]]       
        return cnt
```
#### та же идея,но костыльно
```python
        cnt = 0
        cnt+=(s.count('M')*1000)
        cnt+=(s.count('D')*500)
        cnt+=(s.count('C')*100)
        cnt+=(s.count('L')*50)
        cnt+=(s.count('X')*10)
        cnt+=(s.count('V')*5)
        cnt+=(s.count('I')*1)
        cnt-=(s.count("CM")*200)
        cnt-=(s.count("CD")*200)
        cnt-=(s.count("XC")*20)
        cnt-=(s.count("XL")*20)
        cnt-=(s.count("IV")*2)
        cnt-=(s.count("IX")*2)
        return cnt
```
## 14. Longest Common Prefix

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 14](https://leetcode.com/problems/longest-common-prefix/description/)
</details>

**Example 1**:
Input: strs = ["flower","flow","flight"]
Output: "fl"

### решение 1
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        string = ""
        st = strs[0]
        cnt = 0
        for i in st:
            for j in range(1,len(strs)):
                if len(string) >= len(strs[j]): return string
                if i != strs[j][cnt]:return string
            string+=i
            cnt+=1
        return string
#перебираем по букве и если совпало со всеми прибавляем
```
### решение 2
```python
class Solution:
    def longestCommonPrefix(self, strs):
        if not strs:
            return ""
        prefix = strs[0]
        for string in strs[1:]:
            while string.find(prefix) != 0:
                prefix = prefix[:-1]
                if not prefix:
                    return ""
        return prefix
# префикс уменьшается от каждого слова
```

### новые приколы
```python
string = "12345"
print(string[:-1]) #1234

string.find(prefix) ## аналог prefix in string,только возвращает не bool,а индекс начала вхождения
```

## 20. Valid Parentheses

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 20](https://leetcode.com/problems/valid-parentheses/description/)
</details>

**Example 1**:
Input: s = "()"
Output: true
**Example 2**:
Input: s = "()[]{}"
Output: true
**Example 3**:
Input: s = "(]"
Output: false

### решение моё(4мс вместо 0мс)
```python
        id1 = 0
        id2 = 0
        id3 = 0
        while (id1 + id2 + id3) != -3:
            id1 = s.find("()")
            if id1 != -1:s = s[:id1]+s[id1+2:]
            id2 = s.find("[]")
            if id2 != -1:s = s[:id2]+s[id2+2:]
            id3 = s.find("{}")
            if id3 != -1:s = s[:id3]+s[id3+2:]
            if s == "": return True
        return False
```

### решение магистра
```python
        mapping = {')': '(', '}': '{', ']': '['}
        stack = []

        for char in s:
            if char in mapping.values():
                stack.append(char)
            elif char in mapping:
                if not stack or mapping[char] != stack.pop():
                    return False
        return not stack
#кладем в stack скобки и убиваем парные,то есть там максиумум одновременно 3 разных вида скобок,которые при появлении правых половинок удаляются
```

## 21. Merge Two Sorted Lists

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 21](https://leetcode.com/problems/merge-two-sorted-lists/description/)
</details>

**Example 1**:
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]

### решение
```python 
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        if not list1 and not list2:
            return list1
        if not list1 or not list2:
            return list1 if not list2 else list2
        dum = ListNode()
        lst = dum
        while list1 and list2:
            if list1.val < list2.val:
              lst.next = list1
              list1 = list1.next
              lst = lst.next
            else:
                lst.next = list2
                list2 = list2.next
                lst = lst.next
        if list1: lst.next = list1
        if list2: lst.next = list2
        return dum.next
#если значение меньше - пишшем в lst,двигаем укаазтель и в list и в lst
#в конце дописываем остаток,тобиш просто присваиваем указатель за которым цепочка оставшихся
#тк двигаем указатель lst необходимо заранее создать доп узел,от которого уже и вернем ответ
```
### новые фишки
```python
from typing import Optional # обертка для списков с доп параметрами для каждого элементе
в данном случае ListNode - список, элемент которого хранит значение val и ссылку на следующий элемент next

также в данном примере приведен паттерн решение dum - дополнительный узел
```

## 26. Remove Duplicates from Sorted Array

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
</details>


**Example 1**:
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

### 1 кастыльное решение
```python
dublicate = set()
        k = 0
        cnt = 0
        for i in range(len(nums)):
            if nums[cnt] in dublicate: 
                nums.pop(cnt)
                continue
            else: 
                dublicate.add(nums[cnt])
                cnt+=1
                k+=1
                continue
            if(len(nums) - cnt) <= 1:break
        return k
```

### 2 умное решение через 2 указателя
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 1
        for j in range(1,len(nums)):
            if nums[j] != nums[i-1]:
                nums[i] = nums[j]
                i+=1
        return i
#по условию допускается,что элементы после k будут мусорными
```

### 3 самое быстрое решение (опять я слишком усложняю)
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        nums[:] = sorted(set(nums))
        return len(nums)
```

### новые фишки

```python
dudl = set() / dubl = {1,2,3} - создание множеств
.add() - добавить / .remove() или .discard() - удаление / .clear() - очистка #основные операции с множествами

 nums[:] - дубликат,также можно .copy()
 ```

 ## 27. Remove Element

 ### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 27](https://leetcode.com/problems/remove-element/description/)
</details>

**Example 1**:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
 
### решение моё(опять кастыль)
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if not nums:return 0
        start = 0
        stop = len(nums) -1
        while start <= stop:
            while nums[stop] == val and start <= stop:stop-=1
            if stop < start: break
            if nums[start] == val:
                tmp = nums[start]
                nums[start] = nums[stop]
                nums[stop] = tmp
                start+=1
                stop-=1
            else:start+=1
        if start == 0 and nums[start] == val:return 0
        return start
```

### простое элегантное решение магистра
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0

        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1
        
        return k
```

## 121. Best Time to Buy and Sell Stock

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
</details>

**Example 1**:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
**Example 2**:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.

### решение
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buy = prices[0]
        cost = 0
        for i in prices[1:]:
            buy = min(buy,i)
            cost = max(cost,i - buy)
        return cost
```

## 141. Linked List Cycle

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 141](https://leetcode.com/problems/linked-list-cycle/description/)
</details>

**Example 1**:
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
**Example 2**:
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

### решение через 2 указателя(стандартный ход)
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
    
        fast = head
        slow = head
        
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            
            if fast == slow:
                return True
    
        return False
#проверям есть цикл или нет
```

### решение через хэш таблицу
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        visited_nodes = set()
        current_node = head
        while current_node:
            if current_node in visited_nodes:
                return True
            visited_nodes.add(current_node)
            current_node = current_node.next
        return False
#множество со связными элементами - хэш таблица
#если следующий уже был в таблице,значит цикл - всё просто
```

## 206. Reverse Linked List

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 206](https://leetcode.com/problems/reverse-linked-list/description/)
</details>

**Example 1**:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

**Example 2**:
Input: head = [1,2]
Output: [2,1]

### решение моё(опять намудрил с тремя указателями)
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:return None
        if head.next is None: return head
        fast = head.next
        slow = head
        prev = None
        if fast:
            while fast.next:
                slow.next = slow
                slow.next.next = prev
                prev = slow
                slow = fast
                fast = fast.next
        slow.next = prev
        fast.next = slow
        return fast
```
### правильное решение без лишних строк
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:return None
        if head.next is None: return head
        prev = None
        slow = head
        while slow.next:
            fast = slow.next
            slow.next = prev
            
            prev = slow
            slow = fast
        slow.next = prev
        return slow
#fast нужен чтобы просто не потерять откуда считать
#prev slow fast
#None   0    1       направляем slow в prev
```
