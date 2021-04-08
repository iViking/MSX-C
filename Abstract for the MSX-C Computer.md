# Abstract for the MSX-C Computer

**Ver 1.03**

![](/MSX-C_Logo.png)

**7 April 2021**

## Notice

This documentation is subject to the [GNU Free Documentation License](https://www.gnu.org/licenses/fdl-1.3.html)

Initial version © 2021 Jake Eckert

Permission is granted to copy, distribute and/or modify this document under the terms of the GNU Free Documentation License, Version 1.3 or any later version published by the Free Software Foundation; with the Invariant Sections being 'Rules for Forks and Version Changes', no Front-Cover Texts, and no Back-Cover Texts. A copy of the license is included in the section entitled "GNU Free Documentation License".

![](/gfdl-logo.png)

MSX is a trademark of MSX Licensing Corporation

## Table of Contents

[Notice](#notice)

[Table of Contents](#table-of-contents)

[Rules for Forks and Version Changes](#rules-for-forks-and-version-changes)

[Special Thanks](#special-thanks)

[Version Notes](#version-notes)

[Objective](#objective)

[Summary of Specifications](#summary-of-specifications)

[System on a Chip (SoC)](#system-on-a-chip-soc)

[Memory](#memory)

[ROM](#rom)

[RTC](#rtc)

[Flash Storage](#flash-storage)

[Keyboard](#keyboard)

[Gamepad](#gamepad)

[Cartridge Slots](#cartridge-slots)

[Audio/Video Output](#audiovideo-output)

[Network Output](#network-output)

[Features Not on the MSX-C](#features-not-on-the-msx-c)

[Hardware and Packaging Requirements](#hardware-and-packaging-requirements)

[Online Shop and Licensing to Publishers](#online-shop-and-licensing-to-publishers)

[License for This Document](#license-for-this-document)

## Rules for Forks and Version Changes

For the purposes of maintaining a development history, it is recommended to apply the following rules when modifying the contents of this document:

The trunk branch is authored and maintained by Jake Eckert and other parties with permission. Updates to this branch may only be published by the authors. Any updates to this branch published by any party with the author's permission may be versioned to this branch.

Any other updates to this documentation may be published as a fork branch. Authors of that branch may continue to update this documentation under their branch or under new forks. Any updates to such branch made by a party other than the branch author may be published under a new fork branch.

Version number and date must be reflected accordingly on the Title Page.

Versions of forks may be independent to their parent branches.

Fork versions must be titled in the Title Page as '[FORK NAME] Ver [VERSION]'.

Version Notes must be dated and appended. New forks, as well as child branches, must include Version Notes of their parent branch.

All versions, including forks, fall under the latest version of the GFDL License. The Notice and License pages should reflect the latest version.

Table of contents should be updated accordingly before publishing.

## Special Thanks

As the principal author of this project, I would like to thank the MSX community for their help and support. In particular, I would like to thank [Serge Kiselev](https://github.com/skiselev), the creator of the Omega, for getting me started with the MSX; [Jordi Solis](https://github.com/msx-solis) for helping me with parts and assembly for the Omega; @psxdev, @MSXunderground, @MSXBlog, @msxall (Julio Marchi), and many others on Twitter that have engaged and supported me throughout. Most of all, it is my pleasure to thank the MSX Resource Center and its members for all the resources and information that inspired me to create this project. I sincerely wish for its success, both for you and for the MSX-C. This project was made for you, to create the most affordable MSX computer today, and introduce the MSX for a whole new audience.

I will help as much as I can on this project, just as you all have been a help to me. Thank you, from the bottom of my heart!

## Version Notes

1.02 – 7 Apr 2021 – Base Version; conversion from original docx to md

1.03 - 8 Apr 2021 - markdown formatting improvements (konamiman)

## Objective

Since the MSX line of computers were effectively discontinued in 1993, efforts to create software and hardware compatible with the architecture have been undertaken. The ultimate objective of the MSX-C is to differentiate itself from other hardware 'revivals' of the MSX, by being an affordable system capable of running MSX software. The 'C' in MSX-C stands for 'cost-reduced', reflective of this objective. This reduction in cost is for the benefit of making and selling the system to the consumer. The MSX-C must consist of all the essential elements of an MSX computer, as well as modern improvements relative to the present day, and only excluding elements that aren't necessary to the core experience. Unlike most recent hardware implementations, the MSX-C is made for consumers interested in the MSX but, to date, are turned away by the high cost of owning hardware and software for it.

## Summary of Specifications

#### MSX Turbo R-Compatible System

- SoC (FPGA or ASIC) consisting of logic replicating:

  - CPU: R800 @ 7.16MHz/Z80 @ 3.58MHz
  - VDP: V9958 & V9990 compatible Video for output to HDMI at 720p
  - Sound: YM2149 PSG/SCC+/MSX-AUDIO/MSX-MUSIC/Moonsound/PCM for output to HDMI as 2-channel, 16-bit PCM

- 512kB SRAM (at minimum), 512 kB VRAM
- ROM consisting of:
  - BIOS + Extended BIOS
  - MSX-BASIC
  - Program ROM for programs stored in flash storage
  - "Homebase" Firmware (Menu, Cart, BASIC, Apps, Games, Shop, Settings)
- RTC
- Flash Storage (with possible USB/SD support)

#### Input/Output

- Keyboard – Full-travel Dome-switch, built-in
- 2 Gamepads – (2.4GHz, Bluetooth, or USB)
- Cartridge – 2 Slots
- Audio/Video – HDMI
- Network – Ethernet/WiFi

#### Removed from original specifications

- RCA Audio Output
- Video Outputs: RF/Composite/S-Video/RGB
- Cassette, Disk, Printer, MIDI, other accessories not mentioned

## System on a Chip (SoC)

There are two feasible implementations of the SoC. Field-programmable gate arrays (FPGA) are an ideal implementation for testing and perfecting the needed functions of the MSX-C. The costs of FPGAs is understandably high, so implementation of an FPGA is best for if the predicted sales of the system is uncertain. An FPGA implementation can also allow for improvements to the logic down the road, and account for bugs. With a full understanding of what the logic of the SoC should entail, and should the design of the logic become optimized, the implementation of this logic as an Application-Specific Integrated Circuit (ASIC) becomes more feasible. Applying the SoC as a static ASIC should be considered when the logic is free of bugs, flaws, or oversights, and when projected sales of the MSX-C makes it more cost-effective to install an ASIC SoC, where the bulk costs of ASIC chips is less expensive than the bulk cost of FPGA chips.

#### CPU

The MSX Turbo R was released in 1990 with an ASCII R800 running at 7.16MHz, twice the speed of previous MSX standards that used a Z80 processor. The R800 is binary compatible with MSX software that used Z80 instructions, but because it lacked some undocumented features of the Z80, it was paired with an MSX-Engine chip in the Panasonic Turbo R models (Panasonic was the only manufacturer of Turbo R computers). The SoC of the MSX-C should contain the functionality of the R800 with the inclusion of all Z80 functionality that the R800 originally lacked. This should be clocked at 7.16MHz maximum, with a function to halve the clock speed for non-Turbo R software. This could potentially serve as a 'turbo mode' for non-Turbo R software, if such a feature can come without additional complexity

#### VDP

The Turbo R uses the same VDP as the MSX2+, the Yamaha V9958. Yamaha intended to release an updated VDP, but was delayed by its development. When the MSX was discontinued, Yamaha released the VDP as the V9990. Even though it was not compatible with the V9958, the V9990 was implemented to the MSX as an expansion cartridge, and some software makes use of the V9990 or outright requires it. Therefore, the SoC of the MSX-C should contain the combined functionality of the V9958 and the V9990. Video memory is documented to be 512kB of VRAM for the V9990, but only a combined 192kB (128kB + 64kB expanded) of VRAM for the V9958. Since the V9990 isn't binary compatible with V9958 software, video should only be output in either V9958 mode or V9990 mode, but never at the same time. For video output, HDMI is the only source, with 720p the minimum resolution. More on video output later in this abstract. Additional outputs add to the cost of the system. On the upside, this removes the need of a DAC functionality inherent in both VDPs; only the digital RGB signals are needed.

#### Sound

MSX machines typically come with PSG sound, but the choice of sound chip varies with the machine. For later models of the MSX, the Yamaha YM2149 is the typical PSG sound chip. However, most games would make use of expansion audio. Some games even require expansion audio to properly work, and would typically be included in the game's cartridge. Konami games on cartridges after 1986 would contain the SCC chip if the game requires it. On disk-based games, a separate expansion cartridge is required. That adds to the cost for consumers of the MSX. The MSX-C resolves to have the most common and popular sound options included in its SoC. These sound options are YM2149 PSG, SCC+, MSX-AUDIO, MSX-MUSIC, Moonsound, and the Turbo R-exclusive PCM sound. The sound options should be mixed at optimal volume levels for monaural digital sound, to be output on both channels of 16-bit PCM audio on HDMI. While it may be attractive to implement programming for the user to adjust volume and balance levels of individual sound channels, and it may be a useful feature for an FPGA-based core, it is important to ensure that audio is optimized for a potential ASIC implementation, where it's cost-effective in mass-production.

## Memory

The MSX works with two separate forms of memory: SRAM memory for programs, and Dual-ported DRAM, also known as VRAM, for video. The MSX range of memory spans from 16kB in its first iteration, to 512kB in the last models, with the potential to expand it up to 4MB. 512kB seems to be the best number for both SRAM and VRAM. For VRAM, the reason is most obvious: the V9990 VDP was designed to require 512Mb of VRAM. A partial amount would be used, specifically 192kB (128kB + 64kB expanded), if the SoC was outputting in V9958 mode. For SRAM, it's not clear whether compatibility would become an issue if memory would be expanded beyond 512kB. One would think it would be simple to have 4MB memory built-in, but for the purpose of compatibility with as many MSX titles as feasible, 4MB can only be attainable if compatibility can be assured.

## ROM

Computers can't work without programs, but the ways a program can be loaded to a computer varies. For microcomputers, the most common initial implementation is through on-board Read-Only Memory (ROM). The most common programs to be first run on a computer when powered on is usually its Basic Input/Output System (BIOS) that enables initialization of hardware, followed by an Operating System (OS). If software is programmed into hardware like ROM, it is also known as 'firmware'. As far as the MSX-C is concerned, firmware should be subject to updates, either online or through updates in secondary storage. MSX-C firmware should also adhere to the following details below.

#### BIOS

As an MSX Turbo R machine, the MSX-C must consist of a BIOS + Extended BIOS compatible with the hardware specifications of the MSX Turbo R. What BIOS is used, however, is not as clear-cut. At present, the only legal implementation is a third-party BIOS, like C-BIOS. The BIOS will need to be checked, and modified wherever necessary, for software compatibility, as well as for utilizing the hardware specific to the MSX-C. It is the ambition of the MSX-C project to acquire an official license and implement the MSX BIOS.

#### MSX BASIC

In accordance with the MSX Turbo R specification, the MSX-C firmware must obviously contain a form of version 4.0 of MSX BASIC, with all the functionality thereto. Acquiring a license for the official version of MSX BASIC 4.0 should be pursued.

#### Program ROM

In order for the MSX-C to be viable to current-day consumers, programs and games should be loaded without requiring extra accessories that may cost more, such as cartridges or disks. The MSX-C will have secondary flash storage for systems and programs. Programs that are in flash storage should be loaded into a dedicated space that the system can then access and load into memory, either a dedicated page in firmware or flash storage for such programs, or a separate ROM chip.

#### Homebase (Working Title)

The MSX-C is meant for consumers interested in 1980s era computers and games, or for parents to give their children to as a teaching tool and video game system. To that end, the MSX-C must consist of firmware that takes advantage of contemporary technologies of the current century. The firmware, which this abstract shall call 'Homebase', provides the environment for the end-user to take measured control of the MSX-C. The following describes the desired function of Homebase:

- The menu is the first thing that the user will interface with. This menu contains basic functions such as date and time, as well as selections for the user to navigate to.
- An option to run from inserted cartridges should be a pronounced selection. If the MSX-C can implement hot-swapping, then it may be selectable if a cartridge is inserted. Without hot-swapping, the option must be made selectable at all times, and behave similarly to past MSX machines (ie, run BASIC if no cartridges are inserted). More on hot-swapping later in this abstract when addressing cartridges.
- 'Apps' list what programs are available to the user. Selecting an app would load into ROM and run it from memory. If necessary, some apps should be built-in to, and made non-erasable from, flash storage, as 'pack-in' apps for the user. In such cases, some of these pack-in apps should serve to help the user get acquainted with the system they bought. Other apps should be downloadable to flash storage online, or possibly copied to flash storage through secondary means, such as an SD card or USB. More on secondary storage and online capabilities later. It is recommended that applications stored digitally or published in the online shop should consist of a description of the application, description of controls, and at least a text-based manual, all on-screen.
- 'Games' list what games are available to the user. Selecting a game would load into ROM and run it from memory. If necessary, some games should be built-in to, and made non-erasable from, flash storage as 'pack-in' games for the user. In such cases, some pack-in games should be easy for users to pick up and play, with simple controls for keyboard and gamepad. Other games should be downloadable to flash storage online, or possibly copied to flash storage through secondary means, such as an SD card or USB. More on secondary storage and online capabilities later. It is recommended that games stored digitally or published in the online shop should consist of a description of the game, description of controls, and at least a text-based manual, all on-screen.
- The 'Shop' is its own application that takes the user to a secure online marketplace to buy and download apps and games. The MSX-C should be allowed to run programs without needing a cartridge or disk. The inclusion of a shop to download such programs is required for the convenience and accessibility of the user. The shop allows for software for the MSX, past and present, to be published for download and consumption. Security features and licensing terms of this market should be implemented to attract and protect publishers using this service. The security and digital rights protection provided by the online shop is intended to attract as many developers and publishers as possible, including publishers of popular MSX titles (eg, Konami), and thus attract users to the MSX-C itself. If publishers can be on board with publishing MSX games online, the MSX-C may need to omit SD/USB storage altogether for security reasons (though that should also bring the cost of the system down). Further details of this online shop service, including a licensing model to fund its upkeep, are proposed further in this abstract.
- 'Settings' allows the user to manage programs and saved data in storage, as well as settings related to the MSX-C itself. Such setting should include adjusting the date and time (kept within the system's RTC), gamepad settings, network settings, parental controls, language and region settings, firmware updates, etc.

## RTC

The MSX2 specification and above requires a real-time clock (RTC). The MSX-C should contain an RTC compatible with the MSX2 standard, powered by both the system and a supplementary 2032-sized battery. The battery should be easily accessible and removable by the user without needing to open the casing of the entire system. Firmware should make full use of keeping track of the date and time, as well as allow the user to set the date and time without needing to input commands in BASIC.

## Flash Storage

The MSX-C must contain secondary flash storage for system settings, programs, and saved data. The need for secondary storage for games and other programs is most obvious when the costs of available MSX software in cartridges and disks are prohibitively expensive. The expense of MSX games today makes the MSX far less accessible to most consumers.

There may also be a means to allow a removable storage device, such as SD or USB, to store programs, as well as firmware updates. However, successful implementation of an online shop, and licensing agreements with publishers looking to sell their software on the MSX-C, may require restriction or omission of a removable storage device. A removable storage device may be omitted to lower the costs as well, and firmware updates can be distributed solely online.

## Keyboard

A keyboard must be built-in to the MSX-C, but how it is built-in should be cost-effective. A USB-based solution is easiest to implement, if USB signals are converted to signals that the MSX-C can be read. Most crucially, however, the keyboard itself should be a dome-switch design, with full-travel plastic keys actuating upon carbon-tipped 'domes' lining a rubber or silicone pad, which then contact a circuit membrane underneath. The full-travel dome-switch is the most common and inexpensive keyboard design on the market. Implementing a common keyboard to the case of an MSX-C can also be simple. The keyboard may not consist of a numeric keypad, and keys that aren't used by an MSX (such as page up, page down, print screen, scroll lock, or pause/break) may be removed, and the space left by removing the keys covered up by the casing. This is one of the basic guidelines for implementing a built-in keyboard as cost-effective as necessary. A mechanical keyboard is not an option, nor should it be an option. The MSX-C is not necessarily meant for enthusiasts of the MSX, but for consumers interested in retro systems, like the MSX, that can be turned away by the high costs.

## Gamepad

The most common connector for MSX gamepads have been DE-9 male, but that shouldn't necessarily be the case today. Most video game controllers are either wired to USB, or are wireless. Based on the benefits and drawbacks, the MSX-C is recommended to come with, and be capable of receiving signals from, two 2.4GHz wireless gamepads. These gamepads should consist of at least a d-pad and two face buttons. Where such controllers can be sourced, however, can be discussed further by the MSX community, as well as discuss whether Bluetooth wireless or USB gamepads are a more feasible option. Nevertheless, two gamepads should be included as part of purchasing an MSX-C. Settings to calibrate the controls of the gamepads should also be implemented in the firmware.

## Cartridge Slots

The MSX-C should still be able to run cartridge-based games and applications. There must be only two cartridge slots for this purpose. The MSX-C would be capable enough that additional slots are unnecessary, but there are games that use both cartridge slots in some degree. Konami, for example, was known to hide Easter eggs in games that can be accessed by inserting a second game into the second slot.

Other features for the MSX cartridge slots should be discussed further. Dust covers are a necessary addition to keep the pins clean and free of dust. The capacity to insert and remove cartridges while the machine is running, also known as hot-swapping, should be considered both as a safety feature, as well as a convenience to the user. Hot-swapping, if considered, must be implemented in a way to protect both system and cartridges from damage. Ideally, hot-swapping should also be reflected in firmware, and that removing a cartridge while its program is running would bring the system back to the menu. An implementation in the casing to eject inserted cartridges should be discussed as a way to reduce wear on the system itself, especially when a user may need to apply force on the casing as leverage to remove cartridges by hand.

## Audio/Video Output

As a cost-effective measure, and because it is the most common output at present, audio and video of the MSX-C must be output to HDMI, and only to HDMI. Additional output options add to the cost of the system. Most consumers, including video game players, have an HDMI display, and displays made today commonly exclude other outputs, like RCA connectors. Inclusion of RCA connectors for composite video and analog audio for the MSX-C may be considered if costs to implement them are reasonable. Any other output is out of the question; outputs such as RGB are less common, and are the purview of enthusiast users. The MSX-C should be made with the most common user base in mind, one looking for a quality experience without the prohibitive cost. Because the MSX natively outputs in a way that can be seen on an interlaced 60Hz display like a CRT, it is recommended to output the video in a way that avoids interlacing. The most common method, for example, is line doubling. Drawing blank 'scanlines' between vertical pixels is also popular, but if it were implemented, it must be as an optional feature. Video from the MSX should be, at a minimum, scaled up for 720p at 60 fps. Additional supported resolutions should be a multiple of 480 pixels for proper integer scaling, and also output at 60 fps (960p, 1440p, 4K, etc.). Sound must be 2-channel uncompressed PCM. HDMI conversion should be optimized for minimum possible input lag.

## Network Output

There have been recent releases of 'miniature' retro game consoles and home computers, with games packed-in. While the MSX-C should have some applications and games built-in for the user to start with, it should also serve as a microcomputer on its own right. To that end, the MSX-C must have Ethernet and Wi-Fi built-in to connect to the network. Wi-Fi should be at 802.11n, and the Ethernet connector must be 8P8C. The standard protocol for the network layer should be TCP/IP. The primary purpose for the MSX to have a network connection is to allow for online updates to the firmware, make use of programs that connect to the internet without needing a network cartridge, and be able to sell MSX apps and games, both by independent developers and by past developers of popular MSX titles, such as Konami. Proceeds go to these developers, and any imposition of fees (ie, to license for sale on the shop) would go directly to maintaining the online service. More on the online shop and licensing software for sale to consumers later on in this abstract.

## Features Not on the MSX-C

The MSX-C is meant to be an affordable retro computer for today's video game and computing market. Because the MSX specification itself is decades old, features of that time are obsolete by today's comparison. Most of these features are a necessary novelty as a retro computer, such as sound and video. Other features, however, can be removed without altering the experience. In fact, to keep the costs down, both to produce and to sell the MSX-C, the following features included in the original MSX specification are excluded from this platform.

The MSX-C is not planned to output analog audio and video through RCA. HDMI is the sole planned output for both audio and video, as the MSX-C is meant to be marketed towards a similar base as computers and video game consoles. This market would typically have a monitor with HDMI input. While analog video and audio can make for a more authentic experience, getting the best quality video is also important. HDMI is a practical solution for this purpose. Analog outputs, such as composite, S-Video, and especially RGB, are the purview of a more enthusiast user base, who are likely to spend more money on more faithful hardware.

Implementations of older storage media, such as cassette and floppy disk, are excluded. ROM cartridges that connect to the two slots on the MSX, however, are integral to the MSX as a computer, much like how cartridge slots are integral to retro game consoles. MSX games are still being independently made and sold in cartridge form, and users who own MSX cartridges should be able to use them on the MSX-C. Cassettes and floppy disks are options, and players who have games in such media are likely to own an MSX that runs them. For users who insist on using cartridges or floppy disks, it would be better to acquire an adaptor cartridge that has inputs for them. Most users for the MSX-C would be able to acquire software and games either digitally or as a cartridge, so implementing inputs that may mostly go unused by many users is not worth the expense.

The MSX-C will not have inputs for printers or MIDI devices. The MSX-C, like most MSX computers, is marketed for playing games, but the computer aspect is necessary to a point. Dot-matrix printers were an obvious computer accessory of the time, and MIDI devices are optional features for a niche market. Both are features that will rarely be utilized by users, especially those looking to simply play games on the platform. It may be feasible to add a wireless printing feature, but the complexity and expense of programming a bespoke protocol to convert MSX standard printer signals to a signal that can be sent to a modern-day printer must be considered carefully.

## Hardware and Packaging Requirements

Power output for the entire machine must supply appropriate voltages for the components, including +5V, +12V, and -12V for the cartridge slots. Current supply for the cartridge slots should be at least 1000mA, as cartridges that allow for additional accessories like floppy drives would obviously require more power. For safety from a short, a resettable fuse rated for over 1500mA should be installed for the whole machine. A lower-rating resettable fuse for both cartridge slots could be added as well. All amperage ratings are suggestions, and are open to discussion. A barrel plug is a recommended connection for power. An AC adaptor must be included in packaging.

Dimensions of the computer itself play a part in the costs of shipping, especially in bulk. Still, the computer should be sized to be sturdy, with the width to hold a keyboard, and the length to accommodate the two cartridge slots. For mass production, the case should ideally be injection-molded plastic, with columns attached to the top panel to secure the case from the bottom with shorter screws. Alternatively, a 3D-printed case would suffice, but such a design should include a way to fasten the case with only screws. Dust covers for the slots are recommended. There must also be a way for the user to access the RTC battery without removing the casing.

LED indicators for power, gamepad connections, and the caps lock and kana keys are required, and all LED indicators must be low intensity so they would not distract or irritate the user. Additional switches must include power and reset. The reset switch must be a momentary push-button switch, and must always force a soft reset that takes the user back to the main menu. The power switch may not directly control power to the computer, but rather initiate a sequence that would power on or power off the system safely. The power and reset switch must be accessible from the top, sides or front of the machine. The first cartridge slot must be top-loading. The second cartridge slot must either be top-loading or rear-loading, but never positioned closer to the front than the first cartridge slot. If gamepads are wired, connections must be from the front or the sides, and must be labeled A and B (or 1 and 2) as the first and second connections respectively. All other connectors, such as HDMI and Ethernet, must be at the rear of the machine.

Additional packaging should include a manual, both for getting started with operating the machine and for learning MSX BASIC, but must also include an AC adaptor, an HDMI cable, and two gamepads.

## Online Shop and Licensing to Publishers

The ability to purchase MSX software digitally through a secure online marketplace is the most ambitious challenge of the MSX-C project. Previous releases of 'miniature' retro consoles had software and games already built-in, but it would require licensing agreements to legally include such software. Additionally, new games for the MSX are being made by independent developers, and it is important to support them as well. The online shop is the solution to introducing users to software and games, both new and old, and into the future. Developers and publishers would be able to earn revenue from the sale of their works. Of course, maintaining a service like this is an expense. While upkeep for the service can be funded though other sources, a fee-based licensing program should be considered as a source of funding. The fees should be small enough, and the licensing terms should be for the licensee's benefit, so that it would attract publishers. Most importantly, to attract more prominent publishers, like Konami in particular, to release their library of MSX titles for sale on the MSX-C online shop, the works being published and sold through this service must be kept safe and secure. Digital Rights Management, or DRM, is an unattractive aspect of software, and it is understandable that the MSX community would frown upon any measure intended to protect intellectual property, but implementing DRM in some form should be openly discussed. The MSX community would not be as active today were it not for the works of dedicated developers of the past and present. Whether they are a one-person independent developer or one of the most successful video game companies, their contributions both gave rise to, and are inspired and supported by, this same community. To give developers a safe and secure platform to sell their works to users new and existing, will in turn support and grow the MSX community as a whole. All who contribute to the MSX stand to gain from this platform.

## License for This Document

[GNU Free Documentation License version 1.3](https://www.gnu.org/licenses/fdl-1.3.html)
