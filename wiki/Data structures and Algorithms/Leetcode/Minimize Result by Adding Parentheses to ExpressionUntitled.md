[Leetcode - Minimize Result by Adding Parentheses to Expression](https://leetcode.com/contest/weekly-contest-288/problems/minimize-result-by-adding-parentheses-to-expression/)

#### Submission

```java
package dev.namtx.leetcode;  
  
/**
 * https://leetcode.com/contest/weekly-contest-288/problems/minimize-result-by-adding-parentheses-to-expression/ */public class MinimizeResultByAddingParenthesesToExpression {  
    public String minimizeResult(String expression) {  
        int min = sum(expression);  
        String ans = "(" + expression + ")";  
        int plusPosition = expression.indexOf("+");  
  
        for (int i = 0; i < plusPosition; i++) {  
            for (int j = plusPosition + 1; j < expression.length(); j++) {  
                int first = 1;  
                if (i > 0) {  
                    first = Integer.parseInt(expression.substring(0, i));  
                }  
                int last = 1;  
                if (j < expression.length() - 1) {  
                    last = Integer.parseInt(expression.substring(j + 1));  
                }  
  
                int value = first*sum(expression.substring(i, j + 1))* last;  
                if (value < min) {  
                    min = value;  
                    ans = expression.substring(0, i) + "(" + expression.substring(i, j + 1) + ")" + expression.substring(j + 1);  
                }  
            }  
        }  
  
        return ans;  
    }  
  
    private int sum(String expression) {  
        String[] parts = expression.split("\\+");  
        return Integer.parseInt(parts[0]) + Integer.parseInt(parts[1]);  
    }  
  
    public static void main(String[] args) {  
        System.out.println(new MinimizeResultByAddingParenthesesToExpression().minimizeResult("1+2"));  
    }  
}
```