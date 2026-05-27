---
name: cad-drawing-generator
description: CAD给排水系统图生成 - 根据参数或YAML配置生成GB/T 50106-2010标准的给排水/消防系统轴测图DXF文件。支持快速参数模式和完整配置文件模式，包含40+标准符号库。同义词：生成图纸、系统图、轴测图、给排水图、消防图、绘制管道、CAD图纸生成、画cad、画给排水、生成dxf、plumbing diagram、isometric drawing
---

# CAD Drawing Generator -- 给排水系统图生成

## 概述

程序化生成符合 GB/T 50106-2010 标准的给排水/消防系统轴测图 DXF 文件。两种模式：快速参数生成、完整 YAML 配置生成。

## 项目位置

```
C:\Users\86183\cad-drawing-gen\
```

## 模式选择

| 关键词                         | 模式               | 命令                                                         |
| ------------------------------ | ------------------ | ------------------------------------------------------------ |
| 快速/参数/简单/quick/几个参数  | Quick (A)          | `python main.py quick --system <type> --floors N --risers N` |
| 详细/配置文件/config/YAML/完整 | Config (B)         | `python main.py generate --config <file>.yaml`               |
| 预览/检查/看看                 | 用 cad-reader 打开 | 调用 cad-reader skill                                        |

## 模式 A：快速生成

适用：快速原型，参数简单，不需要精确配置。

### 工作流

1. 收集参数：系统类型、楼层数、立管数、地下层数
2. 构造命令并执行：
   ```bash
   cd C:\Users\86183\cad-drawing-gen
   python main.py quick --system plumbing --floors 6 --risers 2 --basement 1
   ```
3. 可选：用 AutoCAD MCP 打开预览
4. 报告输出路径

### 快速参数

| 参数         | 说明                              | 默认值                    |
| ------------ | --------------------------------- | ------------------------- |
| `--system`   | 系统类型 (plumbing/drainage/fire) | plumbing                  |
| `--floors`   | 地上层数                          | 6                         |
| `--risers`   | 立管数                            | 1                         |
| `--basement` | 地下层数                          | 0                         |
| `--output`   | 输出路径                          | output/system_diagram.dxf |
| `--scale`    | 绘图比例                          | 100                       |

## 模式 B：YAML 配置生成

适用：精确控制每个立管位置、分支、阀门，完整配置。

### 工作流

1. 确认配置文件路径（模板：`config/example_6floor.yaml`）
2. 按需修改配置
3. 执行：
   ```bash
   cd C:\Users\86183\cad-drawing-gen
   python main.py generate --config config/my_building.yaml --output output/my_diagram.dxf
   ```
4. 报告输出

### YAML 配置结构

```yaml
building:
  floors: 6 # 地上层数
  floor_height: 3000 # 层高(mm)
  basement: 1 # 地下层数

systems:
  - type: 给水 # 系统类型
    title: 给水系统图 # 图纸标题
    code: J # 管道代号
    risers:
      - id: JL-1
        position: [100, 100]
        diameter: DN50
        branches: # 分支（可选）
          - floor: 1
            type: 水龙头
```
