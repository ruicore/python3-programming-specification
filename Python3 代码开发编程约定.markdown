Python3代 码 开 发 编 程 约 定 ![](cgft11wn.001.png)

🎉什 么 样 的 代 码 是 好 代 码 ？ 如 何 评 审 别 ⼈ 的 代 码 ？

- 般 来 说 ， 可 以 从 如 下 3个 ⽅ ⾯ 评 判 ⼀ 份 代 码 是 否 是 好 代 码 。 
1. 可 读 性

代 码 的 ⽣ 命 周 期 中 ， ⼤ 部 分 时 间 都 是 被 ⼈ 阅 读 的 ， 好 的 代 码 需 要 做 到 可 以 让别⼈快速⽆障碍地看懂你 的 代 码 ， 不 需 要 太 多 的 解 释 和 注 释 ， 做 到 代 码 即 ⽂ 档 。

所 以 在 写 代 码 的 时 候 ， 不 仅 要 考 虑 写 的 感 受 ， 更 要 多 考 虑 读 代 码 ⼈ 的 感 受 。 可 阅 读 性 可 以 提 ⾼ 代 码 的 可 维 护 性 。

2. 可 扩 展 性

为 了 满 ⾜ 不 同 的 需 求 ， 代 码 可 以 被 更 新 或 修 改 ， 并 且 同 时 不 会 破 坏 原 有 的 功能。可扩展性可以帮助我 们 在 不 断 变 化 的 需 求 中 保 持 代 码 的 可 ⽤ 性 。

3. 健 壮 性

代 码 可 以 在 不 同 的 情 况 下 正 常 ⼯ 作 ， 并 且 可 以 处 理 异 常 情 况 （ 允 许 抛 出 异 常，但不允许不明不⽩的崩 溃 ） 。 健 壮 性 好 的 代 码 可 以 帮 助 防 ⽌ 程 序 崩 溃 和 数 据 丢 失 。

编 程 规 范 正 是 从 以 上 这 些 ⽅ ⾯ ， 来 促 进 我 们 写 出 更 ⾼ 质 量 的 代 码 。

依 据 约 束 性 的 强 弱 ， 此 约 定 将 约 束 依 次 分 为 【 强 制 】 、 【 推 荐 】 、 【 参 考 】 三 类 。 在 每 条 约 定 的 解 释 中 ， 说 明 对 该 条 约 定 做 了 适 当 的 扩 展 和 解 释 ， 正 例 给 出 了 提 倡 使 ⽤ 的 ⽅ 式 ， 反 例 给 出 了 需 要 避 免 使 ⽤ 的 错 误 ⽅ 式 。

对 于 能 够 使 ⽤ 如 Pylint等 ⼯ 具 进 ⾏ ⾃ 动 格 式 化 的 （ 如 赋 值 符 号 = 前 后 空 格 ， 本 约 定 不 再 提 及 ） 。 

✏ ThereareonlytwohardthingsinComputerScience:cacheinvalidationandnaming things.

在 计 算 机 科 学 领 域 只 有 两 件 难 事 ： 「 缓 存 失 效 」 和 「 给 东 西 起 名 字 」 。 ![](cgft11wn.002.png)

--PhilKarlton

- 、 编 码 约 定
1. 【 强 制 】 代 码 的 可 读 性 ⾮ 常 重 要 。 代 码 的 ⽣ 命 周 期 中 ， 绝 ⼤ 部 份 时 间 处 于 被 ⼈ 阅 读 的状态。因此， 当 有 多 个 考 量 相 互 冲 突 时 ， 请 优 先 保 证 可 读 性 。
1. 【 强 制 】 每 ⾏ 最 多 不 超 过 120个 字 符 。 
- 说 明 ： 过 ⻓ 的 ⾏ 会 导 致 阅 读 障 碍 ， 使 得 缩 进 失 效 。
- 确 定 单 ⾏ 字 符 个 数 时 ， 应 该 考 虑 横 屏 ， 竖 屏 ， git对 ⽐ diff等 使 ⽤ 场 景 。 
3. 【 强 制 】 模 块 中 ⼀ 级 函 数 和 类 定 义 之 间 空 2⾏ ， 类 中 函 数 定 义 之 间 空 1⾏ ， 模 块 尾 部有且仅有 1个 空 ⾏ 。
3. 【 强 制 】 在 判 断 条 件 中 应 使 ⽤ isnot， ⽽ 不 使 ⽤ not...is。 
- 正 例 :iffooisnotNone:
- 反 例 :ifnotfooisNone:
5. 【 强 制 】 函 数 参 数 中 ， 禁 ⽌ 使 ⽤ 可 变 类 型 变 量 （ mutable） 作 为 默 认 值 。 
- 正 例

1 def f(x=0, y=None, z=None): 2    if y is None:

3        y = []

4    if z is None:

5        z = {}

- 反 例

1 def f(x=0, y=[], z={}): 2    pass

3

4 def f(a, b=time.time()): 5    pass

6. 【 强 制 】 禁 ⽌ 定 义 了 变 量 却 不 使 ⽤ 。
6. 【 强 制 】 禁 ⽌ 单 个 函 数 超 过 35⾏ 。 
- 说 明 ： ⼈ 脑 的 阅 读 记 忆 能 ⼒ 有 限 。 研 究 表 明 ， ⼈ 的 短 期 记 忆 只 能 同 时 记 住 不 超 过 10名字。因 此 ， 当 某 个 函 数 过 ⻓ （ ⼀ 般 来 说 ， 超 过 ⼀ 屏 的 函 数 被 认 为 过 ⻓ ） ， 应 该 及 时把它拆分为多个⼩ 函 数 。![](cgft11wn.003.png)
8. 【 强 制 】 禁 ⽌ 超 过 2个 for语 句 或 过 滤 器 表 达 式 ， 否 则 使 ⽤ 传 统 for循 环 语 句 替 代 。 
- 说 明 ： 当 两 个 for语 句 的 列 表 解 析 式 ⽐ 较 复 杂 时 候 ， 也 应 该 使 ⽤ 传 统 for循 环 语 句 替代。 
- 正 例

1 number\_list = [1, 2, 3, 10, 20, 55]

2 odd = [i for i in number\_list if i % 2 == 1] 3

4 result = []

5 for x in range(10):

6    for y in range(5):

7        if x \* y > 10:

8            result.append((x, y))

- 反 例

1 result = [(x, y) for x in range(10) for y in range(5) if x \* y > 10]  

9. 【 强 制 】 列 表 推 导 式 适 ⽤ 于 简 单 场 景 。 如 果 语 句 过 ⻓ ， 则 不 应 该 使 ⽤ 列 表 解 析 式 。 
- 正 例

