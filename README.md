# Lenovo Win7 Slim Down
----
## Overview

After performing a system restore/reinstall using the Lenovo Windows 7 Recovery Media, interrupt the initial reboo  and patch the system to prevent the installation of most, if not all of the Lenovo drivers and bloatware applications. This may not play well when reinstalling on bare metal but when virtualizing, the payoff is remarkable.

## Requirements / Prerequisites

- Lenovo Windows 7 Recovery Media (Other OS's may work too)
-- Windows 7 Pro CD 1/2
md5: a4209af89197e52a8c35bca5b4b4e7a6
sha512: 454b8f598e5c19cd85d3cf54537b2eb793576b45bc837f7d8316671f8cc99834e3ccbc9ef08284b9448f404c0751d325c0bea199ba22f954ee90f4bc8d78ca1f
-- Windows 7 Pro CD 2/2
md5: 9fe5d2482b3895bfefe7518bb0af4e1f
sha512: 40957c1e395166e9a1fe398401f4e93982c4754b5fcaf55f5fc7f34032ed7abdab86744f4eabe9d4061c976327d4d15ee1b0f6749cdc052d022ef9210b5594e2
-- Windows 7 Pro CD 1/1
md5: 5d22c93dc1d2aaa9fac826fea385f4ee
sha512: 7c08e5de3b2b63addfac616e0f3137576d3db37353a3986690fc78b74532c85863172e41d59e95849e28537046f795b8eab063c9ca40005601b09c510ca59455

- Linux Live CD/DVD (Other live OS's may work too)

## Details

1. After performing a system reinstall/restore using the "Windows 7 Recovery Media for Windows 7 Products", interrupt the initial reboot process and mount the new 'C:', it will be the 2nd partition, ie /dev/sda2

2. From the root of the new 'C:', apply the downloaded patch:

        $ patch -p1 < [path_to_patch_file]

3. Unmount the drive and boot the Windows 7 system and let it finish the install process.

For a detailed step-by-step guide, depending on how you're virtual machines are setup, see DETAILED_HOW-TO

## Patch Contents

The following will not be installed after patching:

| FILE                                                            | Purpose/Observation                          |
| ---                                                             | ---                                          |
| SWTOOLS/antivirus/NORTONIS/ALL/MODULECUST/SETUP.CMD             | Pre install Norton Internet Sec 2012         |
| SWTOOLS/Apps/Adobe/AdobeReader/MODULECUST/InstallAdbeRdrX.cmd   | Install Adobe Reader                         |
| SWTOOLS/Apps/Adobe/AdobeReader/MODULECUST/SetupMUI.cmd          | Install Adobe Reader                         |
| SWTOOLS/Apps/DMFSD/Utilities/LS_1.4.124.1/Install.bat           | Install LightScribe Software                 |
| SWTOOLS/Apps/Evernote/Evernote-Install-for-Lenovo.cmd           | Evernote                                     |
| SWTOOLS/DRIVERS/ETHINTEL/APPS/SETUP/PUSH/pushcopy.bat           | Install Intel Pro1000 Ethernet drivers       |
| SWTOOLS/DRIVERS/ETHINTEL/APPS/SETUP/PUSH/Win32/Install.bat      | Install Intel Pro1000 Ethernet drivers       |
| SWTOOLS/DRIVERS/ETHINTEL/APPS/SETUP/PUSH/Winx64/Install.bat     | Install Intel Pro1000 Ethernet drivers       |
| SWTOOLS/DRIVERS/RapidBoot/setup.cmd                             | Setup/Install Rapidboot                      |
| SWTOOLS/LenovoWelcome/Install.cmd                               | Lenovo Welcome OOBE                          |
| SWTOOLS/readyapps/usrguide/UGsetup.bat                          | Install Lenovo UserGuide                     |
| SWTOOLS/skype/Skype_Setup.bat                                   | Skype Setup                                  |
| SWTOOLS/WindowsLive_2011/SetForDefaultUser.cmd                  | Windows Live                                 |
| SWTOOLS/WindowsLive_2011/SETUP.CMD                              | Windows Live                                 |
| SWWORK/1STBOOT/DAD016B.cmd                                      | Fix for issue with HDD Pass Detection        |
| SWWORK/1STBOOT/devicemeta.cmd                                   | Windows Device Metadata Store                |
| SWWORK/1STBOOT/DiskUpdate.cmd                                   | ????                                         |
| SWWORK/1STBOOT/DISKUPDT/DiskUpdate.bat                          | ????                                         |
| SWWORK/1STBOOT/LR3GV4AX.CMD                                     | AppShopLauncher for Windows 7                |
| SWWORK/1STBOOT/MSSupCaseNO.CMD                                  | Workaround for MS IE FAV Issue               |
| SWWORK/1STBOOT/Theme1stbootFix.cmd                              | Theme Customization at 1st Boot              |
| SWWORK/ADOWORK0/DELFAV.CMD                                      | DELFAV Command File to detect language       |
| SWWORK/ADOWORK0/localeid.cmd                                    | ????                                         |
| SWWORK/APP1/0VPOWER.CMD                                         | Win7 ThinkPad Default Power Scheme CPP       |
| SWWORK/APP1/checkrecovery.cmd                                   | Check for recovery mode                      |
| SWWORK/APP1/LR39J2A2.CMD                                        | DisplayLink Core Software for ThinkPad       |
| SWWORK/APP1/LR39W1A1.CMD                                        | ThinkPad Power Manager                       |
| SWWORK/APP1/LR3PK9A1.CMD                                        | ThinkPad Power Manager -Source               |
| SWWORK/APP1/M7CBQ003.CMD                                        | WIN7 .NET 4 Language Packs Install           |
| SWWORK/APP1/ZREC65ZA.cmd                                        | SM BUS/BIOS 1020 DRIVER PATCH for win7       |
| SWWORK/APP2/LROHGJA2.CMD                                        | Theme Customization                          |
| SWWORK/APP2/MyLenovoCloud.CMD                                   | Add MyLenovoCloud link                       |
| SWWORK/APP3/LR34P7A2.CMD                                        | Google Desktop Additions                     |
| SWWORK/APP3/LR3JECA2.CMD                                        | Lenovo Solution Center -Source               |
| SWWORK/APP4/LR39Q1A1.CMD                                        | ThinkVantage Comm Utility Install            |
| SWWORK/APP4/LR3B4MA1.CMD                                        | ThinkVantage Comm Utility Source             |
| SWWORK/APP4/LR3JD2A2.CMD                                        | Lenovo Solution Center -Install              |
| SWWORK/APP4/LR3JQ8A2.CMD                                        | Tiles                                        |
| SWWORK/APP4/LS2JT6A2.CMD                                        | ThinkVantage Fingerprint Software            |
| SWWORK/APP4/tvsu40.cmd                                          | TVSU4.0 (Think Vantage System Update)        |
| SWWORK/APP5/4LR2ZO3A2.CMD                                       | Acrobat Reader X                             |
| SWWORK/APP5/DelFolder.cmd                                       | Del Adobe Folder                             |
| SWWORK/APP5/LR2D97A2.CMD                                        | Tiles                                        |
| SWWORK/APP5/LR2DWDA2.CMD                                        | X-Rite Pantone Color Calibrator              |
| SWWORK/APP5/LR2RYCA0.CMD                                        | Intervideo WinDVD 10 SD - CPP2               |
| SWWORK/APP5/LR2ZX3A2.CMD                                        | Evernote                                     |
| SWWORK/APP5/LR33H5A0.CMD                                        | Intervideo DMF 7 SD - CPP2                   |
| SWWORK/APP5/LR35A9A2.cmd                                        | IE favorite for Google PCR remove bing       |
| SWWORK/APP5/LR3LZ1A2.CMD                                        | RapidBoot HDD Accelerator                    |
| SWWORK/APP5/LRJQANA2.CMD                                        | Lenovo Welcome                               |
| SWWORK/APP5/LRWJJ9A2.CMD                                        | Skype                                        |
| SWWORK/APP5/LRXYG8A2.CMD                                        | Lenovo Message Center Plus                   |
| SWWORK/APP5/LRZQPAA2.CMD                                        | Win7-Help and Support -THINKPAD              |
| SWWORK/APP5/LS2JU3A2.CMD                                        | ThinkVantage Fingerprint Software Win7       |
| SWWORK/APP6/LR2DNDA2.cmd                                        | Google Chrome and Toolbar                    |
| SWWORK/APP6/LR2J6EA2.CMD                                        | ThinkVantage Lenovo Mobile BB Activate       |
| SWWORK/APP6/LR2J89A2.CMD                                        | Lenovo User Guide Viewer Source              |
| SWWORK/APP6/LR2VO3A0.CMD                                        | Intervideo BurnNow SD                        |
| SWWORK/APP6/LROBX5A2.CMD                                        | Warranty Viewer                              |
| SWWORK/APP6/LROBX6A2.CMD                                        | Warranty Viewer                              |
| SWWORK/APP6/M7JLCS07.CMD                                        | SugarSync                                    |
| SWWORK/APP6/tvtrnr45.cmd                                        | Rescue and Recovery 4.5                      |
| SWWORK/APP6/Z007004A.cmd                                        | ThinkVantage Lenovo Mobile BB Activate       |
| SWWORK/APP7/LR2GN6A2.CMD                                        | Windows Live Essentials 2011 Custom          |
| SWWORK/APP7/LR2J97A2.CMD                                        | Lenovo User Guide Viewer Installer           |
| SWWORK/APP7/LR2T68A2.CMD                                        | Lenovo Registration                          |
| SWWORK/APP7/LR3EA2A2.CMD                                        | Warranty Viewer - Files                      |
| SWWORK/APP7/LR3PR3A2.CMD                                        | Lenovo User Guide                            |
| SWWORK/APP7/LR3RW5A1.CMD                                        | ThinkVantage Access Con v5.92 for Win7       |
| SWWORK/APP7/LR3SX1A1.CMD                                        | Patch fix Pana ODD S3 BSOD issue             |
| SWWORK/APP7/tvtpwm40.cmd                                        | Password Manager 4.0                         |
| SWWORK/APP8/rec7burncd.cmd                                      | REC7BURNCD FOR Windows 7                     |
| SWWORK/APP8/Z936025P.cmd                                        | running Z936025P.cmd                         |
| SWWORK/APP9/AVNISALL.CMD                                        | Norton Internet Security 2012 30Days         |
| SWWORK/APP9/LR2IC7A2.CMD                                        | ThinkPad Lenovo ThinkVantage Tools 3.2       |
| SWWORK/APP9/LR2XCBA2.CMD                                        | Symantec VIP                                 |
| SWWORK/APP9/LR39XAA1.CMD                                        | RapidBoot 1.20                               |
| SWWORK/APP9/LS2QR2A2.CMD                                        | WiMAX Tutorial Video Gadget                  |
| SWWORK/APP9/rec7burncd.cmd                                      | REC7BURNCD FOR Win7                          |
| SWWORK/APP9/SymSilent.CMD                                       | SymSilent for Norton 2012                    |
| SWWORK/APP9/tvsu40.cmd                                          | TVSU4.0                                      |
| SWWORK/AUDIO/LR3RJ2A1.CMD                                       | Realtek Audio driver with Dolby Advance Audio|
| SWWORK/BurnNowSD/setup.cmd                                      | Installing CD-RW applications                |
| SWWORK/ChromeFavorite/Language.CMD                              | Detect the country Specific Lenovo Fav Links |
| SWWORK/ChromeFavorite/Setup.CMD                                 | Lenovo Chrome                                |
| SWWORK/CTRLWOL.CMD                                              | WOLENABLE script for Energystar compliance   |
| SWWORK/C/WINDOWS/cleanup.cmd                                    | ????                                         |
| SWWORK/C/WINDOWS/CLNDR.CMD                                      | ????                                         |
| SWWORK/C/WINDOWS/MFGCLEAN.CMD                                   | ????                                         |
| SWWORK/DMFSD/setup.cmd                                          | Installing DVD-RW applications               |
| SWWORK/DOWORK2/LR2QE2A2.CMD                                     | Adobe Flash Player 10.0.32.18                |
| SWWORK/DOWORK2/LR2ZO3A2.CMD                                     | Delete Acrobat Reader X launch file          |
| SWWORK/DOWORK2/Office14oobe.en-us.cmd                           | Microsoft Office 2010 14.0 OOBE MSP          |
| SWWORK/DOWORK3/relmbfolder.cmd                                  | Remove LMBA Empty folder                     |
| SWWORK/DOWORK4/DelLSCDecktopIcon.CMD                            | Lenovo Solution Center remove desktop icon   |
| SWWORK/DOWORK4/M7CR23A.CMD                                      | ????                                         |
| SWWORK/DOWORK4/ZDelOemOffice.cmd                                | Remove office source after audit             |
| SWWORK/DOWORK6/ClearCache.CMD                                   | ClearCache                                   |
| SWWORK/factory/doing_backup.cmd                                 | Create recovery image                        |
| SWWORK/FPSINSTALL/DTFPS.CMD                                     | Fingerprint Software (pre-install) for Win7  |
| SWWORK/FPSINSTALL/TPFPS.CMD                                     | Fingerprint Software (pre-install) for Win7  |
| SWWORK/FPSReadyInstall/DTFPSReady.CMD                           | Ready App TPFPS                              |
| SWWORK/FPSReadyInstall/TPFPSReady.CMD                           | Google Desktop Additions for Windows Win7    |
| SWWORK/H_and_S/setup.bat                                        | Lenovo Help and Support                      |
| SWWORK/LR29ROA1.BAT                                             | ThinkPad Wireless LAN - Realtek              |
| SWWORK/LR29ROA1.CMD                                             | ThinkPad Wireless LAN – Realtek              |
| SWWORK/LR2EJQA1.BAT                                             | Intel Wireless LAN (11agn)                   |
| SWWORK/LR2EJQA1.CMD                                             | Intel Wireless LAN (11agn)                   |
| SWWORK/LR2ENPA1.BAT                                             | PMDriver                                     |
| SWWORK/LR2EUNA1.BAT                                             | ThinkPad Bluetooth Software                  |
| SWWORK/LR2EUNA1.CMD                                             | ThinkPad Bluetooth Software                  |
| SWWORK/LR2IQDA1.BAT                                             | Sierra Wireless MC8355 - Gobi 3000           |
| SWWORK/LR2IQDA1.CMD                                             | Sierra Wireless MC8355 - Gobi 3000           |
| SWWORK/LR33TEA1.BAT                                             | ThinkVantage Access Con for Win7             |
| SWWORK/LR33TEA1.CMD                                             | ThinkVantage Access Con for Win7             |
| SWWORK/LR33YJA1.BAT                                             | ThinkPad - Synaptics UltraNav Driver         |
| SWWORK/LR33YJA1.CMD                                             | ThinkPad - Synaptics UltraNav Driver         |
| SWWORK/LR35A9A2/Accelerators/Accelerators_Setup.cmd             | IE Accelerators                              |
| SWWORK/LR35A9A2/TRANSURL.CMD                                    | Specific Lenovo Favorites Links              |
| SWWORK/LR38W1A1.BAT                                             | Thinkpad Ricoh Multi Card Reader Driver      |
| SWWORK/LR38W1A1.CMD                                             | Thinkpad Ricoh Multi Card Reader Driver      |
| SWWORK/LR38XBA1.BAT                                             | Thinkpad Ricoh Integrated Camera Driver      |
| SWWORK/LR38XBA1.CMD                                             | Thinkpad Ricoh Integrated Camera Driver      |
| SWWORK/LR38XBA1/Install.bat                                     | ????                                         |
| SWWORK/LR38YCA1.BAT                                             | Thinkpad Intel USB3.0 Driver                 |
| SWWORK/LR38YCA1.CMD                                             | Thinkpad Intel USB3.0 Driver                 |
| SWWORK/LR39G6A1.BAT                                             | Ethernet Pro1000 drivers                     |
| SWWORK/LR39L7A1.BAT                                             | Ericsson H5321gw Wireless WAN Driver         |
| SWWORK/LR39L7A1.CMD                                             | Ericsson H5321gw Wireless WAN Driver         |
| SWWORK/LR39S3A1.BAT                                             | ????                                         |
| SWWORK/LR39YAA1.BAT                                             | ThinkPad Intel AMT 8.0                       |
| SWWORK/LR39YAA1.CMD                                             | ThinkPad Intel AMT 8.0                       |
| SWWORK/LR3CV4A1.BAT                                             | DisableAMT Profile Sync Pop-up in Windows 7  |
| SWWORK/LR3CV4A1.CMD                                             | DisableAMT Profile Sync Pop-up in Windows 7  |
| SWWORK/LR3EZ1A2/setBIOSxx.cmd                                   | Disable "OS Detect" in BIOS Switch Graphics  |
| SWWORK/LR3ICBA1.BAT                                             | Intel(R) Wireless Display (Windows 7)        |
| SWWORK/LR3ICBA1.CMD                                             | Intel(R) Wireless Display (Windows 7)        |
| SWWORK/LR3SP4A1.BAT                                             | Registry Patch to Disable Instant Internet   |
| SWWORK/LR3SP4A1.CMD                                             | Registry Patch to Disable Instant Internet   |
| SWWORK/LRBKG4A1.BAT                                             | DisableAMT Profile Sync Pop-up in Windows 7  |
| SWWORK/LRBKG4A1.CMD                                             | DisableAMT Profile Sync Pop-up in Windows 7  |
| SWWORK/LRNQFFA1.BAT                                             | Intel Rapid Storage Technology Console       |
| SWWORK/LRNQFFA1.CMD                                             | Intel Rapid Storage Technology Console       |
| SWWORK/LRZMJLA1.BAT                                             | ????                                         |
| SWWORK/LS2BYHA1.BAT                                             | Intel Rapid Storage Technology Driver        |
| SWWORK/LS2BYHA1.CMD                                             | Intel Rapid Storage Technology Driver        |
| SWWORK/LS2BYHA1/PREPARE/install.cmd                             | rundll32.exe setupapi.dll,InstallHinfSection |
| SWWORK/LS2BYHA1/PREPARE/uninstall.cmd                           | undll32.exe setupapi.dll,InstallHinfSection  |
| SWWORK/LS2KTJA1.BAT                                             | ThinkVantage Active Protection System        |
| SWWORK/LS2KTJA1.CMD                                             | ThinkVantage Active Protection System        |
| SWWORK/LS2KU9A1.BAT                                             | ThinkVantage Active Protection System        |
| SWWORK/LS2KU9A1.CMD                                             | ThinkVantage Active Protection System        |
| SWWORK/LS39KFA1.BAT                                             | ThinkPad Video Feature (Chief River)         |
| SWWORK/LS39KFA1.CMD                                             | ThinkPad Video Feature (Chief River)         |
| SWWORK/LS3QB2A1.BAT                                             | ThinkPad Video Feature (NV 52/5400M Optimus) |
| SWWORK/LS3QB2A1.CMD                                             | ThinkPad Video Feature (NV 52/5400M Optimus) |
| SWWORK/LS3QB2A1/Setup.bat                                       | Installing drivers. Please wait.             |
| SWWORK/LS3RI3A1.BAT                                             | ThinkPad VidFea (NV Quadro 11/2100M Optimus) |
| SWWORK/LS3RI3A1.CMD                                             | ThinkPad VidFea (NV Quadro 11/2100M Optimus) |
| SWWORK/LS3RI3A1/Setup.bat                                       | Installing drivers. Please wait.             |
| SWWORK/LSTAK3A0.BAT                                             | ThinkPad SmartCard Reader Driver             |
| SWWORK/LSTAK3A0.CMD                                             | ThinkPad SmartCard Reader Driver             |
| SWWORK/MFGCLEAN/cleanup.cmd                                     | ????                                         |
| SWWORK/NETWORK/LS3S32A2.CMD                                     | ExpressCache                                 |
| SWWORK/OEMOffice14/en-us/oemsetup.en-us.bat                     | Office 14                                    |
| SWWORK/OEMOffice14/Office_2010_RTC_Replicator.cmd               | Office 14                                    |
| SWWORK/OOBE/BALANCE.CMD                                         | OOBECMD RESET POWER BALANCED SCHEME          |
| SWWORK/OOBE/BCDCLEAN.CMD                                        | Boot Config Data                             |
| SWWORK/OOBE/POWER.cmd                                           | Reset OOBE                                   |
| SWWORK/OS/dotNetFx40_Full.CMD                                   | ????                                         |
| SWWORK/OS/LR3EZ1A2.CMD                                          | Disable OS Detection for Switchable Graphics |
| SWWORK/OS/M7D002A.CMD                                           | TOUCH                                        |
| SWWORK/OTHER/LR2ENPA1.CMD                                       | ThinkPad PM Driver                           |
| SWWORK/OTHER/LR2QH2A1.CMD                                       | Enable Maximum Power Saving on WiFi Adapters |
| SWWORK/OTHER/LR39G6A1.CMD                                       | ThinkPad Intel PRO/1000 LAN Adapter Software |
| SWWORK/OTHER/LR3J7GA1.CMD                                       | Lenovo Base Utility Package                  |
| SWWORK/OTHER/LRZMJLA1.CMD                                       | Intel Chipset Support                        |
| SWWORK/POWER/PWRPOL.BAT                                         | THINKPAD DEFAULT POWER SETTINGS Vista RTM    |
| SWWORK/SRV1/LR35A9A2.CMD                                        | IE favorite for Google PCR                   |
| SWWORK/SRV2/IE90_WINDOWS_Update.CMD                             | installs IE 90 Lang Pack                     |
| SWWORK/SRV3/B7DIE0A1.CMD                                        | installs IE 90 Lang Pack                     |
| SWWORK/SRV3/themeset.cmd                                        | Lenovo Themes                                |
| SWWORK/SRV4/LR35A9A2.CMD                                        | IE favorite for Google PCR - Installation    |
| SWWORK/SRV4/LR35B3A2.CMD                                        | Chrome Favorite                              |
| SWWORK/SRV5/IE90_Update_US.CMD                                  | installs IE 90 Lang Pack                     |
| SWWORK/SRV5/OFFQFES.CMD                                         | File Called by servicing qfe installer       |
| SWWORK/SUITES/Office14setup.en-us.cmd                           | Microsoft Office 2010 14.0 RC1               |
| SWWORK/windvd10SD/setup.cmd                                     | WinDVD                                       |
| SWWORK/x86/DRIVERS/dpinst.cmd                                   | DPINST processing Plug and Play drivers      |
| SWWORK/ZDOWORK2/CHECKSKU.CMD                                    | DISM                                         |
| SWWORK/ZDOWORK2/OA2CLN.CMD                                      | ????                                         |
| SWWORK/ZDOWORK6/SETCLEAN.CMD                                    | ????                                         |



## Background / Purpose
While using Linux full time, there are times when I **need** to use Windows due to work or other applications in which there isn't a decent alternative. Virtual Box offers a good medium allowing to me to run Windows in Linux but there are a few issues namely the bloatware that Lenovo has added to their base install. They may see it as a convience, but it's just a lot of stuff that I would never use. Additionally, all the drivers that get installed that will never be utilizied because Virtual Box is providing all that hardware abstraction.

----

## Q&A
Why do I get error messages like "can't find file to patch at input line XXX"..."Skip this patch [y]?"?

I don't know, out of the roughly 10 installs I've done to work through this patching, 2 of them failed to install about 15 files each. Go ahead and press 'y', that you want to skip patching this file. If this issue bothers you, go ahead and try a resintall.


## Authors

* Sean Crites

----
## Change Log
* 2019-03-12 Initial
