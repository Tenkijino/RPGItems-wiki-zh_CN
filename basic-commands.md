# 基础命令

这里列出了 **RPGItems** 中用来管理与制作道具的命令

## 创建道具

```
/rpgitem create myitem
```

## 删除道具

```
/rpgitem delete myitem
```

## 道具列表

```
/rpgitem list [page] <param>
```

附加参数值可以用于筛选。

* `display` - 道具的展示名
* `name` - RPGItem数据库中的物品名

命令示例

```
/rpgitem list display:Hero
```

以上指令将会列出所有展示名中包含Hero的道具

## 给与道具

```
/rpgitem give [item] <target> <amount>
```

命令示例

```
/rpgitem give mysword Notch 2
```

以上指令将会给予玩家`Notch`两个展示名为`mysword`的道具

你同样也可以给与自己展示名为`mysword`的道具

```
/rpgitem give mysword
```

## Load from file

```
/rpgitem loadfile mysword-item.yml
```

Items are stored in `items/` directory under RPGItems plugin directory.

## Reload item from file

```
/rpgitem reloaditem mysword
```

## Reload plugin

```
/rpgitem reload
```

## Import and Export

```
/rpgitem import [GIST|URL] [value]
```

```
/rpgitem export mysword
```

* Note: You need Gist API key to use this feature.

## Clone

```
/rpgitem clone mysword mynewsword
```

## Dump

```
/rpgitem dump mysword
```

Will print raw item configuration content in YAML format for further inspection.

