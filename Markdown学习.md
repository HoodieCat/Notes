[toc]

# Markdown 语法 -*强调*

- 粗体（Bold) 
`****`  **


	wfzi 


# Markdown 标题语法 /*这是一个一级标题*/

# *列表*
- 有序列表  
数字后面紧跟一个英文局点. 数字
	1. first
		1. test3
			- 理解
				1. lv
				2. ge
				3. diangun
			- let
			- it 
			- go
		2. test4
		3. test5
	2. second  
	3. third  
1. test
2. test
3. test3
4. test
	1) test
	2) test

- 无序列表  
```
用-<space>content 的形式来使用，也可以使 * 、 + 看个人习惯
```
- 在列表循环中，使用eol<space><space>换行 如果想跳出列表循环，采取空一行的方式，表示此段列表结束,即列表内容也视为一个段落
- 当在列宾循环中插入符合列表缩进的内容时，内容保持和当前列表同样 的缩进即可比如：
```
1. xxx
    1. xxx
    ```
    funca()
    end 
    ```
    > quote something
```
效果是：
1. xxx
    1. xxx
    ```
    funca()
    end
    ```
    > quote something
