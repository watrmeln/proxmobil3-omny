# MTA OMNY standby emulator  
*(for init proxmobil3 transit card readers)*
> This repo is forked from Jaryn's HOP Fastpass reader emulator. Props to them for the original code, i did next to nothing script-wise!
> I am aware that OMNY uses cubic readers, this is merely a rehash of the designs to fit on the INIT PM3's 800x480 screen.

this is a **standby / idle screen emulator** for init proxmobil3 transit validators that recreates an **OMNY–style look and feel**.

it replaces the stock idle behavior with framebuffer animations and gives visual + audio feedback when a card or barcode is scanned.

> ⚠️ **this is purely an emulator / visual behavior mod**  
> it does **not** connect to the MTA, OMNY, or any real fare systems. You will not be charged if you tap a Credit or Debit card.

---

## important warning (please read)

- this project **remounts the root filesystem (`/`) as read-write**
  - required to install a persistent `systemd` service
  - interrupting this process **can brick the device**
- this is **unsupported firmware modification**
- you are doing this **entirely at your own risk**

if you don’t know how to recover one of these units, **don’t run this**.

---

## hardware / firmware requirements

### hardware
- init proxmobil3 validator
- proxdongl3 by [kevin wallace](https://kevin.wallace.seattle.wa.us/pm3/)

![Init Proxmobil3 reader](https://watrmeln.dev/img/IMG_5609.jpeg)

---

## what the script does

- installs a persistent `standby.service`
- shows:
  - a **startup animation** before nx initializes hardware
  - a **looping standby animation** during idle
- temporarily starts nx to:
  - initialize barcode + nfc hardware
  - create required serial device links
- stops nx and disables the pic32 watchdog
- triggers **hit animation + beep** on:
  - barcode scans
  - nfc taps
- randomly displays "try again" message on occasion to simulate bad reads
- prevents the display from going blank during idle operation

---

## setup instructions

1. download the files from the root of this repo (they are small enough to not zip)
2. format a usb drive as **fat32**
3. copy the files to the **root of the usb**
4. insert the usb into the proxdongl3
5. power on the device
6. wait for the installer to complete

logs will be written to:
- `/tmp/autorun.log`
- `/tmp/standby.log`

---

## final notes

this is a fun reverse-engineering / preservation project meant to keep old transit hardware interesting and usable.

it is **not affiliated with the MTA, OMNY, or init** in any way.
