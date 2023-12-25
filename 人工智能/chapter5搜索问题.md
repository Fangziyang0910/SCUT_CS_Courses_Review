# 人工智能导论
## 第五章 搜索问题

- 5.1 回溯策略
- 5.2 图搜索策略
- 5.3 深度优先、宽度优先
- 5.4 启发式图搜索
- 5.5 博弈树搜索


### 5.1 回溯策略
例：皇后问题（不能在同一行、同一列、同一个对角线）

可行解：
![26](image/26.jpg)

回溯搜索算法：

递归过程BACKTRACK(DATA)
- DATA：当前状态。
- 返回值：从当前状态到目标状态的路径
			（以规则表的形式表示）
			或FAIL。

        1, 	IF TERM(DATA) RETURN NIL;//如果TERM(DATA)为真，则返回空值。TERM(DATA)是一个函数，用于测试数据是否达到了终止条件。
        2, 	IF DEADEND(DATA) RETURN FAIL;//如果DEADEND(DATA)为真，则返回失败。DEADEND(DATA)是一个函数，用于测试数据是否到达了无法继续搜索的死胡同。
        3, 	RULES:=APPRULES(DATA);//APPRULES(DATA)是一个函数，用于生成可能的规则列表，这些规则可以用于扩展数据。
        4,	LOOP: IF NULL(RULES) RETURN FAIL;//进入循环，如果规则列表为空，则返回失败。
        5, 	R:=FIRST(RULES);//取出规则列表中的第一个规则R。
        6,	RULES:=TAIL(RULES);//将规则列表更新为不包括第一个规则R的剩余规则。
        7,	RDATA:=GEN(R, DATA);//用规则R来扩展数据，生成新的数据RDATA。
        8,	PATH:=BACKTRACK(RDATA);//递归地调用BACKTRACK函数，传入新的数据RDATA，并将返回值存储在PATH中。
        9,	IF PATH=FAIL GO LOOP;//如果递归调用BACKTRACK返回失败，则回到循环开始。
        10,	RETURN CONS(R, PATH);//返回一个由规则R和路径PATH组成的列表，表示找到了一个解决方案。如果没有找到解决方案，则返回FAIL。

存在问题及解决办法:
问题：
- 深度问题    对搜索深度加以限制
- 死循环问题  记录从初始状态到当前状态的路径

回溯搜索算法1:

    1. DATA:=FIRST(DATALIST)
    取出数据列表DATALIST中的第一个数据，并将其存储在变量DATA中。

    2. IF MEMBER(DATA, TAIL(DATALIST))RETURN FAIL;		
    如果DATA已经出现在DATALIST的其余部分中，则返回失败。这可以防止在搜索过程中出现无限循环。

    3. IF TERM(DATA) RETURN NIL;如果DATA满足终止条件，则返回空值。

    4. IF DEADEND(DATA) RETURN FAIL;如果DATA到达了无法继续搜索的死胡同，则返回失败。

    5. IF LENGTH(DATALIST)>BOUND
    	 	RETURN FAIL;如果DATALIST的长度超过了预设的上限，返回失败。这可以防止搜索过程过于耗时。

    6. RULES:=APPRULES(DATA);用APPRULES(DATA)函数生成可能的规则列表，这些规则可以用于扩展数据。

    7. LOOP: IF NULL(RULES) RETURN FAIL;进入循环，如果规则列表为空，则返回失败。

    8. R:=FIRST(RULES);取出规则列表中的第一个规则R。

    9. RULES:=TAIL(RULES);将规则列表更新为不包括第一个规则R的剩余规则。

    10. RDATA:=GEN(R, DATA);用规则R来扩展数据，生成新的数据RDATA。

    11. RDATALIST:=CONS(RDATA, DATALIST);将新的数据RDATA添加到DATALIST的开头，生成新的数据列表RDATALIST。

    12. PATH:=BACKTRCK1(RDATALIST)递归地调用BACKTRCK1函数，传入新的数据列表RDATALIST，并将返回值存储在PATH中。

    13. IF PATH=FAIL GO LOOP;如果递归调用BACKTRCK1返回失败，则回到循环开始。

    14. RETURN CONS(R, PATH);
    返回一个由规则R和路径PATH组成的列表，表示找到了一个解决方案。如果没有找到解决方案，则返回FAIL。


回溯搜索：只保留从初始状态到当前状态的一条路径。

图搜索：保留所有已经搜索过的路径。

### 5.2 图搜索算法:
        1, G=G0 (G0=s), OPEN:=(s);
        2, CLOSED:=( );
        3, LOOP: IF OPEN=( ) THEN EXIT(FAIL);
        4, n:=FIRST(OPEN), REMOVE(n, OPEN),
            ADD(n, CLOSED);
        5, IF GOAL(n) THEN EXIT(SUCCESS);
        6, EXPAND(n)→{mi}, G:=ADD(mi, G);
        7, 标记和修改指针：
            ADD(mj, OPEN), 并标记mj到n的指针；
            计算是否要修改mk、ml到n的指针；
            计算是否要修改ml后继节点指向父节点的指针；
        8, 对OPEN中的节点按某种原则重新排序；
        9, GO LOOP；

### 5.3 深度、广度
![24](image/24.jpg)
![25](image/25.jpg)

### 5.4 启发式图搜索
A算法
A*算法

### 5.5 博弈树搜索