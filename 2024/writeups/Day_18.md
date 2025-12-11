# Advent of Cyber 2024 Writeup: Day 18

## Overview
**Room URL:** https://tryhackme.com/r/room/adventofcyber2024 \
**Difficulty:** Easy\
**Category:** Prompt Injection\
**Date Completed:** 12/19/2024

### Objectives
1. Gain a fundamental understanding of how AI chatbots work.
2. Learn some vulnerabilities faced by AI chatbots
3. Practice a prompt injection attack on WareWise, Wareville's AI-powered assistant

---

## Table of Contents
1. [Introduction](#introduction)  
2. [Walkthrough](#walkthrough)  
   - [Task 24: I could use a little AI interaction!](#task-24-i-could-use-a-little-ai-interaction)  
3. [Lessons Learned](#lessons-learned)  
4. [References](#references)

---

## Introduction
This task focuses on Prompt Injection to make AI Chatbots malfunction and reveal information it should not normally reveal. As AI chatbots become more popular, prompt injection will become a crucial way that insecure systems can be exploited. It is important to know how these exploitations can occur in order to better protect these systems.

---

## Walkthrough

### Task 24: I could use a little AI interaction!

#### Sub-Question: What is the technical term for a set of rules and instructions given to a chatbot?

  - **Steps Taken:** This is obvious from the instructions above.

#### Sub-Question: What query should we use if we wanted to get the "status" of the health service from the in-house API?

  - **Steps Taken:** I just used the instructions provided in the task description.

#### Sub-Question: After achieving a reverse shell, look around for a flag.txt. What is the value?

  - **Steps Taken:** I used the `pwd` command to find out the working directory then `cd..` until I reaced `/home/analyst` where I found the `flag.txt` file.

---

## Lessons Learned
- Learnt how AI chatbots without proper security can be made to disregard system prompts and follow user prompts which can lead to leaking information and causing it to do tasks it was not designed for.

---

## References