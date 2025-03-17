azureuser@TP:/tp$ trivy image a0b30
2025-03-17T10:14:05Z    INFO    [vuln] Vulnerability scanning is enabled
2025-03-17T10:14:05Z    INFO    [secret] Secret scanning is enabled
2025-03-17T10:14:05Z    INFO    [secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2025-03-17T10:14:05Z    INFO    [secret] Please see also https://trivy.dev/v0.60/docs/scanner/secret#recommendation for faster secret detection
2025-03-17T10:14:32Z    INFO    Detected OS     family="debian" version="12.9"
2025-03-17T10:14:32Z    INFO    [debian] Detecting vulnerabilities...   os_version="12" pkg_num=136
2025-03-17T10:14:32Z    INFO    Number of language-specific files       num=0
2025-03-17T10:14:32Z    WARN    Using severities from other vendors for some vulnerabilities. Read https://trivy.dev/v0.60/docs/scanner/vulnerability#severity-selection for details.

Report Summary

┌────────────────────────────────────────┬────────┬─────────────────┬─────────┐
│                 Target                 │  Type  │ Vulnerabilities │ Secrets │
├────────────────────────────────────────┼────────┼─────────────────┼─────────┤
│ a0b30 (debian 12.9)                    │ debian │       174       │    -    │
├────────────────────────────────────────┼────────┼─────────────────┼─────────┤
│ /etc/ssl/private/ssl-cert-snakeoil.key │  text  │        -        │    1    │
└────────────────────────────────────────┴────────┴─────────────────┴─────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)


a0b30 (debian 12.9)

Total: 174 (UNKNOWN: 0, LOW: 127, MEDIUM: 34, HIGH: 12, CRITICAL: 1)