1 fizzbuzz = []

2 for n in range(100):

3    if n % 3 == 0 and n % 5 == 0:

4        fizzbuzz.append(f'fizzbuzz {n}') 5    elif n % 3 == 0:

6        fizzbuzz.append(f'fizz {n}')

7    elif n % 5 == 0:

8        fizzbuzz.append(f'buzz {n}')

9    else:

10        fizzbuzz.append(n)

- 反 例

1 #  条 件 过 于 复 杂 ， 应 该 采 ⽤ f or 语 句 展 开 

2 fizzbuzz = [![](cgft11wn.004.png)

3    f'fizzbuzz {n}' if n % 3 == 0 and n % 5 == 0 4    else f'fizz {n}' if n % 3 == 0

5    else f'buzz {n}' if n % 5 == 0

6    else n

7    for n in range(100)

8 ]

a. 【 强 制 】 尽 量 避 免 使 ⽤ f r om  x  i mopr t  \* 。 

10. 【 推 荐 】 变 量 名 要 有 描 述 性 ， 不 能 太 宽 泛 ， 好 的 变 量 名 可 以 极 ⼤ 提 ⾼ 代 码 的 整 体 可 读性。 
- 说 明 ： 在 可 接 受 的 ⻓ 度 范 围 内 ， 变 量 名 能 把 它 所 指 向 的 内 容 描 述 的 越 精 确 越 好 。 因 此 ， 尽 量 不 要 ⽤ 过 于 宽 泛 的 词 来 作 为 变 量 名 。
- 反 例 ： day,host,cards,temp
- 正 例 ： day\_of\_week,hosts\_to\_reboot,expired\_cards
11. 【 推 荐 】 变 量 名 最 好 让 ⼈ 能 猜 出 类 型 。 
- 说 明 ： 即 使 在 PEP484出 现 之 后 ， 合 适 的 命 名 也 能 够 更 有 效 的 帮 助 阅 读 者 的 知 道 变 量 的 类 型 。
- 布 尔 类 型 变 量 的 最 ⼤ 特 点 是 ： 它 只 存 在 两 个 可 能 的 值 「 是 」 或 「 不 是 」 ， 因此推荐使⽤ is、 has等 ⾮ ⿊ 即 ⽩ 的 词 修 饰 的 变 量 名 。 
- 正 例 ： is\_superuser， has\_error， allow\_vip， use\_msgpack， debu g【 约 定 俗成】 
- 阅 读 者 看 到 和 数 字 相 关 的 名 词 时 ， 都 会 默 认 想 到 它 们 是 int、 float类 型 。 
- 正 例 ： 释 义 为 数 字 的 所 有 单 词 ： port（ 端 ⼝ 号 ） 、 age（ 年 龄 ） 、 radius（ 半 径 ） 
- 正 例 ： 使 ⽤ length、 count开 头 或 者 结 尾 的 单 词 ： length\_of\_username、 max\_length。不 要 使 ⽤ 普 通 的 复 数 来 表 ⽰ ⼀ 个 int类 型 变 量 ， ⽐ 如 apples、 trips， 最 好 ⽤  number\_of\_apples、 trips\_count来 替 代 。 
12. 【 推 荐 】 变 量 名 不 能 过 ⻓ ， 也 不 能 过 短 ， 在 1〜 5个 单 词 之 内 较 为 合 适 。 
- 说 明 ： 绝 ⼤ 多 数 情 况 下 ， 都 应 该 避 免 使 ⽤ 只 有 ⼀ 两 个 字 ⺟ 的 短 名 字 。 如 数 组 索 引 三 剑 客 i、 j、 k， ⽤ 有 明 确 含 义 的 名 字 ， ⽐ 如 person\_index来 代 替 它 们 总 是 会 更 好 ⼀ 些。 
13. 【 推 荐 】 不 要 使 ⽤ 带 否 定 含 义 的 变 量 名 。 
- 正 例 ： is\_special
- 反 例 ： is\_not\_normal
14. 【 推 荐 】 变 量 使 ⽤ 应 该 保 持 ⼀ 致 性 。 
- 说 明 ： 如 果 你 在 ⼀ 个 ⽅ 法 内 ⾥ ⾯ 把 图 ⽚ 变 量 叫 做 photo， 在 其 他 的 地 ⽅ 就 不 要 把 它 改成  image， 这 样 只 会 让 代 码 的 阅 读 者 困 惑 ： image和 photo到 底 是 不 是 同 ⼀个东西？
15. 【 推 荐 】 变 量 定 义 尽 量 靠 近 使 ⽤ 。 ![](cgft11wn.005.png)
- 说 明 ： 很 多 ⼈ 在 刚 开 始 学 习 编 程 时 ， 会 有 ⼀ 个 习 惯 。 就 是 把 所 有 的 变 量 定 义 写 在 ⼀起，放在函 数 或 ⽅ 法 的 最 前 ⾯ 。 这 样 做 只 会 让 你 的 代 码 「 看 上 去 很 整 洁 」 ， 但 是 对 提 ⾼代码可读性没有任 何 帮 助 。
- 更 好 的 做 法 是 ， 让 变 量 定 义 尽 量 靠 近 使 ⽤ 。 那 样 当 你 阅 读 代 码 时 ， 可 以 更 好 的 理 解 代 码 的 逻 辑 ， ⽽ 不 是 费 劲 的 去 想 这 个 变 量 到 底 是 什 么 、 哪 ⾥ 定 义 的 。
16. 合 理 定 义 临 时 变 量 ， 提 升 可 读 性 。 
- 说 明 ： 代 码 ⾥ 的 复 杂 表 达 式 可 以 通 过 增 加 临 时 变 量 的 ⽅ 式 明 确 含 义 。
- 反 例 ：

1 #  为 所 有 性 别 为 ⼥ 性 ， 或 者 级 别 ⼤ 于  3  的 活 跃 ⽤ ⼾ 发 放  10000  个 ⾦ 币 2 if user.is\_active and (user.sex == 'female' or user.level > 3): 3    user.add\_coins(10000)

4    return

- 正 例 ：

1 #  为 所 有 性 别 为 ⼥ 性 ， 或 者 级 别 ⼤ 于  3  的 活 跃 ⽤ ⼾ 发 放  10000  个 ⾦ 币 2 user\_is\_eligible = user.is\_active and (user.sex == 'female' or user.level > 3 3

4 if user\_is\_eligible:

5    user.add\_coins(10000)

6    return

- 反 例 ：

