# STM32 UART + ADC Communication Project

This project demonstrates **UART communication between two STM32 boards**.  
- The **Transmitter (TX)** samples analog data using the ADC and sends it via UART.  
- The **Receiver (RX)** processes the received data and blinks LEDs depending on the value.  

It serves as a simple educational example of:  
- **ADC** (Analog-to-Digital Converter)  
- **UART** (Universal Asynchronous Receiver-Transmitter)  
- **Interrupt-based callbacks** in STM32 HAL  

---

##  Hardware Setup

### Board 1 – Transmitter (TX)
- Samples analog input on **PA1 (ADC)**  
- Sends ADC data through **PA2 (USART2 TX)**  

### Board 2 – Receiver (RX)
- Receives UART data on **PA3 (USART2 RX)**  
- Controls **LEDs (PD12–PD15)** based on the ADC value  

### Pin Mapping

| Function   | Pin   | Board        |
|------------|-------|-------------|
| ADC Input  | PA1   | Transmitter |
| UART TX    | PA2   | Transmitter |
| UART RX    | PA3   | Receiver    |
| LEDs       | PD12–PD15 | Receiver |

---

##  Project Behavior

1. The **TX board** samples an analog voltage on **PA1**.  
2. The 12-bit ADC result is split into 2 bytes and sent via **USART2 TX**.  
3. The **RX board** reconstructs the value and blinks LEDs depending on thresholds:  

   - `> 4000` → Blink **4 LEDs**  
   - `> 3000` → Blink **3 LEDs**  
   - `> 2000` → Blink **2 LEDs**  
   - `> 1000` → Blink **1 LED**  

---

##  Build & Flash Instructions

1. Open the project in **STM32CubeIDE**.  

2. In `main.c`, select the board role by defining one of the following:  
   ```c
   //#define TX_IT   // Uncomment for Transmitter
   #define RX_IT     // Uncomment for Receiver
3. Build and flash the firmware to each board.

4. Connect the hardware:

- **PA2 (TX)** of Transmitter → **PA3 (RX)** of Receiver
- **GND** of Transmitter ↔ **GND** of Receiver
- Provide an analog signal (e.g., potentiometer) to **PA1** on the Transmitter

**Demo**

Increasing the input voltage → More LEDs blink on the RX board.

Thresholds can be modified in HAL_UART_RxCpltCallback() to suit your experiment.

**License**

This project is provided as-is under the STMicroelectronics license.