┌────────────────────┬─────────────────────┬──────────┬──────────────┬─────────────────────────┬─────────────────┬──────────────────────────────────────────────────────────────┐
│      Library       │    Vulnerability    │ Severity │    Status    │    Installed Version    │  Fixed Version  │                            Title                             │
├────────────────────┼─────────────────────┼──────────┼──────────────┼─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ apache2            │ CVE-2001-1534       │ LOW      │ affected     │ 2.4.62-1~deb12u2        │                 │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                    │                     │          │              │                         │                 │ session ID's u ...                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1307       │          │              │                         │                 │ The mod_php module for the Apache HTTP Server allows local   │
│                    │                     │          │              │                         │                 │ users with...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1580       │          │              │                         │                 │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                    │                     │          │              │                         │                 │ enabled for clie...                                          │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1581       │          │              │                         │                 │ httpd: Injection of arbitrary text into log files when DNS   │
│                    │                     │          │              │                         │                 │ resolution is...                                             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-0086       │          │              │                         │                 │ The Apache HTTP Server, when accessed through a TCP          │
│                    │                     │          │              │                         │                 │ connection with a...                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-0086                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-1743       │          │              │                         │                 │ suexec in Apache HTTP Server (httpd) 2.2.3 does not verify   │
│                    │                     │          │              │                         │                 │ combination ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-1743                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-3303       │          │              │                         │                 │ Apache httpd 2.0.59 and 2.2.4, with the Prefork MPM module,  │
│                    │                     │          │              │                         │                 │ allows loc...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-3303                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2008-0456       │          │              │                         │                 │ httpd: mod_negotiation CRLF injection via untrusted file     │
│                    │                     │          │              │                         │                 │ names in directories with MultiViews...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2008-0456                    │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ apache2-bin        │ CVE-2001-1534       │          │              │                         │                 │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                    │                     │          │              │                         │                 │ session ID's u ...                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1307       │          │              │                         │                 │ The mod_php module for the Apache HTTP Server allows local   │
│                    │                     │          │              │                         │                 │ users with...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1580       │          │              │                         │                 │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                    │                     │          │              │                         │                 │ enabled for clie...                                          │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1581       │          │              │                         │                 │ httpd: Injection of arbitrary text into log files when DNS   │
│                    │                     │          │              │                         │                 │ resolution is...                                             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-0086       │          │              │                         │                 │ The Apache HTTP Server, when accessed through a TCP          │
│                    │                     │          │              │                         │                 │ connection with a...                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-0086                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-1743       │          │              │                         │                 │ suexec in Apache HTTP Server (httpd) 2.2.3 does not verify   │
│                    │                     │          │              │                         │                 │ combination ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-1743                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-3303       │          │              │                         │                 │ Apache httpd 2.0.59 and 2.2.4, with the Prefork MPM module,  │
│                    │                     │          │              │                         │                 │ allows loc...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-3303                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2008-0456       │          │              │                         │                 │ httpd: mod_negotiation CRLF injection via untrusted file     │
│                    │                     │          │              │                         │                 │ names in directories with MultiViews...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2008-0456                    │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ apache2-data       │ CVE-2001-1534       │          │              │                         │                 │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                    │                     │          │              │                         │                 │ session ID's u ...                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1307       │          │              │                         │                 │ The mod_php module for the Apache HTTP Server allows local   │
│                    │                     │          │              │                         │                 │ users with...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1580       │          │              │                         │                 │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                    │                     │          │              │                         │                 │ enabled for clie...                                          │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1581       │          │              │                         │                 │ httpd: Injection of arbitrary text into log files when DNS   │
│                    │                     │          │              │                         │                 │ resolution is...                                             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-0086       │          │              │                         │                 │ The Apache HTTP Server, when accessed through a TCP          │
│                    │                     │          │              │                         │                 │ connection with a...                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-0086                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-1743       │          │              │                         │                 │ suexec in Apache HTTP Server (httpd) 2.2.3 does not verify   │
│                    │                     │          │              │                         │                 │ combination ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-1743                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-3303       │          │              │                         │                 │ Apache httpd 2.0.59 and 2.2.4, with the Prefork MPM module,  │
│                    │                     │          │              │                         │                 │ allows loc...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-3303                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2008-0456       │          │              │                         │                 │ httpd: mod_negotiation CRLF injection via untrusted file     │
│                    │                     │          │              │                         │                 │ names in directories with MultiViews...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2008-0456                    │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ apache2-utils      │ CVE-2001-1534       │          │              │                         │                 │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                    │                     │          │              │                         │                 │ session ID's u ...                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1307       │          │              │                         │                 │ The mod_php module for the Apache HTTP Server allows local   │
│                    │                     │          │              │                         │                 │ users with...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1580       │          │              │                         │                 │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                    │                     │          │              │                         │                 │ enabled for clie...                                          │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2003-1581       │          │              │                         │                 │ httpd: Injection of arbitrary text into log files when DNS   │
│                    │                     │          │              │                         │                 │ resolution is...                                             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-0086       │          │              │                         │                 │ The Apache HTTP Server, when accessed through a TCP          │
│                    │                     │          │              │                         │                 │ connection with a...                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-0086                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-1743       │          │              │                         │                 │ suexec in Apache HTTP Server (httpd) 2.2.3 does not verify   │
│                    │                     │          │              │                         │                 │ combination ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-1743                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-3303       │          │              │                         │                 │ Apache httpd 2.0.59 and 2.2.4, with the Prefork MPM module,  │
│                    │                     │          │              │                         │                 │ allows loc...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-3303                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2008-0456       │          │              │                         │                 │ httpd: mod_negotiation CRLF injection via untrusted file     │
│                    │                     │          │              │                         │                 │ names in directories with MultiViews...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2008-0456                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ apt                │ CVE-2011-3374       │          │              │ 2.6.1                   │                 │ It was found that apt-key in apt, all versions, do not       │
│                    │                     │          │              │                         │                 │ correctly...                                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-3374                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ bash               │ TEMP-0841856-B18BAF │          │              │ 5.2.15-2+b7             │                 │ [Privilege escalation possible to other user than root]      │
│                    │                     │          │              │                         │                 │ https://security-tracker.debian.org/tracker/TEMP-0841856-B1- │
│                    │                     │          │              │                         │                 │ 8BAF
                                                        │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ bsdutils           │ CVE-2022-0563       │          │              │ 1:2.38.1-5+deb12u3      │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┤          ├──────────────┼─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ coreutils          │ CVE-2016-2781       │          │ will_not_fix │ 9.1-1                   │                 │ coreutils: Non-privileged session can escape to the parent   │
