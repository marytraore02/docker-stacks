
Connect to one of worker node and run :
#Main
spark-submit --deploy-mode client --master spark://spark-master:7077 --total-executor-cores 1 --driver-memory 1G --executor-memory 1G --class com.bigdata.main /apps/spark-lesson2_2.12-0.1.jar
