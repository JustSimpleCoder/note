context 包理解.md


### context ###

使用 wg.add()  wg.done()  wg.wait()  可以满足已知 goroutine 数量的并发管理.任务处理等待.

context 解决未知数量的 goroutine && goroutine 多层嵌套情况中的等待, 取消 goroutine后子携程的退出.


** 多问一下为什么,世界上没有平白无故的代码  哈哈 **  
