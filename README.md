# NUCLEO-H755ZI-Q_001
Cores won't start anymore Nucleo-H755ZI-Q got brikked?

I have made some simple program flashing LED's from both cores and sending data between the two cores using a struct that resided on the same memory space for both.

After adding some more peripherals, I suddenly got programming errors, like:

"No STM32 targets found"

I needed toi use STM32CubeProgrammer to erase the chip, where I only could connect using mode "Power down".

After this, I could download (Download verified successfully), but the cores do not start.

After a few attempts, I again get these errrors.

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

I destroyed two NUCLEO-H755ZI-Q boards.

I'm out of ideas.

How can I recover those?

I don't hope the MCU get easily detroyed.



