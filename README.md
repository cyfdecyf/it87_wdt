# it87_wdt

## Differences with `it87_wdt` in Linux kernel

`it87_wdt.c` in this project is copied from Linux kernel, with
modifications to:

1. Support ITE IT8785E chip
2. Support chip using index register `0x4e`
   - The original one uses only `0x2e`

Makefile and DKMS support code is copied from
[it87](https://github.com/frankcrawford/it87) project. I learned the use of
`0x4e` index register also from the it87 project.

## Usage

```sh
make clean
make
sudo make install
```

### Using DKMS

This is recommended.

Install:

```
sudo make dkms
```

Remove:

```
sudo make dkms_clean
```

## How does this project start

I bought a [Jetway JNC8H-IH310](https://www.jetwaycomputer.com/NC8H.html)
motherboard with IT8785E chip.  One of the main reasons I choose this
motherboard is its watchdog feature.  However, the kernel provided `it87_wdt`
module does not work out of the box.

Loading `iTCO_wdt` shows that it founds device, but running a watchdog service
does not stop the system from rebooting by the watchdog. This made me realize
the actual watchdog used by the motherboard is something else.