1 def get\_best\_trip\_by\_user\_id(user\_id):

2     #  ⼼ 理 活 动 ： 「 嗯 ， 这 个 值 未 来 说 不 定 会 修 改 / ⼆ 次 使 ⽤ 」 ， 让 我 们 先 把 它 定 义 成 变 量 吧 ！ 3    user = get\_user(user\_id)

4    trip = get\_best\_trip(user\_id)

5    result = {

6        'user': user,

7        'trip': trip

8    }

9    return result

正 例 ：

其 实 ， 你 所 想 的 「 未 来 」 永 远 不 会 来 ， 这 段 代 码 ⾥ 的 三 个 临 时 变 量 完 全 可 以去掉，变成这样：![](cgft11wn.005.png)

1 def get\_best\_trip\_by\_user\_id(user\_id): 2    return {

3        'user': get\_user(user\_id),

4        'trip': get\_best\_trip(user\_id) 5    }

17. 【 推 荐 】 如 ⾮ 必 要 ， 不 要 ⽤ gl obal s ( ) 、 l ocal s ( ) 。 
- 说 明 ： 也 许 你 第 ⼀ 次 发 现 gl obal s ( ) 、 l ocal s ( ) 这 对 内 建 函 数 时 很 兴 奋 ， 迫 不 及 待 的 写 下 下 ⾯ 这 种 极 端 「 简 洁 」 的 代 码 ：
- 反 例 ：

1 def render\_trip\_page(request, user\_id, trip\_id): 2    user = User.objects.get(id=user\_id)

3    trip = get\_object\_or\_404(Trip, pk=trip\_id)

4    is\_suggested = judg\_is\_suggested(user, trip) 5     #  利 ⽤  l ocal s( )  节 约 了 三 ⾏ 代 码 ， 我 是 个 天 才 ！ 6    return render(request, 'trip.html', locals())

- 千 万 不 要 这 么 做 ， 这 样 只 会 让 读 到 这 段 代 码 的 ⼈ 「 包 括 三 个 ⽉ 后 的 你 ⾃ ⼰ 」痛恨你。
- 因 为 他 需 要 记 住 这 个 函 数 内 定 义 的 所 有 变 量 ， 更 别 提 l ocal s ( ) 还 会 把 ⼀ 些 不 必 要 的 变 量 传 递 出 去 。
- TheZenofPython（ Python之 禅 ） 说 的 清 清 楚 楚 ： Explicitisbetterthanimplicit.（ 显 式 优 于 隐 式 ） 。 因 此 ， 推 荐 下 ⾯ 的 ⽅ 式 ：
- 正 例 ：

1 return render(request, 'trip.html', { 2        'user': user,

3        'trip': trip,

4        'is\_suggested': is\_suggested 5    })

18. 【 推 荐 】 避 免 多 层 分 ⽀ 嵌 套 。 
- 说 明 ： 要 竭 尽 所 能 的 避 免 分 ⽀ 嵌 套 ， 提 前 结 束 可 以 优 化 很 多 情 况 下 的 分 ⽀ 嵌 套 问 题 。
- 反 例

![](cgft11wn.006.png)

1 def buy\_fruit(nerd, store): ![](cgft11wn.007.png)2     """去⽔果店买苹果

3

4     -  先得看看店是不是在营业

5     -  如果有苹果的话，就买  1  个

6     -  如果钱不够，就回家取钱再来

7    """

8    if store.is\_open():

9        if store.has\_stocks("apple"):

10            if nerd.can\_afford(store.price("apple", amount=1)): 11                nerd.buy(store, "apple", amount=1)

12                return

13            else:

14                nerd.go\_home\_and\_get\_money()

15                return buy\_fruit(nerd, store)

16        else:

17            raise MadAtNoFruit("no apple in store!")

18    else:

19        raise MadAtNoFruit("store is closed!")

- 正 例

1 def buy\_fruit(nerd, store):

2    if not store.is\_open():

3        raise MadAtNoFruit("store is closed!")

4

5    if not store.has\_stocks("apple"):

6        raise MadAtNoFruit("no apple in store!")

7

8    if nerd.can\_afford(store.price("apple", amount=1)): 9        nerd.buy(store, "apple", amount=1)

10        return

11    else:

12        nerd.go\_home\_and\_get\_money()

13        return buy\_fruit(nerd, store)

19. 【 推 荐 】 封 装 过 于 复 杂 的 逻 辑 判 断 。 
- 说 明 ： 如 果 条 件 分 ⽀ ⾥ 的 表 达 式 过 于 复 杂 ， 出 现 了 太 多 not 、 and 、 or ， 那 么 此 代 码 的 可 读 性 就 会 ⼤ ⼤ 降 低 。
- 反 例

1 #  如 果 活 动 还 在 开 放 ， 并 且 活 动 剩 余 名 额 ⼤ 于  10， 为 所 有 性 别 为 ⼥ 性 ， 或 者 级 别 ⼤ 于  3 

2 #  的 活 跃 ⽤ ⼾ 发 放  10000  个 ⾦ 币 ![](cgft11wn.008.png)

3 if activity.is\_active and activity.remaining > 10 and \

4        user.is\_active and (user.sex == 'female' or user.level > 3): 5    user.add\_coins(10000)

6    return

- 正 例 ： 可 以 通 过 将 具 体 的 分 ⽀ 逻 辑 封 装 成 函 数 或 者 ⽅ 法 ， 来 达 到 简 化 代 码 的 ⽬ 的 。

1 if activity.allow\_new\_user() and user.match\_activity\_condition(): 2    user.add\_coins(10000)

3    return

20. 【 推 荐 】 总 是 注 意 不 同 分 ⽀ 下 的 重 复 代 码 
- 说 明 ： 重 复 代 码 是 代 码 质 量 的 天 敌 ， ⽽ 条 件 分 ⽀ 语 句 ⼜ ⾮ 常 容 易 成 为 重 复 代 码 的 重灾区。因 此 ， 当 我 们 编 写 条 件 分 ⽀ 语 句 时 ， 需 要 特 别 留 意 ， 不 要 ⽣ 产 不 必 要 的 重 复 代 码 。
- 反 例

1 #  对 于 新 ⽤ ⼾ ， 创 建 新 的 ⽤ ⼾ 资 料 ， 否 则 更 新 旧 资 料 2 if user.no\_profile\_exists:

3    create\_user\_profile(

4        username=user.username,

5        email=user.email,

6        age=user.age,

7        address=user.address,

8         #  对 于 新 建 ⽤ ⼾ ， 将 ⽤ ⼾ 的 积 分 置 为  0 

9        points=0,

10        created=now(),

11    )

