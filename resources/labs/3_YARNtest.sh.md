#!/bin/sh
# Confirm the path values given below correspond to your installation

HADOOP_MR=/opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce
HADOOP_PATH=/opt/cloudera/parcels/CDH/bin

# Mark start of the loop
echo Testing loop started on `date`

# Mapper containers
for i in 3 6 9    
do
   # Reducer containers
   for j in 3 6 9 
   do                 
      # Container memory
      for k in 512 1024 1536
      do                         
        # Set mapper JVM heap 
        MAP_MB=`echo "($k*0.8)/1" | bc` 

        # Set reducer JVM heap 
        RED_MB=`echo "($k*0.8)/1" | bc` 

        echo "MAP_MB=$MAP_MB"
        echo "RED_MB=$RED_MB"
        echo "Mappers=$i"
        echo "Reducers=$j"
        echo "Container Memory=$k"

        echo "Running teragen"
        time $HADOOP_PATH/hadoop jar $HADOOP_MR/hadoop-examples.jar teragen \
                     -Dmapreduce.job.maps=$i \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     100000 /home/patelliandrea/results/tg-10GB-${i}-${j}-${k} 1>tera_${i}_${j}_${k}.out 2>tera_${i}_${j}_${k}.err                       

        echo "Running terasort"
        time $HADOOP_PATH/hadoop jar $HADOOP_MR/hadoop-examples.jar terasort \
                     -Dmapreduce.job.maps=$i \
                     -Dmapreduce.job.reduces=$j \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     -Dmapreduce.reduce.memory.mb=$k \
                     -Dmapreduce.reduce.java.opts.max.heap=$RED_MB \
	                   /home/patelliandrea/results/tg-10GB-${i}-${j}-${k}  \
                     /home/patelliandrea/results/ts-10GB-${i}-${j}-${k} 1>>tera_${i}_${j}_${k}.out 2>>tera_${i}_${j}_${k}.err                         

        $HADOOP_PATH/hadoop fs -rm -r -skipTrash /home/patelliandrea/results/tg-10GB-${i}-${j}-${k}                         
        $HADOOP_PATH/hadoop fs -rm -r -skipTrash /home/patelliandrea/results/ts-10GB-${i}-${j}-${k}                 
      done
   done
done

echo Testing loop ended on `date`
