 Burp Suite Proxy Configuration Practical

 Objective
To configure **Burp Suite** with **FoxyProxy** in Firefox for capturing and analyzing HTTP and HTTPS traffic.  
This setup is essential for **web application security testing**, **traffic interception**, and **vulnerability analysis**.

---

 Step 1: Launch Burp Suite Proxy Listener
1. Open **Burp Suite**.
2. Navigate to:  
   **Proxy → Options → Proxy Listeners**
3. Confirm or add the default listener:
   - **Interface:** `127.0.0.1`
   - **Port:** `8080`
   - **Running:**  Enabled  
4. Save and verify that it appears as the form that you saved:

SCREENSHOT
<img width="1366" height="768" alt="Screenshot (704)" src="https://github.com/user-attachments/assets/da1138e0-637b-48c0-bd18-03ec3a6e9286" />


step 2: 
 Configure FoxyProxy in Firefox
1. Open Firefox and install **FoxyProxy Standard** extension.  
2. Go to:  
**Add-ons → FoxyProxy Options → Proxies → Add New Proxy**
3. Fill the following details:

| Field | Value |
|-------|--------|
| **Title** | BurpSuite |
| **Type** | HTTP |
| **Hostname** | 127.0.0.1 |
| **Port** | 8080 |
| **Username** | *(Leave Blank)* |
| **Password** | *(Leave Blank)* |

4. Click **Save**, then select the BurpSuite profile to activate the proxy.

SCREENSHOT
<img width="1366" height="768" alt="Screenshot (703)" src="https://github.com/user-attachments/assets/439e492c-3295-4f8d-9e1a-2e2b4f5e1885" />

<img width="1366" height="768" alt="Screenshot (705)" src="https://github.com/user-attachments/assets/8f7ddb66-45e4-46c6-80f4-a23887b38d9a" />

 Step 3
 Configure HTTPS (Install Burp CA Certificate)
To intercept encrypted HTTPS traffic:

1. In Burp Suite → **Proxy → Options**, click  
**“Import / export CA certificate → Export certificate in DER format”**
2. Save the certificate as `burpCA.der`.
3. In Firefox → **Settings → Privacy & Security → Certificates → View Certificates → Authorities → Import**  
- Import `burpCA.der`
 Trust this CA to identify websites

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (709)" src="https://github.com/user-attachments/assets/a32a1cf8-eb4e-4805-b81f-7026c9eb8f26" />
<img width="1366" height="768" alt="Screenshot (711)" src="https://github.com/user-attachments/assets/6247ed84-f026-4717-82dd-e84a1020d01d" />
<img width="1366" height="768" alt="Screenshot (712)" src="https://github.com/user-attachments/assets/220fac8e-5142-498c-9bbe-c70ce3d5e8b9" />


## ▶ Further Steps 
Traffic Analysis, Target Mapping & Logging

After configuring Burp and FoxyProxy I continued with deeper analysis using Burp’s Dashboard, Target and logging tools to inspect traffic, map the target, and capture useful request/response details.

 1. Dashboard & Proxy — Observe All Traffic
- Opened **Burp → Dashboard** to confirm the proxy was receiving traffic and to get a quick overview of recent activity (requests, responses, and issues).
- In **Burp → Proxy → HTTP history** I verified that **all traffic** from Firefox was routed through Burp.
- While observing HTTP history I checked:
  - Request **method** (GET / POST / PUT / DELETE)
  - Request **URL**
  - Status code and response length
  - Timing (response time)
- **Why:** This confirms that interception is working and gives a high-level view of application behavior.



 2. Target — Site Map & Request Inspection
- Opened **Burp → Target → Site map** to build a hierarchical map of the web application.
- Examined individual endpoints and expanded nodes to see associated requests and responses.
- For each interesting endpoint I inspected:
  - **HTTP method** (GET vs POST)
  - **Parameter names & values** (query string, form body, JSON payload)
  - **URL paths** and sub-paths
  - **Ports** used (80, 443, or custom)
  - **Response types** (HTML, JSON, JS, images)
- **Why:** Site mapping helps identify attack surface (authentication endpoints, API calls, upload points) and organizes which endpoints to test further.



 3. Logger / Request Capture — Layout, URL, Query, Port
- Used Burp’s logging features (Logger / HTTP history / Logger++) to capture and filter traffic.
- Inspected request **layout** (full request raw), headers, cookies and request body.
- Logged metadata such as:
  - Hostname and **port**
  - Full **URL path**
  - **Query** string parameters and values
  - Content-type and length
- **Why:** Detailed logs let you replay requests, extract parameters for automated testing, and keep an audit trail of the testing steps.



 4. Applying Logger View & Capture Filters
