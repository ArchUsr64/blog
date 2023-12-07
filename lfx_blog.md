# My growth through The Linux Kernel Mentorship Program
<!-- Why does Github Editor not have a ruler??!  Reference 80 character line -->
## Introduction
### About the program
Form the official [website](https://wiki.linuxfoundation.org/lkmp):
> The Linux Kernel Mentorship Program offers a structured remote learning
> opportunity to aspiring Linux Kernel developers. Experienced Linux Kernel
> developers and maintainers mentor volunteer mentees and help them become
> contributors to the Linux Kernel.  

***TL;DR:*** The program helps beginners like me get started in Kernel Development.

### Application Process
The learning journey started right as I applied for the program through [LFX](https://mentorship.lfx.linuxfoundation.org/#projects_all).
I was assigned a few tasks to complete as precondition for the mentorship as well
as the requirement to complete LFD103 ([A Beginner’s Guide to Linux Kernel Development](https://training.linuxfoundation.org/training/a-beginners-guide-to-linux-kernel-development-lfd103/)) course.
Completing the prerequisite tasks served as a gentle introduction to the upcoming
program. Tasks ranged from detecting PCI and USB devices on the device using sysfs to
compiling and booting your own kernel!

I had to rush to finish LFD103 since the deadline was swiftly approaching, the
course gave me a general overview of the linux development process and how to
work with mailing lists.

With my application done and the course completed, I was eager to put my newly aquired skills to good use.
Excited by the prospects of contributing to **The Linux Kernel**, I submitted a few superfluous [patches](https://lore.kernel.org/lkml/?q=d%3A..2023%2F9%2F1+f%3A%22anshulusr%40gmail.com%22).
Although well intentioned, the patches did not receive the warm open hearted reception
I was expecting. This experience taught me what working on the kernel
was all about. The goal is to provide best possible experience to the users and
patches fixing minor formatting issues don't do that.

<!-- TBH I was afraid I wouldn't be accepted -->
On 30th August, I got my confirmation of being selected into the program.

## Getting Started
Having had a longtime fascination with firmware and drivers, I was intrigued
to see that some of the source files in the `drivers` directory had a similar structure
to the hello world module. Each had `module_init`, `module_exit`, `MODULE_*` macros,
after doing some digging, I learned that drivers are just kernel modules that provide
a common API to the underlying hardware.

This realization gave me the confidence to start exploring how device drivers
function and if I could implement one myself. I had a i2c gamepad with me from one
of my previous projects. So I decided to try my hands on writing a driver for it
since it didn't have any.

I based my [initial patch](https://lore.kernel.org/linux-input/20231007144052.1535417-2-anshulusr@gmail.com/)
on pre-existing driver for a similar gamepad from SparkFun. The subsequent code reviews
from the subsystem maintainers helped in improving the functionality and ironing out
some of the implementation quirks. The exercise helped me understand the use of the
devicetree bindings and the process of writing and testing them. I also gained
experience working with the Input APIs and learned how the events from devices like
keyboard or mouse are reported to the kernel.

[Adafruit Mini i2c gamepad](https://github.com/ArchUsr64/blog/assets/83179501/223a0af8-771a-4c17-a00f-ffefa85d1d03)

## Into the Depths

Continuing the journey, I decided to work on some sensors that lacked linux support.
The idea of working on these smaller devices really intrigued me. I was interested to
learn how these devices were exposed to the userspace and the common abstraction for
the diverse array of sensors worked.

I chose a Lite-On LTR390 UV/Ambient Light Sensor as my device of choice since it used
i2c which I had gotten comfortable with while working on my gamepad driver. The device
also had an exhaustive documentation. I learned of the `regmap` abstraction in the
linux kernel and used it to abstract the underlying i2c communication.

The mystery universal abstraction used by all sensors turned out to be [IIO channels](https://docs.kernel.org/driver-api/iio/core.html#iio-device-channels).
<!-- TODO: Add more here?? -->
[LTR390](https://github.com/ArchUsr64/blog/assets/83179501/e9e66398-60de-42c7-b511-a66a8c5927f2)
