Prerequisites
-------------------------------------------------------------------------------

* Ansible
* Pip 
* Git
* Pull the project repository: sw-project-template from patch-1.

The URL is : git@github.iu.edu:ripandey/sw-project-template.git

Installation
===============================================================================

The following are the installation steps:

1. Make sure the ssh-agent is up and running. Also ensure that pip and git are installed. This instruction manual is with respect to the Chameleon cloud.

2. Clone the project repository to the local working directory.

3. Run the setup.sh file provided in the project repository. This will clone the big-data-stack and install all the necessary requirements.

                command::: $bash setup.sh

4. Now move into the big-data-stack folder that has been cloned and edit the .cluster.py file as follows:
                a. Change the openstack/image : CC-Ubuntu14.04
                b. Change the openstack/create_floating_ip: True
                c. Change the openstack/flavor: m1.medium
                d. Scroll down and change N_MASTER=8 and N_DATA=8
                e. The following configuration is an example for the creation of 8 medium instances:
                         _zookeepernodes = [(master, [0,1,2,3,4,5,6,7])]
		
			 _namenodes = [(master, [0,1,3,4])]
		
			 _journalnodes = [(master, [0,1,2,3,4,5,6,7])]
		
			 _historyservers = [(master, [2,3])]
		
			 _resourcemanagers = [(master, [0,1,3,4])]
		
			 _datanodes = [(master, xrange(N_DATA))]
		
			 _frontends = [(master, [0])]
	        
	        	 _monitor = [(master, [2,3,4])]

To run the project for both hadoop and spark, it is recommended to run at least 16 medium/large instances, owing to the huge dataset of 10 million records.


5. Now run the boot.sh file which will boot up 8 m1.medium instances on the Chameleon cloud.
  
                command::: $bash boot.sh

6. Now, make sure a virtual environment has been activated and test if all nodes can be pinged.

	        command::: $ansible all -m ping

7. If all the 'pongs' are received, from the project directory run the site.yml ansible script using the following command:
		
		command::: $ansible-playbook -i inventory.txt site.yml

The above command will install pip and mrjob on all the nodes and also copy the python files needed for hadoop and spark execution.


8. Move the following files into the big-data-stack directory (N/u/$USER/sw-project-template/src/big-data-stack):
		-  Movie-Similarities-1m.py
		-  MovieSimilaritiesLarge.py
		-  site.yml
		-  hadoop.yml
		-  spark-hdfs.yml
	

		
9. Now, run the hadoop.yml file from the project directory which will run the python file on the remote name node and fetch the results back to the control node:
			
		command::: $ansible-playbook -i inventory.txt hadoop.yml
		
10. Use 
		
		command::: $nano  results/master0/home/hadoop/new_hadoop_output.txt
		
to view the results of running the movie recommendation system python code on the 10 million ratings dataset.

11. Run the spark-hdfs.yml ansible script to copy the necessary data into hdfs for spark execution to proceed.
		
		command::: $ansible-playbook -i inventory.txt spark-hdfs.yml
		
12. Now, log into the frontendnode as per the inventory.txt file and run the following commands:

		command::: $sudo su - hadoop
		
		command::: $spark-submit --master yarn --deploy-mode client --executor-memory 3g Movie-Similarities-1m.py 260 > spark_output.txt
		
The above commands will assume hadoop user privileges and run the python file using spark to get the results of movie recommendations for a particular movie : 260 on the 10 million ratings dataset.

13. Now check the 'spark_output.txt' file for the recommendations for the given movie 260.


NOTES:
1. If the hadoop.yml file does not run as expected, kindly set the $JAVA_HOME path in /opt/hadoop/etc/hadoop/hadoop-env.sh to /usr/lib/jvm/java-7-openjdk-amd64 manually. Also, due to configuration issues of ansible with spark, the python file has to be run by logging into the front end node for spark execution.

2. There are no problems with hadoop execution and it will run through ansible itself and fetch the results back to the control node as well. The hadoop execution results can be found at: results/master0/home/hadoop

3. A directory 'test' has been included in the src directory containing the scripts to run the project on smaller datasets for faster results.

------------------------------------------------------------------------------------------------------------------


MANUAL COMMANDS TO RUN THE PROJECT INCASE THE SITE.YML FILE DOES NOT RUN:

The following steps have to be run after performing steps till STEP NO:6 from the above instruction manual:

1. To install hadoop on all the nodes,

		command::: $ansible-playbook -i inventory.txt play-hadoop.yml

2. To install spark, 

		command::: $ansible-playbook -i inventory.txt play-alladdons.yml

3. To transfer the python files to the frontendnode for execution,

		command::: $scp MovieSimilaritiesLarge.py hadoop@<front-end-node-ip>:MovieSimialaritiesLarge.py

		command::: $scp Movie-Similarities-1m.py hadoop@@<front-end-node-ip>:Movie-Similarities-1m.py

4. On all the nodes as root, 
		
		command::: $sudo su -
		
		command::: $sudo apt-get install python-pip

5. On all the nodes as root, 	
		command::: $pip install mrjob

6. On all nodes as root set $JAVA_HOME in /opt/hadoop/etc/hadoop/hadoop-env.sh to /usr/lib/jvm/java-7-openjdk-amd64.

7. Download the 10 million ratings dataset and unzip it,

		command::: $sudo su - hadoop
		
		command::: $wget http://files.grouplens.org/datasets/movielens/ml-10m.zip

		command::: $unzip ml-10m.zip

8. Run the following command to run the python for hadoop execution:

		command::: $python MovieSimilaritiesLarge.py -r hadoop --items=ml-10M100K/movies.dat ml-10M100K		/ratings.dat --no-conf --hadoop-bin /opt/hadoop/bin/hadoop > hadoop_output.txt

9. Copy the data into hdfs for spark execution:

		command::: $/opt/hadoop/bin/hdfs dfs -put ml-10M100K/ratings.dat hdfs://futuresystems/ratings.dat

10. Run the following command for spark execution:

		command::: $spark-submit --master yarn --deploy-mode client --executor-memory 3g Movie-Similarities-1m.py 260 > spark_output.txt

11. Check the hadoop output in the hadoop_output.txt file and spark output in the spark_output.txt file.

