# Advent of Cyber 2025 Writeup: Day 15

## Overview
**Room URL:** https://tryhackme.com/room/webattackforensics-aoc2025-b4t7c1d5f8

### Objectives
1. To detect and analyze common malicious web activity with help of Apache logs.
2. To identify OS-level attacker actions using Sysmon data.
3. To identify and decode suspicious or obfuscated attacker payloads.
---

## Table of Contents
1. [Introduction](#introduction)   
2. [Walkthrough](#walkthrough)  
   - [Task: Web Attack Forensics](#task--web-attack-forensics)

---

## Introduction
This room is all about using Splunk SIEM to identify web-based attacks. When attackers use a compromised machine to carry out web-based tasks, these show up in error and access logs which are aggregated in the SIEM. These events have common patterns which can be investigated in detail using the SIEM interface.

As an example, if an attacker tries to execute commands, they typically do this using `cmd` or `PowerShell` (`Invoke-Expression`). We can filter for these in our logs using queries. The attacker is often times careful, and tries to encode or obfuscate the actual commands. However, these can be decoded or decrypted by the defender.

Another example of a suspicious event is when a web server spawns system processes. Typically, a web server should only spawn worker threads and not system processes.

A vital indicator of compromise is when you see commands like `whoami` being run in the system. This is the first command that's run by a threat actor to determine which user they are running as.

---

## Walkthrough
>_In all honesty, I didn't do this room because the Splunk instance never loaded...even when the machine's timer was 5 minutes away from expiring. I just looked at the screenshots and inferred answers._

### Task : Web Attack Forensics

#### Sub-Question 1: What is the reconnaissance executable file name?
Based on the investigation, the answer is `whoami.exe`.

#### Sub-Question 2: What executable did the attacker attempt to run through the command injection?
Based on the investigation, the answer is `PowerShell.exe`.


---