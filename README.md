# PENETRATION TESTING REPORT
## FOOTPRINTING, OSINT & NETWORK DISCOVERY

| Report Information | Details |
|---|---|
| **Pentester Name** | Tishayna McFarlane |
| **Designation** | Cybersecurity Professional |
| **Programme / Batch** | B084 – Networkwalks |
| **Reporting Period** | Week 02 |
| **Report Date** | 12 November 2026 |
| **Modules Covered** | W2-PM2: GHDB · W2-PM3: Maltego · W2-PM4: theHarvester · W2-PM5: Zenmap |
| **Client / Target** | 1. Networkwalks (written permission reported as secured)  2. Tester’s own local LAN |
| **Authorization Secured from Client?** | Yes |
| **Assessment Type** | Passive/open-source reconnaissance and local network host discovery |

> **SCOPE NOTE:** This report records the results visible in the supplied lab workbook and the supporting evidence uploaded to this repository. It does not claim exploitation, vulnerability validation, or access to systems. Third-party webcam URLs are recorded only as search results; no attempt to control, compromise, or access restricted devices is reported.

---

# 1. Liability Disclaimer

The activities documented in this report were undertaken for educational and research purposes as part of the Networkwalks cybersecurity internship. Testing should be performed only on systems and networks owned by the tester or for which explicit authorization has been obtained. Publicly indexed resources identified during search-engine research must not be accessed beyond their intended public presentation or tested without the owner's permission.

The observations in this report are limited to the supplied practical results and screenshots. They are not a certification that any system is secure or insecure. The tester, training provider, and report preparer accept no responsibility for unauthorized use of the techniques described.

# 2. Executive Summary

Week 02 practical work covered four activities: Google Hacking Database (GHDB) research, domain footprinting with Maltego, OSINT enumeration with theHarvester, and local network discovery with Zenmap.

The GHDB exercise searched for the term **“cam”** and reviewed webcam-related Google dorks, recording ten webcam-related URLs. A second task recorded ten mathematics e-book/document search results. The Maltego exercise created a domain entity for `networkwalks.com` and ran email-related transforms; the workbook shows an email-related entity/relationship, but does not provide a clearly readable list or count of addresses.

theHarvester was run against `microsoft.com` using Baidu and then all configured sources. The first run returned no IPs, email addresses, people, or hosts, while the second run encountered source/API limitations and also showed no enumerated results.

Zenmap identified one live host on the local `/24` subnet: `192.168.56.1`. The MAC address was unavailable; Zenmap displayed three open ports. A topology export was subsequently saved and uploaded to the repository.

> **OVERALL RESULT:** The activities successfully demonstrated search-engine reconnaissance, domain-entity investigation, attempted OSINT harvesting, and local host discovery. The available evidence does not establish a confirmed exploitable vulnerability.

# 3. Objectives and Scope

The objectives of the practical exercises were to:

- Explore GHDB search operators and understand how indexed content can reveal publicly accessible information.
- Use Maltego to represent a target domain and run email-focused transforms.
- Use theHarvester to search public sources for domain-associated IPs, email addresses, people, and hosts.
- Identify the local IPv4 address and subnet, discover live hosts with Zenmap, review host details, and view/save network topology.

In-scope targets recorded in the practical workbook:

- `networkwalks.com` for domain OSINT exercises.
- The tester's own local LAN for Zenmap discovery.

The sample report mentions written permission for Networkwalks; the lab workbook itself does not independently document the authorization record. Confirm and retain the relevant permission evidence before submitting or conducting further testing.

# 4. Tools and Methodology

| Tool / Utility | Purpose in This Assessment | Activity |
|---|---|---|
| Exploit-DB Google Hacking Database (GHDB) | Find and review search operators (Google dorks) associated with indexed webcam pages and mathematics documents. | PM2 |
| Google Search | Test selected GHDB queries and inspect search result pages. | PM2 |
| Maltego Desktop | Create a domain entity and run email-related transforms against the lab domain. | PM3 |
| theHarvester 4.10.1 | Query public sources for domain-associated IPs, emails, people, and hosts. | PM4 |
| Windows Command Prompt – `ipconfig` | Identify the local IPv4 address and subnet mask. | PM5 |
| Zenmap / Nmap | Perform local host discovery and inspect host status, ports, and topology. | PM5 |

