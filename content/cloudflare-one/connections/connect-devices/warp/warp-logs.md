---
pcx_content_type: reference
title: Debug logs
weight: 7
---

# Debug logs

The WARP client provides diagnostic logs that you can use to troubleshoot connectivity issues on a device.

## macOS/Windows/Linux

### Retrieve logs

To view debug logs on desktop devices:


### `warp-diag` logs

The `warp-debugging-info.zip` archive contains the following files:

{{<table-wrap>}}
| File name          | Description |
| ------------------ | ----------- |
| `boringtun.log`    | Log for the WireGuard tunnel that serves traffic from the device to Cloudflare's edge. |
| `connectivity.txt` | DNS resolution and HTTP trace requests to [validate a successful connection](/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#connectivity-check). The trace for `connectivity.cloudflareclient.com` should show `warp=on` and optionally `gateway=on` (if TCP proxy is enabled). The trace for `engage.cloudflareclient.com` should show `warp=off` and `gateway=off`. |
| `daemon.log`       | Communication between the device and Cloudflare's edge. For more information, refer to the list of [common daemon errors]().|
| `daemon_dns.log`   | Contains detailed DNS logs if **Log DNS queries** was enabled in the WARP client. |
| `date.txt`         | Date and time (UTC) when you ran the `warp-diag` command.|
| `dns-check.txt`    | Verifies that the WARP DNS servers are set as system default. For [operating modes](/cloudflare-one/connections/connect-devices/warp/#warp-client-modes) where DNS filtering is enabled, this file should contain the IPs of the WARP DNS servers (`127.0.2.2` and `127.0.2.3`). |
| `dns_stats.log`    | Number of DNS queries received and resolved by WARP every two minutes. |
| `etc-hosts.txt`    | Static DNS config of device. |
| `gui-launcher.log` | ????? |
| `gui-log.log`      | Log file for the GUI app that users interact with. |
| `hostname.txt`     | Name of the device. |
| `ifconfig.txt` </br> `ipconfig.txt`    | IP configuration of each network interface. |
| `installer.log`    | MSI or PKG installation log |
| `mdm.xml` </br> `mdm.plist` </br> `local_policy_redacted.txt` | [Managed deployment parameters](/cloudflare-one/connections/connect-devices/warp/deployment/mdm-deployment/parameters/) on the device. |
| `netstat.txt` </br> `routetable.txt` | Routing table used by the device.  |
| `netstat-v6.txt`   | IPv6 routing table (Linux only). |
| `platform.txt`     | Operating system of the device. |
| `ps.txt` <br> `processes.txt` | List of all active processes on the device when `warp-diag` was run. |
| `resolv.conf`      |  The contents of the `/etc/resolv.conf` file on Mac/Linux, where system DNS servers are configured. |
| `route.txt`        | Output from the `route get` command used to verify that network traffic is going over the correct interface. Routes to our [client orchestration API IPs](/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#client-orchestration-api) should show an `en` or `wifi` interface. If the API IPs show `utun` or some other adapter, this likely means a third-party firewall or VPN is intercepting the connection. |
| `scutil-dns.txt`   | DNS configuration on Mac/Linux (available in `ipconfig.txt` on Windows). |
| `scutil-proxy.txt` | Proxy configuration on Mac/Linux (available in `ipconfig.txt` on Windows). |
| `stats.log`        | Uptime and throughput stats for the WARP tunnel. ???? WARP tunnel == Wireguard tunnel ???? |
| `sw-vers.txt`      | Operating system of the device. |
| `sysinfo.json`     | CPU and memory usage when `warp-diag` was run. This information is useful for determining whether slow speeds are due to heavy system load. |
| `systeminfo.txt` </br> `system-profile.txt` | System software information.  |
| `timezone.txt`     | Local timezone of the device specified as a UTC offset. |
| `traceroute.txt`   | Traceroute to the [WARP ingress IPs](/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#warp-ingress-ip) showing the path from the device to Cloudflare's edge.|
| `uname.txt`        |  Linux-only system information including kernel version. |
| `v4interfaces.txt` </br> `v4subinterfaces.txt` </br> `v6interfaces.txt` </br> `v6subinterfaces.txt` | Stats for IPv4 and IPv6 interfaces. |
| `version.txt`      | [WARP client version](/cloudflare-one/connections/connect-devices/warp/download-warp/) installed on the device. |
| `warp-account.txt` | WARP client device enrollment information. |
| `warp-device-posture.txt` | [Device posture data](/cloudflare-one/identity/devices/warp-client-checks/) obtained by the WARP client. |
| `warp-dns-stats.txt`| ??????|
| `warp-network.txt` | ??????? |
| `warp-settings.txt`| [WARP client settings](/cloudflare-one/connections/connect-devices/warp/configure-warp/warp-settings/) applied to the device. |
| `warp-stats.txt`   | ????????? |
| `warp-status.txt`  | Status of WARP switch when `warp-diag` was run. |

{{</table-wrap>}}

#### Multiple versions of the same log

The `warp-debugging-info` folder may contain multiple versions of the same log, such as `daemon.log`, `daemon.1.log`, and `daemon.2.log`. Since logs can get very long, they are rotated either daily or when they exceed a certain size.

- `<logfile>.log` is the most current log. This is almost always the log you should be looking at, as it shows events that occured on the day you ran the `warp-diag` command.
- `<logfile>.1.log` shows events from the previous day.
- `<logfile>.2.log` shows events from two days before.

{{<Aside type="note">}}
In timestamped logs such as `daemon.log`, the most recent events will appear at the end of the file.
{{</Aside>}}

## iOS/Android/ChromeOS

### Retrieve logs

To view debug logs on mobile devices:

1. Open the 1.1.1.1 app.
2. Go to **Settings** > **Advanced** > **Diagnostics**.
3. Scroll down to **Debug logs** and choose from the [available logs](#mobile-app-logs).

### Mobile app logs

Mobile app logs contain a subset of the information available for desktop clients. To learn more about these files, refer to their equivalent [warp-diag logs](#warp-diag-logs).

#### iOS

| Name          | Equivalent warp-diag log |
| ------------------ | ----------- | 
| **DNS logs**       | `daemon_dns.log`|
| **Console logs** > **Extension logs** | `daemon.log`|
| **Console logs** > **Application logs** | `connectivity.txt` and `gui-log.log`|
| **Routing table**  | `netstat.txt`|

#### Android/ChromeOS

| Name          | Equivalent warp-diag log |
| ------------------ | ----------- |
| **DNS logs**       | `daemon_dns.log`|
| **Console logs** | `connectivity.txt`, `netstat.log`, and `gui-log.log` |
| **Native logs**  | `daemon.log` |