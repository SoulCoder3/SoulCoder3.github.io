---
layout:     post
title:      JDR, JRK, JVM, and HashMap, HashTable
subtitle:   
date:       2024-5-9
author:     BY David
header-img: img/TechTool.jpg
catalog: true
tags:
    - Java
    - Interview

---

# JDK, JRE, JVM

| JDK | JRE | JVM |
| --- | --- | --- |
| JDK(Java Development Kit) is mainly used for code development and execution.|JRE(Java Runtime Environment) is a mainly used for environment creation to execute the code.|JVM(Java Virtual Machine) provides specifications for all the implementations to JRE. |
JDK is a complete softwae development kit for developing Java application. | JRE software package providing Java class libraries, JVM and all the required components to run the Java applications.|JVM provides specifications for all the implementations to JRE.
 | It comprise JRE, JavaDoc, compiler, debuggers, etc|JRE provides libraries and classes required by JVM to run the program.|JVM = Runtime environment to execute Java byte code.

# HashMap and HashTable in Java

| HashMap | HashTable |
| --- | --- |
| HashMap is not synchronized thereby making it better for non-threaded applications.|HashTable is synchronized and hence it is suitable for threaded applications.|
| Allows only one key but any number of null in the values, because HashMap does special processing for **null**. The HasCode value of **null** is 0.|Doesn't allow **null** in both keys or values. |
Supports order of insertion by making use of its subclass LinkedHashMap.| Order of insertion is not guaranteed in HashTable. |
