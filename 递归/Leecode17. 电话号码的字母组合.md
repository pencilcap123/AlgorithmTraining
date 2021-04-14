# 电话号码的字母组合
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。答案可以按 任意顺序 返回。
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![电话键盘](https://assets.leetcode-cn.com/aliyun-lc-upload/original_images/17_telephone_keypad.png)

示例 1：
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]

示例 2：
输入：digits = ""
输出：[]

示例 3：
输入：digits = "2"
输出：["a","b","c"]

提示：
0 <= digits.length <= 4
digits[i] 是范围 ['2', '9'] 的一个数字。

### 解答:
```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;
import static java.util.stream.Collectors.toList;
class Solution {
    public List<String> letterCombinations(String digits) {
        if(digits.length() ==0){
            return new ArrayList<String>();
        }
        if(digits.length() ==1){
            return getCombinationsByDigit(Integer.parseInt(digits));
        }
        List<String> letterCombinations = new ArrayList<>();

        List<String> combinationsByDigit = getCombinationsByDigit(Integer.parseInt(digits.substring(0,1)));
        List<String> combinationsByLastDigits = letterCombinations(digits.substring(1, digits.length()));
        for (int i = 0; i < combinationsByDigit.size(); i++) {
            if(combinationsByLastDigits.size() ==0){
                letterCombinations = combinationsByDigit;
            }else{
                for (int j = 0; j < combinationsByLastDigits.size(); j++) {
                    letterCombinations.add(combinationsByDigit.get(i)+combinationsByLastDigits.get(j));
                }
            }
        }
        return letterCombinations;
    }

    private List<String> getCombinationsByDigit(int digit){
        switch(digit){
            case 2 :
                return Stream.of("a", "b", "c").collect(toList());
            case 3 :
                return Stream.of("d", "e", "f").collect(toList());
            case 4 :
                return Stream.of("g", "h", "i").collect(toList());
            case 5 :
                return Stream.of("j", "k", "l").collect(toList());
            case 6 :
                return Stream.of("m", "n", "o").collect(toList());
            case 7 :
                return Stream.of("p", "q", "r", "s").collect(toList());
            case 8 :
                return Stream.of("t", "u", "v").collect(toList());
            case 9 :
                return Stream.of("w", "x", "y", "z").collect(toList());
            default :
                return new ArrayList<String>();
        }
    }
}
```
