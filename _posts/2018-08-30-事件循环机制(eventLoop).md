### 事件循环（EventLoop）机制
js引擎为单线程，意味着所有的任务最终都会在js引擎（主线程）中排队执行。而js中的任务又可以分为同步和异步两种。这两种任务都基于事件循环机制
来执行。
> 同步任务

    同步任务作为首要任务在主线程执行
> 异步任务
    
    异步任务被分配到另外一个线程管理的任务队列中等待处理。当异步任务符合执行
    条件时，会在任务队列中添加可执行'事件'。当主线程中的任务执行完毕后，会将
    任务队列中的可执行事件放入主线程中执行。
#### 异步的实现机制
> macro-task(task)宏任务
    
    script, setTimeout, setInterval, setImmediate, I/O,
    UI rendering 
> micro-task(job) 微任务    
    
    process.nextTick, MutationObserver, promise, Object.observe
#### 事件循环执行机制
一个事件循环中的大致过程

    1. 执行主线程中的任务
    2. 到micro-task中读取可执行任务
    3. 主线程执行micro-task中读取到的任务
    4. 主线程到macro-task中读取可执行任务
    5. 执行从macro-task中读取到的任务
    6. ...
    7. 返回第一步
注意：
    由于UI rendering是属于macro-task,在micro-task之后执行，所以需要在UI渲染之前的回调，应该在micro-task中执行。并且micro-task任务队列过长，也会导致UI渲染被阻塞    
    
    