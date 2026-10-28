# 电控组第二次培训作业
- **宁孜轩**
- ***20263008199***
## 流水灯实现思路

本项目使用 STM32CubeMX 配置了 LED0、LED1、LED2 三个 GPIO 输出引脚，并利用 User Label 功能生成对应的宏定义。


### 非阻塞延时实现原理(代码部分使用了AI工具)

**加分项**中不使用 `HAL_Delay()`，而是通过 `HAL_GetTick()` 获取系统启动后的毫秒数，每 500ms 判断一次时间差，期间 CPU 可以执行其他任务。核心代码如下：

```c
if (HAL_GetTick() - lastTick >= 500) {
    lastTick = HAL_GetTick();
    // 切换 LED 状态的逻辑
}