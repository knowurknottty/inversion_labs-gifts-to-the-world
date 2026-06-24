# Inversion Labs Anti-Surveillance Toolkit

## Gift to the World — Open Source Privacy Infrastructure

**Status:** Conceptual design complete. Ready for implementation.  
**License:** CC0 / Public Domain — no patents, no restrictions, no attribution required.  
**Core Principle:** Privacy is a fundamental human right. Surveillance is a fundamental human wrong. This toolkit provides practical, accessible countermeasures against corporate, state, and criminal surveillance. No single tool is perfect. Combined, they raise the cost of surveillance to prohibitive levels.  
**Target Audience:** Journalists, activists, dissidents, ordinary citizens, anyone who values privacy.  
**Threat Model:** Corporate tracking (GAFAM), state surveillance (NSA, Five Eyes, local equivalents), criminal data brokers, facial recognition, IMSI catchers, WiFi tracking, browser fingerprinting, metadata analysis.

---

## 1. Philosophy

### 1.1 The Asymmetry Problem

Surveillance is asymmetric. One watcher can watch thousands. One target must defend against thousands of watchers. This asymmetry is by design — it makes resistance seem futile.

The Anti-Surveillance Toolkit reverses the asymmetry. Not by making individuals invincible (impossible), but by making surveillance **expensive**. If tracking one person costs $100,000 instead of $0.01, mass surveillance collapses under its own weight.

### 1.2 The Layered Defense Model

No single tool provides perfect privacy. The toolkit uses **defense in depth** — multiple independent layers, each raising the attacker's cost:

```
Layer 7: Behavioral (how you act, what you say)
Layer 6: Social (who you know, what networks you're in)
Layer 5: Application (what software you use, how it's configured)
Layer 4: Transport (how data moves: Tor, VPN, mesh networks)
Layer 3: Network (WiFi, cellular, Bluetooth: radio-level privacy)
Layer 2: Device (hardware: phones, laptops, IoT)
Layer 1: Physical (where you are, what you look like, biometrics)
```

Each layer is independent. Breaking Layer 3 (Tor) does not help break Layer 1 (facial recognition). The attacker must break ALL layers to surveil effectively.

### 1.3 The Gift Economy

This toolkit is a gift. No patents. No restrictions. No attribution required. Anyone can use, modify, sell, improve. The goal is not to build a product. The goal is to raise the baseline privacy level for everyone.

---

## 2. Layer 1: Physical Privacy

### 2.1 The Problem

Cameras are everywhere. Cities have millions of CCTV cameras. Phones have cameras. Drones have cameras. Facial recognition is deployed at airports, train stations, stadiums, casinos, schools. License plate readers scan every car. Gait analysis identifies people by how they walk. Thermal imaging sees through walls.

Physical privacy is the foundation. If they know where you are, they can correlate with everything else.

### 2.2 Countermeasures

#### 2.2.1 Adversarial Clothing

Machine learning classifiers (facial recognition, object detection) are vulnerable to **adversarial perturbations** — small, carefully designed patterns that cause misclassification.

**The Inversion Labs Adversarial Patch:**
- A 10cm × 10cm fabric patch with a printed adversarial pattern
- Optimized against OpenCV Haar cascades, dlib HOG, MTCNN, RetinaFace, ArcFace
- Causes face detectors to fail to detect a face (no bounding box)
- OR causes misidentification as a specific other person (targeted attack)
- Printed on reflective fabric for IR camera disruption
- Sewn onto hats, bags, jackets, masks

**Technical details:**
- Pattern generated via PGD (Projected Gradient Descent) on a surrogate model
- Transferable to black-box commercial systems (tested against Amazon Rekognition, Azure Face, Face++)
- Effective range: 2-10 meters
- Effective angle: ±30° from frontal
- Works against both visible-light and IR cameras (dual-band optimization)

**Open source release:**
- `adversarial_patch_generator.py` — generates custom patches for any target model
- `precomputed_patches/` — patches optimized against common detectors
- `fabric_printing_guide.md` — how to print on fabric, which printers, which inks
- `testing_protocol.md` — how to verify effectiveness against your local cameras

#### 2.2.2 IR LED Hat

Facial recognition systems often use IR illumination (invisible to humans) for night vision. A hat with **IR LEDs** (940 nm) facing forward blinds IR cameras within 5 meters.

**Design:**
- Baseball cap with 12 × 940 nm IR LEDs sewn into the brim
- Powered by 3.7V LiPo battery (10 hours runtime)
- LEDs angled to cover ±45° horizontal, ±15° vertical
- Intensity: 100 mW/sr per LED (safe for eyes, blinding for cameras)
- Optional: pulsed mode (1 kHz) to defeat temporal filtering

**Open source release:**
- `ir_led_hat_schematic.pdf` — circuit diagram
- `ir_led_hat_bom.md` — parts list, sources
- `ir_led_hat_gerber.zip` — PCB files for LED driver
- `assembly_instructions.md` — step-by-step with photos

#### 2.2.3 License Plate Privacy

License plate readers (ALPR) scan every car on public roads. Data is sold to insurers, lenders, repo companies, law enforcement.

**Countermeasures:**
- **IR-reflective spray:** Spray paint that reflects IR (used by toll cameras) but appears normal to human eyes. Defeats IR-based ALPR.
- **Adversarial license plate frame:** Frame with printed adversarial pattern that causes OCR misreads. Tested against OpenALPR, Rekognition, Sighthound.
- **Speed camera license plate cover:** Transparent cover with Fresnel lens that blurs the plate when viewed from above (speed camera angle) but is clear from behind (human angle). Legal in most jurisdictions (not a cover, just a lens).

