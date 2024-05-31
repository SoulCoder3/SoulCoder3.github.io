---
layout:     post
title:      Debug with Script and Searching Commands
subtitle:   
date:       2023-10-27
author:     BY David
header-img: img/TechTool.jpg
catalog: true
tags:
    - Commands
    - Debug


---

## Part1 - Bugs  
## The bugs from filter() in ListExamples.java
### A failure-inducing input:
```java
@Test
public void testFilter1() {
  List<String> test = new ArrayList<>();
  test.add("ssoss");
  test.add("qqqqq");
  test.add("abcdefg");
  List<String> result = ListExamples.filter(test, checker);
  List<String> exception = new ArrayList<>();
  exception.add("qqqqq");
  exception.add("abcdefg");
  assertEquals(exception, result);
}

public StringChecker checker = (str) -> { //return False if the String contain 'o'
  if (str.contains("o"))
    return false;
  return true;
};
```  
Result:  
![failure-input](https://raw.githubusercontent.com/SoulCoder3/SoulCoder3.github.io/master/img/2023-10-29-DebugWithScript-SearchingCommands/failure-input.png) 

### An input that doesn’t induce a failure:  
```java
@Test
public void testFilter2() {
  List<String> test = new ArrayList<>();
  test.add("ssoss");
  test.add("qqqqq");
  List<String> result = ListExamples.filter(test, checker);
  List<String> exception = new ArrayList<>();
  exception.add("qqqqq");
  assertEquals(exception, result);
}

public StringChecker checker = (str) -> { //return False if the String contain 'o'
  if (str.contains("o"))
    return false;
  return true;
};
```  
Result:  
![success-input](https://raw.githubusercontent.com/SoulCoder3/SoulCoder3.github.io/master/img/2023-10-29-DebugWithScript-SearchingCommands/success-input.png)  

So the symptom is:  
![symptom-output](https://raw.githubusercontent.com/SoulCoder3/SoulCoder3.github.io/master/img/2023-10-29-DebugWithScript-SearchingCommands/symptom-output.png)  

The bug code before fix:
```java
  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```

The code after fix with deleting '0' argument in add():  
```java
// Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(s);  //delete '0' argument at add()
      }
    }
    return result;
  }
```  
Test pass:  
![success-output](https://raw.githubusercontent.com/SoulCoder3/SoulCoder3.github.io/master/img/2023-10-29-DebugWithScript-SearchingCommands/success-output.png)  

### Description: 
`StringChecker()` return `False` if the String contains 'o'. From the successful test, I can know that the filter function successfully filter by `StringChecker()`, because the result List doesn't contain 'ssoss'.  
According the symptom, I can know that the result List is in reverse order from the expect List. The bug code is `result.add(0, s)`, leading to it insert the new String at head of the List every time. By changing to `result.add(s)`, it would insert the new String at the Last of the List, so that the result List keep in the same order they appeared in the input list.

## Part2 - Researching Commands  
### find ./technical -size -3k
find all the file which size less than 3kb.  
-Nk means less than Nkb and +Nk means greater than N kb.
k represent kilo bytes. There are other units like c, w, M and G, representing different size.
```java
$ find ./technical -size -3k
./technical
./technical/911report
./technical/biomed
./technical/government
./technical/government/About_LSC
./technical/government/Alcohol_Problems
./technical/government/Env_Prot_Agen
./technical/government/Gen_Account_Office
./technical/government/Media
./technical/government/Media/Campaign_Pays.txt
./technical/government/Media/Court_Keeps_Judge_From.txt
./technical/government/Media/Fire_Victims_Sue.txt
./technical/government/Media/It_Pays_to_Know.txt
./technical/government/Media/Justice_requests.txt
./technical/government/Media/Lawyer_Web_Survey.txt
./technical/government/Media/Self-Help_Website.txt
./technical/government/Post_Rate_Comm
./technical/plos
./technical/plos/pmed.0020028.txt
./technical/plos/pmed.0020048.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0020120.txt
./technical/plos/pmed.0020157.txt
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0020226.txt
```
It prints all the work directory, subdirectory and all the file which size less than 3kb including the files in subdirectory.

### find ./technical/plos/*.txt -size -3k
find all the .txt files in the plos directory which size less than 3kb.
```java
$ find ./technical/plos/*.txt -size -3k
./technical/plos/pmed.0020028.txt
./technical/plos/pmed.0020048.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0020120.txt
./technical/plos/pmed.0020157.txt
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0020226.txt
```  
It prints all the txt files in the plos directory and their size all less than 3kb.  

### find ./technical -type d
d means directory. so the command find all the directory and subdirectory under the work directory.
```java
$ find ./technical -type d
./technical
./technical/911report
./technical/biomed
./technical/government
./technical/government/About_LSC
./technical/government/Alcohol_Problems
./technical/government/Env_Prot_Agen
./technical/government/Gen_Account_Office
./technical/government/Media
./technical/government/Post_Rate_Comm
./technical/plos
```
It prints the work directory and all subdirectory.
#### -size option provides a useful way to find the special size files.
### find ./technical/plos/*.txt -type f
f means file, so the command find all the files in work directory and subdirectory.
```java 
$ find ./technical/plos/*.txt -type f
./technical/plos/journal.pbio.0020001.txt
./technical/plos/journal.pbio.0020010.txt
./technical/plos/journal.pbio.0020012.txt
./technical/plos/journal.pbio.0020013.txt
./technical/plos/journal.pbio.0020019.txt
./technical/plos/journal.pbio.0020028.txt
./technical/plos/journal.pbio.0020035.txt
./technical/plos/journal.pbio.0020040.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/journal.pbio.0020047.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020054.txt
./technical/plos/journal.pbio.0020063.txt
./technical/plos/journal.pbio.0020064.txt
./technical/plos/journal.pbio.0020067.txt
./technical/plos/journal.pbio.0020068.txt
./technical/plos/journal.pbio.0020071.txt
./technical/plos/journal.pbio.0020073.txt
./technical/plos/journal.pbio.0020100.txt
./technical/plos/journal.pbio.0020101.txt
./technical/plos/journal.pbio.0020105.txt
./technical/plos/journal.pbio.0020112.txt
./technical/plos/journal.pbio.0020113.txt
./technical/plos/journal.pbio.0020116.txt
./technical/plos/journal.pbio.0020121.txt
./technical/plos/journal.pbio.0020125.txt
./technical/plos/journal.pbio.0020127.txt
./technical/plos/journal.pbio.0020133.txt
./technical/plos/journal.pbio.0020140.txt
./technical/plos/journal.pbio.0020145.txt
./technical/plos/journal.pbio.0020146.txt
./technical/plos/journal.pbio.0020147.txt
...
```
It prints all the file under /plos.
#### -type option will be useful when we want to search a certain type of data.
### find ./technical -empty
Find for empty files or directories. empty.txt and empty folder are a empty file and a empty directory created by me.
```java
$ find ./technical -empty
./technical/government/Post_Rate_Comm/empty.txt
./technical/plos/empty folder
```

### find ./technical/government/Post_Rate_Comm/*.txt -empty
Find all the empty txt files in Post_Rate_Comm. Since there is only empty.txt is a empty file, the command line prints it.
```java
$ find ./technical/government/Post_Rate_Comm/*.txt -empty
./technical/government/Post_Rate_Comm/empty.txt
```
#### -empty option let users to find their empty folder or files, so that they can deal with their empty places.

### find ./technical/ -mmin -60
Search all the modified files in the last 60 minutes from now.
`-mmin` means modified minutes, and -60 means less than 60 minutes from now.
```java
$ find ./technical/ -mmin -60
./technical/
./technical/empty2.txt
./technical/government/Post_Rate_Comm
./technical/government/Post_Rate_Comm/empty.txt
./technical/plos
./technical/plos/empty folder
```
It prints all the files and the directory which modified less than 60 minutes from now.

### find ./technical/plos/*.txt -mmin +60
Search all the txt under ./technical/plos/ which modified over than 60 minutes from now.  
```java
$ find ./technical/plos/*.txt -mmin +60
./technical/plos/journal.pbio.0020001.txt
./technical/plos/journal.pbio.0020010.txt
./technical/plos/journal.pbio.0020012.txt
./technical/plos/journal.pbio.0020013.txt
./technical/plos/journal.pbio.0020019.txt
./technical/plos/journal.pbio.0020028.txt
./technical/plos/journal.pbio.0020035.txt
./technical/plos/journal.pbio.0020040.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/journal.pbio.0020047.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020054.txt
./technical/plos/journal.pbio.0020063.txt
./technical/plos/journal.pbio.0020064.txt
./technical/plos/journal.pbio.0020067.txt
./technical/plos/journal.pbio.0020068.txt
...
```
-N means less than N minutes from now and +N means over than N minutes from now.
#### -mmin option is a useful way to search the files which have been modified at a specific time.

## Reference
The tutorial of -type and -mmin I found is from LinuxTech.  
https://www.linuxteck.com/find-command-in-linux-with-examples/  
The tutorial of -size and -empty I found is from Geeks.  
https://www.geeksforgeeks.org/find-command-in-linux-with-examples/  
These two tutorial are the methods I found that worked for me in multiple Google search results.  