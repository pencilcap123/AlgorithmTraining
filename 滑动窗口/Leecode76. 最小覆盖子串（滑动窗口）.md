# 最小覆盖子串
给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。
注意：如果 s 中存在这样的子串，我们保证它是唯一的答案。

示例 1：
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"

示例 2：
输入：s = "a", t = "a"
输出："a"

提示：
1 <= s.length, t.length <= 105
s 和 t 由英文字母组成

### 解答:
```java
public class Solution {
    Map<Character, Integer> tMap = new HashMap<Character, Integer>();
    Map<Character, Integer> sMap = new HashMap<Character, Integer>();

    public String minWindow(String s, String t) {
        if(t.length() > s.length()){
            return "";
        }
        String minWindows = "";
        for(int i =0; i <t.length();i++){
            tMap.put(t.charAt(i), tMap.getOrDefault(t.charAt(i),0)+1);
        }
        int right = 0;
        int left = 0;
        while(right<s.length()){
            if(t.contains(s.charAt(right)+"")){
                sMap.put(s.charAt(right), sMap.getOrDefault(s.charAt(right),0)+1);
            }
            //第一次获取覆盖子串
            if(minWindows.length() ==0 && check()){
                minWindows = s.substring(left, right+1);
            }
            while(minWindows.length() !=0 && check()){
                //滑动窗口，比较长度，继续获取覆盖子串
                if(minWindows.length()>=(right+1-left)){
                    minWindows = s.substring(left, right+1);
                }
                if(t.contains(s.charAt(left)+"")){
                    sMap.put(s.charAt(left), sMap.getOrDefault(s.charAt(left),0)-1);
                }
                left++;
            }
            right++;
        }

        return minWindows;
    }

    public boolean check(){
        //判断是否满足条件
        for (Map.Entry<Character, Integer> entry : tMap.entrySet()) {
            if(sMap.getOrDefault(entry.getKey(), 0)<entry.getValue()){
                return false;
            }
        }
        return true;
    }
}
```
