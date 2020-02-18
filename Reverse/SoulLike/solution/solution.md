# SoulLike

​	首先用IDA打开程序，main函数很好分析，就是先读取一个字符串，然后首先判断flag格式，之后丢给函数sub_83a，如果函数返回为真就说明是正确的flag。

​	之后我们来看sub_83a函数。刚打开函数看到的就是红色的提示“sorry, this node is too big to display."分析一下下面的一段，发现是一个循环判断，如果不相等就输出false。所以过大的部分就是对flag内的字符进行变换的部分。让我们试着f5一下转换成伪c代码。如果跳出提示说代码段过大记得百度错误原因更改一下设置。

​	慢慢等待一段时间就可以反编译完成了。反编译完成后我们看一下反编译的伪代码，发现每12条语句可以视作从v1[0 ]到v1[11]的一组运算。所以我们可以大胆猜测语句就是这样排列的，将反编译代码复制下来后我们写一个简易的python脚本将总共的3000句语句变成12组。这样每组都是操作数组中的一个数，一组的语句只有250句。这个脚本请参见divide.py。

​	稍微分析一下其中的两组，我们就可以发现，只有三种运算：v1[i]异或一个常数、++v1[i]、v1[i]^=vi[i-k]。所以我们可以通过穷举的方式逐位穷举得出flag。

​	毕竟反编译出来的是能够直接运行的伪c代码，直接写个c程序跑就完事了。具体过程见res.cpp部分。可以直接拖到结尾看main函数。
