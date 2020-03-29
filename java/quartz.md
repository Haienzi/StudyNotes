### Quartz

#### 核心概念
- Job：表示一个工作，要执行的具体的内容，此接口中只有一个方法。  
  void execute(JobExecutionContext context)
- JobDetail:表示一个具体的可执行的调度程序，job是这个可执行调度程序要执行的内容，还包括了这个任务调度的方案和策略。
- Trigger代表一个调度参数的配置，什么时候去调。
- Scheduler代表一个调度容器，一个调度容器里可以注册多个JobDetail和Trigger.当trigger和jobDetail结合就可以被scheduler调用了。 