**Methodology:** Follow the assigned practical steps, record the commands/search patterns and visible output, compare observed results with the task objectives, and assess potential security significance without treating information disclosure alone as a confirmed vulnerability.

# 5. Activities Performed and Results

## 5.1 PM2 – Footprinting with GHDB

The Google Hacking Database on Exploit-DB was opened and searched using the term **“cam”**. Webcam-related dorks were reviewed and tested in Google Search. The workbook records ten webcam-related result URLs and ten mathematics e-book/document URLs.

Examples of webcam dork patterns recorded in the workbook include:

- `intitle:"Webcam" inurl:WebCam.htm`
- `inurl:webcam`
- `intitle:"webcamXP" inurl:8080`
- `inurl:/view.shtml`
- `inurl:"live/cam.html"`

The workbook also records a Kingston / Half-Way Tree live-camera result on SkylineWebcams.

| Task | Recorded Outcome | Assessment Note |
|---|---|---|
| Webcam search | 10 URLs recorded, including public webcam pages and camera-interface paths. | Demonstrates that search operators can locate indexed camera pages. The list alone does not prove that a camera is misconfigured or that unauthorized access is possible. |
| Mathematics e-book search | 10 URLs recorded for mathematics PDFs, learning resources, and document pages. | Demonstrates document discovery through title/file-related search terms. No access-control weakness was validated. |

**Evidence:** [PM2 – Google Hacking Database screenshots](./screenshots/PM2-GHDB/)

> **SECURITY / ETHICS:** Do not attempt login, control functions, stream manipulation, or access to non-public camera feeds. Treat any exposed administrative interface or sensitive content as a lead for responsible disclosure to the owner, not as permission to investigate further.

## 5.2 PM3 – Footprinting with Maltego

Maltego Desktop was installed and configured. A Domain entity was added to the graph and its value was changed to `networkwalks.com`. Email-related transforms were filtered and executed.

The supplied screenshots show the `networkwalks.com` domain entity and an email-related transform output connected to the domain. However, the workbook does not provide a legible, verifiable inventory of the individual email addresses or a confirmed total. Accordingly, this report records the transform as executed but does not invent email addresses or counts.

| Observation | Result |
|---|---|
| Target entity | `networkwalks.com` |
| Transform category | Email-related transforms |
| Evidence available | Screenshots show the domain entity, transform selection, and an email-related result node. |
| Limitations | Individual output values/count are not sufficiently legible in the supplied workbook to report reliably. |

**Evidence:** [PM3 – Maltego screenshots](./screenshots/PM3-Maltego/)

## 5.3 PM4 – Footprinting with theHarvester

theHarvester version 4.10.1 was launched in Kali Linux. Two commands were documented in the practical:

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

```bash
theHarvester -d microsoft.com -l 50 -b all
```

| Run | Configuration | Observed Result |
|---|---|---|
| Task 1 | Domain: `microsoft.com` \| Limit: 1000 \| Source: `baidu` | Output states: no IPs found, no emails found, no people found, and no hosts found. |
| Task 2 | Domain: `microsoft.com` \| Limit: 50 \| Sources: `all` | The screenshot shows source/API errors or limitations (including missing API keys and a search error) and no IPs, emails, people, or hosts found. |

**Interpretation:** The absence of results is not evidence that the target has no public infrastructure or associated personnel. It means that these specific runs, with the selected sources and available API access, did not return enumerated records. Source availability, rate limits, API-key requirements, and tool configuration may affect results.

**Evidence:** [PM4 – theHarvester screenshots](./screenshots/PM4-theHarvester/)

## 5.4 PM5 – Network Scanning with Zenmap

