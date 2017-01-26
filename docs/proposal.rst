Project Proposal (In Progress)
===============================================================================

Implementation of Movie Recommendation System Using Hadoop and Spark
-------------------------------------------------------------------------------

We plan to implement a movie recommendation system on both Hadoop and Spark, and compare the results. Spark is a comparitively newer technology to Hadoop and in most cases has been observed to yield better and faster results (upto 100 times). We plan to test this on our project.

Our project manily aims at building a movie recommendation system on movielens [10 Million dataset] (http://grouplens.org/datasets/movielens/) using collaborative filtering and data mining algorithms.

Criteria for Model Evaluation
-------------------------------------------------------------------------------

For each user i and each movie j they have not seen, we find k most similar users who have seen j and then use them to infer user i's rating on movie j. If we cannot find k users for some movie j, then we take all users who have seen it. We test the performance on our system using cross validation.

Team
-------------------------------------------------------------------------------

  * Rishikesh Pandey, ripandey, ripandey, ripandey (Lead)
  * Krishna Mahajan, krimahaj, krimahaj, krish
  * Ramprasad Bommaganty, rbommaga, rbommaga, rbommaga

Role
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Deployment: Ramprasad Bommaganty
* Configuration: Rishikesh Pandey
* Database: Krishna Mahajan
* Map/Reduce Functions: Rishikesh Pandey
* Algorithm: Krishna Mahajan
* Plot: Ramprasad Bommaganty

Artifacts
-------------------------------------------------------------------------------

* Put here a list of artifacts that you will create (this can be 
  filled out at a later time)

List of Technologies
-------------------------------------------------------------------------------

Development Languages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Python
* Java

Software Tools
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Ansible
* Hadoop
* Spark

Compute Resources
-------------------------------------------------------------------------------

* OpenStack in FutureSystems
* Amazon AWS

System Requirements
-------------------------------------------------------------------------------

* Size: 10 VM instances
* OS: Ubuntu 14.04 LTS
* Storage: 500GB

List of DataSets
-------------------------------------------------------------------------------

* [10 Million dataset] (http://grouplens.org/datasets/movielens/)

Schedule
-------------------------------------------------------------------------------

* Week 1: Initial Meeting
* Week 2: Proposal
* Week 3: Discussion
* Week 4: Presentation
* Week 5: Refine raw dataset
* Week 6: Build systems
* Week 7: Develop modules, test run
* Week 8: Final Report, Review, Submission

Project Style and Type
-------------------------------------------------------------------------------

* Bonus
* Analytics

Acknowledgement
-------------------------------------------------------------------------------

This project idea is obtained from the following sources:

* This project idea is based on assignment 1 problem 5 of Prof. Predrag Data Mining class where it was concluded that high   performance computing resources are needed to build a recommendation engine for 10M dataset.  
cs.indiana.edu/~predrag/classes/2016springb565/hw1.pdf
