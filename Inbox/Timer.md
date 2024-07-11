> Timer Module主要包括三部分：
> * Timer24：主要用于对异步事件进行计时
> * T16PWMx：主要用于PWM和生成循环中断
> * Watchdog：看门狗

# 1. Timer 24
![[Pasted image 20240709104156.png]]

```C
TimerRegs.T24CNTCTRL.bit.OV_INT_ENA = 1;//enable interrupt 
result = TimerRegs.T24CNTCTRL.bit.OV_FLAG;//通过轮询查看是否溢出
```
## 1.1 Prescaler
```C
TimerRegs.T24CNTCTRL.bit.EXT_CLK_SEL = 0;//选择时钟源
TimerRegs.T24CNTCTRL.bit.PRESCALE = 255;//Load with maximum divide ratio
```
> 默认时钟频率15.6MHZ，具体查看datasheet

## 1.2 Capture

```C
TimerRegs.T24CAPCTRL.bit.EDGE = 3; //both edges
```

## 1.3 Compare

# 1.4 Interrupt

# 2. T16PWMx

![[Pasted image 20240709105345.png]]
```C
TimerRegs.T16PWM2CMP0DAT.all = 1587;
TimerRegs.T16PWM2CMP1DAT.all = 0xFFFF;//未用到，为避免影响CMP0，设为最大值
TimerRegs.T16PWM2CMPCTRL.bit.CMP0_INT_ENA = 1;
TimerRegs.T16PWM2CNTCTRL.bit.CMP_RESET_ENA = 1;
TimerRegs.T16PWM2CNTCTRL.bit.SW_RESET = 1;
```

# 3. Watchdog