12 else:

13    update\_user\_profile(

14        username=user.username,

15        email=user.email,

16        age=user.age,

17        address=user.address,

18        updated=now(),

19    )

- 正 例 ：

1 if user.no\_profile\_exists:

2    profile\_func = create\_user\_profile![](cgft11wn.004.png)

3    extra\_args = {'points': 0, 'created': now()} 4 else:

5    profile\_func = update\_user\_profile

6    extra\_args = {'updated': now()}

7

8 profile\_func(

9    username=user.username,

10    email=user.email,

11    age=user.age,

12    address=user.address,

13    \*\*extra\_args

14 )

21. 【 推 荐 】 多 个 条 件 判 断 ： or 条 件 表 达 式 应 该 将 值 为 真 可 能 性 较 ⾼ 的 写 在 前 ⾯ ， and 则 应 该 写 在 后 ⾯ 。 

1 abbreviations = ["cf.", "e.g.", "ex.", "etc.", "flg."] 2

3 for w in ("Mr.", "Hat", "is", "chasing", "."):

4     i f  w  i n  abbr evi at i ons  and  w[ - 1] ==' . ' :  #  这 句 性 能 较 差 5     #  i f  w[ - 1]  ==  ' . '  and  w  i n  abbr evi at i ons:  #  性 能 好 6        pass

22. 【 推 荐 】 使 ⽤ 德 摩 根 定 律 ： not  A  or  not  B 等 价 于 not  ( A  and  B) ， 推 荐 使 ⽤ 前 者 。 
- 说 明 ： ⼈ 类 思 维 不 擅 ⻓ 处 理 过 多 的 【 否 定 】 以 及 【 或 】 这 种 逻 辑 关 系 。
- 正 例

1 #  如 果 ⽤ ⼾ 没 有 登 录 或 者 ⽤ ⼾ 没 有 使 ⽤  chr ome， 拒 绝 提 供 服 务 2 if not user.has\_logged\_in or not user.is\_from\_chrome:

3    return "our service is only available for chrome logged in user

- 反 例

1 if not (user.has\_logged\_in and user.is\_from\_chrome):

2    return "our service is only available for chrome logged in user"

23. 【 推 荐 】 Askforgivenessnotpermission。 
- 说 明 ： 如 果 代 码 执 ⾏ 只 有 极 少 数 情 况 会 产 ⽣ 异 常 ， 此 时 建 议 使 ⽤ t r y/ except i on ⽽ 不 是 提 前 做 条 件 判 断 。![](cgft11wn.003.png)
24. 【 推 荐 】 在 判 断 条 件 中 使 ⽤ al l 和 any 内 置 函 数 ， 可 以 使 代 码 简 洁 ， ⾼ 效 。 
24. 【 推 荐 】 对 序 列 （ 字 符 串 、 列 表 、 元 组 ） ， 空 序 列 为 Fal s e 的 情 况 判 断 ， 不 要 使 ⽤ l en 函 数 。 
- 正 例

1 if not seq: 2   pass

3

4 if seq:

5   pass

- 反 例

1 if len(seq):

2   pass

3

4 if not len(seq): 5   pass

