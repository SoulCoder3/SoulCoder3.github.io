# CSE 15L lab report 4
## Log into ieng6
![image](Step0.png)  
```java
// Key Pressed: 
ssh<space>cs15lfa23gc@ieng6.ucsd.edu<enter>
```
* `ssh`: provides a secure encrypted connection between two hosts over an insecure network.  
* `<space>`: Enter a space.  
* `cs15lfa23gc@ieng6.ucsd.edu`: my ieng6 server address.  
* press `<enter>`to run the command and connect ieng6 server.  
![image](Step0_2.png)  

***

## Clone your fork of the repository from your Github account (using the SSH URL)
![image](Step1.png)  
```java
// Key Pressed:
git<space>clone<space><cltrl+V><enter>
```
* `git clone`: make a copy in a local directory from remote directory.  
* `<cltrl+V>`: paste the SSH key of the clipoard into the current cursor location, where the SSH key already copy from the github page.  
* press `<enter>`to run the command and connect ieng6 server.  

***

## Run the tests, demonstrating that they fail
![image](Step2.png)  
```java 
// key pressed:
1. cd<space>cse<tab><enter>
2. bash<space>tes<tab>.sh<enter>
```
* `cd`: allows user to change the current directory.  
* `<tab>`: command names, parameter names, argument values and file paths can all be autofilled by pressing the Tab key, if the they exist.  
* type `cd ` and then type `cse<tab>`. `<tab>` autofill the folder name `cse-15l-lab/`.  
* press `<enter>` to change the current work directory to `cse-15l-lab/`.  
* `<bash>`: run a command processor.  
* type `bash` and then type `tes<tab>`. `<tab>` autofill the bash file name `test`.  
* press `<enter>` to run the test.  

***

## Edit the code file to fix the failing test
![image](Step3.png)  
![image](Step3_2.png)    
```java
// key pressed:
1. vim<space>List<tab>.java<enter>
2. /index1<enter><n><n><n><n><n><n><n><n><n><i><right><right><right><right>><right><right><backspace>2<esc>:wq<enter>
```
* `vim`: open document by vim editor.  
* type `vim ` and then type `List<tab>.java` to open `ListExamples.java` in vim.  `<tab>` autofill ListExamples.  
![image](Step4.png)  
* `/text`: search a text in document in vim. The cursor will move to the first character of the first matching word.   
* type `/index1<enter>` to search `"index1"` text in the file. It will move the cursor to the first `"i"` of the first matching word `"index1"`.  
![image](Step4_2.png)  
* type `<n>` 9 times, `<n>` will move the cursor to the next matching word. so the cursor move to the `"index1"` we want to fix after 9 times.  
![image](Step4_3.png)  
* type `<i>` change to insert mode, where we can insert and edit text.
* `<right>`: move the cursor one position to the right.  
* press `<right>` 6 times to move the cursor on the character `1`.  
![image](Step4_4.png)  
* press `<backspace>` to delete `1` and then type `2`.  
* press `<esc>` to go back normal mode.  
![image](Step4_5.png)  
* type `:wq<enter>` to save and quit vim.  

***

## Run the tests, demonstrating that they now succeed
![image](Step5.png)  
```java
// key pressed:
<up><up><enter>
```
* type `<up><up>`:  `bash test.sh` command was 2 up in the search history, so I used up arrow to access it.  
* press `<enter>` to run the test and get success.  

***

## Commit and push the resulting change to your Github account (you can pick any commit message!)
```java
// key pressed:
1. git<space>add<space>*<enter>
2. git<space>commit<space><->m<space>"Debug<space>index"<enter>
3. git<space>push<enter>
```
### git add
![image](Step6.png)  
* `git add *` to add all change in the working directory to the staging area.  
* The files methioned in `.gitignore` file would be ignore when add.  

### git commit
![image](Step6_2.png)   
* `git commit -m "Debug index"`: submit changes in the staging area to the local repository, and add message `"Debug index"`.  

### git push
![image](Step6_3.png)  
* `git push`: submit changes in local repository to remote repository.  
![image](Step7.png)  
* double check the change in remote repository.