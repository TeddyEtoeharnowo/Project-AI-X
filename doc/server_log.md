
# Ubuntu Server Configuration Log

A running summary of setup and hardening steps completed.

----------

## User Environment

-   Created non-root user accounts
-   Increased command history size in '.bashrc' file

## SSH & UFW Firewall Setup

-   Enabled UFW firewall
-   Allowed SSH on custom port
-   Confirmed UFW status and active rules
-   Changed SSH port
-   Registered and configured a private DuckDNS domain (details withheld)

## SSH Key Authentication

-   Set directory and file permissions for SSH access
-   Disabled password-based login by setting:
    -   'PasswordAuthentication' to 'no'
    -   'ChallengeResponseAuthentication' to 'no'
    -   'UsePAM' to 'no'
-   Verified overrides in '/etc/ssh/sshd_config.d/*.conf'
-   Restarted SSH service

## Security Hardening

-   Installed 'fail2ban' to block brute-force SSH attempts
-   Enabled and verified jail for SSH

## GPU Maintenance

-   Installed latest driver using 'sudo apt install nvidia-driver-xxx'
-   Rebooted and verified with 'nvidia-smi'

## Wi-Fi PCIe Integration
-   Installed PCIe Wi-Fi card
-   Confirmed persistent connectivity using Netplan configuration
-   Verified public IP and enabled SSH access over Wi-Fi
