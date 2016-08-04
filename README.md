# setup_nRF52_with_iPhone_5
How to setup nRF52 and test it with iPhone 5

The outcome will be a chat program via WIN10 <-> nRF52 <-> iPhone 5

More detailed instruction can be found here: https://devzone.nordicsemi.com/tutorials/36/

The instruction below are summary of the original instruction.

nRF52
- Download and extract nRF5 SDK 11: https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v11.x.x/nRF5_SDK_11.0.0_89a8197.zip
- Connect the nRF5 DK to the computer with a USB cable
- Flip the power switch in the bottom left corner to "ON"
- Download and install the command line tools executable: https://www.nordicsemi.com/eng/nordic/download_resource/48768/25/20208144
	* Version numbers are [SDK: 11.0.0] and [S130: SDS (SoftDevice Specification) 2.0]
- Run Command line editor (CMD.exe, Komentokehote)
	* nrfjprog --help
	  - If not working and printing the help, check the Path. The instruction is only in Finnish, sorry about that. Google will tell you.
		- Win10 Path: C:\Program Files (x86)\Nordic Semiconductor\nrf5x\bin
		- Go to: Asetukset -> Järjestelmä ja suojaus -> Järjestelmä -> Järjestelmän lisäasetukset -> Lisäasetukset -> Ympäristömuuttujat
		- Path -> Muokkaa
- Install SDK to nRF52
	* nrfjprog --family nRF52 --eraseall
	* nrfjprog --family nRF52 --program [SOFTDEVICE_LOCATION]\s132_nrf52_2.0.0_softdevice.hex
		- SOFTDEVICE_LOCATION = <your installation path>\nRF5_SDK_11.0.0_89a8197\components\softdevice\s132\hex
	* final command in my case: nrfjprog --family nRF52 --program C:\Users\Jari-Pekka\Documents\IoT\nRF52\nRF5_SDK_11.0.0_89a8197\components\softdevice\s132\hex\s132_nrf52_2.0.0_softdevice.hex 
- Install ARM Keil uVision to your PC: https://www.keil.com/arm/demo/eval/arm.htm
- "Open project" with ARM Keil uVision: C:\Users\<username>\Documents\IoT\nRF52\nRF5_SDK_11.0.0_89a8197\examples\ble_peripheral\ble_app_uart\pca10040\s132\arm5_no_packs
	* If "If missing software packs" appears press Yes to install those
	* Go to Project -> Build Target
- Check with devmgmt.msc (Device Manager) what is the correct Port to be used
	* Scroll down and expand Ports (COM & LPT)
	* Jlink CDC UART Port (COM5)
- Install Termite to your PC: http://www.compuphase.com/software_termite.htm
	* Open Termite and click Settings
		* Port: COM5 (or what ever you had in Device Manager)
		* Baud rate: 38400
		* Flow control: RTS/CTS
		* Configuring HWFC in Termite
			+ Make sure the DK is connected to the computer, and the ble_app_uart project is running. LED 1 should be blinking.
			+ under Plug Ins, enable Status LEDs. 
		* Click OK
	* In Termite click on the dark green rectangle above RTS to set this signal high.
- Connecting to the nRF5 DK with iPhone 5
	* download the nRF Toolbox app from App Store
	* Open nRF Toolbox, and tap UART, tap connect
	* Select UART as you BT device
	* click Show Log
	* write a message "hello" from Termite and press enter
	* If everything is ok, you should receive the "hello" message with iPhone 5 UART
	* write a message "hi" from iPhone 5 UART and message should appear to Termite console
