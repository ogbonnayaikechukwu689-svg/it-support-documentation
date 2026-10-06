# Blue Screen Crash (IRQL_NOT_LESS_OR_EQUAL): Troubleshooting Report

**Category:** Windows troubleshooting | **Tools:** Reliability Monitor, WinDbg | **Status:** Resolved, follow-up in progress

## Problem
My laptop crashed with a blue screen while in normal use.
- Stop code: `IRQL_NOT_LESS_OR_EQUAL`
- "What failed": `ntoskrnl.exe`
- The screen then froze at "100% complete" for about 10 minutes and did not restart.

## Root Cause
The crash happened inside `win32kbase.sys` (function `EnterCritInternal`), which is part of the Windows graphics and windowing system. A write went to an invalid low memory address (`0x9a00`).

This points to a graphics driver or third-party software giving bad data to a Windows component. It does not point to failing RAM. I could not identify the exact driver or app.

## Solution (Steps I Took)
1. Held the power button for 10-15 seconds to force a shutdown. Unplugged the charger briefly, then powered on.
2. Windows booted normally. Checked **Settings → Windows Update**: "You're up to date".
3. Opened Reliability Monitor (`perfmon /rel`) and found critical events logged at 7:10 PM.
4. Opened the technical details for "Windows stopped working" and read the bugcheck: `0xA (0x9a00, 0x2, 0x1, 0xfffff80029e60e3d)`.
5. Copied `C:\Windows\MEMORY.DMP` to the Desktop (admin permission needed).
6. Opened the dump in WinDbg and ran `!analyze -v`.
7. Read the results:
   - `MODULE_NAME: win32kbase`
   - `IMAGE_NAME: win32kbase.sys`
   - `FAILURE_BUCKET_ID: AV_win32kbase!PrivateAPI::EnterCritInternal`
8. Deleted the dump copy from the Desktop afterwards, because memory dumps can contain sensitive data.

## Outcome
The laptop restarted and ran normally with no repeat crash. Windows was fully updated. The cause was narrowed to the graphics/windowing layer, but not to one specific driver.

**Follow-up to do:**
- [ ] Update the graphics driver
- [ ] Run `sfc /scannow`
- [ ] Run `DISM /Online /Cleanup-Image /RestoreHealth`
- [ ] Monitor for repeat crashes

## Lessons Learned
- How to read a blue screen stop code and its bugcheck parameters
- Hands-on use of Reliability Monitor and WinDbg crash dump analysis
- The file named on the blue screen (`ntoskrnl.exe`) is often the victim. The real cause needs dump analysis.
- Memory dumps are sensitive data. Delete them after use.