The Windows `ipconfig` output recorded an Ethernet IPv4 address of `192.168.56.1` and subnet mask `255.255.255.0`, corresponding to the `192.168.56.0/24` network. Zenmap was then used for host discovery on the local subnet.

| Item | Observed Result |
|---|---|
| Local IPv4 address | `192.168.56.1` |
| Subnet mask | `255.255.255.0` |
| Subnet / CIDR | `192.168.56.0/24` |
| Live hosts reported | 1 host (including the tester's PC, as stated in the workbook) |
| Live host address | `192.168.56.1` |
| MAC address | Not available in Zenmap output |
| Host status | Up |
| Open ports shown | 3 |
| Filtered / closed ports shown | 0 filtered / 0 closed in the displayed host details |
| Topology export | Topology view was opened, exported to PDF, and the PDF was subsequently uploaded and committed to the GitHub repository. |

**Interpretation:** The scan identified one responding host in the tested subnet. The host IP matches the local Ethernet IPv4 address recorded by `ipconfig`, so the evidence is consistent with the tester's own machine being the responding host. The workbook does not identify the three open port numbers or associated services; these are therefore not stated as findings.

The Zenmap topology export is available here:

**[View / Download PM5 Zenmap Topology Export (PDF)](./screenshots/PM5-Zenmap/PM5_Zenmap_Topology_Export.pdf)**

**Evidence:** [PM5 – Zenmap screenshots and supporting files](./screenshots/PM5-Zenmap/)

> **LIMITATION:** The topology PDF's presence in the repository has been verified. Its detailed contents have not been independently reviewed for this report. The three open port numbers and associated services were also not recorded in the supplied workbook.

# 6. Findings and Risk Analysis

Risk ratings below are qualitative assessments of potential exposure based on the supplied evidence. They are not confirmed vulnerability severities. A finding is not considered exploitable unless it is validated through authorized testing.

| ID | Finding / Observation | Potential Impact | Risk |
|---|---|---|---|
| F-01 | GHDB search identified ten webcam-related URLs, including publicly indexed camera pages. | Publicly indexed camera pages may expose intended public video feeds or, in some cases, reveal an interface that warrants owner review. No unauthorized access or control was tested. | Low–Medium |
| F-02 | GHDB search identified ten mathematics e-book/document URLs. | Search-engine indexing can make documents easier to discover. No sensitive or restricted document exposure was confirmed from the workbook. | Low |
| F-03 | Maltego email-focused transforms were run against `networkwalks.com`; screenshots show an email-related result node. | Publicly discoverable email patterns can support targeted phishing or social engineering. Individual addresses and volume were not verifiable from the supplied evidence. | Low |
| F-04 | theHarvester runs against `microsoft.com` returned no enumerated IPs, emails, people, or hosts; second run showed source/API limitations. | No direct exposure was established. Incomplete source coverage means the results should not be interpreted as proof that no public information exists. | Informational |
| F-05 | Zenmap discovered one live host at `192.168.56.1`; three open ports were shown, but port numbers/services were not recorded. | Unexpected open services can increase attack surface. The observed address appears to be the tester's own host; service-level risk cannot be assessed without port/service details. | Low / Needs validation |

**Risk key:**

- **Critical:** Immediate severe exposure.
- **High:** Significant potential compromise.
- **Medium:** Meaningful exposure requiring timely review.
- **Low:** Limited or unvalidated exposure.
- **Informational:** Operational observation without a demonstrated security weakness.

# 7. Recommendations

1. **Review publicly indexed camera pages.** Confirm that each page is intentionally public. Owners should remove unintended listings, disable default credentials, restrict management interfaces, and enforce authentication for non-public streams.

2. **Review search-engine indexing of organizational documents.** Apply appropriate access controls and use supported removal/de-indexing processes for documents that should not be publicly discoverable.

3. **Review publicly exposed organizational contact information.** Maintain anti-phishing controls, including user awareness, email authentication (SPF, DKIM, and DMARC), and monitoring for impersonation.

4. **Improve future theHarvester exercises.** Document source availability and API-key requirements. Repeat only within the authorized scope, record tool errors, and avoid interpreting empty results as proof of absence.

5. **Improve local network scan documentation.** Record the exact Zenmap command/profile, scan date, port numbers, service/version details, and MAC address where available. Verify whether each open service is expected and disable or restrict unnecessary services.

6. **Retain and validate the topology export.** The Zenmap topology PDF has been uploaded to the repository. Confirm that the file opens correctly and contains the intended subnet and host details.

7. **Maintain testing records.** Retain written authorization, scope boundaries, timestamps, and evidence records for all future reconnaissance and scanning activities.

# 8. Limitations

- The report is based on the supplied `Lab WK2.docx` practical workbook and the provided sample report, with the Zenmap topology export's subsequent presence in the GitHub repository also confirmed.
- Maltego output does not provide a sufficiently legible list/count of email addresses to support detailed reporting.
- theHarvester results were constrained by source/API availability; no positive records were returned in the captured output.
- Zenmap evidence does not identify the three open port numbers or services, and the MAC address was unavailable.
- The topology PDF's presence in the repository is confirmed, but its contents have not been independently reviewed for this report.
- No exploitation, credential testing, vulnerability scanning, privilege escalation, or post-exploitation activity is documented.

# 9. Conclusion

The Week 02 practicals provided experience with several reconnaissance and discovery techniques. GHDB research demonstrated how search operators can locate publicly indexed webcam and document pages. Maltego was used to build a domain entity and execute email-related transforms against `networkwalks.com`. theHarvester was run against `microsoft.com`, but the captured output contained no enumerated records and showed limitations with some sources. Zenmap identified one live host on the local `192.168.56.0/24` subnet, with three open ports reported but not individually identified.

The Zenmap topology export was subsequently saved and uploaded to the repository as supporting evidence.

The results reinforce the importance of separating discovery from validation. Publicly indexed information, an email-related graph node, an empty OSINT result, or a live host does not by itself establish a vulnerability. Further work should focus on completing the evidence record, validating expected services within the authorized scope, and ensuring that any potentially exposed resources are reviewed by their owners.

# 10. Evidence Register

The following links provide access to the supporting evidence uploaded to this repository.

| Evidence ID | Source Workbook Section | Evidence Described | GitHub Evidence |
|---|---|---|---|
| E-01 | PM2 – GHDB | Screenshots of GHDB search for “cam”, selected dork, Google search results, and webcam result pages. | [Open PM2 evidence](./screenshots/PM2-GHDB/) |
| E-02 | PM2 – Mathematics dorks | Recorded table of ten mathematics e-book/document URLs and associated search pattern. | [Open PM2 evidence](./screenshots/PM2-GHDB/) |
| E-03 | PM3 – Maltego | Screenshots of Maltego configuration, `networkwalks.com` domain entity, email transform selection, and result graph. | [Open PM3 evidence](./screenshots/PM3-Maltego/) |
| E-04 | PM4 – theHarvester | Kali screenshots showing theHarvester 4.10.1, Baidu run output, and all-sources run output/errors. | [Open PM4 evidence](./screenshots/PM4-theHarvester/) |
| E-05 | PM5 – Zenmap | `ipconfig` output, Zenmap host discovery, host details showing `192.168.56.1` and three open ports, and topology/export workflow. | [Open PM5 evidence](./screenshots/PM5-Zenmap/) |
| E-06 | PM5 – Zenmap Topology | Exported Zenmap network topology PDF. | [Open / Download Topology PDF](./screenshots/PM5-Zenmap/PM5_Zenmap_Topology_Export.pdf) |

---

## Report Author

**Name:** Tishayna McFarlane  
**Designation:** Cybersecurity Intern – B084  
**LinkedIn:** [Tishayna McFarlane](https://www.linkedin.com/in/tishayna-mcfarlane-3417107b/)  
**Programme:** Cybersecurity Programme at Networkwalks  
**Reporting Week:** Week 02  


---

**End of Report**