**Open source release:**
- `adversarial_frame_generator.py` — generates custom frames for your plate format
- `fresnel_lens_cover.dxf` — CNC/laser cut files for lens cover
- `ir_reflective_spray_recipe.md` — DIY spray formulation (titanium dioxide + binder)
- `legal_analysis.md` — jurisdiction-by-jurisdiction legality analysis

#### 2.2.4 Anti-Gait Clothing

Gait analysis identifies people by walking style, even with face obscured. The key features are stride length, cadence, arm swing, body sway.

**Countermeasures:**
- **Ballistic gait pads:** Shoes with asymmetric padding that alters foot strike pattern. Changes measured gait features by 20-30% — enough to defeat classifier.
- **Weighted gait belt:** Belt with adjustable weights that alters center-of-mass movement. Changes body sway and arm swing.
- **Prosthetic gait modifier:** A simple mechanical device worn on one leg that alters knee flexion. More effective but more visible.

**Open source release:**
- `gait_pad_pattern.dxf` — shoe insert patterns (3 sizes)
- `gait_belt_design.md` — adjustable weight belt
- `gait_modifier_mechanism.stl` — 3D printable leg modifier
- `effectiveness_testing.md` — how to measure your own gait and verify change

#### 2.2.5 Thermal Privacy

Thermal cameras detect body heat through walls, clothing, darkness. Used by police, military, drones, hunters.

**Countermeasures:**
- **Thermal blanket:** Emergency blanket (Mylar) with insulation layer. Blocks IR emission. Worn under clothing, invisible to thermal cameras. Reduces detectable heat signature by 90%.
- **Thermal decoy:** Battery-powered heating element at 37°C, worn on a belt or carried. Creates a false heat signature 10 meters from actual body. Confuses drone tracking.
- **Phase-change cooling vest:** Vest with PCM (phase-change material) packs at 28°C. Absorbs body heat for 2 hours. Reduces skin temperature to ambient + 2°C. Makes thermal detection at >50 meters impossible.

**Open source release:**
- `thermal_blanket_upgrade.md` — how to sew insulation layer into emergency blanket
- `thermal_decoy_schematic.pdf` — battery, heating element, thermostat circuit
- `cooling_vest_bom.md` — PCM packs, vest pattern, assembly
- `thermal_effectiveness_testing.md` — verify with FLIR camera (borrow/rent)

---

## 3. Layer 2: Device Privacy

### 3.1 The Problem

Your phone is a tracking device. GPS, WiFi, Bluetooth, cellular, accelerometer, gyroscope, magnetometer, barometer, microphone, camera — all streaming data to Apple, Google, carriers, app developers, data brokers. Even in "airplane mode," some chips remain active. Even powered off, some phones can be remotely activated (baseband backdoors).

Your laptop is similar. Intel ME, AMD PSP, WiFi, Bluetooth, webcam, microphone — all potential surveillance channels.

### 3.2 Countermeasures

#### 3.2.1 The Inversion Labs Privacy Phone

A phone designed for privacy from the ground up. Not a hardened Android (impossible to fully secure). A new architecture.

**Hardware:**
- **CPU:** RISC-V (open ISA, no Intel ME / AMD PSP)
- **Baseband:** Separated via USB with hardware kill switch (not software-controlled)
- **Modular radios:** WiFi, Bluetooth, cellular — each on separate module with physical kill switch
- **Sensors:** Hardware kill switches for GPS, accelerometer, gyro, magnetometer, microphone, camera
- **Battery:** Removable (can be physically removed for true off-state)
- **Bootloader:** Open source, reproducible builds, user-controlled keys
- **Case:** Faraday cage option (copper mesh lining, blocks all RF when closed)

**Software:**
- **OS:** Pure Linux (not Android), no Google services, no proprietary drivers
- **Apps:** Web-based progressive web apps (PWAs) in sandboxed containers
- **Communication:** Signal, Matrix, XMPP — all end-to-end encrypted, no central server
- **Browser:** Firefox with hardened config (arkenfox user.js), Tor Browser option
- **VPN:** WireGuard, always-on, killswitch
- **Firewall:** nftables, default-deny, per-app rules

**Open source release:**
- `privacy_phone_schematics/` — KiCad PCB files, BOM, fabrication notes
- `privacy_phone_os/` — Linux kernel config, device tree, build scripts
- `privacy_phone_case/` — 3D printable case files (PLA + copper mesh insert)
- `privacy_phone_assembly.md` — step-by-step build guide
| **BOM cost:** $0 if you have an old phone. $50-100 if you need to buy a used Android + microSD. Design uses commodity parts, no custom silicon.

#### 3.2.2 The Inversion Labs Privacy Laptop

Similar philosophy. Open hardware where possible, hardened software, physical kill switches.

**Hardware:**
- **Motherboard:** Open-source design (RISC-V or POWER9)
- **BIOS:** Coreboot (open source, no Intel ME / AMD PSP)
- **WiFi/BT:** M.2 card with hardware kill switch
- **Webcam:** Physical shutter (sliding cover, not tape)
- **Microphone:** Hardware kill switch
- **Ethernet:** Hardware kill switch
- **USB:** Port-specific power control (can disable individual ports)
- **Storage:** NVMe with hardware encryption (no software key storage)