- Applied **view filters** to focus on relevant traffic (e.g., only `POST` requests, or only requests to `/api/`).
- Applied **capture filters** to reduce noise and only record traffic matching criteria (e.g., host = `target.example.com`, method = `POST`).
- Example filters used:
  - `Method is POST`
  - `URL contains /login`
  - `Content-Type contains application/json`
- **Why:** Filters speed up analysis by removing unrelated requests (ads, CDNs, browser background calls) so focus stays on application traffic.

---

 5. Findings (Documented Examples)
- **Login endpoint** (`/auth/login`) — `POST` with JSON body containing `username` and `password`.
- **Search endpoint** (`/search`) — `GET` with query parameter `q` (potential injection point for testing).
- **API endpoint** (`/api/v1/items`) — returns JSON array; supports pagination via `page` param.
> *(Replace the above with the actual endpoints/params you observed and add screenshots.)*


 6. Next Practical Steps (recommended)
1. **Save project state** in Burp so logs and site map can be preserved for reporting.  
2. **Use Repeater** to manually modify and replay interesting GET/POST requests (test parameter validation).  
3. **Use Intruder** (controlled) for authenticated or safe fuzzing (rate-limit and respect target rules).  
4. **Install and run active/passive scanner** (if using Burp Professional) or use safe manual checks for the Community edition.  
5. **Export logs and HTTP history** for inclusion in your portfolio report (sanitise any sensitive data first).  
6. **Summarize findings** in the lab file with screenshots and conclusions (vulnerabilities found, tests performed, and remediation suggestions).



 7. What I learned
- How to **observe and filter** web traffic to focus on relevant endpoints.  
- How to **map the target** and extract request parameters for testing.  
- How to use **logger filters** to capture only targeted traffic, improving analysis efficiency.  
- Practical next steps to move from reconnaissance to controlled testing (Repeater / Intruder / Scanner).

---

#  Screenshot 
<img width="1366" height="768" alt="Screenshot (713)" src="https://github.com/user-attachments/assets/1ad28896-a6b6-4d3d-aa82-01d102fc2fc5" />
<img width="1366" height="768" alt="Screenshot (714)" src="https://github.com/user-attachments/assets/91875f83-5e57-4973-824c-ea91c16c577c" />
<img width="1366" height="768" alt="Screenshot (715)" src="https://github.com/user-attachments/assets/d25024c8-0cc5-487e-8284-a64c67265955" />
<img width="1366" height="768" alt="Screenshot (716)" src="https://github.com/user-attachments/assets/5ccd01ba-3ce8-422c-8323-c472c8f9babb" />
<img width="1366" height="768" alt="Screenshot (718)" src="https://github.com/user-attachments/assets/03201d94-a1f7-4859-b23f-2f0ece393880" />
<img width="1366" height="768" alt="Screenshot (717)" src="https://github.com/user-attachments/assets/2f4ee679-eaf8-4a26-a8f3-81863b53c736" />
<img width="1366" height="768" alt="Screenshot (720)" src="https://github.com/user-attachments/assets/0a26ba72-97c9-4516-9e7a-d7ae842345b2" />
<img width="1366" height="768" alt="Screenshot (719)" src="https://github.com/user-attachments/assets/eee30575-7944-4dac-adb4-ebd6f756278a" />
<img width="1366" height="768" alt="Screenshot (720)" src="https://github.com/user-attachments/assets/8a61b5a4-fc9c-423a-ae0e-60f9441aa78d" />
<img width="1366" height="768" alt="Screenshot (721)" src="https://github.com/user-attachments/assets/7bd28f7b-ba60-4778-af55-d8af7453c455" />
<img width="1366" height="768" alt="Screenshot (722)" src="https://github.com/user-attachments/assets/9a916cf0-2853-4f85-8f3d-624101ca2c74" />



               Burp Target
  the section where you configure and manage the scope of your testing, it is essentailly about defining which parts of the web application you want to include of exclude from your security testing 
 

### . Manual Interaction — Opening Burp IP in Browser, Intruder & Decoder Practice

After mapping and logging traffic I performed manual interaction tests and practiced encoding/decoding with Burp’s built-in tools.

#### a. Opened Burp listener in browser
- Copied the **Burp Suite listener IP** (e.g., `http://127.0.0.1:8080` or your VM IP:port) and opened it in **Mozilla Firefox**.
- Verified traffic appeared in **Burp → Dashboard / Proxy → HTTP history** and observed request **methods** (GET, POST).
- Viewed request presentation modes:
  - **Raw** — full HTTP request/response text
  - **Rendered** — how the response renders in a browser
  - **Hex / ASCII** (when needed) for binary or encoded bodies
- **Why:** Directly opening the listener / target URL in the browser confirms connectivity and lets you observe how the application behaves for real GET/POST interactions.