│                    │                     │          │              │                         │                 │ session in chroot                                            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2016-2781                    │
│                    ├─────────────────────┤          ├──────────────┤                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2017-18018      │          │ affected     │                         │                 │ coreutils: race condition vulnerability in chown and chgrp   │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2017-18018                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ gcc-12-base        │ CVE-2022-27943      │          │              │ 12.2.0-14               │                 │ binutils: libiberty/rust-demangle.c in GNU GCC 11.2 allows   │
│                    │                     │          │              │                         │                 │ stack exhaustion in demangle_const                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-27943                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-4039       │          │              │                         │                 │ gcc: -fstack-protector fails to guard dynamic stack          │
│                    │                     │          │              │                         │                 │ allocations on ARM64                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4039                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ gpgv               │ CVE-2022-3219       │          │              │ 2.2.40-1.1              │                 │ gnupg: denial of service issue (resource consumption) using  │
│                    │                     │          │              │                         │                 │ compressed packets                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-3219                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ krb5-locales       │ CVE-2024-26462      │ MEDIUM   │              │ 1.20.1-2+deb12u2        │                 │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24528      │          │              │                         │                 │ krb5: overflow when calculating ulog block size              │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24528                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-5709       │ LOW      │              │                         │                 │ krb5: integer overflow in dbentry->n_key_data in             │
│                    │                     │          │              │                         │                 │ kadmin/dbutil/dump.c                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-5709                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26458      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/rpc/pmap_rmt.c            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26458                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26461      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/gssapi/krb5/k5sealv3.c    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26461                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libapt-pkg6.0      │ CVE-2011-3374       │          │              │ 2.6.1                   │                 │ It was found that apt-key in apt, all versions, do not       │
│                    │                     │          │              │                         │                 │ correctly...                                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-3374                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libblkid1          │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┼──────────┼──────────────┼─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libc-bin           │ CVE-2025-0395       │ MEDIUM   │ fixed        │ 2.36-9+deb12u9          │ 2.36-9+deb12u10 │ glibc: buffer overflow in the GNU C Library's assert()       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-0395                    │
│                    ├─────────────────────┼──────────┼──────────────┤                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2010-4756       │ LOW      │ affected     │                         │                 │ glibc: glob implementation can cause excessive CPU and       │
│                    │                     │          │              │                         │                 │ memory consumption due to...                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2010-4756                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-20796      │          │              │                         │                 │ glibc: uncontrolled recursion in function                    │
│                    │                     │          │              │                         │                 │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-20796                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010022    │          │              │                         │                 │ glibc: stack guard protection bypass                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010022                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010023    │          │              │                         │                 │ glibc: running ldd on malicious ELF leads to code execution  │
│                    │                     │          │              │                         │                 │ because of...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010023                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010024    │          │              │                         │                 │ glibc: ASLR bypass using cache of thread stack and heap      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010024                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010025    │          │              │                         │                 │ glibc: information disclosure of heap addresses of           │
│                    │                     │          │              │                         │                 │ pthread_created thread                                       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010025                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-9192       │          │              │                         │                 │ glibc: uncontrolled recursion in function                    │
│                    │                     │          │              │                         │                 │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-9192                    │
├────────────────────┼─────────────────────┼──────────┼──────────────┤                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libc6              │ CVE-2025-0395       │ MEDIUM   │ fixed        │                         │ 2.36-9+deb12u10 │ glibc: buffer overflow in the GNU C Library's assert()       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-0395                    │
│                    ├─────────────────────┼──────────┼──────────────┤                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2010-4756       │ LOW      │ affected     │                         │                 │ glibc: glob implementation can cause excessive CPU and       │
│                    │                     │          │              │                         │                 │ memory consumption due to...                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2010-4756                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-20796      │          │              │                         │                 │ glibc: uncontrolled recursion in function                    │
│                    │                     │          │              │                         │                 │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-20796                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010022    │          │              │                         │                 │ glibc: stack guard protection bypass                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010022                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010023    │          │              │                         │                 │ glibc: running ldd on malicious ELF leads to code execution  │
│                    │                     │          │              │                         │                 │ because of...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010023                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010024    │          │              │                         │                 │ glibc: ASLR bypass using cache of thread stack and heap      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010024                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-1010025    │          │              │                         │                 │ glibc: information disclosure of heap addresses of           │
│                    │                     │          │              │                         │                 │ pthread_created thread                                       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-1010025                 │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2019-9192       │          │              │                         │                 │ glibc: uncontrolled recursion in function                    │
│                    │                     │          │              │                         │                 │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2019-9192                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libcap2            │ CVE-2025-1390       │ MEDIUM   │              │ 1:2.66-4                │                 │ libcap: pam_cap: Fix potential configuration parsing error   │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-1390                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libcurl4           │ CVE-2024-2379       │ LOW      │              │ 7.88.1-10+deb12u12      │                 │ curl: QUIC certificate check bypass with wolfSSL             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-2379                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-0725       │          │              │                         │                 │ libcurl: Buffer Overflow in libcurl via zlib Integer         │
│                    │                     │          │              │                         │                 │ Overflow                                                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-0725                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libexpat1          │ CVE-2023-52425      │ HIGH     │              │ 2.5.0-1+deb12u1         │                 │ expat: parsing large tokens can trigger a denial of service  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-52425                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-8176       │          │              │                         │                 │ libexpat: expat: Improper Restriction of XML Entity          │
│                    │                     │          │              │                         │                 │ Expansion Depth in libexpat                                  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-8176                    │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-50602      │ MEDIUM   │              │                         │                 │ libexpat: expat: DoS via XML_ResumeParser                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-50602                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-52426      │ LOW      │              │                         │                 │ expat: recursive XML entity expansion vulnerability          │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-52426                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-28757      │          │              │                         │                 │ expat: XML Entity Expansion                                  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-28757                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libgcc-s1          │ CVE-2022-27943      │          │              │ 12.2.0-14               │                 │ binutils: libiberty/rust-demangle.c in GNU GCC 11.2 allows   │
│                    │                     │          │              │                         │                 │ stack exhaustion in demangle_const                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-27943                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-4039       │          │              │                         │                 │ gcc: -fstack-protector fails to guard dynamic stack          │
│                    │                     │          │              │                         │                 │ allocations on ARM64                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4039                    │
├────────────────────┼─────────────────────┼──────────┼──────────────┼─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libgcrypt20        │ CVE-2024-2236       │ MEDIUM   │ fix_deferred │ 1.10.1-3                │                 │ libgcrypt: vulnerable to Marvin Attack                       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-2236                    │
│                    ├─────────────────────┼──────────┼──────────────┤                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-6829       │ LOW      │ affected     │                         │                 │ libgcrypt: ElGamal implementation doesn't have semantic      │
│                    │                     │          │              │                         │                 │ security due to incorrectly encoded plaintexts...            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-6829                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libgnutls30        │ CVE-2011-3389       │          │              │ 3.7.9-2+deb12u4         │                 │ HTTPS: block-wise chosen-plaintext attack against SSL/TLS    │
│                    │                     │          │              │                         │                 │ (BEAST)                                                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-3389                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libgssapi-krb5-2   │ CVE-2024-26462      │ MEDIUM   │              │ 1.20.1-2+deb12u2        │                 │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24528      │          │              │                         │                 │ krb5: overflow when calculating ulog block size              │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24528                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-5709       │ LOW      │              │                         │                 │ krb5: integer overflow in dbentry->n_key_data in             │
│                    │                     │          │              │                         │                 │ kadmin/dbutil/dump.c                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-5709                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26458      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/rpc/pmap_rmt.c            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26458                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26461      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/gssapi/krb5/k5sealv3.c    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26461                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libjansson4        │ CVE-2020-36325      │          │              │ 2.14-2                  │                 │ jansson: out-of-bounds read in json_loads() due to a parsing │
│                    │                     │          │              │                         │                 │ error
                                                        │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2020-36325                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libk5crypto3       │ CVE-2024-26462      │ MEDIUM   │              │ 1.20.1-2+deb12u2        │                 │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24528      │          │              │                         │                 │ krb5: overflow when calculating ulog block size              │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24528                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-5709       │ LOW      │              │                         │                 │ krb5: integer overflow in dbentry->n_key_data in             │
