***Hands-on #4: MapReduce : Movie Script Analysis***
Setup and Execution
*1. Start the Hadoop Cluster*
Run the following command to start the Hadoop cluster:
**docker compose up -d**
*2. Build the Code*
Build the code using Maven:
**mvn install**
*3. Move JAR File to Shared Folder*
Move the generated JAR file to a shared folder for easy access:
**mv target/*.jar input/**
*4. Copy JAR to Docker Container*
Copy the JAR file to the Hadoop ResourceManager container:
**docker cp input/codehands-on2-movie-script-analysis-1.0-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/**
*5. Move Dataset to Docker Container*
Copy the dataset to the Hadoop ResourceManager container:
**docker cp input/data/movie_dialogues.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/**
*6. Connect to Docker Container*
Access the Hadoop ResourceManager container:
**docker exec -it resourcemanager /bin/bash**
Navigate to the Hadoop directory:
**cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/**
*7. Set Up HDFS*
Create a folder in HDFS for the input dataset:
**hadoop fs -mkdir -p /input/dataset**
Copy the input dataset to the HDFS folder:
**hadoop fs -put ./movie_dialogues.txt /input/dataset**
*8. Execute the MapReduce Job*
Run your MapReduce job using the following command:
**hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreducehands-on2-movie-script-analysis-1.0-SNAPSHOT.jar com.example.controller.Controller /input/dataset/movie_dialogues.txt /output**
*9. View the Output*
To view the output of your MapReduce job, use:
**hadoop fs -cat /output/***
**hadoop fs -cat /output/task1/***
**hadoop fs -cat /output/task2/***
**Hadoop fs -cat /output/task3/***
*10. Copy Output from HDFS to Local OS*
To copy the output from HDFS to your local machine:
*1.	Use the following command to copy from HDFS:*
**hdfs dfs -get /output /opt/hadoop-3.2.1/share/hadoop/mapreduce/**
*2.	use Docker to copy from the container to your local machine:*
**exit**
*3.	Commit and push to your repo so that we can able to see your output*
**docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output/ output/**


