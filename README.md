# cisco
# Understand ASR1000-RP2 CPLD and FPGA Upgrade Common Issues - Cisco
https://www.cisco.com/c/en/us/support/docs/routers/asr-1000-series-aggregation-services-routers/216564-asr1000-rp2-cpld-and-fpga-upgrade-common.html#toc-hId-767007475

# case study - upgrade from asr1002x-universalk9.03.12.00.S.154-2.S-std.SPA.bin" to asr1000rpx86-universalk9.17.06.05.SPA.bin"
# Old : Cisco IOS XE Software, Version 03.12.00.S - Standard Support Release
# New : Cisco IOS Software [Bengaluru], ASR1000 Software (X86_64_LINUX_IOSD-UNIVERSALK9-M), Version 17.6.5, RELEASE SOFTWARE (fc2)
# have to upgrade the ROMMON , CPLD and FPGA version
# As the previous version dont have FPGA version - the device need to load with OS at least asr1000rpx86-universalk9.16 
Old version :
a01.cbjaml04.ml.bb#sh platform
Chassis type: ASR1002-X

Slot      Type                State                 Insert time (ago)
--------- ------------------- --------------------- -----------------
0         ASR1002-X           ok                    3y24w
 0/0      6XGE-BUILT-IN       ok                    3y24w
 0/1      SPA-8X1GE-V2        ok                    3y24w
 0/2      SPA-1X10GE-L-V2     ok                    3y24w
 0/3      SPA-1X10GE-L-V2     ok                    1y22w
R0        ASR1002-X           ok, active            3y24w
F0        ASR1002-X           ok, active            3y24w
P0        ASR1002-PWR-AC      ok                    3y24w
P1        ASR1002-PWR-AC      ok                    3y24w

Slot      CPLD Version        Firmware Version
--------- ------------------- ---------------------------------------
0         14012203            15.3(1r)S
R0        14012203            15.3(1r)S
F0        14012203            15.3(1r)S

a01.cbjaml04.ml.bb#sh hw-programmable all
Hw-programmable versions

Slot              CPLD version              FPGA version
-----------------------------------------------------------
R0                14012203                  N/A
F0                14012203                  N/A
0                 14012203                  N/A
============================================

Procedure should 
1 . be upgrade the ROMMON 
2 . Load the new OS with 9.16
3 . Upgrade the CPLD and FPGA version

to verify is the hw-program is upgrade-able can perform below command :

router #show upgrade hw-programmable file bootflash:asr1000rpx86-hw-programmables.16.11.01.SPA.pkg

After ROMMON , CPLD and FPGA upgrade to the requirement.
New IOS can be load and reboot.
to avoid 2 RE running on diff version IOS, the RE can be manual remove and install back after all RE running is the same IOS