│                    │                     │          │              │                         │                 │ kadmin/dbutil/dump.c                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-5709                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26458      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/rpc/pmap_rmt.c            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26458                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26461      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/gssapi/krb5/k5sealv3.c    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26461                   │
├────────────────────┼─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libkrb5-3          │ CVE-2024-26462      │ MEDIUM   │              │                         │                 │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24528      │          │              │                         │                 │ krb5: overflow when calculating ulog block size              │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24528                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-5709       │ LOW      │              │                         │                 │ krb5: integer overflow in dbentry->n_key_data in             │
│                    │                     │          │              │                         │                 │ kadmin/dbutil/dump.c                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-5709                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26458      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/rpc/pmap_rmt.c            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26458                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26461      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/gssapi/krb5/k5sealv3.c    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26461                   │
├────────────────────┼─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libkrb5support0    │ CVE-2024-26462      │ MEDIUM   │              │                         │                 │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24528      │          │              │                         │                 │ krb5: overflow when calculating ulog block size              │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24528                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2018-5709       │ LOW      │              │                         │                 │ krb5: integer overflow in dbentry->n_key_data in             │
│                    │                     │          │              │                         │                 │ kadmin/dbutil/dump.c                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2018-5709                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26458      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/rpc/pmap_rmt.c            │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26458                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-26461      │          │              │                         │                 │ krb5: Memory leak at /krb5/src/lib/gssapi/krb5/k5sealv3.c    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-26461                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libldap-2.5-0      │ CVE-2023-2953       │ HIGH     │              │ 2.5.13+dfsg-5           │                 │ openldap: null pointer dereference in ber_memalloc_x         │
│                    │                     │          │              │                         │                 │ function                                                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-2953                    │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2015-3276       │ LOW      │              │                         │                 │ openldap: incorrect multi-keyword mode cipherstring parsing  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2015-3276                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2017-14159      │          │              │                         │                 │ openldap: Privilege escalation via PID file manipulation     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2017-14159                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2017-17740      │          │              │                         │                 │ openldap: contrib/slapd-modules/nops/nops.c attempts to free │
│                    │                     │          │              │                         │                 │ stack buffer allowing remote attackers to cause...           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2017-17740                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2020-15719      │          │              │                         │                 │ openldap: Certificate validation incorrectly matches name    │
│                    │                     │          │              │                         │                 │ against CN-ID                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2020-15719                   │
├────────────────────┼─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libldap-common     │ CVE-2023-2953       │ HIGH     │              │                         │                 │ openldap: null pointer dereference in ber_memalloc_x         │
│                    │                     │          │              │                         │                 │ function                                                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-2953                    │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2015-3276       │ LOW      │              │                         │                 │ openldap: incorrect multi-keyword mode cipherstring parsing  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2015-3276                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2017-14159      │          │              │                         │                 │ openldap: Privilege escalation via PID file manipulation     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2017-14159                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2017-17740      │          │              │                         │                 │ openldap: contrib/slapd-modules/nops/nops.c attempts to free │
│                    │                     │          │              │                         │                 │ stack buffer allowing remote attackers to cause...           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2017-17740                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2020-15719      │          │              │                         │                 │ openldap: Certificate validation incorrectly matches name    │
│                    │                     │          │              │                         │                 │ against CN-ID                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2020-15719                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libmount1          │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libncursesw6       │ CVE-2023-50495      │ MEDIUM   │              │ 6.4-4                   │                 │ ncurses: segmentation fault via _nc_wrap_entry()             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-50495                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libpam-modules     │ CVE-2024-10041      │          │              │ 1.5.2-6+deb12u1         │                 │ pam: libpam: Libpam vulnerable to read hashed password       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-10041                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-22365      │          │              │                         │                 │ pam: allowing unprivileged user to block another user        │
│                    │                     │          │              │                         │                 │ namespace                                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-22365                   │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libpam-modules-bin │ CVE-2024-10041      │          │              │                         │                 │ pam: libpam: Libpam vulnerable to read hashed password       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-10041                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-22365      │          │              │                         │                 │ pam: allowing unprivileged user to block another user        │
│                    │                     │          │              │                         │                 │ namespace                                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-22365                   │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libpam-runtime     │ CVE-2024-10041      │          │              │                         │                 │ pam: libpam: Libpam vulnerable to read hashed password       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-10041                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-22365      │          │              │                         │                 │ pam: allowing unprivileged user to block another user        │
│                    │                     │          │              │                         │                 │ namespace                                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-22365                   │
├────────────────────┼─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ libpam0g           │ CVE-2024-10041      │          │              │                         │                 │ pam: libpam: Libpam vulnerable to read hashed password       │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-10041                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-22365      │          │              │                         │                 │ pam: allowing unprivileged user to block another user        │
│                    │                     │          │              │                         │                 │ namespace                                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-22365                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libperl5.36        │ CVE-2023-31484      │ HIGH     │              │ 5.36.0-7+deb12u1        │                 │ perl: CPAN.pm does not verify TLS certificates when          │
│                    │                     │          │              │                         │                 │ downloading distributions over HTTPS...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2011-4116       │ LOW      │              │                         │                 │ perl: File:: Temp insecure temporary file handling           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-4116                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31486      │          │              │                         │                 │ http-tiny: insecure TLS cert default                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31486                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libproc2-0         │ CVE-2023-4016       │          │              │ 2:4.0.2-3               │                 │ procps: ps buffer overflow                                   │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4016                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libsmartcols1      │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libsqlite3-0       │ CVE-2021-45346      │          │              │ 3.40.1-2+deb12u1        │                 │ sqlite: crafted SQL query allows a malicious user to obtain  │
│                    │                     │          │              │                         │                 │ sensitive information...                                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2021-45346                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libssl3            │ CVE-2024-13176      │ MEDIUM   │              │ 3.0.15-1~deb12u1        │                 │ openssl: Timing side-channel in ECDSA signature computation  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-13176                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libstdc++6         │ CVE-2022-27943      │ LOW      │              │ 12.2.0-14               │                 │ binutils: libiberty/rust-demangle.c in GNU GCC 11.2 allows   │
│                    │                     │          │              │                         │                 │ stack exhaustion in demangle_const                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-27943                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-4039       │          │              │                         │                 │ gcc: -fstack-protector fails to guard dynamic stack          │
│                    │                     │          │              │                         │                 │ allocations on ARM64                                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4039                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libsystemd0        │ CVE-2013-4392       │          │              │ 252.33-1~deb12u1        │                 │ systemd: TOCTOU race condition when updating file            │
│                    │                     │          │              │                         │                 │ permissions and SELinux security contexts...                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2013-4392                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31437      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ modify a...                                                  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31437                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31438      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ truncate a...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31438                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31439      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ modify the...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31439                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libtinfo6          │ CVE-2023-50495      │ MEDIUM   │              │ 6.4-4                   │                 │ ncurses: segmentation fault via _nc_wrap_entry()             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-50495                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libudev1           │ CVE-2013-4392       │ LOW      │              │ 252.33-1~deb12u1        │                 │ systemd: TOCTOU race condition when updating file            │
│                    │                     │          │              │                         │                 │ permissions and SELinux security contexts...                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2013-4392                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31437      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ modify a...                                                  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31437                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31438      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ truncate a...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31438                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31439      │          │              │                         │                 │ An issue was discovered in systemd 253. An attacker can      │
│                    │                     │          │              │                         │                 │ modify the...                                                │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31439                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libuuid1           │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ libxml2            │ CVE-2024-25062      │ HIGH     │              │ 2.9.14+dfsg-1.3~deb12u1 │                 │ libxml2: use-after-free in XMLReader                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-25062                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-56171      │          │              │                         │                 │ libxml2: Use-After-Free in libxml2                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-56171                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-24928      │          │              │                         │                 │ libxml2: Stack-based buffer overflow in xmlSnprintfElements  │
│                    │                     │          │              │                         │                 │ of libxml2                                                   │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-24928                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2025-27113      │          │              │                         │                 │ libxml2: NULL Pointer Dereference in libxml2 xmlPatMatch     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2025-27113                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2022-49043      │ MEDIUM   │              │                         │                 │ libxml: use-after-free in xmlXIncludeAddNode                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-49043                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-39615      │          │              │                         │                 │ libxml2: crafted xml can cause global buffer overflow        │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-39615                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-45322      │          │              │                         │                 │ libxml2: use-after-free in xmlUnlinkNode() in tree.c         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-45322                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-34459      │ LOW      │              │                         │                 │ libxml2: buffer over-read in xmlHTMLPrintFileContext in      │
│                    │                     │          │              │                         │                 │ xmllint.c                                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-34459                   │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ login              │ CVE-2023-4641       │ MEDIUM   │              │ 1:4.13+dfsg1-1+b1       │                 │ shadow-utils: possible password leak during passwd(1) change │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4641                    │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-5686       │ LOW      │              │                         │                 │ initscripts in rPath Linux 1 sets insecure permissions for   │
│                    │                     │          │              │                         │                 │ the /var/lo ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-5686                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-29383      │          │              │                         │                 │ shadow: Improper input validation in shadow-utils package    │
│                    │                     │          │              │                         │                 │ utility chfn                                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-29383                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-56433      │          │              │                         │                 │ shadow-utils: Default subordinate ID configuration in        │
│                    │                     │          │              │                         │                 │ /etc/login.defs could lead to compromise                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-56433                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ TEMP-0628843-DBAD28 │          │              │                         │                 │ [more related to CVE-2005-4890]                              │
│                    │                     │          │              │                         │                 │ https://security-tracker.debian.org/tracker/TEMP-0628843-DB- │
│                    │                     │          │              │                         │                 │ AD28
                                                        │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ mount              │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ ncurses-base       │ CVE-2023-50495      │ MEDIUM   │              │ 6.4-4                   │                 │ ncurses: segmentation fault via _nc_wrap_entry()             │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-50495                   │
