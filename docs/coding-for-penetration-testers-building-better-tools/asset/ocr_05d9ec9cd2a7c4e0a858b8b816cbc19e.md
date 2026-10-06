# CHAPTER 7

# Scanner scripting

# Abstract

This chapter covers the use of Netcat, Nmap, and Ness/OpenVAS, and what we can do with them through scripting languages. We talk about automating Netcat through shell scripts, in order to allow us to send files, run simple network services, and forward ports, altering or adding to the behavior of Nmap, customization of Nessus and OpenVAS through the use of the Ness Attack Scripting Language, and several other similar tasks.

# Keywords

Netcat; Nmap; Nessus; OpenVAS; services; ports; NASL

# INFORMATION IN THIS CHAPTER

+   * Working With Scanning Tools
* Netcat
* Nmap
* Nessus/OpenVAS

# Introduction

When conducting a penetration test, scanning tools can be pretty handy. Because their functionality can be customized or their behavior scripted, their capabilities can be expanded considerably. This chapter focuses on Netcat, Nmap, and Nessus/OpenVAS—three tools that can be customized and/or automated with relative ease. First it explains how Nmap can be altered or enhanced through the use of Lua scripts