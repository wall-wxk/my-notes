# 事件循环机制

## 任务区分

- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval，IO / UI Rendering
- micro-task(微任务)：Promise，process.nextTick，ajax， Object.observe




## 执行顺序

执行一个宏任务，然后执行清空微任务列表，循环再执行宏任务，再清微任务列表


## node.js事件循环

根据Node.js官方介绍，每次事件循环都包含了6个阶段

- timers 阶段：这个阶段执行timer（setTimeout、setInterval）的回调
- I/O callbacks 阶段：执行一些系统调用错误，比如网络通信的错误回调
- idle, prepare 阶段：仅node内部使用
- poll 阶段：获取新的I/O事件, 适当的条件下node将阻塞在这里
- check 阶段：执行 setImmediate() 的回调
- close callbacks 阶段：执行 socket 的 close 事件回调

## 区别

在Node.js中，microtask会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行microtask队列的任务
