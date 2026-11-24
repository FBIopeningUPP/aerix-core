---
title: "Aerix Core"
author: "I AM LITREALLY FBI"
description: "a stm32h743iik6 system on module"
created_at: "2026-11-04"
---

# 2026-11-12: finsihed

**Total time spent: 40 min**

![image.png](https://cdn.hackclub.com/01a1d0f6-c3e1-7a66-8dc9-f0958071671c/image.png)
![image.png](https://cdn.hackclub.com/01a1d0f7-04c7-761f-aa71-e42ece6c2001/image.png)

completed the rounting routed all the 8 layers made the production gerber and bom will be moving to making readme

# 2026-11-06: trying to trace

**Total time spent: 1h 1m**

![image.png](https://cdn.hackclub.com/01a1b208-551e-7ecb-96ba-a7a626af141c/image.png)
figured out everything fixed some net labels and eveyrthing and start tracing the tracks layer by layer

# 2026-11-06: layout

**Total time spent: 56 min**

![image.png](https://cdn.hackclub.com/01a1b072-68bb-7948-9213-5c4d72360870/image.png)

so i set the board settings and figure out the layout of the compoennts and everything to be optimal and do able 

# 2026-11-04: schematic done without connector pinout

**Total time spent: 1h 19m**

![image.png](https://cdn.hackclub.com/01a1a841-f1f8-7b47-9cb5-08bf5fcc54d4/image.png)
![image.png](https://cdn.hackclub.com/01a1a842-0e4c-7a11-8456-eee5bf176b13/image.png)
![image.png](https://cdn.hackclub.com/01a1a842-2cef-7960-87ad-c97c4f220f17/image.png)
![image.png](https://cdn.hackclub.com/01a1a842-4549-7bd9-a5c4-457a437e3f01/image.png)
![image.png](https://cdn.hackclub.com/01a1a842-6308-7903-9e46-7d081eb9b5b1/image.png)

soo the schematic is done i figured out the h743 pinout and the imu and everything required to start everything out like start out the pcb design part

# 2026-11-04: Research

**Total time spent: 2 hr**

I'm making a tiny flight controller for drones. It's a small board that solders flat onto a bigger board, like a chip does. It runs the same software that real Pixhawk flight controllers use.

![image.png](https://cdn.hackclub.com/01a1a7c8-a876-7885-8eea-f641a3f7ddd6/image.png)

I started with a board called the ARK V6X, because it's small and the software already supports it. I didn't want to copy it. I wanted my own shape and my own layout. This is how I picked each part and what else I looked at.

## The main chip

The main chip is the brain of the board, so I did the most research here. The big question was which chips the drone software already runs on. If it doesn't support a chip, I'd have to rewrite a lot of it myself, and I didn't want that.

I looked at a few chips:

- **STM32H743:** the same chip the ARK uses. The software supports it.
- **STM32H753:** almost the same, but it adds a security feature I don't need.
- **STM32F765:** older and slower.
- **NXP i.MX RT1170:** very fast, but the software doesn't support it well.
- **Newer STM32 chips:** the software doesn't support them yet.

I went with the **STM32H743**. It also comes in three sizes. The smallest has too few pins for everything I want. The middle one is very hard to wire up. So I took the biggest, which is still only 10 × 10 mm.

## The motion sensors (IMUs)

These sensors tell the drone how it's moving and turning. I'm using three of them, and from different brands. If one type has trouble with vibration, the other two keep working.

- **IIM-42653 (TDK):** the one the ARK uses, so I know it works well on drones.
- **ICM-45686 (TDK):** a newer one, so I get a different generation on the board.
- **BMI088 (Bosch):** made to cope with vibration, and it's a different brand from the other two.

I also looked at the ICM-42688-P. I dropped it, because the IIM-42653 is the same kind of chip with a bigger range.

I'll put the sensors on a small island of the board, cut free with slots and held by three thin bridges. That way the board's vibration and heat don't reach them as much.

## The air pressure sensors

These tell the drone how high it is. I'm using two from different brands again: the **BMP390** (Bosch, the one the ARK uses) and the **ICP-20100** (TDK, the one on the Pixhawk 6X). I also saw the BMP388, but the BMP390 is the newer one, so I skipped it.

## Memory

I picked three kinds, and each one does a different job:

- **FRAM:** keeps settings safe, even with no power, and it never wears out.
- **Flash chip:** 16 MB of extra space for files.
- **microSD slot:** for big flight logs.

## Power

I first wondered why I couldn't just use one small regulator to turn 5 V into 3.3 V. The problem is that it turns the extra voltage into heat. That's about 0.85 W at 0.5 A, right next to the sensors. A switching regulator wastes much less, about 0.18 W.

So I'm using a small switching regulator, the **TPSM828224**. It has the coil built in, which saves a lot of space. Switching regulators are a bit noisy, though. So the sensors get their own tiny, quiet regulators (**TPS7A2033**) with a filter in front. I almost used another one, the TPS7A20135, but I found out it only makes 1.35 V, so that would have been wrong.

## Other parts

- **Two CAN chips (TCAN1044AV):** drones use CAN to talk to GPS and motor controllers.
- **16 MHz crystal:** the clock for the main chip.
- **About 98 solder pads along the edges:** this is how the board solders onto the bigger board.
- **Size:** the board is about 28 × 39 mm.

