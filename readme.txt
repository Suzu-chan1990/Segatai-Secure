=== Tegatai Secure ===
Contributors: tegatai
Tags: security, firewall, malware scanner, wordpress security, hardening, 2fa
Requires at least: 6.0
Tested up to: 6.5
Requires PHP: 7.4
Stable tag: 1.0.2
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Enterprise-grade WordPress security suite: WAF, deep scanning, login protection, integrity monitoring, hardening, and logs.
== Description ==

**Tegatai Secure** is a high-performance, enterprise-grade security suite for WordPress. Unlike traditional security plugins that process everything at the PHP level, Tegatai integrates directly with your server (**Nginx, Apache, or LiteSpeed**) to block malicious traffic, bots, and brute-force attacks *before* WordPress is even loaded.

It features a zero-load architecture, 8 deep-scanning engines, and military-grade encryption for remote backups.

Key features:

* Key Advantages
* Complete Feature List
* Installation & Setup

== Installation ==

1. Upload the plugin folder to `/wp-content/plugins/`
2. Activate the plugin in WordPress
3. Open **Tegatai Secure** and configure your modules

== Frequently Asked Questions ==

= Does this plugin use external services? =
No. Tegatai Secure is self-hosted and runs on your server.

= Will the firewall block legitimate users? =
It can if rules are too aggressive. Use whitelists and safe mode while tuning.

== Screenshots ==

1. Security Dashboard
2. Firewall Settings
3. Malware Scanner
4. Login Security
5. Logs & Timeline

== Changelog ==

= 1.0.2 =

# 🚀 Release v1.0.2 (Performance & Management Update)

This major update introduces high-performance infrastructure integrations, timeout-free background scanning, and significant quality-of-life improvements for server administrators.

## ✨ New Features & Enhancements
* **In-Memory WAF (Redis Integration):** The firewall now automatically detects and utilizes Redis (`SETEX`) to store IP bans and rate limits directly in RAM. This drastically reduces database load during severe brute-force or DDoS attacks, with a seamless fallback to DB transients if Redis is unavailable.
* **Asynchronous Background Scanner:** Malware and FIM scans now utilize WP-Cron for background processing. You can start a scan from the dashboard and safely close the tab while the server processes files in chunks without triggering HTTP/PHP timeouts.
* **Native WP-CLI Support:** Added the `wp tegatai scan` command. Server administrators can now execute full malware scans directly from the terminal for maximum performance on massive websites.
* **1-Click Quarantine Restore:** Added a new "Restore" action in the Quarantine dashboard. Administrators can now instantly revert false-positive files from the `.bin` quarantine back to their original file paths.
* **Built-in WP-Cron Manager:** The Cron Monitor tab now features a fully functional native UI to view all active scheduled tasks (hooks, schedules, next run time) and includes a 1-click "Delete" function to clear stuck or malicious cron jobs without requiring third-party plugins.

## 🛡️ Security & Core Fixes
* **Accurate Proxy/Cloudflare IP Detection:** Replaced direct `$_SERVER['REMOTE_ADDR']` calls with a robust fallback chain (`HTTP_CF_CONNECTING_IP`, `HTTP_X_FORWARDED_FOR`). Tegatai now correctly identifies the attacker's real IP behind proxies and load balancers instead of accidentally banning the proxy node.
* **Bulletproof Backup Directory:** The `tegatai-backups/` folder is now strictly secured against public directory traversal. The plugin automatically generates `.htaccess` (Apache/LiteSpeed), `web.config` (IIS), and provides native block rules for Nginx servers.
* **Cache-Safe Anti-Spam Timer:** Replaced the PHP-based form timestamp with a dynamic, client-side JavaScript execution timer. The bot-protection timer now works flawlessly on sites heavily optimized by page caching plugins (e.g., WP Rocket, LiteSpeed Cache).

## 🐛 Bug Fixes & UX Polish
* **Dashboard Stats Logic:** Fixed a rendering logic flaw where the 24-hour block and failed login statistics always displayed "0" due to premature HTML output. Metrics now calculate and display in real-time.
* **Mobile Session Guard Warning:** Added a clear UI warning to the "IP Guard" feature, alerting administrators that dynamic mobile network IPs (4G/5G) will trigger forced logouts.
* **Fatal Error Resolution:** Cleaned up duplicate AJAX method declarations (`ajax_restore_quarantine`, `ajax_delete_cron`) that caused fatal crashes in strict PHP environments during updates.
* **CLI Dashboard Hint:** Added a clean UI prompt within the Scanner tab to educate users about the available WP-CLI terminal commands.

---
*Recommended update for all users to ensure optimal WAF performance and strict proxy compatibility.*

== Upgrade Notice ==

== Changelog ==

= 1.0.1 =

🐛 Bug Fixes & Backend Polish

    Enterprise Features Activation: Added missing feature toggles (Admin Honeypot, Privilege Escalation Guard, Turnstile CAPTCHA, and Auto-Quarantine) to the strict internal whitelist. These enterprise protections can now be activated and saved without triggering AJAX validation errors.

    PHP Fatal Error Resolution: Fixed a critical typo in the form handler where a missing variable identifier ($_POST) caused the settings panel to crash on strict PHP environments.

    Syntax & Parsing Stability: Cleaned up residual syntax parsing errors in the admin dashboard controller to ensure flawless compatibility with PHP 8.1+.

    GeoIP UI Correction: Resolved a character encoding bug (mojibake) within the GeoIP settings tab that displayed corrupted text instead of the intended clean UI elements.

== Upgrade Notice ==

= 1.0.0 =
Initial release.