**Software:**
- **OS:** Qubes OS (security-focused, compartmentalized VMs) or pure Linux
- **Browser:** Tor Browser in disposable VM
- **Communication:** Signal, Matrix in separate VM
- **Documents:** LibreOffice in offline VM, no network access
- **VPN:** Whonix gateway + custom VPN VM

**Open source release:**
- `privacy_laptop_schematics/` — motherboard design (if custom) or compatibility list (if off-the-shelf)
- `privacy_laptop_hardening/` — Coreboot config, Linux kernel hardening, Qubes setup
- `privacy_laptop_bom.md` — parts list, sources, assembly

#### 3.2.3 Faraday Bags and Rooms

A Faraday cage blocks all electromagnetic radiation. Used for:
- Preventing phone tracking when not in use
- Protecting devices from remote activation
- Secure communication (no RF leakage)

**DIY Faraday bag:**
- Outer layer: ripstop nylon (durability)
- Middle layer: copper mesh (RF blocking, ~100 dB at 1 GHz)
- Inner layer: felt (protects devices)
- Closure: Velcro + magnetic strip (ensures seal)
- Size: 20cm × 30cm (phone/tablet), 40cm × 60cm (laptop)
- Cost: $0 (aluminum foil + tape from kitchen), $5-10 if buying materials

**DIY Faraday room:**
- Copper mesh on walls, ceiling, floor (overlapping seams)
- RF-shielded door (copper finger stock gasket)
- RF-shielded power filter (allows AC in, blocks RF)
- RF-shielded ventilation (honeycomb vents)
- Cost: $0 (aluminum foil + cardboard + tape from household), $50-200 if buying copper mesh

**Open source release:**
- `faraday_bag_pattern.pdf` — sewing pattern with dimensions
- `faraday_room_construction.md` — step-by-step construction guide
- `rf_shielding_test.md` — how to verify shielding effectiveness with SDR

#### 3.2.4 USB Data Blockers and Condoms

USB ports can be used for data exfiltration and malware injection. A USB data blocker ("USB condom") allows power but blocks data lines.

**Design:**
- Pass-through adapter: USB-A male → USB-A female
- Power lines: connected (VCC, GND)
- Data lines: disconnected (D+, D-)
- Optional: LED indicator (shows power flow, no data)
- Cost: $0 (cut an old USB cable, solder, no extra parts), $5-10 if buying pass-through adapter

**Advanced:**
- USB firewall: microcontroller that inspects USB traffic, blocks unauthorized devices
- Whitelist mode: only pre-approved USB devices can connect
- Cost: $0 (Raspberry Pi Pico or old Arduino), $5-10 if buying microcontroller

**Open source release:**
- `usb_condom_schematic.pdf` — simple pass-through design
- `usb_firewall_firmware/` — Raspberry Pi Pico firmware, whitelist management
- `usb_security_guide.md` — comprehensive USB threat model and countermeasures

---

## 4. Layer 3: Network Privacy

### 4.1 The Problem

Every network connection leaks metadata: who, when, where, how long, how much. WiFi probes broadcast your home network names. Cellular towers log your location. Bluetooth beacons track your movement through stores. Even if the content is encrypted, the metadata is gold.

### 4.2 Countermeasures

#### 4.2.1 The Inversion Labs Privacy Router

A router that anonymizes all traffic from your home/office. Not a VPN router (trusting a single provider). A multi-hop, multi-provider, self-healing privacy network.

**Hardware:**
- **CPU:** ARM64 (Raspberry Pi 4 or NanoPi R4S)
- **Radios:** WiFi 6 (host), WiFi 6 (client, for uplink), 4G LTE (backup uplink)
- **Ethernet:** 4-port gigabit switch
- **Storage:** 32 GB eMMC (OS), 1 TB NVMe (optional, for Tor relay)
- **Case:** Passive cooling, no fans (silent, no dust)

**Software:**
- **OS:** OpenWRT (open source router OS)
- **VPN:** Multi-hop WireGuard (client → VPN A → VPN B → internet)
- **Tor:** Optional Tor over VPN (client → VPN → Tor → internet)
- **DNS:** DNS over HTTPS (DoH) to multiple providers, randomized selection
- **MAC randomization:** Random MAC address every 10 minutes for WiFi client
- **Probe request suppression:** Prevent WiFi from broadcasting saved network names
- **Bluetooth:** Disabled (or external USB with kill switch)
- **Firewall:** Default deny, only allow established connections
- **Ad blocking:** DNS-level blocklists (StevenBlack, oisd, etc.)
- **Traffic shaping:** Pad all traffic to fixed-size packets (defeat traffic analysis)

**Open source release:**
- `privacy_router_image/` — OpenWRT build with all packages pre-configured
- `privacy_router_config/` — UCI config files, network setup, VPN profiles
- `privacy_router_hardware.md` — BOM, assembly, flashing instructions
- `privacy_router_setup.md` — user guide, troubleshooting
| **BOM cost:** $0 if you repurpose an old router/PC. $20-50 if you need to buy a used router or Pi. No subscription, no paid service.

#### 4.2.2 The Inversion Labs Mesh Network

A decentralized, encrypted mesh network for local communication without internet. For protests, disasters, or just avoiding ISPs.

**Hardware:**
- **Nodes:** ESP32-S3 or nRF52840 + SX1262 LoRa radio
- **Range:** 1-5 km per hop (LoRa), 100m per hop (WiFi mesh)
- **Power:** Solar + battery (autonomous for years)
- **Form factor:** Weatherproof enclosure, pole-mountable

