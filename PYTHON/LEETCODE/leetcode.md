# Решения задач на leetcode (python/c++)

## Содержание
* [1. Two Sum](#1-two-sum)
* [2. Add Two Numbers ](#2-add-two-numbers)
* [9. Palindrome Number](#9-palindrome-number)
* [13. Roman to Integer](#13-roman-to-integer)
* [14. Longest Common Prefix](#14-longest-common-prefix)
* [20. Valid Parentheses](#20-valid-parentheses)
* [21. Merge Two Sorted Lists](#21-merge-two-sorted-lists)
* [26. Remove Duplicates from Sorted Array](#26-remove-duplicates-from-sorted-array)
* [27. Remove Element](#27-remove-element)
* [28. Find the Index of the First Occurrence in a String](#28-find-the-index-of-the-first-occurrence-in-a-string)
* [35. Search Insert Position](#35-search-insert-position)
* [58. Length of Last Word](#58-length-of-last-word)
* [66. Plus One](#66-plus-one)
* [121. Best Time to Buy and Sell Stock](#121-best-time-to-buy-and-sell-stock)
* [141. Linked List Cycle](#141-linked-list-cycle)
* [206. Reverse Linked List](#206-reverse-linked-list)
* [344. Reverse String](#344-reverse-string)
* [1071. Greatest Common Divisor of Strings](#1071-greatest-common-divisor-of-strings)
* [1768. Merge Strings Alternately](#1768-merge-strings-alternately)


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

## 28. Find the Index of the First Occurrence in a String

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
</details>

**Example 1**:
Input: haystack = "sadbutsad", needle = "sad"
Output: 0

**Example 2**:
Input: haystack = "leetcode", needle = "leeto"
Output: -1

### решение моё(оно же идеальное)
```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.size() > haystack.size()){return -1;}
        if(needle.empty() || needle == haystack){return 0;}
        int size = needle.size();
        for(int i = 0;i<haystack.size()-size+1;++i){
            string res = haystack.substr(i,size);
            if(res == needle){return i;}
        }
        return -1;
    }
};
```
### решение на питоне той же задачки
```python
class Solution:
    def strStr(self, haystack, needle):
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i:i+len(needle)] == needle:
                return i
        return -1
```

## 35. Search Insert Position

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 35](https://leetcode.com/problems/search-insert-position/description/)
</details>

**Example 1**:
Input: nums = [1,3,5,6], target = 5
Output: 2

**Example 2**:
Input: nums = [1,3,5,6], target = 2
Output: 1

### решение моё(оно же идеальное,даже компактнее многих из топа)
```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        if(nums.empty()){return 0;}
        int first = 0;
        int end = nums.size()-1;
        while(first <= end){
            int ind = first + (end - first)/2;
            if(nums[ind] < target){first = ind+1;}
            else if(nums[ind] > target){end = ind-1;}
            else{return ind;}
        }
        return first;
    }
};
```
### решение на питоне той же задачки(обычный бинарный поиск)
```python
class Solution:
    def searchInsert(self, nums, target):
        start = 0
        end = len(nums) - 1
        mid = 0
        while start <= end:
            mid = start + (end - start) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid + 1
            else:
                end = mid - 1
        return mid + 1 if target > nums[mid] else mid
```

## 58. Length of Last Word

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 58](https://leetcode.com/problems/length-of-last-word/description/)
</details>

**Example 1**:
Input: s = "Hello World"
Output: 5

**Example 2**:
Input: s = "   fly me   to   the moon  "
Output: 4

### решение моё(оно же идеальное)
```c++
class Solution {
public:
    int lengthOfLastWord(string s) {
        int size = s.length();
        int count = 0;
        for(int i = size-1;i>=0;--i){
            if(s[i] == ' ' && count == 0){continue;}
            if(s[i] == ' '){break;}
            count++;
        }
        return count;
    }
};
```
### решение на питоне той же задачки
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        words = s.split()
        if not words:
            return 0
        return len(words[-1])
```

## 66. Plus One

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 66](https://leetcode.com/problems/plus-one/description/)
</details>

**Example 1**:
Input: digits = [1,2,3]
Output: [1,2,4]

**Example 2**:
Input: digits = [9]
Output: [1,0]

### решение моё(оно же идеальное)
```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int size = digits.size();
        if(digits[size-1] != 9){digits[size-1]++;return digits;}
        auto it = digits.end()-1;
        while(*it == 9){
            *it = 0;
            if(it == digits.begin()){++(*it);digits.push_back(0);return digits;}
            it--;
        }
        ++(*it);
        return digits;
    }
};

прикольное наблюдение - если делать пуш,то после этого итератор слетает с адреса
```
### решение на питоне той же задачки
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        carry = 1
        for i in range(len(digits) - 1, -1, -1):
            s = digits[i] + carry
            digits[i] = s % 10
            carry = s // 10
        if carry:
            digits = [1] + digits
        return digits
```

## 2. Add Two Numbers 
```diff
! middle lvl
```

### условие:

<details>
<summary><b>развернуть</b></summary>

[Задача 2](https://leetcode.com/problems/add-two-numbers/description/)
</details>

**Example 1**:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

**Example 2**:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

### решение моё(немного костыльное,но решил)
```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int one = l1->val,two = l2->val;
        int ost = (one + two)/10;
        ListNode* start = new ListNode((one+two)%10);
        ListNode* res = start;
        if(l1){one = l1->val;l1 = l1->next;}
        if(l2){two = l2->val;l2 = l2->next;}
        while(l1|| l2){
            one = 0,two = 0;
            if(l1){one = l1->val;l1 = l1->next;}
            if(l2){two = l2->val;l2 = l2->next;}
            ListNode* res = new ListNode((one+two+ost)%10);
            ost = (one+two+ost)/10;
            start->next = res;
            start = start->next;
        }
        if(ost!=0){
            ListNode* finish = new ListNode(ost);
            start->next = finish;
        }
        return res;
    }
};

прикольное наблюдение - если использовать if(l1.next == nullptr),то это работает в разы дольше,чем просто if(l1)
```
### более чистое решение той же задачки
```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* start = head;
        int ost = 0;
        while(l1 || l2 || ost != 0){
            int one = (l1) ? l1->val : 0;
            int two = (l2) ? l2->val : 0;
            ListNode* res = new ListNode((one+two+ost)%10);
            ost = (one+two+ost)/10;

            start->next = res;
            start = start->next;

            l1 = (l1) ? l1->next : nullptr;
            l2 = (l2) ? l2->next : nullptr;

        }
        ListNode* result =head->next;
        delete head;
        return result;
    }
};
```
### решение на питоне
```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = cur =ListNode(0)
        carry = 0
        while l1 or l2 or carry:
            if l1:
                carry += l1.val
                l1 = l1.next
            if l2:
                carry += l2.val
                l2 = l2.next
            cur.next = ListNode(carry%10)
            cur = cur.next
            carry //=10
        return dummy.next
```
