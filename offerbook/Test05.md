## 面试题5：替换空格


题目：请实现一个函数，把字符串中的每个空格替换成"%20"，例如“We are happy.”，则输出“We%20are%20happy.”。

```java
public class Test05 {
    public static String replaceSpace(StringBuffer str) {
        //条件判断
        if (str == null || str.length() < 1) {
            return str.toString();
        }
        //原长度
        int oldLength = str.length();

        //遍历空格个数
        int spaceCount = 0;
        for (int i = 0; i < oldLength; i++) {
            if (str.charAt(i) == ' ') {
                spaceCount++;
            }
        }


        if (spaceCount == 0) {
            //没有空格，直接返回str
            return str.toString();
        }

        //确定替换后的字符串长度
        int length = oldLength + spaceCount * 2;


        for (int index = str.length() - 1; index >= 0; index--) {
            if (str.charAt(index) == ' ') {
                str.deleteCharAt(index);
                str.insert(index, "0");
                str.insert(index, '2');
                str.insert(index, '%');
            }
        }
        return str.toString();
    }

    public static void main(String[] args) {
        StringBuffer str = new StringBuffer("We are happy.");
        System.out.println(replaceSpace(str));
    }
}
```

result:
```
We%20are%20happy.                                               
```