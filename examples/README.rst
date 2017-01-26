Examples
===============================================================================

TODO
-------------------------------------------------------------------------------

* Add examples (at least one) in this directory
* Update contents of this 'README.rst' file

Example Guideline
-------------------------------------------------------------------------------

- Describe prerequisite e.g. compile code, set environment variables, or
  prepare input files 
- Describe commands/steps to run your example program. 
- Describe output messages/files.

For instance, if you have a word count example, example instructions look like
the following.

Example (Word Count)
-------------------------------------------------------------------------------

- Confirm environment variables
  ::

    export JAVA_HOME=/usr/java/default
    export PATH=${JAVA_HOME}/bin:${PATH}
    export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar

- Compile programs::
  
  $ bin/hadoop com.sun.tools.javac.Main WordCount.java
  $ jar cf wc.jar WordCount*.class

- Prepare input files where /usr/joe/wordcount/ is a main directory in HDFS::

  $ bin/hadoop fs -ls /user/joe/wordcount/input/ /user/joe/wordcount/input/file01 /user/joe/wordcount/input/file02

  $ bin/hadoop fs -cat /user/joe/wordcount/input/file01
  Hello World Bye World

  $ bin/hadoop fs -cat /user/joe/wordcount/input/file02
  Hello Hadoop Goodbye Hadoop

- Run::

  $ bin/hadoop jar wc.jar WordCount /user/joe/wordcount/input /user/joe/wordcount/output

- Find output::

  $ bin/hadoop fs -cat /user/joe/wordcount/output/part-r-00000`
  Bye 1
  Goodbye 1
  Hadoop 2
  Hello 2
  World 2`
