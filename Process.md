# Process
Since I have never tried to write updated examples or updating a toolchain for a book before, I thought it might be useful for myself, and potentially others, to document the process in the form of a diary. I didn't start documenting the process until March 4th, so please excuse the lack of detail until then.

## xx.12.2020

Decided that I wanted to learn how to program C for small microcontrollers. I like projects like MicroPython, but working on it made me interested in what is going on at the lower level. Searching online for recommendations for good books about C for embedded systems, I came across Barr & Massa's Programming Embedded Systems with C and GNU Development Tools. People online highly recommended it, with the only criticism being that the development board used can't be obtained anymore.

I set an ambition to learn C using this book, and use the opportunity to challenge myself to use a modern development board to complete all the examples in the book. I really like the STM32-suite from ST, have some experience working with them from my professional career, and they seem to have gained popularity the recent years. Their development boards are also fairly priced, hopefully lowering the entry for people who are excited to get into this field.

Because I have a personal ambition about doing something with wireless communication, I opted for the STM32WB55 NUCLEO development board.

As for the toolchain, I wanted it to be free, so decided early to go for something that would work with VSCode since that's become my favorite IDE, and their extensions platform is great.

In summary, my setup:
- Computer: MacBook 15" 2012 running MacOS Catalina
- IDE: VSCode
- Development Board: ST [P-NUCLEO-WB55](https://www.st.com/en/evaluation-tools/p-nucleo-wb55.html)
- Book: [Programming Embedded Systems: With C and GNU Development Tools - Second Edition](https://www.amazon.com/gp/product/0596009836/ref=ppx_yo_dt_b_asin_title_o09_s00?ie=UTF8&psc=1)

## 30.12.2020

- Received the [P-NUCLEO-WB55](https://www.st.com/en/evaluation-tools/p-nucleo-wb55.html).

## 06.01.2020

- Attempted to install STM32CubeMX 5.5.0, but [ran into problems because of MacOS Catalina](https://community.st.com/s/question/0D50X0000BXlh6q/problem-loading-stm32cubemx-on-mac), where the installer wouldn't run. 

## 12.02.2020

Searching in the VSCode extensions marketplace, I found the [stm32-for-vscode](https://marketplace.visualstudio.com/items?itemName=bmd.stm32-for-vscode). Installed everything listed in the Prerequisites-section:
- STM32CubeMX [(found a fix)](https://marketplace.visualstudio.com/items?itemName=bmd.stm32-for-vscode)
- Cortex-Debug extension
- ST-Link (from Github, more on that later)
- GNU Arm Embedded Toolchain

Set up `MyFirstProject` using STM32CubeMX as per the `stm32-for-vscode` extension's instructions.
Built the project using VSCode, but couldn't figure out how to flash the `.bin`-file, since I had only ever worked with `.dfu`-files

## 04.03.2020

According to the [dfu-util documentation](http://dfu-util.sourceforge.net/dfuse.html), when flashing a `.bin`, you have to supply what address to start at. Found an article online explaining that `STM32CubeProgrammer` can be used to find that address for any STM32-board. I connected the board and determined the start-address for the STM32WB55 is `0x08000000`.

Installing `STM32CubeProgrammer`, like `STM32CubeMX` required the the `java -jar ./SetupSTM32CubeProgrammer-2.4.0.exe`-"hack".

With this I could finally flash the board using the bin-file:

    MyFirstProject kevinandersen$ dfu-util --alt 0 -D ./build/MyFirstProject.bin -s 0x08000000
    dfu-util 0.9
    
    Copyright 2005-2009 Weston Schmidt, Harald Welte and OpenMoko Inc.
    Copyright 2010-2016 Tormod Volden and Stefan Schmidt
    This program is Free Software and has ABSOLUTELY NO WARRANTY
    Please report bugs to http://sourceforge.net/p/dfu-util/tickets/
    
    dfu-util: Invalid DFU suffix signature
    dfu-util: A valid DFU suffix will be required in a future dfu-util release!!!
    Opening DFU capable USB device...
    ID 0483:df11
    Run-time device DFU version 011a
    Claiming USB DFU Interface...
    Setting Alternate Setting #0 ...
    Determining device status: state = dfuIDLE, status = 0
    dfuIDLE, continuing
    DFU mode device DFU version 011a
    Device returned transfer size 1024
    DfuSe interface name: "Internal Flash   "
    Downloading to address = 0x08000000, size = 11664
    Download        [=========================] 100%        11664 bytes
    Download done.
    File downloaded successfully

And just like that, the first hello world example from `Chapter 3` was done!

# 05.03.2020

Added this document and Chapter 3 examples tonight. 

As I discovered that the two main functions written in the examples were already provided by the boilerplate-project, I decided to write [notes](Examples/Chapter3/Notes.md) to allow readers to make their own choice whether they want to write everything themselves, or take advantage of the convenient functions already provided.