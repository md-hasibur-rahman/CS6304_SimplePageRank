# SimplePageRank

### General Information:

* Operating System:         Mac -> Microsoft Remote Desktop, Windows -> Default Remote Desktop, Ubuntu -> Remmina
* Machine:                  cs6304-<mst_username>-01.class.mst.edu
* User:                     <mst_username>
* Default Password:         <mst_password>

### Importing Project:
* Open “eclipse”, right click on “Package Explorer” window, click import.
* Select “Git”-> “Projects from Git” and click “next”.
* Select “clone url” and click “next”.
* Paste “ https://github.com/md-hasibur-rahman/CS6304_SimplePageRank ” in the “url” textbox, and click “next”. 
* Choose “Import existing project” and click “finish”.

### Referencing libraries:
* Right click on project and select “build path”-> “configure build path” ->”libraries”->”add external jars”.
* Go to "home" -> "git" -> "SimplePageRank" -> "lib" and select all jars and click ok.

### Input file:
* Open folder "file", you will see the input file named "PageRank.txt"

### Output jar:
* Right click on project and select "Export".
* Choose type "Java" -> "Jar file" and click "next".
* Select the export destination as "home" -> "git" -> "SimplePageRank" -> "jar" and click "Finish".

### Hadoop Commands:
If OutputFolder and/or InputFolder already exist, remove them (using below two commands) before running the next hadoop code.
```
hadoop fs -rm -r OutputFolder                                     //to remove "OutputFolder" directory and all its files
hadoop fs -rm -r InputFolder					    //to remove "InputFolder" directory and all its files
```
Use below commands to run your code.  
```
hadoop fs -mkdir InputFolder                                      //to create a new input folder
hadoop fs -copyFromLocal <input file> InputFolder                  //to copy a file from local directory to hadoop environment
hadoop fs -ls InputFolder                                          //to see the files inside "InputFolder"
hadoop jar <jar file name> <class name> InputFolder OutputFolder   //running mapreduce operation
hadoop fs -ls OutputFolder                                        //to see the files inside "OutputFolder"
hadoop fs -cat OutputFolder/part-r-00000                          //to see the content inside "OutputFolder/part-r-00000" file
```

- remove OutputFolder before generating the next results.
- remove/clean InputFolder if you want to use a different file as input.
  
### Common error fix:
Error 1: mkdir: Call From cs6304-akkcm-02/127.0.1.1 to localhost:9000 failed on connection exception: java.net.ConnectException: Connection refused  
Explanation and Fix: In general this error comes if you are running hadoop first time on your VM after a reset. The below commands will fix it.
```
stop-all.sh
hadoop namenode -format
start-all.sh
```
You can use the below command to check if namenode, datanode and nodemanager are running.
```
jps

```

Error 2: mkdir: `hdfs://localhost:9000/user/<username>': No such file or directory  
Explanation and Fix: The error comes when there is no directory /user and /user/<username> in hdfs and you are trying to create a folder using "hadoop fs -mkdir InputFolder ".   
Below command will create the directory structure if required and solves the problem.
```
hdfs dfs -mkdir -p InputFolder
```
Error: "shell-init: error retrieving current directory: getcwd"  
- the directory at which you are when you try to run hadoop command does not exist anymore.  

Warning 1: WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable  
Fix: You can just ignore this warning.
