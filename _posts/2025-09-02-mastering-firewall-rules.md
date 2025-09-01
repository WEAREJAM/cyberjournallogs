---
layout: post
title: "Mastering Firewall Rules: Blocking & Allowing Traffic Made Simple"
date: 2025-09-02
categories: [cyberjournallogs, firewall-security]
tags: [firewall, traffic-control, rules, inbound, outbound, ufw, network-security]
---
# FIREWALL 
What is a firewall? A firewall is an agent responsible for allowing or denying traffic based on rules. Coming to every system/agent, it can't decide the right/wrong traffic. 
Note: Here, the traffic refers to the request we are sending to the servers. 
The firewall always follows the rules and decides which traffic is to be allowed and denied. We can also add rules manually so it works the way we want. 
Example: Let's say we are using an application, and I don't want the telnet port to be open and exposed to attackers, so I add a rule to deny the port connection 

For this i am using ufw which is a firewall solution where we can filter the traffic. 
Note: Every web traffic is classified into two types, which are inbound and outbound traffic. The inbound traffic are which connections coming into our system, and where outbound traffic are the connections going out from our system. 

lets start ufw with  
>sudo ufw enable

this command activate firewall and enable system startup

To check if the ufw status we can use 
>sudo systemctl status ufw

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam1.png?raw=true)

Now with this we can confirm the system is active and ready to proceed.
In order to see the added rule list
>sudo ufw status numbered

Note: No rules will be added as this Kali Linux machine is set to default and none restrictions are added to the list.

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam2.png?raw=true)

Here in the above image, we see only the status, which indicates active, and no rules.

Let's add a rule to firewalls and see how we can allow or deny the traffic. 
Before adding the rules, all we have to know is whether we can allow or deny the traffic.

Port 443 
We all know how this port works, we make the request it reaches the server, and gets to the application, so is this it? No, the sent request is passed through inbound and outbound rules. And what are these types of rules?

I can set the rules to control the incoming and outgoing traffic. The outer traffic coming to our network is called inbound traffic, and the traffic going out from our system is called outbound traffic.

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam3.png?raw=true)

The above image is a well-opened application, the UFW by default have any specific rules.
Let's add the rule to deny 443 port and see how the webpage behaves 

>sudo ufw deny out 443/tcp //This "deny out" says to stop the traffic going from our network, if i want to stop traffic coming then deny <port no>

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam4.png?raw=true)

As the rule is added, let's check 

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam3.png?raw=true) 

As we see that the website is loaded, BUT WHY? 
Here i used Firefox application,the requests are dealt with 53 DNS port here. With this observation lets try to deny the DNS port traffic and see

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam6.png?raw=true)

Heres what i observes after rule is added

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam7.png?raw=true)

The search engine does its work perfectly with browsing the content 

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam8.png?raw=true)

![Firewall example](https://github.com/WEAREJAM/WEAREJAM-Kickstart_at_ElevateLabs-firewall-rule/blob/main/assets/sam9.png?raw=true)

Application is not loaded here, when it reaches the limit it pops limit message.

This is just an example of how the traffic is and can be controlled with a firewall. 

___Jamming with JAM___
