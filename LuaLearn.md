[:toc]
# LuaLearn (especially for nvim config)
## 注释
- 单行注释 `--`
- 多行注释 
	```lua
	--[[
	**content
	--]]
	```
- 标识符 最好不要使用行如 _ABC 这样的下划线加大写字母的标识符，因为lua保留字也是这样的方式,且lua区分大小写，A a 是不用的变量

## 变量默认全局（即不用local 标识，申明的变量默认为global）

## 数据类型 
- lua为动态数据类型语言，变量不需要定义类型，只需要为变量赋值，值可以储存在变量中，作为参数传递或结果返回
- 八个基本数据类型：
	- nil(无效值 或false`在条件表达式中`), 可以使用nil撤销变量的定义，`var = nil`
	- boolean (true or false)
	- number (双精度的float)
	- string 使用’‘  或 “” 表示 支持 [[ ]]形式去给变量赋值多行文字，这样的句法在init.lua配置中经常出现，如`vim.cmd([[ multiple lines content ]])`, 相当于变相的在lua中 使用vimscript去做配置
	- function lua或者C定义的函数
	- userdata 表示存储在变量中的C数据结构
	- thread 
	- **table** lua中的表其实是一个关联数组，数组的索引可以是数字、字符串或表类型。有点类似json（？）,通过“构造表达式”来创建，最简单的构造表达式是{},这是一个空表 - type() 可以测试给定变量或者值的类型,返回值是一个string  
	> note:type（a）== nil 结果是false,因为nil看作string的话是一个无效值，故应该用 type(a）== “nil"('nil'),return true
- table（表）,关联数组，索引可以是数字或者字符串
	```lua
	-- table_test.lua lua script
	a = {}  
	a["key"]= "value"
	key = 10
	a[key] = 22
	a[key] = a[key] + 10
	for k,v in pairs(a) do 
		print(k..":"..v)
	end	
	```
	脚本执行结果：
	```lua
	key:value
	10:32
	```
## 变量
lua有三种变量类型：全局变量、局部变量、表中的域
> lua中的变量都是全局变量,哪怕是语句块或者函数里的,除非用local显式声明为局部变量

局部变量的生命周期从声明位置开始到所在语句块结束,没有赋值的任何变量默认值为nil
- 索引 对table的索引使用方括号,同时
t[i]
t.i  --当索引是字符串时,可以简化为此种方式
getttable_event(t,i) --采用索引的本质是使用了类似这样的函数调用

## 函数 
在lua中,函数是对语句和表达式进行抽象的主要方法
- 完成指定任务,作为调用语句使用
- 计算值并返回,使用赋值语句的表达式使用

*函数定义*格式如下:
```lua
optianal_function_scope function functionname(arguement1, arguement2, arguement3...)
	function_body
	return result_parameter_seperated --返回值,可以有多个,使用逗号隔开
```
- 可以将函数作为参数传递给函数(类似与cpp中的callback?)
- 多返回值,比如,string.find(),返回匹配串开始和结束的下标
	```lua
	s,e=string.find("www.find.com","find")
	print(s,e)

	--result :5   8 
	```
- 可变参数 ,类C,在参数列表中,使用三点 ... 表示函数有可变的参数 ... 指代了那些参数,可以当作参数使用
	```lua
	function add(...)
	local s = 0 
		for i,v in ipairs{...}do  --{...}表示由可变长参数构成的数组
			s = s + v
		end
		return s
	end
	print(add(3,4,5,6,7))

	-- result 25
	```
	- Note: select('#',...),select(n, ...)使用在确定不定长参数的个数,和选择上
## 三元操作 同c/js a?b:c -> a and b or c

## 函数
支持匿名函数和闭包函数
```lua
    function fib(n)
        if n<2 then return end
        return fib(n-1) + fib(n-2)
    end
```
```lua
function adder(x)
    return function(y) return x+y end
end

a1 = adder(9)
a2 = adder(36)
print(a1(16)) --> 25
print(a2(64)) --> 100
--相当于一个 “函数宏”
```
## table 表
lua table 是一种关联型数组,associative array,用来解决 module package object

## lua Module/Package
**lua的模块是有变量和函数等已知元素组成的table(类似c struct/class?),因此创建一个module很简单,就是创建一个table,然后把需要倒入的常量,函数放入其中,返回这个table
```lua
-- filename module.lua
-- define module name(module)
module = {}
-- define const
module.constant = "这是个常量"

-- 定义一个函数
function module.func()
	io.write("这是一个共有函数")
end

local function func2()
	print("这是一个私有函数")

function module.func3()
	func2()
end
```

### require函数
用来加载模块的函数
```
-- require("<ModuleName>")
require(module)
print(module.constant)
module.func3()
```
可以给加载的模块定义一个变量别名,方便调用:
```
local m = require("module")

print(m.constant)
m.func3()
```
## C包
Lua和C包很容易结合,使用C为Lua写包,与Lua中写包不用,C包在使用前必须加载并链接,可以通过动态链接,Lua提供了一个叫做loadlib的函数提供了所有的动态链接功能.
```lua
local path = "/usr/local/lua/lib/libluasocket.so"
local f = loadlib(path,"luaopen_socket")
-- 第一个参数路径,第二个参数 是初始化函数
local f = assert(package.loadib(path,"function_outside")
f(); -- actually execute
```
## metatable 元表
元表实现了让一个lua对象可以重载一些方法，每一个重载的对象都有一个对应的原表方法与其对应，类似于 其他语言中的运算符重载 [referrence](http://lua-users.org/wiki/MetamethodsTutorial)


