## --
`--` 是bash 的一个开关表示禁用参数
### Example:
ls * 代表的是 列出下面所有的文件
```
~/test/ls_test » ls *                                                                                                                                                                      piao@piao-All-Series
a  b
```
现在假定当前文件夹下面创建了 -l 这样一个文件
```
> -l   
~/test/ls_test » ls                                                                                                                                                                        piao@piao-All-Series
a  b  -l

```
那么 `ls *`呢？
```
------------------------------------------------------------
~/test/ls_test » ls *                                                                                                                                                                      piao@piao-All-Series
-rw-rw-r-- 1 ll ll 0 Aug 17 14:05 a
-rw-rw-r-- 1 ll ll 0 Aug 17 14:05 b
```
那我们的 -l 这个文件呢？
为什么又会展开呢？
是因为 * 被 展开后 变成了 `ls a b -l`

Ref: [Unix的缺陷](http://kb.cnblogs.com/page/153843/)
```
~/test/ls_test » ls a b -l                                                                                                                                                                 piao@piao-All-Series
-rw-rw-r-- 1 piao piao 0 Aug 17 14:05 a
-rw-rw-r-- 1 piao piao 0 Aug 17 14:05 b
-----------------------------------------
```
自然得不到想要的结果了

加上 `--` 后
```
~/test/ls_test » ls -- *                                                                                                                                                                   piao@piao-All-Series
a  b  -l
```
就可以了 删掉这个文件也是一样的
```
~/test/ls_test » rm -l                                                                                                                                                                     piao@piao-All-Series
rm：无效选项 -- l
Try 'rm ./-l' to remove the file '-l'.
Try 'rm --help' for more information.

~/test/ls_test » rm '-l'                                                                                                                                                                   piao@piao-All-Series
rm：无效选项 -- l
Try 'rm ./-l' to remove the file '-l'.
Try 'rm --help' for more information.

~/test/ls_test » rm -- -l                                                                                                                                                                  piao@piao-All-Series
------------------------------------------------------------
~/test/ls_test » ls                                                                                                                                                                        piao@piao-All-Series
a  b
-----------
```