26. 【 推 荐 】 使 ⽤ def 定 义 简 短 函 数 ⽽ 不 是 使 ⽤ Lambda 匿 名 函 数 。 
- 说 明 ： 使 ⽤ def 定 义 函 数 有 助 于 在 t r ackbacks 中 打 印 有 效 的 类 型 信 息 。 
- Python曾 经 想 要 [移 除 Lambda](https://www.artima.com/weblogs/viewpost.jsp?thread=98196)， 后 来 妥 协 了 ， [参 考 这 ⾥ ](https://www.quora.com/Why-did-Guido-van-Rossum-want-to-remove-lambda-from-Python-3)。 
27. 【 推 荐 】 经 常 改 动 的 列 表 定 义 、 字 典 定 义 、 函 数 参 数 ， 建 议 每 ⾏ ⼀ 个 元 素 ， 并 且 每 ⾏增加⼀ 个 , 。 
- 正 例

1 yes  =  ( ' y' ,  ' Y' ,  ' yes' ,  ' TRUE' ,  ' Tr ue' ,  ' t r ue' ,  ' On' ,  ' on' ,  ' 1' )   #  基 本 不 再 改 2

3 kwlist = [

4    'False',

5    ...

6     ' yi el d' ,   #  最 后 ⼀ 个 元 素 也 增 加 ⼀ 个 逗 号  ， ⽅ 便 以 后 di f f 不 显 ⽰ 此 ⾏ 

7 ]

8

9 person = {

10    'name': 'bob',

11     ' age' :  12,       #  可 能 经 常 增 加 字 段 ![](cgft11wn.004.png)12    }

- 反 例

1 kwlist = ['False', 'None', 'True', 'and', 'as',

2          'assert', 'async', ...

3 ]

4

5 per son  =  {' name' :  ' bob' ,  ' age' :  12}  #  经 常 增 加 字 段 ， 不 利 于  gi t  做  di f f  ⽐ 较 

28. 【 推 荐 】 过 ⻓ 的 计 算 表 达 式 ， 操 作 符 应 该 在 换 ⾏ 符 之 后 出 现 。 
- 正 例

1 #  YES:  易 于 将 运 算 符 与 操 作 数 匹 配 ， 可 读 性 ⾼ 2 income = (gross\_wages

3          + taxable\_interest

4          + (dividends - qualified\_dividends) 5          - ira\_deduction

6          - student\_loan\_interest)

- 反 例

1 #  No:  运 算 符 的 位 置 远 离 其 操 作 数 

2 income = (gross\_wages +

3          taxable\_interest +

4          (dividends - qualified\_dividends)  - 5          ira\_deduction  -

6          student\_loan\_interest)

29. 【 推 荐 】 公 共 函 数 、 类 、 模 块 需 要 包 含 ⽂ 档 字 符 串 。 内 部 使 ⽤ 的 函 数 ， 在 函 数 名 不 能让使⽤者⼀ 眼 就 明 ⽩ 作 ⽤ 的 情 况 下 ， 需 要 提 供 注 释 。 
- 说 明 ： ⼀ 个 函 数 如 果 被 设 计 为 可 以 直 接 被 其 他 开 发 者 使 ⽤ ， 那 么 请 提 供 详 细 ⽂ 档明确其含义， 明 确 指 出 输 ⼊ 、 输 出 、 以 及 异 常 内 容 。
30. 【 推 荐 】 ⽂ 档 字 符 串 （ docstring） 必 须 使 ⽤ 三 重 双 引 号 """。 
30. 【 推 荐 】 在 使 ⽤ ⽂ 档 字 符 串 时 ， 推 荐 使 ⽤ reStructuredText⻛ 格 类 型 。 
- 前 三 引 号 后 不 应 该 换 ⾏ ， 应 该 紧 接 着 在 后 ⾯ 概 括 性 的 说 明 模 块 、 函 数 、 类 、⽅法的作⽤，然后 再 空 ⼀ ⾏ 进 ⾏ 详 细 的 说 明 。 后 三 引 号 应 该 单 独 占 ⼀ ⾏ 。![](cgft11wn.003.png)
- 其 中 函 数 的 docstring推 荐 ⼤ 致 顺 序 是 ： 概 述 、 详 细 描 述 、 参 数 、 返 回 值 、 异常。 
- ⼀ 般 不 要 求 描 述 实 现 细 节 ， 除 ⾮ 其 中 涉 及 ⾮ 常 复 杂 的 算 法 。
- ⽰ 例

1 def fetch\_bigtable\_rows(big\_table: Table, keys: list[str], other\_silly\_variab 2    """Fetches rows from a Bigtable.

3

4    Retrieves rows pertaining to the given keys from the Table instance

5    represented by big\_table.  Silly things may happen if

6    other\_silly\_variable is not None.

7

8    :param big\_table: An open Bigtable Table instance.

9    :param keys: A sequence of strings representing the key of each table row 10        to fetch.

11    :param other\_silly\_variable: Another optional variable, that has a much 12        longer name than the other args, and which does nothing.

13

14    :return: A dict mapping keys to the corresponding table row data

15        fetched. Each row is represented as a tuple of strings. For

16        example:

17

18        {'Serak': ('Rigel VII', 'Preparer'),

19         'Zim': ('Irk', 'Invader'),

20         'Lrrr': ('Omicron Persei 8', 'Emperor')}

21

22        If a key from the keys argument is missing from the dictionary,

23        then that row was not found in the table.

24

25    :raises ValueError: if `keys` is empty.

26    :raises IOError: An error occurred accessing the bigtable.Table object. 27    """

28    pass

32. 【 推 荐 】 在 except ⼦ 句 中 重 新 抛 出 原 有 异 常 时 ， 不 能 ⽤ r ai s e  ex ， ⽽ 是 ⽤ r ai s e 。 
- 正 例

1 try:

2      int("hello")

3  except ValueError:

4       r ai se  #  可 以 保 留 原 始 的  t r aceback 

5![](cgft11wn.004.png)

6 Traceback (most recent call last):

7 Fi l e  "〜 / t emp. py",  l i ne  2,  i n  <modul e>

8    int("hello")

9 ValueError: invalid literal for int() with base 10: 'hello'

10

11  try:

12      raise MyException()

13  except MyException as ex:

14       r ai se  Anot her Except i on( st r ( ex) )   #  允 许 ： 建 议 保 留 之 前 的 异 常 栈 信 息 ， ⽤ 于 定 位 问

- 反 例

1 try:

2      int("hello")

3  except ValueError as e:

4       r ai se  e  #  异 常 栈 信 息 从 这 ⾥ 开 始 

5 Traceback (most recent call last):

6   Fi l e  "〜 / t emp. py",  l i ne  2,  i n  <modul e> 7    raise e

8   Fi l e  "〜 / t emp. py",  l i ne  2,  i n  <modul e> 9    int("hello")

10 ValueError: invalid literal for int() with base 10: 'hello'

33. 【 推 荐 】 所 有 t r y/ except ⼦ 句 的 代 码 要 尽 可 的 少 ， 以 免 屏 蔽 其 他 的 错 误 。 

1 try:

2    value = collection[key]

3 except KeyError:

4    return key\_not\_found(key)

5 else:

6    return handle\_value(value)

7 反例

8 try:

9     #  范 围 太 ⼴ 

10    return handle\_value(collection[key]) 11 except KeyError:

12     #  会 捕 捉 到  handl e\_val ue( )  中 的  KeyEr r or 13    return key\_not\_found(key)

34. 【 推 荐 】 函 数 的 返 回 类 型 要 单 ⼀ ， 不 能 返 回 不 同 的 类 型 【 允 许 返 回 None 】 。 

- 正 例

1 def add(a, b):![](cgft11wn.005.png)

2      if isinstance(a, int) and isinstance(b, int): 3          return a + b

4      else:

5          raise Exception("Only int are allowed")

- 反 例

1 def add(a, b):

2      if isinstance(a, int) and isinstance(b, int): 3          return a + b

4      else:

5          return str(a) + str(b)

35. 【 推 荐 】 对 于 未 知 的 条 件 分 ⽀ 或 不 应 进 ⼊ 的 分 ⽀ ， 应 该 抛 出 异 常 ， ⽽ 不 是 返 回 ⼀ 个 值【如  None 、 Fal s e 】 。 
- 正 例

1 def foo(x):

2    if x in ('SUCCESS',):

3        return True

4    else:

5         #  如 果 ⼀ 定 不 会 ⾛ 到 的 条 件 ， 应 该 增 加 异 常 ， 防 ⽌ 将 来 未 知 的 语 句 执 ⾏ 。 6        raise Exception() 

- 反 例

1 def foo(x):

2    if x in ('SUCCESS',): 3        return True

4    return None

36. 【 参 考 】 应 该 充 分 使 ⽤ Python的 语 法 ， 但 是 不 应 该 过 度 的 使 ⽤ Python的 奇 技 淫 巧 
- 说 明 ： ⽐ 如 Python的 Slice语 法 

1 a = [1, 2, 3, 4]![](cgft11wn.005.png)

2 c = 'abcdef'

3 print(list(reversed(a))) 4 print(list(reversed(c)))

- 反 例

1 a = [1, 2, 3, 4] 2 c = 'abcdef'

3 print(a[::-1])

4 print(c[::-1])

37. 【 参 考 】 使 ⽤ di ct 来 返 回 多 个 值 。 

1 #  ⼀ 个 函 数 返 回 多 个 值 

2 def latlon\_to\_address(lat, lon):

3    return country, province, city

4

5 #  但 是 ， 这 样 的 ⽤ 法 会 产 ⽣ ⼀ 个 ⼩ 问 题 ： 

6 #  如 果 某 ⼀ 天 ， l at l on\_t o\_addr ess  函 数 需 要 增 加 返 回 城 区 「 Di st r i ct 」 时 怎 么 办 ？ 

7 #  如 果 是 上 ⾯ 这 种 写 法 ， 你 需 要 找 到 所 有 调 ⽤  l at l on\_t o\_addr ess  的 地 ⽅ ， 

8 #  补 上 多 出 来 的 这 个 变 量 ， 否 则 就 会 抛 出  Val ueEr r or :  t oo  many  val ues  t o  unpack  异 常 。

• 对 于 这 种 可 能 变 动 的 多 返 回 值 函 数 ， 使 ⽤ di ct 会 更 ⽅ 便 ⼀ 些 。 当 你 新 增 返 回 值 时 ， 不 会 对 之 前 的 函 数 调 ⽤ 产 ⽣ 任 何 破 坏 性 的 影 响

1 def latlon\_to\_address(lat, lon):

2    return {

3        'country': country,

4        'province': province,

5        'city': city

6    }

7

8 addr\_dict = latlon\_to\_address(lat, lon)

38. 【 参 考 】 多 参 考 标 准 库 ， 标 准 库 中 有 很 多 很 好 的 功 能 。 如 operator.methodcaller()等。


39. 【 参 考 】 使 ⽤ [ ] ， {} ⽽ 不 是 l i s t ， di ct （ 速 度 更 快 ） 。 ![](cgft11wn.009.png)
39. 【 参 考 】 使 ⽤ f or / el s e 简 化 异 常 处 理 。 
- 以 下 两 段 代 码 等 价
- 我 们 借 助 了 ⼀ 个 标 志 量 f ound 来 判 断 循 环 结 束 是 不 是 由 br eak 语 句 引 起 的 



|<p>1 2 3 4 5 6</p><p>7 8 9 10 11</p><p>12</p>|<p>def find\_index(nums: list[int], target: int) -> None:     found = False</p><p>`    `for index, num in enumerate(nums):</p><p>`        `if num == target:</p><p>`            `found = True</p><p>`            `break</p><p>`    `if found:</p><p>`        `print("not find {target}")</p><p>`    `else:</p><p>`        `print("find {target} at index {index}")</p>|
| - | :- |
|||
|<p>1 2 3 4</p><p>5 6 7</p>|<p>def find\_index(nums: list[int], target: int) -> None:     for index, num in enumerate(nums):</p><p>`        `if num == target:</p><p>`            `print("find {target} at index {index}")</p><p>`            `break</p><p>`    `else:</p><p>`        `print("not find {target}")</p>|
⼆ 、 编 码 原 则

此 部 分 提 供 ⼀ 些 编 码 的 指 导 ， 特 别 是 在 多 种 写 法 在 语 法 上 都 正 确 的 时 候 ， 应该如何抉择。

1. 【 推 荐 】 进 攻 式 实 现 、 防 御 式 调 ⽤
- 对 于 实 现 ： 没 有 ⼈ 能 保 证 ⾃ ⼰ 的 代 码 「 完 美 」 地 处 理 所 有 case。 
- 对 于 调 ⽤ ： 没 有 不 出 错 的 代 码 ， 但 没 有 ⼈ 希 望 ⾃ ⼰ 的 系 统 因 别 ⼈ 的 ⼿ 残 挂 掉（假定外部系统是 沙 ⼦ ） 。
2. 【 推 荐 】 不 要 为 了 正 确 ⽽ 正 确 ， 隐 藏 错 误

- 如 果 对 于 ⼀ 个 字 典 my\_di ct ， 其 中 键 my\_key 是 ⼀ 个 必 要 的 key 。 就 永 远 不 要 写  ![](cgft11wn.005.png)my\_di ct . get ( my\_key) 。 这 样 的 程 序 只 会 莫 名 其 妙 的 对 了 。 根 据 墨 菲 定 律 ， 总 有 ⼀ 天 ， 这 段 代 码 会 坑 了 整 个 团 队 。
- 必 要 的 情 况 ⽤ 异 常 通 知 上 层 发 ⽣ 了 不 可 预 知 的 错 误 ， 异 常 需 要 带 有 必 要 的 信息，要辅助快速定 位 问 题
- 反 例

1 value = my\_dict.get(my\_key)

- 正 例

1 value = my\_dict[my\_key] # my\_key must exists 2

3 #  或 者 

4 if my\_key not in my\_dict:

5  raise KeyError

3. 【 推 荐 】 不 放 ⼤ 错 误
- raise不 是 ⽤ 来 推 卸 责 任 。 合 理 的 as s er t 、 r ai s e 只 是 向 外 声 明 ： 我 的 代 码 发 ⽣ 了 ⼀ 个 不 可 忽 视 的 错 误 。 代 码 的 调 ⽤ 者 必 须 负 责 处 理 这 个 错 误 （ 因 为 我 声 明 了 它 不 可忽视）。
- 维 护 者 ： r ai s e 不 是 推 卸 责 任 ， 维 护 者 有 义 务 抛 出 并 且 只 抛 出 被 认 为 不 对 的 case。 
- 调 ⽤ 者 ： 调 ⽤ 别 ⼈ 的 函 数 ， 就 应 该 遵 守 别 ⼈ 的 规 范 。 调 ⽤ ⽅ 需 要 ⾃ ⼰ 判 断 ， 是 否 需 要 继 续 raise 给 上 层 。
4. 【 推 荐 】 严 厉 排 查 死 循 环
- ⽆ 论 多 么 ⼩ 的 whi l e  t r ue 循 环 ， 当 br eak 条 件 ⽆ 法 触 发 时 （ 因 为 各 种 bug） ， 我 们 的 服 务 就 死 掉 了 。 
5. 【 推 荐 】 合 理 的 处 理 异 常

代 码 不 可 能 永 不 出 错 ， 合 理 的 处 理 错 误 ， 能 提 ⾼ 代 码 的 健 壮 性 。 对 于 出 错 的处理情况，可以⼤致分 为 三 类 。

- 调 ⽤ 者 不 关 ⼼ 的 异 常 ： 降 级 函 数 代 替 （ 确 保 降 级 函 数 不 会 出 错 ）
- 关 键 功 能 异 常 ： 使 ⽤ r ai s e 抛 出 
- 重 要 但 是 不 应 该 影 响 主 流 程 的 异 常 ： 降 级 函 数 +⽇ 志 报 警 
6. 【 推 荐 】 接 ⼝ 返 回 类 型 统 ⼀
- 接 ⼝ 的 返 回 类 型 尽 量 统 ⼀ ， 减 少 None 值 的 返 回 。 

1 def get\_number\_list(num: int):![](cgft11wn.010.png)

2    if num < 10:

3        return 0

4    elif 10 <= num < 100:

5        return [10 for i in range(10)] 6    else:

7        return None

- ⼀ 个 命 名 为 get \_number \_l i s t 的 函 数 应 当 总 是 返 回 数 组 或 者 抛 出 异 常 。 
7. 【 推 荐 】 只 做 ⾃ ⼰ 该 做 的 事 情

1 def pickup\_slotcard(feeds):

2    ...

3    for feed in feeds:

4        if feed.type == slot\_card:

5            return format\_feed(slot\_card) 6    return None

- pickup\_slotcard： 找 出 feed中 的 slotcard， 只 要 负 责 找 就 ⾏ 了 ， 不 要 ⼲别的事情。 
- format\_feed不 需 要 做 。 
8. 【 推 荐 】 尽 量 避 免 默 认 参 数

默 认 意 味 着 参 数 可 以 不 传 ， 容 易 给 调 ⽤ 者 造 成 困 扰 ： 是 传 递 还 是 不 传 ？

- 不 负 责 的 调 ⽤ 者 ： 直 接 就 不 传 了 。
- 负 责 的 调 ⽤ 者 ： 看 下 ⽂ 档 ， 代 码 才 知 道 怎 么 传 。
- 代 码 维 护 者 ： 如 果 对 默 认 值 进 ⾏ 修 改 ， 则 必 须 排 查 所 有 调 ⽤ ⽅ 。
9. 【 推 荐 】 合 理 分 层 ， 判 断 参 数 是 否 合 理

对 于 那 些 只 是 为 了 控 制 调 ⽤ 流 程 的 参 数 ， 可 以 考 虑 拆 分 单 独 函 数 。

1 def func(control, a, b ,c): 2    if control == 1:

3        pass

4    elif control == 2:

5        pass

6    else:

7        pass

8 return

9

10 #  只 实 现 功 能 逻 辑 ，  调 ⽤ 掌 管 业 务 逻 辑 ![](cgft11wn.008.png)11 def f\_control\_1(a, b, c)

12 def f\_control\_2(a, b, c)

13 def f\_control\_3(a, b, c)

10. 【 推 荐 】 类 设 计 ， 少 ⽤ 继 承 ， 多 ⽤ 组 合 。 
    1. 过 深 的 继 承 链 会 导 致 代 码 维 护 成 本 成 倍 的 增 加 。
10. 【 推 荐 】 压 缩 类 属 性 

如 果 ⼀ 个 类 有 很 多 相 互 关 联 的 属 性 ， 其 中 某 些 熟 悉 由 其 他 属 性 计 算 ⽽ 出 。 那么这样的属性应该被去 除 ， 转 ⽽ 使 ⽤ get\_xx⽅ 法 获 取 ， 或 者 使 ⽤ pr oper t y 。 

没 有 衍 ⽣ 属 性 ， 类 的 init变 得 简 单 ， 代 码 的 可 测 试 性 得 到 提 ⾼ ， 可 维 护 性 得 到 提⾼。 

1 class Sample:

2

3    def \_\_init\_\_(self, price: float, amount: int): 4        self.price = price

5        self.amount = amount

6

7    @property

8    def profit(self):

9        return self.price \* self.amount

12. 【 推 荐 】 禁 ⽌ 改 变 函 数 签 名 【 ⾥ ⽒ 替 换 原 则 】 
- 所 有 ⽤ 到 ⽗ 类 ⽅ 法 的 地 ⽅ ， 都 可 以 ⽤ ⼦ 类 替 换 的 同 时 ⽽ 不 产 ⽣ 代 码 语 法 错 误，类型错误。

1 class Base:

2    def func(self, a: int):

3        raise NotImplementedError() 4

5

6 class ClassA(Base):

7    def func(self, a: int):

8        pass

9

10

11 class ClassB(Base):

12    def func(self, a: int): 13        pass

14

15

16 class ClassC(Base):![](cgft11wn.004.png)

17     def  f unc( sel f ,  b:  l i st [ st r ] ) :   #  作 者 觉 得 参 数 不 满 ⾜ 

18        pass

19

20  #  代 码 调 ⽤ 者 

21 ClassA().func(a)   # no bug

22 ClassB().func(a)   # no bug

23 Cl assC( ) . f unc( a)    #  bug?   why?   怎 么 会 挂 ？ ？ ？ 代 码 维 护 者 脑 ⼦ 抽 了 ？ 

13. 【 推 荐 】 考 虑 使 ⽤ 者 的 感 受 
- 写 代 码 时 ， 【 考 虑 的 是 怎 么 写 ， 还 是 怎 么 ⽤ 】 是 区 分 是 否 是 优 秀 ⼯ 程 师 的 ⼀ 个 重 要 指 标 。 只 对 作 者 友 好 的 代 码 绝 对 称 不 上 是 优 秀 的 代 码 。 ⾯ 向 ⼯ 程 ， ⾯ 向 合 作 ， 要 让 ⽤ 的⼈舒服，让⽤的⼈

⼼ 理 成 本 低 。

14. 【 推 荐 】 稍 后 等 于 ⽤ 不 【 LeBlanc（ 勒 布 朗 ） 法 则 】 
- 如 果 旧 的 架 构 不 能 满 ⾜ 新 的 需 求 ， 那 就 需 要 调 整 ， ⽽ 且 是 尽 快 调 整 。
- 合 理 的 时 间 进 ⾏ 合 理 的 重 构 才 能 让 架 构 ⾜ 够 的 活 ⼒ ， ⽽ 不 是 「 下 次 再 说 」 。所有的新功能都是

「 应 该 在 哪 ⾥ 」 ， ⽽ 不 是 「 狗 ⽪ 膏 药 」 漫 天 ⻜ 。

15. 【 推 荐 】 尽 量 ⽆ 状 态 设 计 
- 有 状 态 的 代 码 ， 可 维 护 性 ， 可 测 试 性 都 会 ⼤ ⼤ 降 低 。 测 试 代 码 时 ， 维 护 者 需要痛苦的构造上下

⽂ ， debug场 景 难 以 复 现 

16. 【 推 荐 】 删 除 ⽆ ⽤ 代 码 （ YAGNI原 则 ）  YouAin'tGonnaNeedIt（ 你 不 会 需 要 它 ） ， 好 处 ： 
- 节 约 ⼯ 程 成 本 ， 避 免 编 写 不 必 要 代 码 ， ⽆ 需 维 护 这 些 代 码 。
- 提 ⾼ 代 码 质 量 ， 不 会 让 暂 时 ⽆ ⽤ 甚 ⾄ 永 远 ⽆ ⽤ 的 代 码 ， 污 染 项 ⽬ 。

开 发 者 不 应 该 编 写 ⽆ ⽤ 逻 辑 ， 也 不 应 该 允 许 ⽆ ⽤ 逻 辑 的 存 在 。 所 有 下 线 的 逻 辑 （ 被 注 释 的 代 码 、 没 有 调 ⽤ 的 函 数 、 永 远 为 False的 判 断 ） 必 须 ⼲ 掉 代 码 ！ 

如 果 将 来 某 天 需 要 ， 可 以 依 赖 git版 本 控 制 、 仓 库 打 tag、 ⽂ 档 维 护 commit节点等等，会有⽆ 数 个 ⽐ 注 释 掉 代 码 更 ⾼ 效 的 ⽅ 案 。

17. 【 推 荐 】 好 的 代 码 胜 过 注 释 【 代 码 本 ⾝ 即 注 释 】 
- 良 好 的 变 量 、 函 数 命 名 是 最 好 的 注 释 。
- 因 为 注 释 没 有 任 何 机 制 保 证 强 制 更 新 ， 不 及 时 的 注 释 容 易 更 其 他 ⼈ 带 来 更 多的理解上的困惑。 依 赖 注 释 的 代 码 很 可 能 由 「 ⼯ 程 导 向 」 恶 化 成 「 ⽂ 档 导 向 」 。 漫 天 都 是 解 释这个⼏百⾏函数在

⼲ 嘛 ， 可 是 没 ⼈ 能 看 懂 。

18. 【 推 荐 】 减 少 变 量 ， 让 变 量 尽 量 局 部 
- 变 量 的 中 间 赋 值 、 写 逻 辑 ， 往 往 是 代 码 千 奇 百 怪 bu g的 导 ⽕ 索 。 让 变 量 的 使⽤限制在尽量⼩的 范 围 。![](cgft11wn.005.png)

a. 可 以 通 过 使 ⽤ ⼦ 函 数 、 代 码 块 等 ⼿ 段 ， 来 减 少 变 量 漫 天 ⻜ 的 情 况 。

19. 【 推 荐 】 接 ⼝ 隔 离 原 则 【 InterfaceSegregationPrinciple】 
    1. ⼀ 个 类 ， ⽅ 法 ， 不 应 该 依 赖 于 它 不 需 要 的 接 ⼝ （ 与 单 ⼀ 职 责 原 则 有 相 似 之 处）
19. 【 推 荐 】 依 赖 倒 置 原 则 （ DependenceInversion） 
- ⾼ 层 ⽅ 法 不 依 赖 于 低 层 ⽅ 法 ， ⼆ 者 都 应 该 依 赖 于 抽 象 。

三 、 类 型 注 释

🍰为 什 么 Python类 型 注 释 （ TypeAnnotation） 越 来 越 重 要 且 逐 渐 被 ⼴ 泛 使⽤？ 

1. 提 ⾼ 代 码 可 读 性 ： 类 型 注 释 使 得 开 发 者 更 容 易 理 解 函 数 、 类 和 ⽅ 法 的 预 期 输⼊和输出，从⽽⼤⼤提
   1. 代 码 的 可 读 性 ， 使 得 其 他 ⼈ 更 容 易 维 护 和 扩 展 代 码 。
1. 更 好 的 ⽂ 档 ： 类 型 注 释 提 供 了 关 于 函 数 的 输 ⼊ 和 输 出 类 型 的 清 晰 说 明 ， ⽽ ⽆需额外的注释（代码即
   1. 档 ） 。
1. ⼯ 具 ⽀ 持 ： 许 多 IDE⼯ 具 和 linter可 以 基 于 类 型 注 释 提 供 代 码 的 改 进 提 ⽰ ， 错误检查和重构⽀持。 
1. 提 ⾼ 代 码 质 量 ： 类 型 注 释 可 以 帮 助 开 发 者 在 开 发 过 程 中 尽 早 发 现 潜 在 错 误 ，因为类型不匹配能在编 译 时 检 测 到 。
1. 更 好 的 性 能 ： 类 型 注 释 也 可 以 被 ⼯ 具 ⽤ 来 ⽣ 成 优 化 的 代 码 ， 从 ⽽ 产 ⽣ 更 快 、更有效的程序。
1. 相 关 ⽂ 档 ： 参 考 1， 参 考 2， 参 考 3， 参 考 4， 参 考 5， PEP484

📌因 此 ， 在 Python编 程 过 程 中 ， 强 烈 推 荐 使 ⽤ 类 型 注 解 。 

从 Python3.5版 本 开 始 ， Python将 typing作 为 标 准 库 引 ⼊ 。 

四 、 代 码 审 核

🎨提 交 PR时 请 求 他 ⼈ 审 核 代 码 的 ⽬ 的 

1. 发 现 代 码 不 合 理 的 结 构 设 计 ， 提 ⾼ 代 码 质 量 ， 提 ⾼ 代 码 可 读 性 ， 可 维 护 性 ，可测试性。
2. 降 低 开 发 者 之 间 的 沟 通 成 本 ， ⿎ 励 开 发 者 之 间 互 相 帮 助 学 习 。![](cgft11wn.011.png)
2. CodeReview不 是 ⼤ 家 来 找 茬 ， 不 要 刻 意 找 Bug， 不 要 鸡 蛋 ⾥ 挑 ⻣ 头 ， 不 要 把 代 码 审 查 搞成批判 会 。
2. 遇 到 不 合 常 理 的 情 况 ， 先 了 解 项 ⽬ 背 景 ， 可 能 是 原 有 架 构 不 合 理 。 要 做 到 不 妥 协 ， 不 执 拗 ， 共 同 改 善 框 架 。
2. 有 争 议 的 问 题 可 暂 时 搁 置 【 记 下 问 题 ， 整 理 思 路 ， 开 会 讨 论 】 。 🏖评 审 代 码 时 ， 可 以 对 CodeReview进 ⾏ 分 级 
1. 【 request】 xxxxxxx       此 条 评 论 的 代 码 必 须 修 改 才 能 予 以 通 过 
1. 【 advise】 xxxxxxxx       此 条 评 论 的 代 码 建 议 修 改 ， 但 不 修 改 也 可 以 通 过 
1. 【 question】 xxxxxx       此 条 评 论 的 代 码 有 疑 问 ， 需 代 码 提 交 者进⼀步解释 

五 、 扩 展 阅 读

- 些 Python规 范 ⽂ 档 和 检 查 ⼯ 具 。 
1. PythonEnhancementProposals
1. TheZenofPython
1. PreCommit
1. Pylint
1. Pyright
1. Mypy