#### b. Sent target requests to Intruder
- From the Proxy / HTTP history, selected interesting requests and **Sent to Intruder** (Target → Send to Intruder).
- Prepared Intruder positions on parameters (e.g., username, password, q) for later controlled fuzzing.
- **Why:** Intruder automates controlled payload delivery for testing input validation, enumeration, and other weaknesses (use responsibly and within scope).

SCREENSHOTS
  <img width="1366" height="768" alt="Screenshot (726)" src="https://github.com/user-attachments/assets/7e7f9300-c3fa-4cc6-88ea-fa3ff67d6e34" />
<img width="1366" height="768" alt="Screenshot (725)" src="https://github.com/user-attachments/assets/d0b87a40-62be-4be7-94ed-6ada0f4320ab" />
<img width="1366" height="768" alt="Screenshot (724)" src="https://github.com/user-attachments/assets/2b084abd-a66d-4dad-8115-787e3e14e346" />
<img width="1366" height="768" alt="Screenshot (723)" src="https://github.com/user-attachments/assets/d9d6ed3f-16a5-43f1-b705-1bf83312f0e3" />


#### c. Decoder practice — encoding & hashing workflow
- Opened **Burp → Decoder** to experiment with encoding/decoding and hashing.
- Test string used:

  hello this is kaleem ALBALOSHI

  - Performed these transformations manually in the Decoder:
- **Convert to HTML form** (HTML entities / encoded representation)
- **Convert to URL form / percent-encoding**
- **Convert to ASCII / Hex** (byte-level hex representation)
- **Compute hashes** using different algorithms (e.g., MD5, SHA1, SHA256 — choose appropriate types in the Decoder)
- Workflow notes:
1. Pasted the test string into Decoder.
2. Used the **Encode as HTML** function to produce HTML-escaped output.
3. Used **URL encode** to produce percent-encoded form suitable for query strings.
4. Used **To Hex / From Hex** to view raw ASCII hex bytes.
5. Selected different **hash algorithms** in Decoder to compute and compare digests.
- **Why:** Practicing these conversions helps when analyzing encoded payloads, identifying obfuscated data, or preparing payloads for injection testing.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (734)" src="https://github.com/user-attachments/assets/03175c06-f891-456c-810b-03e3381de7da" />
<img width="1366" height="768" alt="Screenshot (733)" src="https://github.com/user-attachments/assets/d885111a-0c7f-4083-9164-765388944157" />
<img width="1366" height="768" alt="Screenshot (732)" src="https://github.com/user-attachments/assets/1eda0372-4713-44a3-8eb6-4bd895309223" />
<img width="1366" height="768" alt="Screenshot (731)" src="https://github.com/user-attachments/assets/fbabf04e-09ab-4aac-b760-7237d8b6801e" />
<img width="1366" height="768" alt="Screenshot (730)" src="https://github.com/user-attachments/assets/2a7545e1-170f-41f5-b99a-bcc7a4fbce5c" />
<img width="1366" height="768" alt="Screenshot (729)" src="https://github.com/user-attachments/assets/d85984fd-4dc2-4343-badf-6af482beeb3d" />
<img width="1366" height="768" alt="Screenshot (728)" src="https://github.com/user-attachments/assets/1a435837-c9b4-4b2b-bda0-8476a23c953b" />
<img width="1366" height="768" alt="Screenshot (727)" src="https://github.com/user-attachments/assets/b199cfd8-290c-4997-bb72-46134318fe7c" />


 d. Payload practice from GitHub
- Took a sample payload list from a GitHub repository (for practice only).
- For each payload, converted into:
- HTML-encoded form
- URL-encoded form
- Various hash digests (as required)
- Verified conversions in Decoder and documented successful conversions for learning purposes.
- **Why:** Converting community payloads into different encodings/hashes prepares you to test real-world inputs and to recognize common obfuscation techniques during assessments.



 Notes & Safety
- **Always sanitize** and remove any sensitive data before committing logs or screenshots to your public repo (tokens, real credentials, IPs of targets outside your consent scope).
- When using Intruder or any automated testing, **limit rate** and **ensure permission** for the target.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (739)" src="https://github.com/user-attachments/assets/6fd2d0ec-e4f6-4e62-aec1-40009e942d13" />
<img width="1366" height="768" alt="Screenshot (738)" src="https://github.com/user-attachments/assets/41f511b5-8176-4336-8a0d-804f14878e66" />
<img width="1366" height="768" alt="Screenshot (737)" src="https://github.com/user-attachments/assets/69c0b985-06d2-4235-a574-0bc11cd94811" />
<img width="1366" height="768" alt="Screenshot (736)" src="https://github.com/user-attachments/assets/e493670c-a207-46d3-b484-9d358579d680" />





 9. Interceptor, Comparer & Controlled Payload Testing (Education / Lab Only)

