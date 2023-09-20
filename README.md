# strings2execel
strings 转 execel，python3

## 使用方法

将需要导出的多语言`.lproj`文件导入该目录下的`examples/ios`目录下

CD 到该目录下

执行：

``` shell
python3 python/Strings2Xls.py -f examples/ios/ -t examples/output
```

excel 文件生成路径在该目录下的 `examples/ios`

参考链接：https://blog.csdn.net/weixin_41732253/article/details/110288709

Python3 参考链接

https://blog.csdn.net/zyf13187056417/article/details/108346101

### 报错解决方案：

ModuleNotFoundError: No module named ‘xlwt’，需要安装xlwt，执行 `pip3 install xlwt`

## 注意事项

以下情况建议提前搜索 stings 文件检查（使用正则表达式`(=\s{2,})|(=\S)|(\"=)|(\\\".*=)`）。或者导出后手动修复。

所以建议 string 文件格式最好为`"key" = "value"`.尽量避免 key 中包含引号。

### 缺少空格

如果多语言中含如下格式：

```shell
“key”=“value”
```

`=`前后没有空格，则无法识别，导出的 excel 会导致该 key 和 value 缺失。

正确格式应该是（等号前后有一个空格）

```shell
“key” = “value”
```

> 可以修改为正确格式，或手动补充excel

### 多余空格

同理，如果`=`前后有超过一个空格，导出的对应的 value 也有问题。示例

``` shell
"key" =  "value"
```

导出的 excel 错误值`"value`，多了一个引号

> 可以修改为正确格式，或手动修改 excel

### key 中含有“

如果 key 中含有引号，则会导致引号后的 key 都无法匹配到，示例如下：

```shell 
"ke\"y" = "value"
```

导出的 excel 错误值为 `ke`，后面的`y`被忽略了。

> 只能手动补充 excel 值，可以通过搜索正则`\\\".*=`来匹配查找。



