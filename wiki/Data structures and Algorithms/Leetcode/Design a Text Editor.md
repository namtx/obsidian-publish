[Leetcode - Design a Text Editor](https://leetcode.com/problems/design-a-text-editor/)

### Submission

```java
class TextEditor {
    Stack<Character> left;
        Stack<Character> right;

        TextEditor() {
            this.left = new Stack<>();
            this.right = new Stack<>();
        }

        void addText(String text) {
            for (char c: text.toCharArray()) {
                this.left.push(c);
            }
        }

        int deleteText(int k) {
            int count = 0;
            while(!left.isEmpty() && k > 0) {
                left.pop();
                count++;
                k--;
            }

            return count;
        }

        String cursorLeft(int k) {
            while(!left.isEmpty() && k > 0) {
                char c = left.pop();
                right.push(c);
                k--;
            }

            return cursorString();
        }

        String cursorRight(int k) {
            while(!right.isEmpty() && k > 0) {
                char c = right.pop();
                left.push(c);
                k--;
            }

            return cursorString();
        }

        private String cursorString() {
            StringBuilder sb = new StringBuilder();
            int count = 10;
            while(!left.isEmpty() && count > 0) {
                sb.insert(0, left.pop());
                count--;
            }
            String ret = sb.toString();
            for (char c: ret.toCharArray()) {
                left.push(c);
            }
            return ret;
        }
}
```