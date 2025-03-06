# tsc-err_inj

- Inject error to hpet to make TSC mistaken to mark unstable
- The error would be seen as follow:

```bash
# cat /sys/devices/system/clocksource/clocksource0/current_clocksource
tsc
# insmod tsc_err_inj.ko
# dmesg -T |tail -10
[Thu Mar  6 17:41:57 2025] Planted return probe at read_hpet: 000000008bac67fb
[Thu Mar  6 17:41:58 2025] retval: 1211573873, changed: 1231573873
[Thu Mar  6 17:41:58 2025] clocksource: timekeeping watchdog on CPU177: Marking clocksource 'tsc' as unstable because the skew is too large:
[Thu Mar  6 17:41:58 2025] clocksource:                       'hpet' wd_now: 49685371 wd_last: 47c9095f mask: ffffffff
[Thu Mar  6 17:41:58 2025] clocksource:                       'tsc' cs_now: 544775984b9 cs_last: 5442de33e58 mask: ffffffffffffffff
[Thu Mar  6 17:41:58 2025] tsc: Marking TSC unstable due to clocksource watchdog
[Thu Mar  6 17:41:58 2025] TSC found unstable after boot, most likely due to broken BIOS. Use 'tsc=unstable'.
[Thu Mar  6 17:41:58 2025] sched_clock: Marking unstable (1887075743358, 3091088717)<-(1890476585288, -309749862)
[Thu Mar  6 17:41:58 2025] clocksource: Switched to clocksource hpet
[Thu Mar  6 17:41:58 2025] retval: 1211589964, changed: 1231589964
# cat /sys/devices/system/clocksource/clocksource0/current_clocksource
hpet
```