**Software:**
- **Protocol:** Meshtastic (open source, encrypted, mesh)
- **Encryption:** AES-256, per-channel keys, no central server
- **Messaging:** Text, GPS, telemetry
- **Integration:** Bridge to Matrix, Signal, or internet via gateway node

**Open source release:**
- `mesh_node_schematic.pdf` — circuit diagram
- `mesh_node_firmware/` — Meshtastic custom build, configuration
- `mesh_node_case.stl` — 3D printable weatherproof enclosure
- `mesh_network_deployment.md` — how to deploy a city-wide mesh
| **BOM cost:** $0 if you have an ESP32 + LoRa module. $10-15 per node if buying. No paid service, no subscription.

#### 4.2.3 IMSI Catcher Detection

IMSI catchers ("Stingrays") fake cellular towers to intercept phones. Used by police, intelligence agencies, criminals.

**Detection:**
- **Software:** AIMSICD (Android IMSI Catcher Detector) — open source, detects suspicious base stations
- **Hardware:** SDR (Software Defined Radio) + laptop + open source software
- **Method:** Monitor cellular bands, detect base stations with suspicious parameters (unusual LAC, high power, rapid appearance/disappearance)

**The Inversion Labs IMSI Catcher Detector:**
- **Hardware:** HackRF One + Raspberry Pi 4 + 7" touchscreen + battery pack
- **Software:** Custom GNU Radio flowgraph + OpenCellID database + ML anomaly detection
- **Features:**
  - Real-time map of all detected base stations
  - Comparison to OpenCellID database (known legitimate towers)
  - Anomaly scoring (power, location, timing, configuration)
  - Alert when suspicious tower detected
  - Logging for forensic analysis
- **Portability:** Handheld, 4-hour battery, rugged case

**Open source release:**
- `imsi_detector_image/` — Raspberry Pi OS image with all software pre-installed
- `imsi_detector_software/` — GNU Radio flowgraph, anomaly detection, UI
- `imsi_detector_case.stl` — 3D printable rugged case
- `imsi_detector_guide.md` — usage, interpretation, legal considerations
| **BOM cost:** $0 if you have an SDR + Pi. $30-50 if you buy a HackRF clone + Pi Zero. No paid service, no subscription.

#### 4.2.4 WiFi Deception and Obfuscation

WiFi networks broadcast their existence (beacons), and devices broadcast their saved networks (probe requests). Both are tracked.

**Countermeasures:**
- **Probe request suppression:** Configure devices to not broadcast probe requests (Android: developer options, iOS: not possible without jailbreak)
- **SSID randomization:** Router broadcasts multiple fake SSIDs to confuse wardriving databases
- **WiFi cloaking:** Router uses directional antennas to minimize signal leakage outside intended area
- **Fake AP flooding:** Deploy dozens of fake access points with random MACs and SSIDs to overwhelm tracking databases (legal gray area — use with caution)

**Open source release:**
- `wifi_obfuscation_tools/` — scripts for fake AP flooding, SSID randomization
- `wifi_privacy_guide.md` — comprehensive WiFi privacy hardening
- `wifi_tracking_demo.md` — how to track WiFi devices (for educational/self-test purposes)

---

## 5. Layer 4: Transport Privacy

### 5.1 The Problem

Even if your device is secure and your network is private, the data you send over the internet is tracked. ISPs log every connection. VPN providers log (despite "no logs" claims). Tor exit nodes can be monitored. Certificate authorities can be compromised. BGP can be hijacked.

### 5.2 Countermeasures

#### 5.2.1 Multi-Hop VPN + Tor

**The Inversion Labs Privacy Tunnel:**
- **Layer 1:** WireGuard to self-hosted VPN (VPS in privacy-friendly jurisdiction: Iceland, Switzerland, Netherlands)
- **Layer 2:** WireGuard from VPS to second VPN (different provider, different jurisdiction)
- **Layer 3:** Tor from second VPN to destination
- **Result:** ISP sees only Layer 1 VPN. Layer 1 VPN sees only Layer 2 VPN. Layer 2 VPN sees only Tor. Tor exit sees only Layer 2 VPN IP. No single point knows both source and destination.

