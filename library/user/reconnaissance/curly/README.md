# Curly - Web Recon & Vulnerability Scanner (WiFi Pineapple Pager Payload)

**Curly** transforms your WiFi Pineapple Pager into a portable web reconnaissance and vulnerability scanning tool using curl. Perfect for pentesting and bug bounty hunting on the go!

- **Author:** curtthecoder
- **Version:** 3.0

---

## What it does

Curly performs comprehensive web security testing using only curl:

- **IP Geolocation Lookup** - Resolves target IP and queries ipinfo.io for location, ISP, timezone data
- **WAF/CDN Detection** - Identifies Cloudflare, Akamai, AWS CloudFront, Incapsula, Sucuri, ModSecurity
- **Technology Fingerprinting** - Detects web servers, CMS (WordPress, Drupal, Joomla), frameworks (React, Vue, Angular)
- **WordPress Security Tests** - Auto-runs when WordPress detected: user enumeration, xmlrpc, debug logs
- **Subdomain Enumeration** - Tests 50+ common subdomains (api, admin, dev, staging, etc.)
- **Information Gathering** - Headers, server fingerprinting, security header analysis
- **HTML Source Analysis** - Extracts emails, comments, API keys, internal URLs, TODOs
- **Enhanced Endpoint Discovery** - 50+ endpoints including Spring Boot Actuator, Laravel Telescope, Django debug
- **Cloud Metadata Endpoints** - Tests for AWS/GCP/Azure metadata SSRF vulnerabilities
- **Backup File Hunter** - Finds .bak, .old, .sql, .zip backup files
- **HTTP Methods Testing** - Smart detection of dangerous methods (PUT, DELETE, TRACE, PATCH)
- **Header Injection** - Tests for X-Forwarded-For, Host header, and bypass techniques
- **Cookie Security** - Analyzes HttpOnly, Secure, and SameSite flags
- **CORS Misconfiguration** - Detects weak CORS policies
- **Open Redirects** - Accurate detection of open redirect vulnerabilities
- **API Reconnaissance** - Discovers API endpoints and checks for sensitive data exposure

---

## Features

### 6 Scan Modes

1. **Quick Scan** - Fast reconnaissance (IP geo + WAF + tech + info + endpoints + HTML source)
2. **Full Scan (All Modules)** - Comprehensive security testing (all 15 modules!)
3. **API Recon** - Focused API endpoint discovery + subdomain enumeration
4. **Security Audit** - Deep security testing (IP geo + tech + HTML + methods + headers + cookies + CORS + redirects + cloud metadata)
5. **Tech Fingerprint** - Identify IP location, WAF, CDN, web server, and technology stack
6. **Subdomain Enum** - Test 50+ common subdomains for the target

### Visual & Audio Feedback

- **LED Patterns:**
  - Blue blinking = Scanning in progress
  - Red solid = Vulnerability found
  - Green solid = Scan complete

- **Sounds:**
  - Scan start notification
  - Alert when vulnerability detected
  - Completion chime

- **Vibration:** On scan completion

---

## Usage

