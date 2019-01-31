# 硬盘操作

## 分区扩容
分区扩容有两种方式:
1. 在原分区的位置上追加空间
2. 移动整个分区到更大的空间

其实, 这个思路和编程语言中对向量/切片的处理是类似的, 移动整个分区产生更多的消耗.

流程如下
1. 使用 fdisk 划分更大的分区: `fdisk /dev/sda`, 然后删掉要扩容的分区, 在 **原起始位置** 创建新分区.
    - 注意, 要保证是在删除分区的原起始位置, 并且保证分配的地址连续, 即后续有空间.
2. 使用 `resize2fs /dev/sda3` 使变化生效.

如果是移动整个分区, 思路如上. 注意提前将文件copy到新分区即可(注意避免改变文件权限)