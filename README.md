# STM32 User Button Interrupt (EXTI) – BSP 기반 구현

> STM32 NUCLEO 보드에서 User Button(PC13)을  
> 외부 인터럽트(EXTI)로 처리하여  
> LED2(PA5)를 토글하는 임베디드 펌웨어 실습

**Interrupt-driven GPIO 설계와 IRQHandler–Callback 구조 이해를 목표로 함**


## 🎯 Why This Project?

이 프로젝트는 단순 GPIO 제어가 아닌,
STM32에서 외부 인터럽트(EXTI)가 어떻게 동작하는지를
IRQHandler → HAL Handler → Callback 구조로 이해하기 위해 진행하였다.

Polling 방식이 아닌 Interrupt 기반 설계를 통해
CPU 자원 효율성과 구조적 안정성을 확보하는 것을 목표로 했다.


## 🔍 Key Implementation

### EXTI Interrupt Flow

```c
void EXTI4_15_IRQHandler(void)
{
    HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_13);
}
```

```c
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{
    if (GPIO_Pin == USER_BUTTON_PIN)
    {
        BSP_LED_Toggle(LED2);
    }
}
```

## ✅ Result

- Button input is handled via EXTI interrupt
- Main loop remains empty (event-driven design)
- LED toggles reliably on each button press
- IRQHandler and Callback roles are clearly separated
