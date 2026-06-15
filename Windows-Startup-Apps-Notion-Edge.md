# Unwanted Apps Launching at Startup (Notion & Microsoft Edge)

**Date:** June 15, 2026
**Device:** HP EliteBook 840 G3 (DESKTOP-PFPKUI6)
**Error Code:** N/A
**Category:** Windows Configuration / System Optimization
**Status:** Resolved

## Issue

Notion and Microsoft Edge were automatically launching every time the laptop booted, without the user intentionally enabling this behavior.

## Troubleshooting Steps

1. Opened Task Manager (`Ctrl + Shift + Esc`)
2. Navigated to the **Startup apps** tab
3. Found both Notion and Microsoft Edge enabled as startup items
4. Disabled both entries

## Resolution

After disabling the startup entries for Notion and Microsoft Edge in Task Manager, both apps stopped launching automatically on boot.

## Lesson Learned

Many applications silently enable "launch at startup" during installation. Task Manager's **Startup apps** tab is a fast way to audit and clean these up — useful both for system performance and for avoiding unexpected clutter on login.
