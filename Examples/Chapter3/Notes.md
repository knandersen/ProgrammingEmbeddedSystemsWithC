# Notes for Chapter 3 examples

I included all the source- and include-files, but the code from the book can be found in [Src/main.c](Src/main.c):

[ledToggle()](Src/main.c#L64)

[delay_ms()](Src/main.c#L75)

[main()](Src/main.c#L88)

I tried to stay as true to the code from the book. However, I couldn't see a reason to re-write `ledInit()` since that's all taken care of in a much different way by `MX_GPIO_Init()`, which was provided by the boilerplate project from STM32CubeIDE

Actually, this example could have been made a lot simpler, since `ledToggle()` and `delay_ms()` are provided by the boilerplate code through `HAL_GPIO_TogglePin()` and `HAL_Delay()` respectively. Conveniently in VSCode, by right-clicking the function and selecting `Go to Definition`, you can even see how they're implemented.