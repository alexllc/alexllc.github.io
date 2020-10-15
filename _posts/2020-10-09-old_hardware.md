---
title: Old ass hand me down tower
date: 2020-10-09 01:58 +8000
categories: [Computers]
tags: [hardware, mobo]

---

# My experiences with gaming/using/upgrading decade old machines
I'm broke, so I have plenty of these machines to deal with all day :cry: 

## 12-year-old desktop tower

## Issue: Tried installing an overclocked set of 1866Hz RAMs on a 1333Hz mobo
Never ever trust what they tell you at the hardware store, always double/triple check everything! I was told my mobo would be able to use these 8GB HyperX DDR3 RAM sticks, and I purchased them without a second thought. It turned out that this frequency is way beyond what the mobo could handle. It wouldn't get past the power-on-self-test (POST) while being stuck in a power on and off loop. This issue persisted even when I have swapped back the old RAM sticks in. I have tried most of the popular solutions: wrong dual channel placement, resetting CMOS, trying alternative dual channel slots... none of these worked! It turned out this is the issue of my somewhat incompatible new graphics card, replacing it with the old ass Gigabyte GT420, I was able to boot in with the original RAM sticks.


### Issue: Installed new graphics card but booting took FOREVER and cannot load into BIOS/UEFI
Initially, there were plenty of people suggesting going into UEFI and make sure the new graphics card is enabled etc. But I can't even load into the BIOS! I kept pressing `DEL` (mine was a Gigabyte) and nothing happened. I went on a pretty desperate Google search (up until page 5) and I managed to find a [thread on Tom's hardware](https://forums.tomshardware.com/threads/installed-new-graphics-card-and-post-boot-took-forever-and-i-can-not-get-into-the-bios.2296695/) where alexoiu (Alexes are the best) suggested upgrading BIOS, I had version 2 and I went to version 11. It worked perfectly. It's not a grand solution but it did work perfectly and I would like to write this down here, just in case I came across this issue again or others might need it.