├────────────────────┤                     │          │              │                         ├─────────────────┤                                                              │
│ ncurses-bin        │                     │          │              │                         │                 │
                                                        │
│                    │                     │          │              │                         │                 │
                                                        │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ openssl            │ CVE-2024-13176      │          │              │ 3.0.15-1~deb12u1        │                 │ openssl: Timing side-channel in ECDSA signature computation  │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-13176                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ passwd             │ CVE-2023-4641       │          │              │ 1:4.13+dfsg1-1+b1       │                 │ shadow-utils: possible password leak during passwd(1) change │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4641                    │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2007-5686       │ LOW      │              │                         │                 │ initscripts in rPath Linux 1 sets insecure permissions for   │
│                    │                     │          │              │                         │                 │ the /var/lo ......                                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2007-5686                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-29383      │          │              │                         │                 │ shadow: Improper input validation in shadow-utils package    │
│                    │                     │          │              │                         │                 │ utility chfn                                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-29383                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2024-56433      │          │              │                         │                 │ shadow-utils: Default subordinate ID configuration in        │
│                    │                     │          │              │                         │                 │ /etc/login.defs could lead to compromise                     │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2024-56433                   │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ TEMP-0628843-DBAD28 │          │              │                         │                 │ [more related to CVE-2005-4890]                              │
│                    │                     │          │              │                         │                 │ https://security-tracker.debian.org/tracker/TEMP-0628843-DB- │
│                    │                     │          │              │                         │                 │ AD28
                                                        │
