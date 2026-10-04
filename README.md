# 2048

> Java + Swing 实现的 2048 游戏 — CS61B (UC Berkeley) Project 0

![Java](https://img.shields.io/badge/Java-17-orange)
![Tests](https://img.shields.io/badge/JUnit-75%20个测试全部通过-brightgreen)

## 项目简介

经典 2048 的 Java 实现，棋盘与方块用 Swing 绘制，支持方向键操作。
界面与数据结构的骨架由课程提供，**核心游戏逻辑由本人实现**。

## 我实现的部分

集中在 `game2048/Model.java`（296 行）：

| 方法 | 作用 |
| --- | --- |
| `tilt(Side side)` | 四个方向的移动与合并，游戏的核心算法 |
| `helper(int col)` | 单行 / 单列的压缩与合并 |
| `atLeastOneMoveExists(Board b)` | 判断是否还有合法移动（游戏结束判定） |
| `maxTileExists(Board b)` | 判断是否已出现 2048（胜利判定） |
| `emptySpaceExists(Board b)` | 判断棋盘是否还有空位 |

## 玩法

方向键控制移动，相同数字的方块相撞时合并，出现 2048 获胜，无路可走则游戏结束。
支持 `--seed=NUM` 指定随机种子、`--log` 记录每次移动，便于复现某一局。

## 目录结构

```
2048/
├── game2048/
│   ├── Model.java      # 游戏核心逻辑（本人实现）
│   ├── Board.java      # 棋盘
│   ├── Tile.java       # 方块
│   ├── GUI.java        # Swing 界面
│   ├── Main.java       # 程序入口
│   └── Test*.java      # JUnit 测试
└── javalib/            # 依赖：junit / hamcrest / ucb.jar（GUI 组件库）
```

## 如何运行

需要 JDK 17+。

> ⚠️ 源码含中文、为 UTF-8 编码。**中文 Windows 上必须加 `-encoding UTF-8`**，
> 否则 `javac` 会按 GBK 解析而报 "不可映射字符" 错误。

```bash
javac -encoding UTF-8 -cp "javalib/*" -d out game2048/*.java
java -cp "out;javalib/*" game2048.Main
```

> Linux / macOS 下 classpath 分隔符是 `:` 而不是 `;`。

## 跑测试

```bash
java -cp "out;javalib/*" org.junit.runner.JUnitCore game2048.TestModel
```

5 个测试类共 **75 个用例，全部通过**：

| 测试类 | 用例数 |
| --- | --- |
| `TestModel` | 45 |
| `TestAtLeastOneMoveExists` | 10 |
| `TestEmptySpace` | 8 |
| `TestMaxTileExists` | 8 |
| `TestUpOnly` | 4 |

> `TestUtils` 是测试基类（提供构造棋盘的辅助方法），不是测试套件。

## 关于

CS61B (Spring 2021) Project 0 课程项目。课程提供的起始代码与测试归 UC Berkeley 所有。
