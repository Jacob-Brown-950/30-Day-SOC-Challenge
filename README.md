## 30-Day SOC Challenge

I’ve decided to take on the **30-Day SOC Analyst Challenge**, a fantastic project created by [MyDFIR](https://www.youtube.com/@MyDFIR). The goal of this challenge is to gain practical, hands-on experience in various areas of cybersecurity, while also getting familiar with a new cloud platform—**Vultr**. As someone who’s still building a solid foundation in cybersecurity, I believe this challenge will not only enhance my knowledge but also strengthen my skills through real-world scenarios.

Here’s a breakdown of what each week focuses on and some insights into why I chose these topics:

---

### Week 1: Introduction to ELK
- **Topics**:
  - **Introduction to the ELK Stack**: The ELK stack (Elasticsearch, Logstash, Kibana) is a powerful set of tools for log management and security monitoring. ELK is widely used in SOC environments, so mastering this will be key for my future work in cybersecurity.
  - **How to set up ELK**: I’ll be deploying the ELK stack on the Vultr cloud service. This will teach me not only the setup but also troubleshooting common issues with cloud deployments—an essential skill in today’s remote infrastructure-heavy world.
  - **How to ingest logs using Sysmon**: Sysmon is invaluable for gathering detailed event logs on Windows. I’ll be integrating it into ELK for log ingestion, which is a critical process for monitoring system activities and detecting potential threats early.

Setting up ELK and Sysmon helps lay the groundwork for monitoring and alerting, two critical functions in any SOC. Plus, ELK is a must-know tool for anyone aspiring to work in security operations.

---

### Week 2: Brute Force Attack Detection
- **Topics**:
  - **Introduction to brute force attacks**: I’ll learn how attackers use brute force to try and gain access to systems by guessing credentials. Understanding this attack vector is essential because it’s one of the most common techniques used by cybercriminals.
  - **How to set up SSH and RDP servers**: By setting up these servers, I’ll not only simulate real-world environments that hackers typically target but also learn how to configure them securely.
  - **How to create alerts and dashboards**: Building custom alerts and dashboards will give me practical skills in detecting brute force attacks in real time, as well as creating visual representations of those detections in Kibana.

*Why I chose this*: Brute force attacks are a common threat, especially in public-facing environments. Detecting and defending against them is a core SOC responsibility. I wanted to get hands-on experience with both recognizing the signs of brute force and mitigating the damage.

---

### Week 3: Command and Control (C2)
- **Topics**:
  - **Introduction to command and control (C2)**: Command and control is a crucial component of many cyberattacks, allowing hackers to remotely control infected machines. Learning how C2 works will give me insights into how attackers operate after gaining a foothold.
  - **How to set up your own C2 server using Mythic**: By setting up a C2 server, I’ll experience first-hand how attackers manage compromised systems. I’ll use **Mythic**, a popular open-source C2 framework, which will give me exposure to the tools attackers often use.
  - **How to attack public servers**: I’ll be simulating attacks on public servers to see how attackers use C2 to exploit vulnerabilities and maintain persistence in a network.

*Why I chose this*: Understanding C2 is a game changer. It’s one thing to defend against attacks, but knowing how attackers maintain control within a network will allow me to think like a hacker, which is invaluable for any cybersecurity professional.

---

### Week 4: Ticketing System Integration and Investigations
- **Topics**:
  - **Introduction to ticketing systems**: A huge part of a SOC analyst’s job involves managing incidents through a ticketing system. In this week, I’ll be integrating one into my SOC environment, simulating how real-world teams work together to resolve issues.
  - **Conducting investigations**: I’ll walk through the process of investigating security incidents, from initial detection to remediation. This will involve pulling logs, analyzing patterns, and understanding what happened during the attack, along with communicating those findings via a ticketing system.

*Why I chose this*: Investigation skills are fundamental to cybersecurity. Learning how to work through an incident from detection to closure, especially within a structured ticketing system, will help me develop real-world workflows that SOC teams use daily.

---

### Conclusion
By the end of this challenge, I aim to have a much deeper understanding of how to detect and respond to cybersecurity threats in a SOC environment. Not only will I gain technical skills—like setting up servers and monitoring systems—but I’ll also get a better sense of how attackers think and operate, which is just as important. This challenge is designed to push me out of my comfort zone and introduce me to tools and techniques that are widely used in the cybersecurity industry.

If you're following along, I hope my journey inspires you to try these techniques and build your skills too. It's all about learning through doing, and there's no better way to do that than diving into real-world simulations like this!