1. Load the **Curly** payload on your WiFi Pineapple Pager
2. Enter target URL when prompted (e.g., `example.com` - no need for https://)
3. Select scan mode (1-6) using number picker
4. Press **A** to start the scan
5. Watch results in real-time on the Pager display
6. Results auto-saved to `/root/loot/curly/`

---

## What it Detects

### Security Issues

- ✅ **IP Geolocation** - IP address, hostname, city, region, country, ISP/organization, coordinates, timezone
- ✅ **WAF/CDN Protection** - Cloudflare, Akamai, AWS CloudFront, Incapsula, Sucuri, ModSecurity
- ✅ **Technology Stack** - Web servers, CMS platforms, frontend frameworks, libraries with versions
- ✅ **WordPress Vulnerabilities** - User enumeration API, xmlrpc.php, debug logs, wp-admin access
- ✅ **Subdomains** - Tests 50+ common subdomains (api, admin, dev, staging, mail, etc.)
- ✅ **HTML Source Secrets** - Email addresses, API keys, internal URLs, TODO comments, stack traces
- ✅ **Missing security headers** - X-Frame-Options, CSP, HSTS, X-Content-Type-Options
- ✅ **Information disclosure** - Server version, X-Powered-By, tech stack leakage
- ✅ **Exposed sensitive files** - `.git`, `.env`, `.aws/credentials`, `.svn`, `.hg`
- ✅ **Enhanced endpoints** - Spring Boot Actuator, Laravel Telescope, Django debug, Tomcat manager (50+ paths)
- ✅ **Cloud SSRF** - AWS/GCP/Azure metadata endpoint testing via SSRF
- ✅ **Backup files** - .bak, .old, .sql, .zip, .tar.gz with 80+ combinations tested
- ✅ **API documentation** - `/swagger.json`, `/openapi.json`, GraphQL endpoints
- ✅ **Dangerous HTTP methods** - PUT, DELETE, TRACE, PATCH (smart detection, filters rate limiting)
- ✅ **Cookie security** - Missing HttpOnly, Secure, SameSite flags
- ✅ **CORS misconfigurations** - Wildcard and reflected origins
- ✅ **Open redirect vulnerabilities** - Accurate detection (no false positives!)
- ✅ **SSRF vectors** - Tests 8 common redirect parameters + cloud metadata
- ✅ **Sensitive data exposure** - API responses with passwords, tokens, keys

### Enhanced Endpoints Tested (50+)

**Common Files:**
```
/robots.txt, /sitemap.xml, /.git/config, /.git/HEAD, /.git/index
/.svn/entries, /.hg/, /.env, /.aws/credentials, /phpinfo.php
/.well-known/security.txt
```

**Admin & Auth:**
```
/admin, /admin.php, /administrator, /login, /console
```

**API Endpoints:**
```
/api, /api/v1, /api/v2, /api/docs, /swagger.json, /swagger-ui.html
/openapi.json, /graphql, /graphiql
```

**Spring Boot Actuator:**
```
/actuator, /actuator/env, /actuator/health, /actuator/metrics
/actuator/mappings, /actuator/trace
```

**Debug & Monitoring:**
```
/debug, /trace, /metrics, /health, /status, /info
```

**Framework-Specific:**
```
/telescope (Laravel)
/__debug__/ (Django)
/manager/html, /manager/status (Tomcat)
```

### Subdomains Tested (50+)

```
www, api, admin, dev, staging, test, beta, demo, portal, dashboard
app, mail, ftp, vpn, ssh, remote, store, shop, blog, forum
status, help, support, cdn, static, assets, images, media, upload
files, mobile, m, secure, login, auth, sso, sandbox, uat, qa
prod, old, new, v2, api2, backend, server, db, database, cloud
git, gitlab, jenkins, monitor
```

---

## Output

All results are saved to timestamped files in `/root/loot/curly/`:

```
/root/loot/curly/example.com_20260106_143022.txt
```

Each loot file contains:
- Full scan report with timestamps
- Discovered vulnerabilities
- HTTP status codes
- Found endpoints
- Security header analysis

---

## Bug Bounty Tips

This tool is perfect for initial reconnaissance:

1. **Quick triage** - Run quick scan on multiple targets
2. **API hunting** - Use API Recon mode to find undocumented endpoints
3. **Header bypass** - Identify potential authentication bypasses
4. **Information gathering** - Collect server fingerprints and tech stack info
5. **Sensitive files** - Find exposed configuration and credential files

---

## Technical Details

- **Timeout:** 10 seconds per request (prevents hanging on slow targets)
- **HTTP/HTTPS:** Auto-detects or defaults to HTTPS
- **Non-blocking:** LED and sound feedback during scans
- **Portable:** All results stored locally on Pager

---

## Example Output

### IP Geolocation Lookup
```
[+] IP GEOLOCATION LOOKUP
[*] Target IP: 73.*.*.*

━━━ IP Information ━━━
  Hostname    : hostname
  Location    : Not Doxing myself
  Country     : US
  Postal Code : *****
  Coordinates : latitude.longitude
  Organization: Org
  Timezone    : America/New_York
━━━━━━━━━━━━━━━━━━━━━━
```

### Full Example Workflow

```bash
# Scenario: Bug bounty reconnaissance

1. Target: api.example.com (just type the domain!)
2. Select: Quick Scan (mode 1)
3. Results:
   [+] IP GEOLOCATION LOOKUP
   [*] Target IP: 104.26.*.*
   [*] Organization: AS13335 Cloudflare, Inc.

   [*] WAF: Cloudflare detected
   [*] Web Server: nginx/1.18.0
   [*] CMS: WordPress detected
   [*] Frontend: React detected
   [!] Missing: X-Frame-Options
   [!] Missing: CSP
   [!] FOUND [200]: /api/v1
   [!] FOUND [200]: /swagger.json
4. Loot saved to: /root/loot/curly/api.example.com_20260107_143022.txt
5. Next steps: Behind Cloudflare, WordPress + React stack, review swagger.json
```

---

## Notes

- Designed for **authorized penetration testing** and bug bounty programs
- Always obtain permission before scanning targets
- Some tests may trigger WAFs or security monitoring
- Results are indicators - manual verification recommended
- Combine with other Pineapple payloads for complete assessment

---

## What's New in v3.0

### New Modules Added (v3.0):
- 🌍 **IP Geolocation Lookup** - Queries ipinfo.io for target IP location, ISP, timezone, and more
- 🔧 **Improved Detection** - Fixed false positives in TODO/FIXME, backup files, and error detection
- 🔄 **Automatic Redirect Following** - Now follows www redirects automatically (e.g., example.com → www.example.com)

### Previous Additions (v2.5):
- 💎 **HTML Source Analysis** - Extracts emails, comments, API keys, internal URLs, developer TODOs
- 🎯 **Enhanced Endpoint Discovery** - 50+ endpoints (Spring Boot, Laravel, Django, Tomcat)
- ☁️ **Cloud Metadata Endpoints** - SSRF testing for AWS/GCP/Azure metadata APIs
- 🎨 **WordPress Security Tests** - Auto-detects and tests WordPress-specific vulnerabilities

### Previous Additions (v2.0):
- 🛡️ **WAF/CDN Detection** - Identifies 6+ protection systems
- 🔍 **Technology Fingerprinting** - CMS, frameworks, libraries with versions
- 🌐 **Subdomain Enumeration** - Tests 50+ common subdomains
- 🗂️ **Backup File Hunter** - Tests 80+ backup file combinations
- 🍪 **Cookie Security Analysis** - HttpOnly, Secure, SameSite flag checking

### Improvements:
- ✅ **Smarter HTTP Methods Testing** - Filters rate limiting (429/503), only flags real vulnerabilities
- ✅ **Accurate Redirect Detection** - Fixed false positives, uses regex pattern matching
- ✅ **Better UX** - No need to type "https://", just enter domain name
- ✅ **6 Scan Modes** - More options for different use cases
- ✅ **Progress Indicators** - Live updates during subdomain scanning
- ✅ **Conditional Testing** - WordPress tests only run when WordPress is detected
- ✅ **Subdomain Summary** - Clear list of discovered subdomains at scan end

## Future Enhancements

Potential additions:
- JWT token testing and validation
- SQL injection probes
- XSS reflection testing
- Directory brute forcing with custom wordlists
- Proxy support for Burp Suite integration
- Subdomain takeover detection
- DNS zone transfer testing
- SSL/TLS certificate analysis

---

## Disclaimer

This tool is for **authorized security testing only**. Unauthorized access to computer systems is illegal. Always ensure you have explicit permission before testing any target. I am not responsible for misuse of this tool.

---

**Happy Hunting!** 🎯
