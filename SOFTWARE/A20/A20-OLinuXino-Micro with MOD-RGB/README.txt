This is a tutorial how to build a simple project for A20-OLinuXino-Micro Rev.F with demo for MOD-RGB Rev.B.

In addition to the boards you also need SD card with Debian image (tested with "A20_debian_kernel_3_4_LAN_USBx2_Cards_LCD_HDMI_SATA_TS_X_GPIO_OTG_MIC_Video_accel_release7.img"), LAN, USB serial cable (like USB-SERIAL-CABLE-F) and a LED strap (the demo is tested with EIAJ-RRM-12-B: http://www.dx.com/p/zhuoyao-waterproof-72w-5400lm-300-x-smd-5050-led-rgb-decoration-light-strip-dc-12v-5m-269903#.U9JT5PmSyac).

1) Connect all the hardware and supply the board - USB serial cable to UART0 - TX0, RX0 and GND; and the MOD-RGB to UEXT1. On the MOD-RGB UPWR_E and DMX_EN jumpers must be opened. Power up the board and connect LED strap's inputs (12V, Red, Green and Blue) to the connector.

2) Open a console terminal program (like PuTTY, HyperTerminal etc.) with baudrate 115200

3) Wait until the board is initialized (you must see this: "root@a20-OLinuXino:~#")

4) Make a directory where the project files will be stored (this step is optional and it's only for better arrangement of the files in the directory tree). You can do this with the command:
Input:

	mkdir MOD-RGB

5) Set the created directory as current directory:
Input:

	cd MOD-RGB

6) Since we are going to download the source and header files from GitHUB we must enable the internet connection:
Input:

	ifup eth0

6.1) Allow the https protocol. (This step could be skipped if https is allowed by default)

Input

	export https_proxy="192.168.0.1:80"

7) Download the files from GitHUB:
Input:

	wget <URL>
	
In order to get the URL, go to GitHUB find the directory of the project: https://github.com/OLIMEX/OLINUXINO/tree/master/SOFTWARE/A20/A20-OLinuXino-Micro%20with%20MOD-RGB; select the file you want to download and click on the "Raw" button; then copy the URL and trigger the command (wget) in the console of A20-OLinuXino-Micro. Do this for the four files: makefile; i2c.c; i2c.h; RGB.c.

8) Just to make sure everything is fine and all three files are downloaded check the content of the directory:
Input:

	ls

The respond of the host board should be:
Output:

	i2c.c  i2c.h  makefile  RGB.c

9) Compile all source files:
Input:

	make

A 3 new files (2 objects and 1 executable) should appear. We check the content of the directory again:
Input:

	ls
	
Output:

	i2c.c  i2c.h  i2c.o  makefile  MOD-RGB  RGB.c  RGB.o

10) Execute the generated file
Input:

	./MOD-RGB

You will be prompted for the number of I2C which is about to be used. 

	I2C-bus:

On UEXT1 it is I2C2

After this a menu will be shown with few options:
	MOD-RGB
	--------------------

	1. START PWM
	2. STOP PWM
	3. SET RGB
	4. START AUDIO
	5. STOP AUDIO
	6. SET ADDRESS
	0. EXIT

In order to set the color of the LEDs on the strap we must choose option 3.
The next step is to input the I2C address of the MOD-RGB (by default it is 0x20) and the values for Red, Green and Blue.
	Address:
	R:
	G:
	B:

2014/07/25
