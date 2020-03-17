在JavaScript中，ASI(Automatic semicolon insertion，自动分号插入)允许在行尾省略分号。请注意，ASI不需要实际上“插入分号”，只需在引擎的解析器中终止语句即可。

#### 分号插入常见规则

有关ASI的具体规则，请参见规范[§11.9.1自动分号插入规则](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-rules-of-automatic-semicolon-insertion)。

其中包含以下三种规则：

1. 当遇到语法不允许的标记（`行终止符`或`}`）时，如果出现以下情况，则会在该标记前插入分号：

   + 标志和上一个标志至少被一个行终止符隔开
   + 该标志是`}`

   **e.g.**

   ```js
   { 1
   2 } 3
   ```

   被转化为：

   ```js
   { 1
   ;2 ;} 3;
   ```

2. 当到达标志的输入流的末尾并且解析器无法将输入的标志流解析为单个完整程序，分号会自动插入到输入流的末尾。

   **e.g.**

   ```js
   a = b
   ++c
   ```

   被转化为：

   ```js
   a = b;
   ++c;
   ```

3. 标志在非严格模式下是允许的，在生产环境的严格模式下会在前面插入分号。

   **e.g.**

   ```js
   UpdateExpression :
       LeftHandSideExpression [no LineTerminator here] ++
       LeftHandSideExpression [no LineTerminator here] --
   
   ContinueStatement :
       continue ;
       continue [no LineTerminator here] LabelIdentifier ;
   
   BreakStatement :
       break ;
       break [no LineTerminator here] LabelIdentifier ;
   
   ReturnStatement :
       return ;
       return [no LineTerminator here] Expression ;
   
   ThrowStatement :
       throw [no LineTerminator here] Expression ; 
   
   ArrowFunction :
       ArrowParameters [no LineTerminator here] => ConciseBody
   
   YieldExpression :
       yield [no LineTerminator here] * AssignmentExpression
       yield [no LineTerminator here] AssignmentExpression
   ```

   return语句为例：

   ```js
   return 
     "something";
   ```

   转化为：

   ```js
   return;
     "something";
   ```

   