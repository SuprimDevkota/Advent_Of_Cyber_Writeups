# Advent of Cyber 2025 Writeup: Day 5

## Overview
**Room URL:** https://tryhackme.com/room/idor-aoc2025-zl6MywQid9

### Objectives
1. To understand the concept of authentication and authorization in the context of IDORs/authorization bypass.
2. To learn how to spot and exploit IDOR opportunities.
3. To understand the vulnerability in `UUIDv1` and how that translates to an authorization bypass.

---

## Table of Contents
1. [Introduction](#introduction)   
2. [Walkthrough](#walkthrough)  
   - [Task: IDOR on the Shelf](#---)

---

## Introduction
This room deals with `IDORs` (Insecure Direct Object References) and provides ample theory on the need for checking authorization before granting access to resources. It emphasizes that authentication comes before authorization. It also states that masking or hashing resource numbers is an ill-fated way of concealing IDORs as these can be broken. The only thing that is secure is making sure that every request to access a resource is met with robust authorization checks. This makes sure that the user has sufficient permissions to access the resource that they are requesting.

---

## Walkthrough
### Task : IDOR on the Shelf

#### Sub-Question 1: What does IDOR stand for?
Answer is obvious.

#### Sub-Question 2: What type of privilege escalation are most IDOR cases?
Answer is obvious.

#### Sub-Question 3: Exploiting the IDOR found in the view_accounts parameter, what is the user_id of the parent that has 10 children?
This question can be solved with the help of Burp Suite's `Proxy` and `Intruder` modules. First, I made sure all of my web requests travelled through the Burp Proxy which intercepted them. The appropriate request containing the IDOR vulnerable parameter was sent to the Intruder. In the Intruder, I added a simple list from `1` to `20` in the `user_id` parameter and started the attack.
![burp_intruder](../screenshots/day_5/burp_intruder.png)

On analyzing the responses produced by the Intruder and inspecting the number of children, the answer to the question can be found simply by counting the number of children associated with the iterated parents.
![user_id_breeder](../screenshots/day_5/user_id_breeder.png)

#### Sub-Question 4: If you want to dive even deeper, use either the base64 or md5 child endpoint and try to find the id_number of the child born on 2019-04-17? To make the iteration faster, consider using something like Burp's Intruder. If you want to check your answer, click the hint on the question.
I used a different approach here. This can be simply inspected in the responses of the previous intruder attack itself.
![child_id](../screenshots/day_5/child_id.png)

#### Sub-Question 5: Want to go even further? Using the `/parents/vouchers/claim endpoint`, find the voucher that is valid on 20 November 2025. Insider information tells you that the voucher was generated exactly on the minute somewhere between 20:00 - 24:00 UTC that day. What is the voucher code? If you want to check your answer, click the hint on the question.
This question was a bit tricky since it required the generation of an appropriate `UUID`. I used ChatGPT to help me with this. Since I already had some sample valid vouchers in the application itself, I pasted it into ChatGPT and asked it to generate the required 240 voucher codes for every minute of the given timestamp. 
![chat-gpt](../screenshots/day_5/chatgpt_to_generate_uuidv1.png)

I pasted this list into the `Intruder` tab and started the attack. 
![intruder_uuid](../screenshots/day_5/intruder_uuid.png)

On analyzing the responses of the attack, only one voucher got a successfull response which is the required answer.
![voucher](../screenshots/day_5/voucher.png)

---