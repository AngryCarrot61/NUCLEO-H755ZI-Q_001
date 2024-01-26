# NUCLEO-H755ZI-Q_001

I dead-locked two NUCLEO-H755ZI-Q boards, the cores didn't start anymore and I could not reflash them.

I made a simple program flashing LED's from both cores and sending data between the two cores using a struct that resided on the same memory space for both.

After adding some more peripherals, I suddenly got programming errors, like:

"No STM32 targets found"

I needed to use STM32CubeProgrammer to erase the chip, where I only could connect using mode "Power down".

After this, I could download (Download verified successfully), but the cores do not start, and the problem reappears, so some config must be wrong.

Starting server with the following options:
Persistent Mode : Disabled
Logging Level : 1
Listen Port Number : 61234
Status Refresh Delay : 15s
Verbose Mode : Disabled
SWD Debug : Enabled
InitWhile : Enabled

Target no device found

Error in initializing ST-LINK device.
Reason: No device found on target.

I tried several setting in STM32CubeMX, 5V external power, and suning ST-Link V3 probe.


Solved:

void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

  /** Supply configuration update enable
  */
//  HAL_PWREx_ConfigSupply(PWR_LDO_SUPPLY);       /* Wrong */
  HAL_PWREx_ConfigSupply(PWR_DIRECT_SMPS_SUPPLY); /* For the Nucleo board */

How can I recover those?

I found this in the board user manual:
If a deadlock is faced due to a mismatch between the
hardware board setting and the firmware setting (LDO/SMPS),
the user can recover the board by doing the following:
- Power off the board
- Connect CN11 ‘BT0’ pin (BOOT0) to VDD using a wire
- This changes the BOOT0 pin to HIGH instead of LOW and
thus the device boot address is changed to boot address 1
making the bootloader starting in System memory, instead of
starting the firmware in the user Flash (Firmware that is
setting a wrong LDO/SMPS configuration)
- Power on the board and connect using STM32CubeProgrammer
- Erase the user Flash
- Power off the board and remove the wire between BOOT0 and VDD
- The recovery is now completed and the board can be used normally.




