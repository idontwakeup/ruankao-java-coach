# 校准示例

这些示例只用于校准推理方式和输出粒度。每道新题都必须从它自己的代码、类图和调用点重新推导，不能按模式名称套答案。

## 示例一：Strategy

结构：

- `PrintStrategy` 接口。
- `PrintIntervalsComma`、`PrintIntervalsDots`、`PrintIntervalsLine` 三个实现类。
- `Interval.printIntervals(PrintStrategy)` 使用传入的策略。
- `Main.getStrategy(TYPE)` 根据枚举创建具体策略。

推理：

1. 三个实现类都有 `doPrint(Interval val)`，因此接口声明相同方法。
2. `ptr` 是 `PrintStrategy` 参数，空位必须使用它，因此调用 `ptr.doPrint(this)`。
3. 三个具体策略类没有 `new`，三个 `switch` 分支分别创建它们。

关键答案：

```java
public void doPrint(Interval val);
ptr.doPrint(this);
st = new PrintIntervalsComma();
st = new PrintIntervalsDots();
st = new PrintIntervalsLine();
```

讲解重点：接口规定方法，具体类实现方法，接口变量保存具体对象，运行时多态决定实际执行哪个 `doPrint`。

## 示例二：Facade

结构：

- `Patient` 接口由 `ConcretePatient` 实现。
- `Disposer` 接口由 `Registry`、`Doctor`、`Pharmacy` 实现。
- `Facade` 保存 `Patient`，统一调用三个部门。
- `FacadeTest.main()` 创建患者和 Facade。

推理：

1. 三个实现类都调用 `patient.getName()`，且 `ConcretePatient` 提供 `getName()`，因此 `Patient` 接口声明 `public String getName()`。
2. 三个 `Disposer` 实现类都有 `public void dispose(Patient patient)`，因此接口声明相同方法。
3. `Patient` 是接口，不能直接 `new`；创建 `new ConcretePatient(...)`。
4. `Facade` 没有在入口代码中创建，因此声明变量类型 `Facade` 并执行 `new Facade(patient)`。
5. `Facade` 提供统一入口 `dispose()`，因此调用 `f.dispose()`。

关键答案：

```java
public String getName();
public void dispose(Patient patient);
Patient patient = new ConcretePatient("Tom");
Facade f = new Facade(patient);
f.dispose();
```

讲解重点：Facade 把多个子系统的复杂调用封装成一个入口。解题仍以接口实现、对象创建、属性和调用链为依据，不要求先背 Facade 定义。

## 练习题骨架

生成新题时使用以下骨架，并更换业务域：

```text
interface A { blank 1 }
interface B { blank 2 }

class B1 implements B { method(B) uses A.get... }
class B2 implements B { method(B) uses A.get... }
class B3 implements B { method(B) uses A.get... }

class FacadeOrContext {
    private A a;
    constructor(A a)
    entry() { create B1/B2/B3 and call each method(a); }
}

class ConcreteA implements A {
    private field;
    constructor(field)
    getField()
}

main:
    A a = blank 3;
    FacadeOrContext obj = blank 4/5;
    blank 6;
```

题目覆盖接口签名、具体对象创建、属性读写、参数传递和 Facade/Context 调用。答案后说明每个空对应哪条口诀。
