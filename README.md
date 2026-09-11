**Please see this project for OpenWrt progress: https://github.com/Vaibhav-Solanki/openwrt-motorola-mh7021
**

# Motorola MH7601 (MH7603)
To access factory OpenWrt luci admin pages go to <code>https://[device-ip]/cgi-bin/luci/admin/minim/enable_admin</code>

Log in using <code>username 'root'</code> and the wifi password printed on the bottom of the case.
You will get an error message, but can now access and configure everything. 

Known issue: If you go to the System>Startup menu it will crash and reboot. You'll have to configure services through the command line.

Enable ssh: <code>https://[device-ip]/cgi-bin/luci/admin/minim/start_sshd</code>

Log in using <code>username 'root'</code> and the wifi password printed on the bottom of the case.
You will get an error message, but can now access via ssh.

I know this is a Broadcom device, but I picked up a set of 3 for $10 at Amazon to play around with. I was able to get a serial connection and reset the root password on the device. It is running some custom version of OpenWrt and the web interface points to a landing.html under /www/luci-static/resources that just tells you to download an app. I realize a fully supported and working open version of OpenWrt is likely not happening, but if I can get Luci working to speed up clearing off the junk configs and potential spyware services I could use it as an AP. Here is the boot log along with version information. What other information can I gather to help?

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


More information on disabling the call home:

sajjoseph on Jan 18

Here are some more details around what the system does. Current OS is configured to talk to minim.co site.

support.minim.co,
api.minim.co,
my.minim.co,
releases.minim.co,
provision.minim.co
Minim guys have their unum code published here.
https://github.com/MinimSecure/unum-sdk?tab=readme-ov-file

/usr/bin/unum --> This binary is talking to the minim.co site servers.
You can see that there is another script - /usr/bin/unum_status_report.sh which checks /tmp/provision_info.json.
I renamed /usr/bin/unum and noticed that the system is not making calls to the minim server anymore.
Note that if you are managing your router instance through the mobile app, the above steps will break it. Hope you know what you are doing.
