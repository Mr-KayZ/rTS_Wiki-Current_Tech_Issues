---
layout: default
title: Intel 13th and 14th issues
nav_exclude: false
has_children: false
parent: docs
search_exclude: false
last_modified_date: 2024-10-12
---
# Intel 13th and 14th CPUs - Overvoltage and oxidized vias
## Background

The issue with 13th and 14th gen Intel CPUs has been covered greatly by many tech youtubers. If you wish to learn more, I highly recommend watching GamersNexus's and Level1Tech's videos that go into deep details about what the issue is about and how it is impacting users:
- [Intel has a Pretty Big Problem (youtube.com)](https://www.youtube.com/watch?v=QzHcrbT5D_Y)
- [Intel's CPUs Are Failing, ft. Wendell of Level1 Techs (youtube.com)](https://www.youtube.com/watch?v=oAE4NWoyMZk)

The gist of the issue is that users notice an out of GPU memory (VRAM) error, especially when running Unreal Engine games, whether it is UE4 or UE5. As a matter of fact, any game that utilizes lots of decompression when gaming for textures and loading can trigger this failure. Despite the fact that Windows reports a GPU issue, it in fact is a CPU issue.

Other reports include general instability, crashes, etc. ever since the 13th and 14th gen CPUs have came out, on all different types of motherboards, even those with extremely conservative values for clock speeds and memory speeds.

Both the 13th and 14th gen Intel BIOS's have been discovered to send way too much voltage into the CPUs, causing it to fail when running different tasks, most notably decompression tasks. In effect, the BIOS, even in its default state has been overclocking the CPU beyond it's capabilities to the point of failure, suffering physical degradation (hardware failure).

The 13th generation CPUs have been hit with a bigger issue. On top of the incorrect BIOS voltage, manufacturing defects have been found in the CPUs in the form of oxidized vias, killing the CPU cores and causing further issues.

According to the [official statement from Intel]([Addressing Manufacturing Speculation on Intel Core 13th/14th Gen Desktop Processors - Intel Community](https://community.intel.com/t5/Processors/Addressing-Manufacturing-Speculation-on-Intel-Core-13th-14th-Gen/td-p/1620097#:~:text=The%20issue%20was%20identified%20in,early%202024%20as%20a%20result): 
*"The issue was identified in late 2022, and with the manufacturing improvements and additional screens implemented Intel was able to confirm full removal of impacted processors in our supply chain by early 2024. However, on-shelf inventory may have persisted into early 2024 as a result."*

Do note that due to these issues, Intel has issued a extension to the warranty to the affected CPUs (both 13th and 14th generation), more details can be found here: [Additional Warranty Updates on Intel Core 13th/14th Gen Desktop Processors - Intel Community](https://community.intel.com/t5/Processors/Additional-Warranty-Updates-on-Intel-Core-13th-14th-Gen-Desktop/m-p/1620853)

*NOTE: If you are running a 13th or 14th gen Intel CPU, please update the BIOS IMMEDIATELY to microcode update 0x129 to address the overvoltage issues!*

Do note that Intel 12th gen CPUs, despite being on the same socket of LGA 1700, do not face these issues as their architecture is different (Alder Lake), compared to the 13th and 14th gen who's architectures are similar (Raptor Lake).

---
## Symptoms and Diagnosis

- Frequent crashes stating an "Out of GPU memory" when playing Unreal Engine games, even on higher end graphics cards with plenty of VRAM.
- Instability of the systems, and general crashes, BSODs with no clear description as to what is possibly causing the issue, etc.

In short, if you have a 13th or 14th gen Intel CPU, and not have an updated BIOS, any general instability issues is most likely caused by the misbehaving BIOS.

To recheck if you have a failing CPU, after updating BIOS, run the following tests:
- If you have an NVidia GPU:
	- Reinstall the NVidia driver at least ten times, which following the procedures for a [DDU](https://rtech.support/docs/factoids/ddu.html) every time.
	- If the test fails during any one of these installations, this means the CPU is potentially faulty and you may need to issue an [RMA request with Intel](https://www.intel.com/content/www/us/en/support/articles/000024255/processors.html).
	- This is because NVidia drivers during installation utilize lots of decompression, and is in fact ideal for general purpose troubleshooting. Other advanced decompression methods exist, but NVidia's reinstallation method has been shown to work the best so far.
- If you do not have an NVidia GPU (AMD or Intel GPU):
	- You will need to run multiple different CPU tests including:
		- Prime95 for 2 hours (by following our [HWinfo logging](https://rtech.support/docs/guides/hwinfo.html) guide, also ensure to log with HWinfo as well).
		- [Cinebench R23](https://www.guru3d.com/download/download-maxon-cinebench-r23/) for 2 hours.
		- Play Unreal Engine games, particularly Unreal Engine 5 games.
	- These methods are not as good the NVidia driver test but some form of testing is better than none at all.

## Known Solution

- **Update BIOS immediately to microcode update 0x129.** This is the only known fix approved by Intel directly at the time of writing.

After updating BIOS, follow the testing procedures outlined above to ensure that the CPU seems fine or works accordingly. If it fails in any of these tests, it may be possible your CPU already is physically damaged hardware wise, and the only way to fix that is to issue a RMA request directly to Intel.

You may refer to these guidelines to understand how the warranty procedure works and claim yours if you believe you have a faulty CPU: [Additional Warranty Updates on Intel Core 13th/14th Gen Desktop Processors - Intel Community](https://community.intel.com/t5/Processors/Additional-Warranty-Updates-on-Intel-Core-13th-14th-Gen-Desktop/m-p/1620853)