<div align="center">
  <h1>Case 02: Full-Scale Red Team Simulation - Core Infrastructure Compromise via Physical Intrusion and Signal Jamming</h1>
  <p><b>Target Domain: Financial Institution (National Banking Infrastructure)</b></p>
  
  <!-- BADGES -->
  <img src="https://img.shields.io/badge/Severity-CRITICAL-danger?style=for-the-badge" alt="Severity">
  <img src="https://img.shields.io/badge/Attack%20Type-Red%20Teaming%20%7C%20Physical%20%7C%20Hardware-red?style=for-the-badge" alt="Attack Type">
  <img src="https://img.shields.io/badge/Status-Remediated-success?style=for-the-badge" alt="Status">
</div>

<br>

<!-- EXECUTIVE SUMMARY BOX -->
<div style="background-color: #f8d7da; color: #721c24; padding: 15px; border-left: 6px solid #dc3545; border-radius: 4px; margin: 20px 0;">
  <strong>EXECUTIVE SUMMARY:</strong><br>
  This case study documents a multi-layered coordinated Red Team simulation designed to test the physical, human, and cyber resilience of a National Bank. By systematically staging a local network blackout via radio frequency jamming, exploiting a compromised communications channel (WhatsApp hijack), and deploying an automated ESP-based hardware microcontroller, the team successfully established an undetected persistence backdoor inside the core internal network.
</div>

<hr>

<!-- ATTACK LIFECYCLE TIMELINE -->
<h2>Coordinated Attack Lifecycle</h2>
<p>The operation relied on strict synchronization between electronic warfare, social engineering, and hardware-level exploitation:</p>

<table width="100%">
  <tr style="background-color: #fafbfc;">
    <th width="20%">Phase</th>
    <th width="30%">Vector & Tools</th>
    <th width="50%">Tactical Execution Details</th>
  </tr>
  <tr>
    <td><b>1. Signal Disruption</b></td>
    <td><code>Portable RF Jammer</code></td>
    <td>Deployed a localized signal jammer concealed inside a bag from an adjacent perimeter to forcefully sever the office network connectivity, creating an immediate infrastructure anomaly.</td>
  </tr>
  <tr>
    <td><b>2. Social Engineering</b></td>
    <td><code>Pretexting & Identity Impersonation</code></td>
    <td>Infiltrated the premises disguised as an IT/Network Technician, leveraging open-source intelligence (OSINT) by using the exact name of the branch manager as the authority pretext.</td>
  </tr>
  <tr>
    <td><b>3. Out-of-Band Validation</b></td>
    <td><code>Coordinated WhatsApp Hijack</code></td>
    <td>When local staff attempted verification, a remote team memberâ€”who had previously intercepted the manager's WhatsApp communicationsâ€”intercepted and forged the validation message, granting full physical access to the network closet.</td>
  </tr>
  <tr>
    <td><b>4. Hardware Implant</b></td>
    <td><code>Custom ESP Microcontroller</code></td>
    <td>Planted a miniature ESP-based hardware implant hidden behind the router setup. The microcontroller remained dormant until the jamming ceased and specific Wi-Fi triggers signatures were detected.</td>
  </tr>
</table>

<hr>

<!-- HARDWARE EXPLOITATION & LATERAL MOVEMENT -->
<h2>Phase 2: Hardware Weaponization & Lateral Infection</h2>
<p>Unlike standard software exploits, the physical hardware implant provided a reliable pivot point that completely bypassed the bank's perimeter firewalls and local Endpoint Detection and Response (EDR) agents.</p>

<div style="background-color: #e2e3e5; color: #383d41; padding: 12px; border-left: 4px solid #6c757d; font-family: monospace; font-size: 13px; margin: 15px 0;">
  <strong>Microcontroller Automation Flow:</strong><br>
  1. RF Jammer deactivated -> Internal office Wi-Fi connection restored.<br>
  2. The custom ESP microcontroller detects the Wi-Fi beacon trigger and initializes its network stack.<br>
  3. Executes an automated local network scanning and poisoning sequence.<br>
  4. Drops a lightweight automated payload that spreads laterally through the flat internal network, connecting all integrated branch endpoints back to the operator's dashboard.
</div>

<hr>

<!-- SECURITY CONTROLS BYPASSED -->
<h2>Security Vulnerabilities Exposed</h2>
<p>The success of this operation highlighted critical flaws in the target's holistic security posture:</p>

<!-- EXPOSED FLAWS CARD -->
<div style="padding: 15px; border: 1px solid #ced4da; border-radius: 6px; background-color: #f8f9fa; margin-top: 15px;">
  <h4>Bypassed Controls & Architectural Flaws:</h4>
  <ul>
    <li><b>Lack of Out-of-Band (OOB) Identity Verification:</b> Trusting third-party chat messengers (WhatsApp) as a definitive verification method for physical building access.</li>
    <li><b>Physical Access Port Security:</b> Absence of port security (e.g., 802.1X Network Access Control) allowing unauthorized rogue hardware devices to dynamically obtain an IP address and communicate on the internal LAN.</li>
    <li><b>Flat Network Architecture:</b> Lack of proper network segmentation (VLANs), enabling an infection on a basic office Wi-Fi endpoint to pivot directly into core banking system servers.</li>
  </ul>
</div>

<hr>

<!-- REMEDIATION -->
<h2>Strategic Mitigation Roadmap</h2>
<p>The following strategic patches were handed over to the financial institution's C-level executives:</p>

<ol>
  <li><b>Implement 802.1X Authentication:</b> Enforce strict Network Access Control (NAC) to ensure only white-listed, authenticated MAC addresses can bind to physical Ethernet ports or internal Wi-Fi access points.</li>
  <li><b>Formalize Physical Access Protocols:</b> Mandate corporate token-based ID cards or explicit, independent multi-factor verification systems for external field technicians”completely independent of external consumer chat apps.</li>
  <li><b>Strict Network Micro-Segmentation:</b> Isolate core banking systems, operational administrative offices, and general corporate Wi-Fi into strictly separated VLANs regulated by strict firewall rule-sets.</li>
</ol>