> **Disclaimer (Educational Purpose Only)**  
> All testing described in this lab was performed **only** in an authorized, legal, and controlled environment for learning purposes. I did not attempt these actions against systems for which I do not have explicit permission. The techniques described are included here to demonstrate lab skills and understanding — not to enable unauthorized testing.

 a. Using Burp’s built-in browser / Interceptor
- Enabled **Interceptor** in **Burp → Proxy → Intercept** to capture requests in real time.
- Opened Burp’s own embedded browser (or navigated to the Burp listener IP in Firefox) and browsed the target page so requests could be captured directly by the proxy.
- Confirmed captured requests appeared in the **Intercept** queue and reviewed the request methods, headers and bodies in the raw view and rendered view.
- **Why:** Capturing requests in the intercept queue allows close inspection and controlled forwarding of individual requests while learning how web apps communicate.

 b. Comparer — selecting & comparing request parts
- Sent an intercepted request to **Comparer** to inspect differences between multiple requests.
- Selected a portion of the URL or request (for example, a parameter or path fragment) and used the **Add** function to create a comparison entry.
- Used Comparer to highlight differences between two requests (helpful when comparing normal vs. modified requests).
- **Why:** Comparer helps spot subtle differences in requests or payloads that may affect application behaviour.

 c. Controlled payload testing (lab practice)
- For practice, I imported example payloads (community payload lists) solely from reputable GitHub repositories into my lab environment.
- Pasted payloads into the appropriate testing tool (e.g., Intruder) **only** within the authorized lab target.
- Initiated a **controlled test** (e.g., started the Intruder job) while monitoring server responses, ensuring rate limits to avoid service disruption.
- Documented the behaviour observed on the admin page (requests attempted, responses received) and captured logs for reporting.
- **Important:** This repo entry does **not** include payload sets or detailed attack workflows. Those are intentionally omitted to avoid enabling misuse. Keep all testing within scope and with explicit permission.

 d. Extensions / Add-ons used for learning
- Visited various browser extension pages (e.g., extension store) and installed selected extensions into the lab browser/profile to support testing and automation tasks.
- Verified each extension was installed and available in the test environment before use.
- **Why:** Extensions can assist with debugging, request generation, and workflow efficiency during authorized assessments. Only install extensions from trusted sources and only into controlled lab environments.

---

### 10. Documentation & Ethics Notes
- **Record everything:** Save HTTP history, site map, and logs for your report; redact any sensitive data before publishing.  
- **Rate limits & safety:** Always throttle automated tests and avoid actions that could disrupt services.  
- **Authorization:** Never perform active testing against production systems or systems without explicit written permission. Include a short authorization statement in any report that details the scope and permission for testing.

 Suggested screenshots
<img width="1366" height="768" alt="Screenshot (753)" src="https://github.com/user-attachments/assets/ee41851b-9574-4f25-b668-9ca272fab438" />
<img width="1366" height="768" alt="Screenshot (752)" src="https://github.com/user-attachments/assets/8a4b371a-00c5-4eb3-96b5-07dca30de6e8" />
<img width="1366" height="768" alt="Screenshot (751)" src="https://github.com/user-attachments/assets/386faecf-070b-435e-83de-f8e8a87a7c48" />
<img width="1366" height="768" alt="Screenshot (750)" src="https://github.com/user-attachments/assets/711a8740-78be-4a5e-95e5-d3686420c91c" />
<img width="1366" height="768" alt="Screenshot (749)" src="https://github.com/user-attachments/assets/4c4cb679-d3ab-444c-bdb0-6e161d914e5d" />
<img width="1366" height="768" alt="Screenshot (748)" src="https://github.com/user-attachments/assets/3e33dbba-82ca-4459-a79a-815702a13073" />
<img width="1366" height="768" alt="Screenshot (747)" src="https://github.com/user-attachments/assets/41ac64f6-41fd-4a7b-98fa-e20e59047de9" />
<img width="1366" height="768" alt="Screenshot (746)" src="https://github.com/user-attachments/assets/90b506e6-a1c2-4eb5-92ba-77aedab6d863" />
<img width="1366" height="768" alt="Screenshot (744)" src="https://github.com/user-attachments/assets/5bf3e0f6-d54f-4d60-930b-9e3769b159b3" />
<img width="1366" height="768" alt="Screenshot (743)" src="https://github.com/user-attachments/assets/62bf5d7e-0c80-45f4-9f5d-ba58b4e3302c" />
<img width="1366" height="768" alt="Screenshot (742)" src="https://github.com/user-attachments/assets/e63ac15a-1ecb-4396-8849-cd2ff15d6993" />
<img width="1366" height="768" alt="Screenshot (741)" src="https://github.com/user-attachments/assets/a850e72d-a7a8-45dc-8f7f-12dbe3fdec20" />
<img width="1366" height="768" alt="Screenshot (740)" src="https://github.com/user-attachments/assets/23588518-d4b3-4b57-81f2-271ce15ac10e" />
















