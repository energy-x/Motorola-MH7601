# Motorola-MH7601

I know this is a Broadcom device, but I picked up a set of 3 for $10 at Amazon to play around with. I was able to get a serial connection and reset the root password on the device. It is running some custom version of OpenWrt and the web interface points to a landing.html under /www/luci-static/resources that just tells you to download an app. I realize a fully supported and working open version of OpenWrt is likely not happening, but if I can get Luci working to speed up clearing off the junk configs and potential spyware services I could use it as an AP. Here is the boot log along with version information. What other information can I gather to help?

After gaining serial console access I was able to mount_root and run passwd to change the root password for full device access.

I also found that there are a couple URLs under luci that will trigger enabling sshd and full access to luci.

<code>/cgi-bin/luci/admin/minim/enable_admin : after a log in will enable full luci
/cgi-bin/luci/admin/minim/start_sshd : after a log in will enable a basic dropbear sshd</code>

uname:
<code>
root@MH7601:/usr/bin# uname -a
Linux MH7601 4.19.151 #1 SMP PREEMPT Mon Sep 20 17:22:16 EDT 2021 armv7l GNU/Linux
</code>
ubus:
<code>
root@MH7601:/usr/bin# ubus call system board
{
        "kernel": "4.19.151",
        "hostname": "MH7601",
        "system": "ARMv7 Processor rev 5 (v7l)",
        "model": "Broadcom BCM947622",
        "board_name": "brcm,bcm947622",
        "release": {
                "distribution": "OpenWrt",
                "version": "2.0.0.224",
                "revision": "unknown",
                "target": "brcmbca/bcm947622",
                "description": "OpenWrt 2.0.0.224 e35b5f7"
        }
}
</code>
