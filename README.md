# ruankao-java-coach

一个用于 Codex 的软考软件设计师 Java 大题教练 Skill。

它面向 Java 基础薄弱、准备软考软件设计师下午题的考生。核心理念是：不要求背完 23 种设计模式，而是从类、属性、方法、接口、参数和调用关系中反推代码填空。

## 适合什么题目

- 软考软件设计师或软件中级设计师下午 Java 大题
- 根据类图和 Java 代码填写空白的题目
- 需要逐空解释、核对参考答案或补充 Java 基础的场景
- 根据真题结构生成类似练习题

它不用于普通 Java 作业，也不会默认分析同一题的 C++ 版本，除非你明确要求比较。

## 核心方法

1. 列出所有类、接口、抽象类、枚举、属性和方法。
2. 标记已经出现的 `new`、方法调用、继承、实现和属性读写。
3. 判断每个空属于对象创建、方法声明、方法调用、参数、返回值还是表达式。
4. 从调用点和实现类反推方法名、返回类型和参数类型。
5. 先填有把握的空，再利用后续关系消解不确定答案。
6. 最后检查接口实现、方法签名、返回值、参数和对象创建是否一致。

## 五条检查口诀

```text
看到具体类：哪里 new 了它？
看到接口或抽象类：哪个类 implements 或 extends 了它？
看到属性：哪里设置值，哪里读取值？
看到方法：哪里调用它？
看到参数：方法体有没有使用它？
```

## 安装

### Windows PowerShell

```powershell
git clone https://github.com/idontwakeup/ruankao-java-coach.git "$HOME\.codex\skills\ruankao-java-coach"
```

### macOS / Linux

```bash
git clone https://github.com/idontwakeup/ruankao-java-coach.git "$HOME/.codex/skills/ruankao-java-coach"
```

安装后重新打开或刷新 Codex，让技能列表重新加载。

## 使用示例

```text
使用 $ruankao-java-coach 指导我完成这个 PDF 里的 Java 大题。
```

```text
使用 $ruankao-java-coach 按五条口诀逐空讲解这道软考 Java 下午题。
```

```text
使用 $ruankao-java-coach 根据这道 Facade 题给我出一道类似练习题。
```

也可以直接提到“软考软件设计师 Java 下午题”“Java 大题代码填空”等关键词，Skill 会自动匹配。

## 输出内容

当提供题目、代码、截图或 PDF 时，Skill 会尽量给出：

- 最终答案和作答边界
- 类、接口、属性和方法清单
- 每一个空的推理过程
- 涉及的 Java 基础概念
- 填好的关键代码
- 在环境允许时的编译和运行验证
- 五条口诀复盘
- 用于巩固的类似练习题

## 仓库结构

```text
ruankao-java-coach/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
`-- references/
    `-- worked-examples.md
```

`SKILL.md` 是 Codex 加载的核心说明；`agents/openai.yaml` 提供界面元数据；`references/worked-examples.md` 包含 Strategy 和 Facade 两个校准示例。

## 说明

本项目只提供学习方法、代码推导和练习辅助，不是软考官方资料，也不分发试卷或答案 PDF。正式考试作答时，应结合题目原文、类图和官方考试要求进行判断。