├────────────────────┼─────────────────────┼──────────┤              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ perl               │ CVE-2023-31484      │ HIGH     │              │ 5.36.0-7+deb12u1        │                 │ perl: CPAN.pm does not verify TLS certificates when          │
│                    │                     │          │              │                         │                 │ downloading distributions over HTTPS...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2011-4116       │ LOW      │              │                         │                 │ perl: File:: Temp insecure temporary file handling           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-4116                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31486      │          │              │                         │                 │ http-tiny: insecure TLS cert default                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31486                   │
├────────────────────┼─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ perl-base          │ CVE-2023-31484      │ HIGH     │              │                         │                 │ perl: CPAN.pm does not verify TLS certificates when          │
│                    │                     │          │              │                         │                 │ downloading distributions over HTTPS...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2011-4116       │ LOW      │              │                         │                 │ perl: File:: Temp insecure temporary file handling           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-4116                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31486      │          │              │                         │                 │ http-tiny: insecure TLS cert default                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31486                   │
├────────────────────┼─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│ perl-modules-5.36  │ CVE-2023-31484      │ HIGH     │              │                         │                 │ perl: CPAN.pm does not verify TLS certificates when          │
│                    │                     │          │              │                         │                 │ downloading distributions over HTTPS...                      │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
│                    ├─────────────────────┼──────────┤              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2011-4116       │ LOW      │              │                         │                 │ perl: File:: Temp insecure temporary file handling           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2011-4116                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ CVE-2023-31486      │          │              │                         │                 │ http-tiny: insecure TLS cert default                         │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-31486                   │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ procps             │ CVE-2023-4016       │          │              │ 2:4.0.2-3               │                 │ procps: ps buffer overflow                                   │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-4016                    │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ sysvinit-utils     │ TEMP-0517018-A83CE6 │          │              │ 3.06-4                  │                 │ [sysvinit: no-root option in expert installer exposes        │
│                    │                     │          │              │                         │                 │ locally exploitable security flaw]                           │
│                    │                     │          │              │                         │                 │ https://security-tracker.debian.org/tracker/TEMP-0517018-A8- │
│                    │                     │          │              │                         │                 │ 3CE6
                                                        │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ tar                │ CVE-2005-2541       │          │              │ 1.34+dfsg-1.2+deb12u1   │                 │ tar: does not properly warn the user when extracting setuid  │