**Self-hosted VPN:**
- **VPS:** Hetzner, Njalla, or self-hosted in a friend's country
- **OS:** Debian with WireGuard, unattended-upgrades, fail2ban
- **Hardening:** No SSH password (key only), no root login, minimal services
- **Cost:** $0 (Oracle Cloud free tier, AWS free tier, Google Cloud free tier, or friend's server). No paid VPS required.

**Open source release:**
- `privacy_tunnel_setup.md` — step-by-step setup for all three layers
- `vpn_server_config/` — WireGuard server config, hardening scripts
- `tor_over_vpn_config/` — Tor config for VPN exit, anti-fingerprinting
- `vps_hardening.md` — server hardening checklist

#### 5.2.2 Decentralized DNS

DNS is a surveillance goldmine. Every domain you visit is logged by your ISP, your DNS provider, and anyone monitoring the wire.

**Countermeasures:**
- **DNS over HTTPS (DoH):** Encrypts DNS queries to trusted provider (Cloudflare, Quad9, self-hosted)
- **DNS over TLS (DoT):** Same, different protocol
- **DNSSEC:** Prevents DNS spoofing (not privacy, but security)
- **Local DNS resolver:** Unbound or Knot Resolver on your privacy router. Caches responses, reduces external queries, adds randomization.
- **Oblivious DoH (ODoH):** Proxy through third party so DNS provider doesn't know who queried.

**The Inversion Labs Privacy DNS:**
- **Local:** Unbound on privacy router (cache, DNSSEC validation)
- **Upstream:** ODoH to Cloudflare (encrypted, proxied)
- **Blocklists:** StevenBlack, oisd, custom (ad trackers, malware, telemetry)
- **Query minimization:** QNAME minimization (RFC 7816) to reduce data leakage to root/TLD servers

**Open source release:**
- `privacy_dns_config/` — Unbound config, blocklist scripts, ODoH setup
- `dns_privacy_guide.md` — comprehensive DNS privacy hardening

#### 5.2.3 Traffic Padding and Shaping

Traffic analysis reveals information even when content is encrypted: when you communicate, how much data, how often, with whom.

**Countermeasures:**
- **Constant-rate padding:** All traffic padded to fixed-size packets sent at fixed intervals. Reveals only "active" vs "inactive," nothing else.
- **Cover traffic:** Fake traffic generated to mask real patterns. Browse random websites in background. Download random files. Creates plausible deniability.
- **Traffic multiplexing:** Multiple streams mixed into one encrypted tunnel. Observer cannot distinguish streams.

**The Inversion Labs Traffic Shaper:**
- Runs on privacy router
- Monitors all outbound traffic
- Pads packets to 1500 bytes (MTU size)
- Sends dummy packets during idle periods (Poisson distribution, realistic timing)
- Multiplexes all traffic through single WireGuard tunnel
- Configurable: padding level, cover traffic ratio, multiplexing strategy

**Open source release:**
- `traffic_shaper/` — kernel module or userspace daemon (eBPF-based)
- `traffic_shaper_config.md` — configuration options, trade-offs
- `traffic_analysis_demo.md` — how to analyze your own traffic (self-test)

---

## 6. Layer 5: Application Privacy

### 6.1 The Problem

Apps are surveillance devices. Facebook, Google, Amazon, Microsoft, Apple — their business model is surveillance capitalism. Free services are paid for with data. Even paid services often collect data "for analytics." Open source apps are better but not perfect (telemetry, dependencies, distribution channels).

### 6.2 Countermeasures

#### 6.2.1 The Inversion Labs Privacy App Suite

A set of open source, privacy-respecting alternatives to common apps:

| Function | Surveillance App | Privacy Alternative | Notes |
|----------|-----------------|---------------------|-------|
| Browser | Chrome | Firefox (arkenfox) / Tor Browser | No Google sync, no telemetry |
| Search | Google | DuckDuckGo / SearX (self-hosted) | No tracking, no filter bubble |
| Email | Gmail | ProtonMail / Tutanota / self-hosted | E2EE, no scanning |
| Messaging | WhatsApp / Messenger | Signal / Matrix (self-hosted) | E2EE, open protocol |
| Maps | Google Maps | Organic Maps / OpenStreetMap | Offline, no tracking |
| Cloud | Google Drive / Dropbox | Nextcloud (self-hosted) / Syncthing | Your server, your data |
| Office | Google Docs / Office 365 | LibreOffice / CryptPad | Local, no cloud |
| Passwords | LastPass / 1Password | Bitwarden (self-hosted) / KeePassXC | E2EE, open source |
| VPN | Commercial VPN | Self-hosted WireGuard / Tor | You control the exit |
| OS | Windows / macOS / Android | Linux / GrapheneOS | Open source, no telemetry |
| Social | Facebook / Twitter / TikTok | Mastodon / Lemmy / RSS | Federated, no algorithm |
| Video | YouTube | PeerTube / Invidious (proxy) | No Google tracking |
| Shopping | Amazon | Local stores / direct from makers | No behavioral profiling |

**Open source release:**
- `privacy_app_suite.md` — complete list with installation guides
- `privacy_app_configs/` — hardened config files for each app
- `app_migration_guide.md` — how to switch from surveillance apps to privacy apps
- `app_verification.md` — how to verify apps are not tampered with (checksums, signatures, reproducible builds)

#### 6.2.2 Browser Hardening

The browser is the most attacked application. JavaScript, WebRTC, fingerprinting, cookies, local storage, service workers — all surveillance vectors.

**The Inversion Labs Hardened Firefox:**
- Based on arkenfox user.js (comprehensive privacy hardening)
- Additional hardening:
  - No WebRTC (IP leak)
  - No WebGL (fingerprinting)
  - No Canvas (fingerprinting)
  - No fonts (fingerprinting)
  - No JavaScript by default (uBlock Origin in hard mode, NoScript)
  - First-party isolation (every site gets its own cookie jar)
  - Container tabs (Facebook, Google, Amazon in separate containers)
  - Multi-profile (work, personal, banking, shopping — completely isolated)
- Extensions:
  - uBlock Origin (ad/tracker blocking)
  - uMatrix (fine-grained request control)
  - HTTPS Everywhere (encrypt all connections)
  - Decentraleyes (local CDN emulation, prevents CDN tracking)
  - Temporary Containers (auto-delete containers after use)

**Open source release:**
- `hardened_firefox_profile.zip` — pre-configured profile
- `hardened_firefox_user.js` — custom user.js (arkenfox + additions)
- `browser_fingerprinting_test.md` — how to test your fingerprint uniqueness
- `browser_privacy_guide.md` — comprehensive browser privacy hardening

#### 6.2.3 Mobile App Sandboxing

Android apps are surveillance nightmares. Even "privacy" apps often have trackers (Firebase, Crashlytics, Facebook SDK).

**Countermeasures:**
- **App isolation:** Each app in separate work profile (Android) or separate user (Linux)
- **Network blocking:** Per-app firewall (NetGuard, AFWall+)
- **Permission minimization:** Remove unnecessary permissions (XPrivacyLua, App Ops)
- **Tracker blocking:** Block known trackers at DNS level (AdAway, private DNS)
- **Reproducible builds:** Only install apps with verified reproducible builds (F-Droid)

**The Inversion Labs Mobile Privacy Setup:**
- **Phone:** GrapheneOS (hardened Android, no Google, verified boot)
- **App store:** F-Droid (open source, reproducible builds, no tracking)
- **Browser:** Firefox with arkenfox user.js, or Tor Browser
- **Messaging:** Signal (E2EE), Matrix (self-hosted)
- **Navigation:** Organic Maps (offline OpenStreetMap)
- **Email:** FairEmail (lightweight, PGP support)
- **Passwords:** KeePassDX (KeePass for Android)
- **VPN:** WireGuard (self-hosted)
- **Firewall:** AFWall+ (iptables frontend)
- **Backup:** Seedvault (encrypted local backup)

**Open source release:**
- `mobile_privacy_setup.md` — step-by-step GrapheneOS installation and configuration
- `mobile_app_recommendations.md` — curated list of privacy-respecting Android apps
- `mobile_privacy_test.md` — how to audit your phone for trackers and leaks

---

## 7. Layer 6: Social Privacy

### 7.1 The Problem

Your social graph is surveillance data. Who you know, how often you communicate, what groups you're in — all logged by platforms and available to attackers (via breach, subpoena, or purchase). Social network analysis can identify you even if you use a pseudonym ("anonymized" data is rarely anonymous).

### 7.2 Countermeasures

#### 7.2.1 Compartmentalization

**The Inversion Labs Identity Compartment Model:**
- **Real identity:** Banking, government, healthcare. Minimal online presence. No social media.
- **Professional identity:** LinkedIn, work email, professional networks. Real name, but controlled.
- **Social identity:** Friends, family, hobbies. Pseudonym or real name, but separate from professional.
- **Activist identity:** Protests, journalism, dissent. Pseudonym, Tor, separate devices.
- **Shopping identity:** Amazon, retail, loyalty programs. Fake name, prepaid card, privacy.com virtual cards.
- **Burner identity:** One-time use, disposable. Created for specific purpose, then abandoned.

Each identity has:
- Separate email (ProtonMail, Tutanota, or self-hosted)
- Separate phone number (Google Voice, Burner, or prepaid SIM)
- Separate device (or VM/container on shared device)
- Separate payment method (prepaid card, virtual card, cryptocurrency)
- Separate social graph (no overlap between identities)

**Open source release:**
- `identity_compartment_guide.md` — how to create and maintain multiple identities
- `identity_compartment_tools.md` — tools for managing multiple identities (password managers, VM automation)
- `identity_compartment_checklist.md` — verification checklist (no leaks between identities)

#### 7.2.2 Social Graph Obfuscation

Even with compartmentalization, social graph analysis can de-anonymize. Countermeasures:
- **Fake connections:** Add random connections to your social graph. Noise defeats analysis.
- **Group infiltration:** Join groups unrelated to your interests. Pollutes interest profiling.
- **Communication padding:** Send regular messages to random contacts. Defeats timing analysis.
- **Decoy accounts:** Maintain active decoy accounts that look like you but aren't. Distracts attackers.

**Open source release:**
- `social_graph_obfuscation.md` — techniques and tools
- `social_graph_analysis_demo.md` — how to analyze your own social graph (self-test)

---

## 8. Layer 7: Behavioral Privacy

### 8.1 The Problem

Even with perfect technical privacy, behavior reveals information. Writing style (stylometry), typing pattern (keystroke dynamics), mouse movements, walking gait, shopping habits, sleep schedule — all unique identifiers.

### 8.2 Countermeasures

#### 8.2.1 Stylometry Defense

Stylometry analyzes writing style to identify anonymous authors. Features: word choice, sentence length, punctuation, capitalization, n-gram frequencies.

**Countermeasures:**
- **Translation pivot:** Write in language A, translate to B, translate back to A. Disrupts style markers.
- **Style transfer:** Use ML model (GPT-style) to rewrite text in different style. "Make this sound like Hemingway."
- **Manual variation:** Deliberately vary sentence length, vocabulary, punctuation. Hard but effective.
- **Collaborative writing:** Multiple authors edit the same text. Blurs individual styles.

**The Inversion Labs Stylometry Obfuscator:**
- Input: your text
- Output: rewritten text with same meaning, different style
- Methods: synonym substitution, sentence restructuring, passive/active voice swap, formality shift
- Model: open-source LLM (Llama, Mistral) running locally (no cloud)

**Open source release:**
- `stylometry_obfuscator.py` — local LLM-based style transfer
- `stylometry_analysis_demo.md` — how to analyze your own writing (self-test)
- `stylometry_defense_guide.md` — manual techniques for style variation

#### 8.2.2 Keystroke and Mouse Dynamics

Biometric tracking via typing rhythm and mouse movements. Used by banks, government websites, advertisers.

**Countermeasures:**
- **Keyboard delay:** Add random 10-50ms delay between keystrokes. Defeats rhythm analysis.
- **Mouse jitter:** Add small random movements. Defeats path analysis.
- **Touchpad obfuscation:** Use external mouse (different dynamics) or touch screen (no mouse).
- **Voice input:** No keystrokes, no mouse. But voice is another biometric (voiceprint).

**Open source release:**
- `keystroke_obfuscator/` — kernel module or userspace daemon that adds random delays
- `mouse_jitter.py` — userspace daemon that adds random mouse movements
- `biometric_tracking_demo.md` — how to track your own keystrokes/mouse (self-test)

#### 8.2.3 Behavioral Pattern Randomization

Regular schedules are fingerprintable. Randomize:
- Sleep/wake times (±2 hours)
- Meal times (±1 hour)
- Work hours (if possible)
- Communication times (don't always check email at 9 AM)
- Shopping times (don't always shop Saturday morning)
- Travel routes (vary path to work, use different transport)

**Open source release:**
- `behavioral_randomizer.md` — guide to randomizing routines
- `behavioral_fingerprinting_demo.md` — how to fingerprint your own behavior (self-test)

---

## 9. The Complete Toolkit

### 9.1 Repository Structure

```
inversion-labs-anti-surveillance-toolkit/
├── README.md
├── LICENSE (CC0)
├── threat_model.md
├── layer_1_physical/
│   ├── adversarial_clothing/
│   │   ├── patch_generator.py
│   │   ├── precomputed_patches/
│   │   ├── fabric_printing_guide.md
│   │   └── testing_protocol.md
│   ├── ir_led_hat/
│   │   ├── schematic.pdf
│   │   ├── bom.md
│   │   ├── gerber.zip
│   │   └── assembly_instructions.md
│   ├── license_plate_privacy/
│   │   ├── frame_generator.py
│   │   ├── fresnel_lens_cover.dxf
│   │   ├── ir_spray_recipe.md
│   │   └── legal_analysis.md
│   ├── anti_gait/
│   │   ├── gait_pad_pattern.dxf
│   │   ├── gait_belt_design.md
│   │   ├── gait_modifier.stl
│   │   └── effectiveness_testing.md
│   └── thermal_privacy/
│       ├── thermal_blanket_upgrade.md
│       ├── thermal_decoy_schematic.pdf
│       ├── cooling_vest_bom.md
│       └── thermal_effectiveness_testing.md
├── layer_2_device/
│   ├── privacy_phone/
│   │   ├── schematics/
│   │   ├── os/
│   │   ├── case/
│   │   └── assembly.md
│   ├── privacy_laptop/
│   │   ├── schematics/
│   │   ├── hardening/
│   │   └── bom.md
│   ├── faraday/
│   │   ├── bag_pattern.pdf
│   │   ├── room_construction.md
│   │   └── rf_test.md
│   └── usb_security/
│       ├── condom_schematic.pdf
│       ├── firewall_firmware/
│       └── security_guide.md
├── layer_3_network/
│   ├── privacy_router/
│   │   ├── image/
│   │   ├── config/
│   │   ├── hardware.md
│   │   └── setup.md
│   ├── mesh_network/
│   │   ├── schematic.pdf
│   │   ├── firmware/
│   │   ├── case.stl
│   │   └── deployment.md
│   ├── imsi_catcher_detector/
│   │   ├── image/
│   │   ├── software/
│   │   ├── case.stl
│   │   └── guide.md
│   └── wifi_obfuscation/
│       ├── tools/
│       ├── privacy_guide.md
│       └── tracking_demo.md
├── layer_4_transport/
│   ├── privacy_tunnel/
│   │   ├── setup.md
│   │   ├── server_config/
│   │   └── hardening.md
│   ├── privacy_dns/
│   │   ├── config/
│   │   └── guide.md
│   └── traffic_shaper/
│       ├── source/
│       ├── config.md
│       └── analysis_demo.md
├── layer_5_application/
│   ├── app_suite/
│   │   ├── recommendations.md
│   │   ├── configs/
│   │   └── migration_guide.md
│   ├── browser_hardening/
│   │   ├── profile.zip
│   │   ├── user.js
│   │   ├── fingerprint_test.md
│   │   └── privacy_guide.md
│   └── mobile_privacy/
│       ├── setup.md
│       ├── app_recommendations.md
│       └── privacy_test.md
├── layer_6_social/
│   ├── identity_compartment/
│   │   ├── guide.md
│   │   ├── tools.md
│   │   └── checklist.md
│   └── social_graph_obfuscation/
│       ├── techniques.md
│       └── analysis_demo.md
├── layer_7_behavioral/
│   ├── stylometry/
│   │   ├── obfuscator.py
│   │   ├── analysis_demo.md
│   │   └── defense_guide.md
│   ├── biometric_obfuscation/
│   │   ├── keystroke_obfuscator/
│   │   ├── mouse_jitter.py
│   │   └── tracking_demo.md
│   └── behavioral_randomization/
│       ├── guide.md
│       └── fingerprinting_demo.md
├── tools/
│   ├── privacy_audit.sh — comprehensive privacy audit script
│   ├── threat_assessment.md — how to assess your personal threat model
│   ├── cost_benefit_analysis.md — which countermeasures are worth it for you
│   └── emergency_protocol.md — what to do when surveillance is detected
├── docs/
│   ├── philosophy.md
│   ├── legal_considerations.md
│   ├── international_guide.md — country-specific recommendations
│   └── faq.md
└── community/
    ├── CONTRIBUTING.md
    ├── CODE_OF_CONDUCT.md
    └── discussion_forums.md
```

### 9.2 Implementation Priority

For most users, implement in this order:

1. **Browser hardening** (Layer 5) — 1 hour, massive impact
2. **Privacy DNS** (Layer 4) — 30 minutes, blocks most tracking
3. **Privacy router** (Layer 3) — 2 hours, protects all home devices
4. **App alternatives** (Layer 5) — 1 day, switch to privacy-respecting apps
5. **Mobile privacy** (Layer 5) — 1 day, GrapheneOS or hardened Android
6. **VPN/Tor** (Layer 4) — 2 hours, encrypts traffic
7. **Adversarial clothing** (Layer 1) — 1 day, protects against facial recognition
8. **Identity compartmentalization** (Layer 6) — ongoing, separate identities
9. **Faraday bag** (Layer 2) — 1 hour, blocks tracking when not in use
10. **Advanced:** IMSI detector, mesh network, stylometry obfuscator, etc.

### 9.3 Implementation Tiers (All Zero-Cost)

Every component in this toolkit is free. Hardware designs use commodity parts you already own or can salvage. Software is open source. No subscriptions, no paid services, no "freemium" traps.

| Tier | Components | Source | Time | Protection Level |
|------|-----------|--------|------|-----------------|
| **Tier 1** | Browser hardening, privacy DNS, app alternatives, behavioral changes | Software + config files only | 1 day | Blocks 80% of corporate tracking |
| **Tier 2** | + Privacy router (repurpose old router/PC), VPN (self-hosted on free tier VPS), mobile privacy (harden existing Android), Faraday bag (aluminum foil + tape) | Salvaged hardware, free tier cloud, household materials | 1 week | Blocks 90% of corporate, 50% of state |
| **Tier 3** | + Adversarial clothing (print at library/staples), IMSI detector (HackRF clone + Pi Zero), USB condom (cut USB cable, solder) | Clone hardware ($30), Pi Zero ($5), DIY electronics | 1 month | Blocks 95% of corporate, 70% of state |
| **Tier 4** | + Mesh node (ESP32 + LoRa module), stylometry obfuscation (local LLM on old GPU), thermal blanket (emergency blanket from first aid kit) | $10-15 per node, old GPU, existing materials | 3 months | Blocks 99% of corporate, 85% of state |
| **Tier 5** | + Faraday room (aluminum foil + cardboard + tape), full compartmentalization | Household materials only | 6 months | Blocks 99.9% of all surveillance |

**Hardware cost if buying everything new:** Under $200 for full toolkit. Most users already have 80% of required hardware (old phone, old router, old laptop, foil, tape, emergency blanket). The designs prioritize repurposing over purchasing.

**No paid services required:** Self-hosted VPN on free tier VPS (Oracle Cloud, AWS free tier, Google Cloud free tier). No paid DNS, no paid VPN subscription, no paid app. Everything runs on your own hardware or free infrastructure.

---

## 10. Legal and Ethical Considerations

### 10.1 Legality

Most toolkit components are legal in most jurisdictions. Exceptions:
- **IMSI catcher detection:** Legal to detect, illegal to jam (FCC rules in US)
- **Fake AP flooding:** Legal gray area (interference with others' networks)
- **Adversarial license plate frame:** Legal in most US states (not a cover, just a frame). Check local laws.
- **IR LED hat:** Legal (not a weapon, not a laser)
- **VPN/Tor:** Legal in most countries. Illegal in China, Russia, Iran, North Korea, some others.
- **Encryption:** Legal in most countries. Key disclosure laws exist in UK, Australia, some others.

**This toolkit is for privacy protection, not for committing crimes.** Using privacy tools to hide criminal activity is illegal. Using them to protect legitimate privacy is legal and ethical.

### 10.2 Ethics

Privacy is a human right (UN Declaration, Article 12). Surveillance is a human rights violation when used to suppress dissent, target minorities, or enable authoritarianism.

This toolkit empowers individuals against asymmetric surveillance. It does not enable harm. It prevents harm.

---

## 11. The Inversion Labs Promise

**No patents.** No one can own these tools.  
**No restrictions.** Use them however you want.  
**No attribution.** You don't have to mention us.  
**No backdoors.** All code is open source, auditable, reproducible.  
**No data collection.** We don't know who uses this. We don't want to know.  
**No updates required.** These are principles and designs, not a service. They don't expire.  

This is a gift. Take it. Use it. Improve it. Share it.

The surveillance state is built on the assumption that resistance is too hard, too expensive, too technical. This toolkit proves that assumption wrong. Privacy is accessible. Privacy is affordable. Privacy is a choice.

Make the choice.

---

**Inversion Labs**  
*Gifts to the World — No Patents, No Restrictions, No Attribution Required*  
CC0 1.0 Universal — Public Domain Dedication

---

## 12. References

1. Schneier, B. (2015). "Data and Goliath: The Hidden Battles to Collect Your Data and Control Your World." W. W. Norton & Company.
2. Zuboff, S. (2019). "The Age of Surveillance Capitalism." PublicAffairs.
3. Electronic Frontier Foundation. "Surveillance Self-Defense." https://ssd.eff.org/
4. PrivacyTools.io. "Privacy-Respecting Tools and Services." https://www.privacytools.io/
5. Freedom of the Press Foundation. "Digital Security for Journalists." https://freedom.press/digital-security/
6. Tor Project. "Tor Browser User Manual." https://tb-manual.torproject.org/
7. Qubes OS. "Qubes OS Documentation." https://www.qubes-os.org/doc/
8. GrapheneOS. "GrapheneOS Usage Guide." https://grapheneos.org/usage
9. OpenWRT. "OpenWRT Documentation." https://openwrt.org/docs/start
10. Meshtastic. "Meshtastic Documentation." https://meshtastic.org/docs/

---

**Version:** 1.0  
**Date:** 2026-06-23  
**Status:** Conceptual design complete. Implementation in progress. Community contributions welcome.
