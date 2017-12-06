异步编程模型 (APM) 模式（也称 IAsyncResult 模式），在此模式中异步操作需要 Begin 和 End 方法（比如用于异步写入操作的 BeginWrite 和 EndWrite）。 对于新的开发工作不再建议采用此模式。


Begin OperationName 方法开始异步操作 OperationName，并返回实现 IAsyncResult 接口的对象。 IAsyncResult 对象存储有关异步操作的信息。
AsyncState 
一个特定于应用程序的可选对象，其中包含有关异步操作的信息。
AsyncWaitHandle 
一个 WaitHandle，可用来在异步操作完成之前阻止应用程序执行。
CompletedSynchronously 
一个值，指示异步操作是否是在用于调用 BeginOperationName 的线程上完成，而不是在单独的 ThreadPool 线程上完成。
IsCompleted 
一个值，指示异步操作是否已完成。

Begin OperationName 方法采用该方法的同步版本的签名中声明的任何参数（由值传递或由引用传递）。 Begin OperationName 方法签名中不包含任何输出参数。 Begin OperationName 方法签名另外还包括两个其他参数。 第一个参数定义一个 AsyncCallback 委托，此委托引用在异步操作完成时调用的方法。
 第二个参数是一个用户定义的对象。 此对象可用来向异步操作完成时调用的方法传递应用程序特定的状态信息。 如果 BeginOperationName 方法还采用其他一些操作特定的参数（例如，一个用于存储从文件读取的字节的字节数组），则 AsyncCallback 和应用程序状态对象将是 BeginOperationName 方法签名中的最后两个参数。


End OperationName 方法可结束异步操作 OperationName。 End OperationName 方法的返回值与其同步对应方法的返回值类型相同，并且是特定于异步操作的。
End OperationName 方法采用该方法同步版本的签名中声明的所有输出参数或引用参数。 除了来自同步方法的参数外，EndOperationName 方法还包括 IAsyncResult 参数。 调用方必须将对应调用返回的实例传递给 BeginOperationName。
如果调用 EndOperationName 时 IAsyncResult 对象表示的异步操作尚未完成，则 EndOperationName 将在异步操作完成之前阻止调用线程。 异步操作引发的异常是从 EndOperationName 方法引发的。 未定义多次使用同一 IAsyncResult 调用 EndOperationName 方法的效果。 同样，也未定义使用不是相关 Begin 方法返回的 IAsyncResult 调用 EndOperationName 方法的效果。