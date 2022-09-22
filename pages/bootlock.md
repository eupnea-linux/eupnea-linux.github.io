# Sleep bootlock

When the lid is closed or the system is idle for a long time, Linux distributions tend to sleep to S4(Hibernate). On a Chromebook this triggers an NVRAM reset and forces the Chromebook to boot into an operating system with an officially signed kernel(only ChromeOS has one). It is not possible to re-enable USB and unsigned kernel booting without booting into ChromeOS(Eupnea cannot be booted without those flags).

This is really problematic as going into sleep doesn't properly work and if ChromeOS has been wiped, one cannot re-enable USB and unsigned kernel booting without it.

To fix this, the systemd config file for power and sleep had to be overriden to sleep to S3. Sleeping to S3 is slightly less power efficient, but prevents the aforementioned NVRAM reset.
