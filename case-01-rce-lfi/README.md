<div align="center">
  <h1>Case 01: Chaining LFI to RCE via PHP Session Upload Progress</h1>
  <p><b>Target Domain: Government Infrastructure (E-Government Public Service Portal)</b></p>
  
  <!-- BADGES -->
  <img src="https://img.shields.io/badge/Severity-CRITICAL-danger?style=for-the-badge" alt="Severity">
  <img src="https://img.shields.io/badge/Attack%20Vector-Web%20App%20Hacking-blue?style=for-the-badge" alt="Attack Vector">
  <img src="https://img.shields.io/badge/Status-Remediated-success?style=for-the-badge" alt="Status">
</div>

<br>

<!-- EXECUTIVE SUMMARY BOX -->
<div style="background-color: #f8d7da; color: #721c24; padding: 15px; border-left: 6px solid #dc3545; border-radius: 4px; margin: 20px 0;">
  <strong>EXECUTIVE SUMMARY:</strong><br>
  During a target reconnaissance session, a critical vulnerability chain consisting of <b>Local File Inclusion (LFI)</b> and <b>Remote Code Execution (RCE)</b> was discovered on a regional Public Service portal. By chaining these flaws, it was possible to bypass input validation, leverage temporary session allocation mechanisms, and establish persistent administrative access using a proprietary custom backdoor.
</div>

<hr>

<!-- METHODOLOGY TIMELINE -->
<h2>Reconnaissance & Exploitation Methodology</h2>
<p>The penetration testing followed a strict multi-stage attack lifecycle to maintain objectivity and structure:</p>

<table width="100%">
  <tr style="background-color: #fafbfc;">
    <th width="25%">Phase</th>
    <th width="25%">Tools Used</th>
    <th width="50%">Technical Operation & Description</th>
  </tr>
  <tr>
    <td><b>1. Target Discovery</b></td>
    <td><code>Shodan OSINT</code></td>
    <td>Filtered assets using targeted queries (<code>port:80 country:ID</code>) to isolate regional public service endpoints.</td>
  </tr>
  <tr>
    <td><b>2. Vulnerability Scan</b></td>
    <td><code>Nikto Scanner</code></td>
    <td>Conducted automated web scanning in the terminal to identify standard misconfigurations and potential path traversal endpoints.</td>
  </tr>
  <tr>
    <td><b>3. Interception & Analysis</b></td>
    <td><code>Burp Suite (Repeater)</code></td>
    <td>Routed traffic to isolate and manually fuzz vulnerable parameters on the target HTTP request strings.</td>
  </tr>
</table>

<hr>

<!-- LFI MANIFESTATION -->
<h2>Phase 1: Local File Inclusion (LFI) Verification</h2>
<p>Using Burp Suite Repeater, various path traversal payloads were executed against input vectors. The server failed to validate directory structures, returning raw local file systems.</p>

<ul>
  <li><b>Trigger Payload:</b> <code>../../../../../../../../etc/passwd</code></li>
  <li><b>Exploit Proof:</b> The response rendered the absolute contents of the Linux <code>/etc/passwd</code> file, confirming an unauthenticated LFI vulnerability.</li>
</ul>

<hr>

<!-- RCE ESCALATION -->
<h2>Phase 2: Weaponization to RCE (PHP Session Upload Progress)</h2>
<p>Due to restrictive permissions on server log files (preventing standard <i>Log Poisoning</i>), the exploitation was escalated via the <b>PHP Session Upload Progress</b> mechanism by manipulating <code>session.upload_progress.enabled</code> settings.</p>

<div style="background-color: #e2e3e5; color: #383d41; padding: 12px; border-left: 4px solid #6c757d; font-family: monospace; font-size: 13px; margin: 15px 0;">
  <strong>Exploitation Mechanics:</strong><br>
  1. Initiated a standard file upload POST request while passing a custom <code>PHP_SESSION_UPLOAD_PROGRESS</code> parameter.<br>
  2. Injected a lightweight PHP execution stager inside the session token attribute.<br>
  3. Pre-calculated and race-conditioned the session path (e.g., <code>/var/lib/php/sessions/sess_&lt;session_id&gt;</code>) using LFI before cleanup occurred.
</div>

<hr>

<!-- PERSISTENCE -->
<h2>Phase 3: Persistence & Custom Backdoor Deployment</h2>
<p>To ensure long-term administrative control independent of public framework updates, a proprietary custom web shell was deployed to the target directory.</p>

<!-- CUSTOM WEB SHELL BENEFITS CARD -->
<div style="padding: 15px; border: 1px solid #ced4da; border-radius: 6px; background-color: #f8f9fa; margin-top: 15px;">
  <h4>Advantages of Proprietary Web Shell Deployment:</h4>
  <ul>
    <li><b>Signature Bypassing:</b> Avoided generic signatures used by standard tools (like <i>b374k</i> or <i>China Chopper</i>), easily evading signature-based Web Application Firewalls (WAF) and local AV scanners.</li>
    <li><b>Cross-Platform Mobility:</b> Coded independently to enable immediate, secure, and encrypted communication tunnels accessible from any device or device layout at any time.</li>
  </ul>
</div>

<hr>

<!-- REMEDIATION -->
<h2>Remediation Guidelines</h2>
<p>The following defensive patches were recommended to secure the platform infrastructure:</p>

<ol>
  <li><b>Strict Path Whitelisting:</b> Hardcode permitted file names or use ID mappings instead of executing raw user-supplied strings directly into inclusion functions.</li>
  <li><b>Harden PHP Configurations:</b> Set <code>session.upload_progress.enabled = Off</code> within the global <code>php.ini</code> environment if file upload multi-tracking is redundant.</li>
  <li><b>Access Control Lists (ACL):</b> Minimize privileges on the web execution account (<code>www-data</code>), preventing system read access to critical root paths like <code>/etc/passwd</code>.</li>
</ol>
