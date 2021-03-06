# Lua代码风格

# 目录

+ [一、程序的版式](#1)
	+ [1.1 空行](#1.1)
	+ [1.2 空格](#1.2)
	+ [1.3 长行拆分](#1.3)
	+ [1.4 使用缩进](#1.4)
+ [二、命名规则](#2)
	+ [2.1 共性规则](#2.1)
	+ [2.2 文件命名](#2.2)
	+ [2.3 类的命名](#2.3)	
	+ [2.4 变量命名](#2.4)
	+ [2.5 常量，事件名的命名](#2.5)
	+ [2.5 枚举](#2.5)
+ [三、文件组织](#2)
    + [3.1 文件描述](#3.1)
    + [3.2 文件中变量的定义](#3.2)
    + [3.3 类变量的定义](#3.3)
    + [3.4 函数参数的定义](#3.4)
    + [3.5 函数的定义规则](#3.5)
    + [3.6 注释的使用](#3.6)
+ [三、分隔和缩进](#3)
    + [3.1 使用空行](#3.1)
    + [3.2 使用空格符](#3.2)
    + [3.3 使用换行符](#3.3)
    + [3.4 使用小括号](#3.4)
    + [3.5 使用缩进](#3.5)
* [四、编程技巧](#4)
    * [4.1 应该尽量使用local变量而非global变量](#4.1)
    * [4.2 临时变量的处理](#4.2)
    * [4.3 利用逻辑运算的短路效应](#4.3)
+ [五、代码建议](#5)
    + [5.1 代码的调试](#5.1)
    + [5.2 复杂度和性能问题](#5.2)
    + [5.3 函数的优化思考](#5.3)
    + [5.4 提交代码的检查](#5.4)
    + [5.5 表结构的引用](#5.5)


<span id="1"></span>
## 一、程序的版式

> Code is read much more often than it is written.
> 
> Programming style is an art.

<span id="1.1"></span>
### 1.1 空行

* 需加空行：
	* 函数之间都要加空行；
	* 函数内部代码概念与逻辑之间，逻辑段落小节之间，都应该加空行；
	* 注释行之前。
* 不加空行：
	* 在一个函数体内，逻揖上密切相关的语句之间不加空行；
	* 多行注释解释参数的时候，注释之间不加空行。

<span id="1.2"></span>
### 1.2 空格

* 需加空格：
    * "`and`"，"`or`"等关键字前后留`一个`空格，便于辨析；
    * 逗号"`,`"后面要留`一个`空格；
    * 赋值操作符、比较操作符、算术操作符如"`=`"、 "`==`"、"`~=`"、"`>=`"、"`<=`"、"`>`"、"`<`"、"`+`"、"`-`"、"`*`"、"`/`"、"`%`"、"`^`",等二元操作符的`前后`应当加空格；
    * `if`、`for`、`while`等关键字之后如果要加左括号"`(`"，关键字与左括号之间应留一个空格，以突出关键字；  
 
* 不加空格：
    * 函数名之后不要留空格，紧跟左括号"`(`"；
    * 左括号"`(`" 向`后`紧跟，紧跟处不留空格；
	* 右括号"`)`"、逗号"`,`"、分号"`;`"，向`前`紧跟，紧跟处不留空格；
	* 字符串连接符"`..`"前后不加空格；
	* "`:`"，"`.`"，"`[`"，"`]`"这类操作符前后不加空格；
	
    
          
            a > b and a or b           -- 良好的风格
            a > b  and a or  b         -- 不良的风格
            
            local a, b, c, max         -- 良好的风格
            local a,b,c,max            -- 不良的风格
            
            if a > b then              -- 良好的风格
                max = a 
            end 
            if a>b then max=a end      -- 不良的风格
            
            data = dataTable[index]    -- 良好的风格
            data = dataTable [ index ] -- 不良的风格
        
            function(posX, posY)       -- 良好的风格
            function (posX,posY)       -- 不良的风格


<span id="1.3"></span>
### 1.3 长行拆分

* 代码行最大长度宜控制在70至80个字符以内。代码行不要过长，否则眼睛看不过来，也不便于打印；
* 长表达式要在低优先级操作符处拆分成新行，操作符放在新行之首（以便突出操作符）。
       
         -- 良好的风格
         local newBuindingBtn = UI.newButton({             
             text = btnName,
             x = self.x,
             y = self.y,
             parent = self, 
             style = {
                 normal = ResConfig.png.commonBtnBlue
             }
         })
         
         -- 不良的风格
         local newBuindingBtn = UI.newButton({text = btnName,x = self.x,y = self.y,parent = self, style = {normal = ResConfig.png.commonBtnBlue}})
         
         
         -- 良好的风格
         if veryLongerVariable1 >= veryLongerVariable2		     and veryLongerVariable3 <= veryLongerVariable5			 and veryLongerVariable4 <= veryLongerVariable6 then			 doo()
         end
         
         -- 不良的风格
         if veryLongerVariable1 >= veryLongerVariable2 and veryLongerVariable3 <= veryLongerVariable5 and veryLongerVariable4 <= veryLongerVariable6 then
			 doo()
         end
         
         
<span id="1.4"></span>
### 1.4 使用缩进

* 类中的成分
* 方法体或语句块中的成分
* 换行时的非起始行 
               
---
---

<span id="2"></span>
## 二、命名规则     

>三思而命名。


<span id="2.1"></span>
### 2.1 共性规则

* 命名应当直观且可拼读，可望文知意；
* 标识符的长度应当符合“min-length && max-information”原则；
* 采用英文单词或单词组合，英文单词不要复杂，但用词需准确，`切忌使用汉语拼音命名`；
* 切勿为了避免命名过长而随意截取单词，以丢失可读性；
* 所有命名都不要与－x已有的命名风格冲突，例如不要以CC，UI开头；

<span id="2.2"></span>
### 2.2 文件命名

* 所有Lua文件的命名时使用大驼峰法；
* 根据文件的特性，一般以文件里的模块名或者类名作为同名文件名；
* 确定命名前，请检查下，不要跟其他文件同名；
       
        CCArmature.lua    -- 不良的风格
        UILayout.lua      -- 不良的风格


<span id="2.3"></span>
### 2.3 类的命名

* 所有类命名时使用大驼峰法；
* 类名一般由"名词"或"多名词"组成，不要简写；
* 根据类的特性，加上相关的后缀或者前缀；
        
        后缀：  
        管理类  Manager
        缓存类  Cache
        控制类  Controller
        模块    Module
        网络类  Proxy


<span id="2.4"></span>
### 2.4 变量命名

* 通用规则

	* 使用 “名词” 或是 “形容词+名词” 命名；
	* 使用小驼峰法命名；
	* 为了可读性，尽量避免变量名中出现标号，如value1， value2；
	* 不要出现仅靠部分字母大小写区分的相似的变量；
	* 除非是局部变量功能等价全局变量，不然局部变量不要与已有的全局变量同名；
	* 尽量不要使用已有的类名作为变量名；
	    
	        local data          -- 良好的风格  
	        local oldData       -- 良好的风格 
	        local newData       -- 良好的风格     
	        local pairs = pairs -- 良好的风格
	            
	        local posx,posX     -- 不良的风格 
	        local btn1,btn2     -- 不良的风格
	        local TABLE = {}    -- 不良的风格
	        local uILabel       -- 不良的风格
	       
* 类的成员变量
    * 类的成员变量以"self."开头，以区分于局部变量；
        
            例如:
                function init()
                    
                    self.mainPanel = false -- 常用格式
                    
                    topPanel = false       -- 这样是全局变量，占用全局资源，而且难以区分于局部变量 
                    ...
                end
            
* 全局变量
    * 全局变量使用双下划线("`__`")开头以及结尾，中间的命名以名词拼接，或"形容词＋名词"拼接，不同单词之间用（"`_`"）隔开；
            
            例如：
                __VERSION_CODE__ = "1.0.0.0"            

* 局部变量
    * M常用做模块里面表示模块本身
            
            module("MainGame.Module.IntegrationTest.MapModule",package.seeall)
            
            local M = class(SceneView,"MapScene")

            --数据的初始化
            function M:init()
                ...
            end
            
            ...
            return M
     * 引用进来的类或模块，用大驼峰法命名，引用路径统一带括号；
            
            module("MainGame.Module.IntegrationTest.MapModule",package.seeall)

            local M = class(SceneView,"MapScene")
            local Surface = require("xx.xx")
            local TestButtonPanel = require("xx")
            ...
* 临时变量
   * 常用下划线"_"作为可以忽略的变量
           
            for _,v in ipairs(t) do print(v) end
    * i,k,v,t常做临时变量
    
            for k,v in pairs(t) ... end
            for i,v in ipairs(t) ... end
            mt.__newindex = function(t, k, v) ... end
            

<span id="2.5"></span>
### 2.5 常量，事件名的命名

* 常量，事件名所用单词均大写，单词用下划线('`_`')分割；
    
        例如：
            -- 常量 默认宽度
            LIST_DEFAULT_WIDTH = 100
            
            -- 事件 添加到场景
            ADDED_TO_STAGE = getId() 


<span id="2.6"></span>
### 2.6 枚举的命名

* 枚举名命名，与类名命名一致；
* 枚举值命名，与常量，事件名的命名一致；
         
        例如：
            ControllerViewType = {
	            SCENE = "SCENE",
	            PANEL = "PANEL",
	            POP = 	"POP",
            }

---
---

##三、文件组织
<span id="3.1"></span>
### 3.1 文件描述

* 文件开头加上此文件的简要功能作用描述；

        -- MapModule.lua
        --Author:xx
        --Email:xx@flamingo-inc.com
        --20xx年x月x日 xx:xx
        --Using:创建地图       
        module("MainGame.Module.IntegrationTest.MapModule",package.seeall)
        ...
        
<span id="3.2"></span>
### 3.2 文件中变量的定义
* 如果在文件中需要多次使用的某些导入文件，可以在文件开头用局部变量存储导入信息，而不是在每次使用的时候都重新导入一次；          例如:            ...
            local Surface = require("xx.xx")
            local TestButtonPanel = require("xx")
            
            function M:xx()
                local testBtn = TestButtonPanel.newCC()
                ...
            end
            
            function M:yy()
                local panel = TestButtonPanel.newCC()
                local surface = Surface.newCC()
                ...
            end

            ...
            
 <span id="3.3"></span>
### 3.3 类变量的定义
* 类中的成员变量需要在init中先声明，并赋予初始值，`不允许不声明直接使用`；
           
<span id="3.4"></span>
### 3.4 函数参数的定义

* 所有函数的参数都用统一的params做参数，并加入如下格式的注释：
 
        --[[
            普通按钮 可缩放 scale9
            @param #string text 按钮名称
            @param #table style 按钮样式
        ]]
        function UI.newButtonScale9(params)
           ...
        end


<span id="3.5"></span>
### 3.5 函数的定义规则
* 函数的行数过长(大于 100 行)时,尽量拆分为多个子函数;
* 函数中一些晦涩的部分,一定要加上注释；


<span id="2.6"></span>
### 3.6 注释的使用
* 短小的注释用--；
* 长注释用--[[]]；

---
---

<span id = "4"></span>
## 四、编码技巧

<span id = "4.1"></span>
### 4.1 应该尽量使用`local`变量而非`global`变量

* 全局变量实际是放入全局表中，每次调用是用传入变量名作为key去获取，而local变量是直接通过lua的堆栈访问的；
* 推荐写法
    * 在能用局部变量解决的地方，不要使用全局变量，这点很容易被忽略；    
    * 多次重复使用的全局接口，可以用局部变量保存下再使用，这样做有两个好处：
        * 避免某些类型的全局变量被修改
        * 提高访问速度
        
        
                * 比如需要多重遍历操作一个大表：
                写法1:
                for k1,v1 in pairs(tbl) do
                    for k2,v2 in pairs(v1) do
                        ...	
                    end
                end
            
                写法2:
                do
                    local pairs = pairs
                    for k1,v1 in pairs(tbl) do
                        for k2,v2 in pairs(v1) do
                            ...	
                        end
                    end
                end
            
                -- 由于pairs是一个全局变量应用的函数，所以写法2在这里有稍微效率上的提升，但要是单层遍历的没有这个效果了。
            
                * 当作常量来多次使用的全局变量可以存为局部变量使用
                local playerName = Cache.playerCache.username 
                ...
                local function itemTemplate(data)            
                    nameLabel:setText(playerName)
                end
            
                local list = NewList.newCC(,{
                    itemTemplate = itemTemplate,
                    ... 
                })
            

<span id = "4.2"></span>            
###4.2 临时变量的处理
* 字符串的连接 .. <br>
  由于字符串的管理机制，字符串在使用..连接时，会产生新的对象。由于lua在VM内对相同的string永远只保留一份唯一copy。
           
        例如:
        local description ＝ ""
        for i = 1,20 do
            description = description.."xxx"
        end
        -- 这样会生成21份string的copy，但实际上我们只需要最后那一份 
        
   如果是轻量级的简单连接还是可以使用的，因为影响不大，但要是大量的类似拼接，推荐使用`string.format`
   
* 类似于字符串的管理机制，表也存在类似的临时变量copy：
   
        函数传参数
        function func({x,y})
            ...
        end
  这种传参方式，每次都会生成一份copy，所以推荐以下的用法：
        
        function func(x,y)
            ...
        end
        
        function func({posX = x, posY = y})
            ...
        end

<span id = "4.3"></span>        
###4.3 利用逻辑运算的短路效应
* and or 的返回值是表达式中的左值或者右值，可用来简化代码
  
        function foo(arg)
            arg = arg or "default"
            ...
        end
        
        -- 但要注意当赋值为bool值时候，容易出bug
        a = a or true  -- 错误的写法，当 a 明确写为 false 的时候，也会被改变成 true 。
        a = a ~= false -- 正确的写法，当 a 为 nil 的时候，被赋值为 true ；而 false 则不变。
* 另外，巧妙使用 and or 还可以实现类似 C 语言中的 ?: 三元操作：

        function max(a,b)
            return a > b and a or b
        end
        
        -- 这里相当于 return (a > b) ? a : b;      

---
---   

## 五、代码建议


<span id="5.1"></span>
### 5.1 代码的调试
* 用Luastudio工具调试，代替Sublime调试Lua代码；


<span id="5.2"></span>
### 5.2 复杂度和性能问题
* 写代码时尽可能写的简单,考虑性能时先做好推断,看看能提升多少,增加的复杂度以及造成的代码晦涩有多严重,然后再决定如何做；


<span id="5.3"></span>
### 5.3 函数的优化思考
* 开销大的函数，调用次数低的话，可以不做优化；
* 开销较小的函数，但调用频率很高，则从如何降低调用频率以及减少函数的开销两个角度去思考优化；


<span id="5.4"></span>
### 5.4 提交代码的检查
* 提交代码前，在svn commit中验证提交的代码，去掉或注释掉无关的代码，保证提交的代码无误；


<span id="5.5"></span>
### 5.5 表结构的引用
* 尽量减少表中的成员是另个表的引用；

---

参考资料：

[1] [lua代码编写规范](https://ldb.googlecode.com/files/lua代码编写规范.pdf)

[2] [Lua Style Guide](http://lua-users.org/wiki/LuaStyleGuide)

[3] [Lua 编程技巧](http://blog.codingnow.com/cloud/LuaTips)

[4] [Lua 5.1 参考手册](http://www.codingnow.com/2000/download/lua_manual.html)


