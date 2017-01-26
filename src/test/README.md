
----------------------------------------------------------------------------------------------------------------
This directory consists of scripts to run the movie recommendation system on smaller datasets for faster results.
----------------------------------------------------------------------------------------------------------------

INSTRUCTIONS TO RUN THE SCRIPTS IN TEST DIRECTORY:

1. Follow all the steps till STEP 6 from the installation.rst manual.

STEP 7:     command::: $ansible-playbook -i inventory.txt site.yml

STEP 8:     command::: $ansible-playbook -i inventory.txt hadoop.yml

STEP 9: Log into the frontendnode and run the command in the file 'Command to run spark'.

STEP 10: The hadoop output can be found in hadoop_output.txt on the control node and the spark output can be found in 
the spark_output.txt file on the frontendnode.
