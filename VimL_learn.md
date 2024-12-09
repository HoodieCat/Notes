# chp01 vimL的特点
1.1 Hello World 的四种写法
- 命令行方式
```vimscript
:echo "hello world!“ 
"single quote  or Double Quotes is  okay
```
> 其实，是映射到了msg里，map中有提到，还有echoerror,用错误的方式 显示出来 1.2 vimscprit
	- 以.vim 作为suffix的文件一般看做vim脚本，用"做注释
	- 每一行其实对应了 在ex mode 下进行输入，但是可以不在行首写冒号`:`
	- finish 表示直接结束脚本（optional），otherwise till the eof
1.3 &vim.options返回 vim.options中的value值


