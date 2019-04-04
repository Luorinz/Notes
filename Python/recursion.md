In Python, head recursion is different from tail recursion.

head recursion needs to reach the bottom to do all the calculation, thus the memory will exceed the python limit.

tail recursion finish all the operations before calling next layer of recursion, thus losing the calling stack. Tail recursion can ignore the Python recursion limit.



####Difference

```pla
头递归：递归发生在函数的其他处理代码之前（或理解为，递归发生在函数的头部或顶部）

尾递归：与头递归正好相反，递归发生在函数其他处理代码的后面（或理解为，递归发生在函数的尾部）	
	
	头递归与尾递归相比，将处理过程置后，从递归的目的出发，将大问题细化成小问题，细化到可以解决的程度后，将结果一层层反馈，而较大细度的问题可以直接将该结果作为已知数据进行计算使用，使递归过程更加方便清晰。尾递归过程是先对当前细度的问题进行处理，但是该结果只是一个暂时值，需要将问题一层层细化后，每层对当前的暂时值进行计算操作，得到最终的结果，可以看做是一个不断修正的过程，所以尾递归过程相对头递归来说，计算较慢，所占资源也会较多。所以，建议采用头递归。

  一般来说，头递归更加体现了递归的思想，大递归思想，在使用递归解决问题时，我们的思维应该有别于其他的函数的实现过程，在实现其他函数时，我们会细化各个过程，用程序化的思维来思考各个步骤，这个思维用在递归函数时，将会以尾递归的方式呈现出来，因为，我们都想尽可能完成函数功能，就会不自觉的将可以实现的功能写在了前面。大递归的思想就是让我们多在意递归函数的意义，我们在用递归函数实现某一功能时，应该时时牢记该递归函数的功能，多关注该问题与子问题之间的关系，尽可能用头递归的方式实现递归函数。
```
---------------------
作者：fight_girl 
来源：CSDN 
原文：https://blog.csdn.net/fight_girl/article/details/78676985 
版权声明：本文为博主原创文章，转载请附上博文链接！