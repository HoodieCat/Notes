## Plugin **surround.vim**
- 传统用法：删改surround. ds",cs"
    ```
    ************* 
           "abcd" 
    ds"   -> abcd 
    cs")  -> (abcd)
    ```
    > 需要说明的是cursor处于任何*的位置使用该命令都可以实现跳转并修改
- 等待选择模式：operator pending mode :增加surround, ys(motion){symbo},范围和motion的范围有关
    ``` 
    ***************
           abcd.123
           ysw" -> "abcd".123
           ysW" -> "abcd.123"
           yss" -> "abcd.123"
    ``` 
- 一般地，yss用于本行内容全部包括,yS用于 将文字包括在单独一行中,并且为文本添加一个缩进
    ```
    lua config
    ySw" ->
    "
        lua
    " config

    ySS" ->
    "
        lua config
    "
    ```
- 在visual mode中，S 即可包括所选文本

- Note: ys{motion}f 可以把文本变成function里面的参数，function name 在命令行输入
    ```
    int a, int b
    yssffunctionA<CR> ->
    functionA(int a, int b)
    ys2wffunctionB<CR> ->
    functionB(int a), int b
    ```


