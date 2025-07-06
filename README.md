# CyberSim: Incident Response - Ransomware Attack

A single-player, web-based simulated environment to learn the fundamentals of cyber security incident response. No installation or external assets required—just open the `index.html` file in a browser.

---

## About The Project

This simulation places you in the role of an Incident Response Analyst at a mid-sized financial firm. You arrive at work to find a full-blown ransomware attack in progress. Your mission is to use the provided tools—a simulated desktop with an email client, a functional terminal, and log files—to triage, analyze, eradicate, and report on the incident.

This project was built to be a self-contained, no-fluff learning tool. It runs entirely in your browser with a single HTML file and has no external dependencies.

### Features

*   **Simulated Desktop Environment:** A familiar UI with draggable windows, desktop icons, and a taskbar.
*   **Interactive Terminal:** A powerful terminal that simulates a Unix-like file system (`ls`, `cd`, `cat`, `clear`) and includes custom incident response commands (`siem_query`, `isolate_host`, etc.).
*   **Quest & Story System:** Guided main quests and optional side quests track your progress and tell the story of the incident.
*   **Realistic Scenario:** Investigate phishing emails, analyze SIEM and VPN logs, find a CVE, and patch the vulnerability.
*   **Zero Dependencies:** Runs offline. Everything is packed into a single HTML file. No external libraries, no assets to load, no setup required.

---

## How to Play (Walkthrough)

Stuck? Here is a step-by-step guide to successfully completing the simulation.

<details>
<summary><strong>⚠️ Spoiler Warning: Click to reveal the full walkthrough</strong></summary>

1.  **Triage & Containment:**
    *   **Goal:** Find and isolate all infected machines.
    *   **Action:** Open the **Email Client** to find two hostnames from panicked user emails (`FIN-WKS-07`, `MKT-WKS-12`).
    *   Open the **Terminal** and query the SIEM for all errors: `siem_query --service=system --level=error`. This reveals a third host: `HR-WKS-02`.
    *   Isolate all three hosts:
        *   `isolate_host FIN-WKS-07`
        *   `isolate_host MKT-WKS-12`
        *   `isolate_host HR-WKS-02`

2.  **Forensic Analysis:**
    *   **Goal:** Figure out how the attackers got in.
    *   **Action 1 (Find the vulnerability):** In the terminal, look at the logs: `ls /var/log` and then `cat /var/log/vpn.log`. You will find a log entry mentioning an exploit for `CVE-2023-35078`.
    *   **Action 2 (Find Patient Zero):** In the **Email Client**, find the phishing email. Note the suspicious link: `http://megacorp-finance-auth.com/update`.
    *   Use this URL to query the SIEM in the terminal: `siem_query --url=http://megacorp-finance-auth.com/update`.
    *   The output reveals `bob.johnson@megacorp.finance` was the user who clicked the link.

3.  **Eradication & Recovery:**
    *   **Goal:** Patch the vulnerability and restore the systems from backup.
    *   **Action 1 (Patch):** Use the CVE you found earlier to patch the system: `run_patch CVE-2023-35078`.
    *   **Action 2 (Restore):** Restore each of the isolated hosts from backup. You must do at least one:
        *   `restore_from_backup FIN-WKS-07`

4.  **Communication:**
    *   **Goal:** Report your findings to leadership.
    *   **Action:** Open the **Incident Report** application. Fill in the form with the information you discovered:
        *   **Attack Vector:** `phishing` or `vpn`
        *   **Infected Hosts:** `3`
        *   **Vulnerability:** `CVE-2023-35078`
        *   **Remediation Summary:** A brief description of the steps you took.
    *   Click "Submit Final Report".

Once all four main quests are complete, you win the simulation!

</details>

---

## Technology Stack

*   **HTML5**
*   **CSS3** (with CSS Variables for theming)
*   **Vanilla JavaScript (ES6+)**

No frameworks, no libraries, no dependencies.

## Contributing

Contributions are welcome! If you have ideas for new quests, apps, or improvements, feel free to fork the repository and submit a pull request. You can also open an issue with the "enhancement" tag.

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.