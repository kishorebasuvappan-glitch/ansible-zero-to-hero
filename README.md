# Ansible: Zero to Hero Automation Challenge

This repository serves as a comprehensive progress tracker and code log as I scale from absolute zero to mastering enterprise-level IT automation with Ansible. The primary goal is to gain full competency in managing cloud infrastructure, multi-node configuration deployments, and orchestration workflows.

---

## Technical Stack and Environment
- Configuration Language: YAML
- Control Engine: Ansible (Agentless Architecture)
- Protocols: Secure Shell (SSH)
- Environment Target: Ubuntu Linux Nodes

---

## Folder Architecture
The repository is structured daily to keep implementations clean and isolated:
- day-01/ : Installation, basic inventory files, and SSH key verification setup.
- day-02/ : Ad-hoc command executions, package setups, and service control tasks.
- day-03/ : Developing first playbooks using variables and handlers.
- day-04/ : Applying advanced loops and logic conditionals.
- day-05/ : Reusable structures and creating custom modular Roles.
- day-06/ : Managing secrets with Ansible Vault and dynamic data gathering.
- day-07/ : Production scale-up, automation platform components, and CI/CD pipelines.

---

## 7-Day Roadmap and Progress Tracker

- [x] Day 1: Fundamentals and Environment Setup
- [ ] Day 2: Ad-Hoc Power and Command Line Basics
- [ ] Day 3: Structuring Your First Playbooks
- [ ] Day 4: Advanced Flow Control (Loops and Conditionals)
- [ ] Day 5: Defining Modular Roles for Reusable Code
- [ ] Day 6: Advanced Playbooks (Vault Encryption and System Facts)
- [ ] Day 7: Enterprise Automation Scale-Up and CI/CD Pipelines

---

## How to Check Progress Locally
To review the operational files or run verification tests against your test nodes, navigate directly to the specific daily directory:

cd day-01
ansible all -m ping -i hosts.ini
