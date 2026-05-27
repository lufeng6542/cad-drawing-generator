# cad-drawing-generator CLI 命令参考

## 项目位置

```
C:\Users\86183\cad-drawing-gen\
```

## 快速生成

```bash
# 生成6层给水系统图
python main.py quick --system plumbing --floors 6 --risers 2

# 生成带地下室的排水系统图
python main.py quick --system drainage --floors 6 --basement 1 --risers 3

# 生成消防系统图
python main.py quick --system fire --floors 12 --risers 4 --output output/fire_diagram.dxf
```

## YAML配置生成

```bash
# 模板文件
python main.py generate --config config/example_6floor.yaml

# 自定义配置
python main.py generate --config config/my_building.yaml --output output/my_diagram.dxf --scale 50
```

## 参数说明

| 参数         | 说明                   | 默认值                    |
| ------------ | ---------------------- | ------------------------- |
| `--system`   | plumbing/drainage/fire | plumbing                  |
| `--floors`   | 地上层数               | 6                         |
| `--basement` | 地下层数               | 0                         |
| `--risers`   | 立管数                 | 1                         |
| `--output`   | 输出DXF路径            | output/system_diagram.dxf |
| `--scale`    | 绘图比例               | 100                       |

## 依赖安装

```bash
pip install ezdxf pyyaml
```