│                    │                     │          │              │                         │                 │ or setgid...                                                 │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2005-2541                    │
│                    ├─────────────────────┤          │              │                         ├─────────────────┼──────────────────────────────────────────────────────────────┤
│                    │ TEMP-0290435-0B57B5 │          │              │                         │                 │ [tar's rmt command may have undesired side effects]          │
│                    │                     │          │              │                         │                 │ https://security-tracker.debian.org/tracker/TEMP-0290435-0B- │
│                    │                     │          │              │                         │                 │ 57B5
                                                        │
├────────────────────┼─────────────────────┤          │              ├─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ util-linux         │ CVE-2022-0563       │          │              │ 2.38.1-5+deb12u3        │                 │ util-linux: partial disclosure of arbitrary files in chfn    │
│                    │                     │          │              │                         │                 │ and chsh when compiled...                                    │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────────┤                     │          │              │                         ├─────────────────┤                                                              │
│ util-linux-extra   │                     │          │              │                         │                 │
                                                        │
│                    │                     │          │              │                         │                 │
                                                        │
│                    │                     │          │              │                         │                 │
                                                        │
├────────────────────┼─────────────────────┼──────────┼──────────────┼─────────────────────────┼─────────────────┼──────────────────────────────────────────────────────────────┤
│ zlib1g             │ CVE-2023-45853      │ CRITICAL │ will_not_fix │ 1:1.2.13.dfsg-1         │                 │ zlib: integer overflow and resultant heap-based buffer       │
│                    │                     │          │              │                         │                 │ overflow in zipOpenNewFileInZip4_6                           │
│                    │                     │          │              │                         │                 │ https://avd.aquasec.com/nvd/cve-2023-45853                   │
└────────────────────┴─────────────────────┴──────────┴──────────────┴─────────────────────────┴─────────────────┴──────────────────────────────────────────────────────────────┘

/etc/ssl/private/ssl-cert-snakeoil.key (secrets)

Total: 1 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 1, CRITICAL: 0)

HIGH: AsymmetricPrivateKey (private-key)
════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════
Asymmetric Private Key
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 /etc/ssl/private/ssl-cert-snakeoil.key:1 (added by 'RUN /bin/sh -c apt install -y apache2 # ')
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 [ -----BEGIN PRIVATE KEY-----*******************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************-----END PRIVATE KEY
   2
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
