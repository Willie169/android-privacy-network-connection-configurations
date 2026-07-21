## Android Privacy Network Connection Configurations (Old)

Here's my old network connection configurations on Android 16.

For app debloating, which is also important for privacy, refer to my [**Samsung-Android-Debloat-List**](https://github.com/Willie169/Samsung-Android-Debloat-List) repo. Even if you are not using Samsung phone, many parts of the repo still apply.

It may be even better for privacy to switch Personal and Work profile below. Note that Termux and functions requiring accessibility services only work in personal profile. You can access files in work profile via FTP server in apps such as [Material Files](https://github.com/zhanghai/MaterialFiles) from [F-Droid](https://f-droid.org/packages/me.zhanghai.android.files) in work profile, or ADB with Shizuku.

### Apps Configurations

- [Insular](https://gitlab.com/secure-system/Insular) (`com.oasisfeng.island.fdroid`) from [F-Droid](https://f-droid.org/packages/com.oasisfeng.island.fdroid) manages work profile. You can also use [Shelter](https://gitea.angry.im/PeterCxy/Shelter) (`net.typeblog.shelter`) from [F-Droid](https://droidify.app/app/?id=net.typeblog.shelter&repo_address=https://fdroid.typeblog.net). All apps with unwanted trackers are used in personal profile (also known as
    primary or main profile). Only trusted app are used in work profile. No account is in work profile. [Aurora Store](https://gitlab.com/AuroraOSS/AuroraStore) (`com.aurora.store`) from [F-Droid](https://f-droid.org/packages/com.aurora.store) is used to install apps from Google Play Store in it.
- [TrackerControl (TC)](https://github.com/TrackerControl/tracker-control-android) (`net.kollnig.missioncontrol.fdroid`) from [F-Droid](https://f-droid.org/packages/net.kollnig.missioncontrol.fdroid) in personal profile as VPN of personal profile except the rare case of [Tailscale personal profile](#tailscale-personal-profile)
  - Both Always-on VPN and Block connections without VPN turned on, ignoring the notification from TrackerControl about turning off Block connections without VPN
  - No app is excluded from VPN
  - Tracker blocker
  - UDP tracker blocker
  - Port forwarding: 53/UDP -> 5354, 53/TCP -> 5354
  - Socks5 proxy: -> 1080
  - You can see what domains each app (tried to) connect to in home page and log of connection attempts in three dots in the top right corner > Traffic log if enabled. I disabled internet connection for all system apps that do unnecessary internet connection. System apps that I didn't do so to avoid breaking things include:
    - Google Play Services, Google Services Framework, Google Play Store, Captive Portal Login, and MulticastDNSResponder: All the time.
    - Software update (which will also enable internet connection for a lot of Samsung apps): Only when downloading Software update.
- [InviZible Pro: Tor & Firewall, DNSCrypt & I2P](https://github.com/Gedsh/InviZible) (`pan.alexander.tordnscrypt.stable`) from [F-Droid](https://f-droid.org/packages/pan.alexander.tordnscrypt.stable) proxy mode in personal profile
  - Firewall: Only allow trusted apps to access internet
  - DNSCrypt server at port 5354
    - DNSCrypt servers: adguard-dns-unfiltered-doh/adguard-dns-unfiltered-doh-ipv6/cloudflare/cloudflare-ipv6
    - Bootstrap resolver: 1.1.1.1, 1.0.0.1, 2606:4700:4700::1111, 2606:4700:4700::1001, 94.140.14.140, 94.140.14.141, 2a10:50c0::1:ff, 2a10:50c0::2:ff
    - Remote blacklist: <https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts>
    - Local blacklist: Add if needed, e.g. social media block
    - Socks5 proxy: -> 1080 (when [without Tor](#without-tor)) or 9051 (when [with Tor](#with-tor))
  - Tor server when [with Tor](#with-tor)
    - Socks5 server at port 9051
    - Socks5 outbound proxy: -> 1080
- [Sock5](https://github.com/heiher/socks5) (`hev.socks5`) from [GitHub release](https://github.com/heiher/socks5/releases) in work profile:
  - Listen Address: 127.0.0.1
  - Listen Port: 1080
  - UDP Listen Address: 127.0.0.1
  - UDP Listen Port: 1080
  - Bind IPv4 Address: 0.0.0.0
  - Bind IPv6 Address: ::
  - Bind Interface: (empty)
  - Auth Username: (empty)
  - Auth Password: (empty)
- [Tailscale](https://github.com/tailscale/tailscale-android) (`com.tailscale.ipn`) from [F-Droid](https://f-droid.org/packages/com.tailscale.ipn) in work profile as VPN of work profile when using Tailscale
- [InviZible Pro: Tor & Firewall, DNSCrypt & I2P](https://github.com/Gedsh/InviZible) (`pan.alexander.tordnscrypt.stable`) from [F-Droid](https://f-droid.org/packages/pan.alexander.tordnscrypt.stable) VPN mode in work profile as VPN of work profile when not using Tailscale
  - DNSCrypt server at port 5355
    - DNSCrypt servers: adguard-dns-unfiltered-doh/adguard-dns-unfiltered-doh-ipv6/cloudflare/cloudflare-ipv6
    - Bootstrap resolver: 1.1.1.1, 1.0.0.1, 2606:4700:4700::1111, 2606:4700:4700::1001, 94.140.14.140, 94.140.14.141, 2a10:50c0::1:ff, 2a10:50c0::2:ff
    - Remote blacklist: <https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts>
    - Local blacklist: Add if needed, e.g. social media block
  - Tor server when needed
    - Socks5 server at port 9053
- [Tailscale](https://github.com/tailscale/tailscale-android) (`com.tailscale.ipn`) from [F-Droid](https://f-droid.org/packages/com.tailscale.ipn) in personal profile as VPN of personal profile when Tailscale UDP multicast is needed in personal profile
- [Snowflake Volunteer](https://github.com/blocoio/snowflake) (`io.bloco.snowflake`) from [F-Droid](https://f-droid.org/packages/io.bloco.snowflake) in work profile when charging to helping bypass censorship.
- [Tor Browser](https://www.torproject.org/download/#android) (`org.torproject.torbrowser`) from [FFUpdater](https://github.com/Tobi823/ffupdater) in work profile: If the goal is anonymity, use this instead of the [with Tor](#with-tor) configurations because Tor Browser not only change your IP but also protects fingerprints.
- [Material Files](https://github.com/zhanghai/MaterialFiles) from [F-Droid](https://f-droid.org/packages/me.zhanghai.android.files) in personal profile:
  - FTP server at port 12121 with password authorization when needed
- [Material Files](https://github.com/zhanghai/MaterialFiles) from [F-Droid](https://f-droid.org/packages/me.zhanghai.android.files) in work profile:
  - FTP server at port 12221 with password authorization

### Without Tor

- personal profile DNS over UDP or TCP requests at port 53 -> TrackerControl port forwarding to port 5354 -> personal profile InviZible Pro DNSCrypt server at port 5354 outbound through Socks5 proxy at port 1080 -> Socks5 Sock5 server at port 1080 -> work profile VPN -> DNS resolved
- personal profile other requests -> TrackerControl outbound through Socks5 proxy at port 1080 -> Socks5 Sock5 server at port 1080 -> work profile VPN -> Outbound
- work profile requests -> work profile VPN -> Outbound

### With Tor

UDP in personal profile won't work in this configuration.

- personal profile DNS over UDP or TCP requests at port 53 -> TrackerControl port forwarding to port 5354 -> personal profile InviZible Pro DNSCrypt server at port 5354 outbound through Socks5 proxy at port 9051 -> personal profile InviZible Pro Tor Socks5 server at port 9051 -> outbound through Socks5 proxy at port 1080 -> Socks5 Sock5 server at port 1080 -> work profile VPN -> DNS resolved
- personal profile other requests -> TrackerControl outbound through Socks5 proxy at port 9051 -> personal profile InviZible Pro Tor Socks5 server at port 9051 -> outbound through Socks5 proxy at port 1080 -> Socks5 Sock5 server at port 1080 -> work profile VPN -> outbound
- work profile requests -> work profile VPN -> Outbound

### Tailscale personal profile

Tailscale UDP multicast won't work in personal profile when Tailscale is running in work profile. Apps such as [RustDesk](https://github.com/rustdesk/rustdesk) (`com.carriez.flutter_hbb`) from [F-Droid](https://f-droid.org/packages/com.carriez.flutter_hbb) and [KDE Connect](https://invent.kde.org/network/kdeconnect-android) (`org.kde.kdeconnect_tp`) from [F-Droid](https://f-droid.org/packages/org.kde.kdeconnect_tp) rely on it to connect devices over Tailscale, while some use case such as RustDesk Input control only work in personal profile. In such case, Tailscale in personal profile may be used as personal profile VPN with the trade-off of disabling protection by TrackerControl and InviZible Pro in personal profile temporarily.
