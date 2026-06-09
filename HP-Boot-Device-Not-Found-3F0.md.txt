# HP Laptop — Boot Device Not Found (Error 3F0)

## Problem
Laptop displayed "Boot Device Not Found" error with Hard Disk (3F0) code on startup. Windows would not load.

## Device
- Brand: HP
- Error Code: 3F0
- OS: Windows

## Root Cause
BIOS boot mode was set to UEFI only, but Windows was installed 
in Legacy mode. The laptop could not locate the OS because of 
this mismatch.

## Solution
1. Power off the laptop and power back on
2. Press **F10** to enter BIOS
3. Navigate to **System Configuration → Boot Options**
4. Enable **Legacy Support**
5. Press **Escape** → Select **Exit Saving Changes** → Press Enter
6. Laptop restarts — enter confirmation code **3925** when prompted
7. Windows loads successfully ✅

## Outcome
Issue resolved. Laptop booted into Windows normally after enabling Legacy Support.

## Date
June 2026

## Lessons Learned
- Learned the difference between UEFI and Legacy boot modes
- Gained hands-on experience navigating HP BIOS settings