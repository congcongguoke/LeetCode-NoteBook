# 28. Implement strStr() | Determine If One String Is Another's Substring

```ruby
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```



- Clarification:
  - What should we return when needle is an empty string? This is a great question to ask 
    during an interview.
  - For the purpose of this problem, we will return 0 when needle is an empty string. 
    This is  consistent to C's strstr() and Java's indexOf().


### Analysis:

- Assume:
  - s1 = "abcde"          s2 = "cde"
  - <U>abc</U>de
  - a<U>bcd</U>e
  - ab<U>cde</U>


```ruby
      0 1 2 3 4 5 6 7 8                       0 1 2  
s1 = [a b c d e f g h i]                s2 = [c d e]
      i->                                     j->     #every loop init j = 0

assume i = 2,
                 2   0               
'c' :  s1.charAt(i + j) == s2.charAt(0)           # j : [0 .. 2]


                 2   0               
'd' :  s1.charAt(i + j) == s2.charAt(1)


                 2   0
'e' :  s1.charAt(i + j) == s2.charAt(2)
```



- Time = O(n^2)

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack == null || needle == null || haystack.length() < needle.length()){
            return -1;
        }
        if(needle.length() == 0){
            return 0;
        }
        for(int i = 0; i <= haystack.length() - needle.length(); i++){
            int j = 0;
            while(j < needle.length() && haystack.charAt(i + j) == needle.charAt(j)){
                j++;
            }
            if(j == needle.length()){
                return i;
            }
        }
        return -1;
    }
}
```


