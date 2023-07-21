# T9/T9+/S9-works-NOW
A repository trying to make ant miner T9/T9+/S9 run OpenWrt
![github-small](https://cdn.discordapp.com/attachments/857047152684564523/1131909660031590470/FB_IMG_1685144491590.jpg)	
2023/5/27 works!! internet phy ok!!

T9/T9+/S9 control board has very similar layout .Which the firmware can be compatible!

# What is working
| Part | Detail        |
|-----:|---------------|
|  CORE|XC7Z010        (Y)|
|  RAM |512M*2 DDR3    (Y)|
|  ROM |NAND FLASH 128M(N)|
| Ether|B546512e,B50612e/d(Y)|

# How to run prebuilt firmware

you will need to replace uboot.bin+system.bit+u-boot.img unzipped from braiins-os after u use rufus to write the OpenWrt firmware to sd card 

braiins-os:https://drive.google.com/drive/folders/1HSWCoHGiV81ASeOtdmrZhL9fIG85YdeR

pre-build openwrt firmware:https://drive.google.com/file/d/15deutg02OlLBpyRNEkhwHvhg7zQw6uVR/view?usp=drive_link


DEBUG TTL baudrate=115200




# STORY

Back in 2020 I accidentally received some broken Ant Miner t9+, A ASIC Miner got ZYNQ XC7Z010 init, and I want them to have some extra usage for so hard!! So I was thinking about OpenWrt. but the advanced firmware structure of ZYNQ beat me (I only had Android building experience back then). QAQ
2023 after 2.5 years, I saw a news on my smartphone it was about OpenWrt .this made me recall 
my scraped  ASIC miner. this time I have some more experience from building a few smartphone kernels and a few failed x86 Openwrt build.

the hardest part was porting the .dts for Openwrt from braiins os seems that braiins os made some changes to their kernel to make the 5.10 kernel "fully" support the 4.4 kernel .dts structure for zynq on the 5.10 kernel. if you try to build openwrt with old structure .dts the internet bridge Ic won't able to find driver for it self (what I think the reason why internet bridge Ic not working is because "emacps.c" got deleted from 5.10 kernel) 
so I start to port from a similar device already supported by OpenWrt the structure of them, and they were so different from each other, you simply can not leave them 50% new and 50% old. after porting the problem coincidentally back to the internet bridge Ic. I was guessing that caused by RGMII BUS or device id of  Boardcom B546512e,B50612e/d address incorrect or maybe that kernel doesn't even support Boardcom B546512e, B50612e/d, then I start with the simple one. changing the RGMII interface address and hope it works, what I was using is the address from the dts. inside the UBOOT source code but I found that source code from braiins os have two different RGMII interface address  one from the .dts inside UBOOT and it was  0x07 another one from kernel was 0x01 .so I change it from 0x07 to 0x01. this time, I finally get a 3 years project basically working 





