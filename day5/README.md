### Revision 

### rev 1 

<img src="rev.png">

### Revision 2 

<img src="rev2.png">

### Revision 3 

<img src="rev3.png">

### spark streaming getting started 

<img src="stream.png">

###  spark stream using python --/ pyspark for word count 

### code 

```
from pyspark import SparkContext
from pyspark.streaming import StreamingContext
# creating spark context 
sc=SparkContext("local[2]","ashu-network-data-wc")
# creating socket stream to recv data in batch interval of 2 seconds 
stream_sc=StreamingContext(sc,10) 
# use stream socket to connect target -- (hostname:port) --/localhost port
my_dataline=stream_sc.socketTextStream("localhost",9876)
# above my_dataline -- is a Dstream -- sequence of rdd 
ashu_word=my_dataline.flatMap(lambda ashu_data: ashu_data.split(" "))
# print it 
ashu_mapper=ashu_word.map(lambda ashumap: (ashumap,1))
# reducing for counting each word
ashu_wc=ashu_mapper.reduceByKey(lambda ashuk,ashuv: ashuk+ashuv)
# printing by collect / pprint 
ashu_wc.pprint()

## start listener socket 
stream_sc.start() # start compute socket 
stream_sc.awaitTermination() # wait for the computation 


```

### to test open two terminal 

### terminal 1 create socket tcp 

```
ubuntu@ip-172-31-1-160:~/ashu-project$ nc -lk 9876 
hey hello hey hii ashu hello



```

### terminal 2 

```
ubuntu@ip-172-31-1-160:~/ashu-project$ spark-submit  spark_live_wordcount.py     localhost 9876 

=====
Time: 2023-03-17 07:12:30
-------------------------------------------
('hii', 1)
('hey', 2)
('hello', 2)
('ashu', 1)

```

### setting logging level in spark context 

```
from pyspark import SparkContext
from pyspark.streaming import StreamingContext
import logging
# creating spark context 
sc=SparkContext("local[*]","ashu-network-data-wc")
# setting logging options 
sc.setLogLevel("ERROR")
logging.getLogger("py4j").setLevel(logging.ERROR)
# creating socket stream to recv data in batch interval of 2 seconds 
stream_sc=StreamingContext(sc,10) 
# use stream socket to connect target -- (hostname:port) --/localhost port
my_dataline=stream_sc.socketTextStream("localhost",9876)
# above my_dataline -- is a Dstream -- sequence of rdd 
ashu_word=my_dataline.flatMap(lambda ashu_data: ashu_data.split(" "))
# print it 
ashu_mapper=ashu_word.map(lambda ashumap: (ashumap,1))
# reducing for counting each word
ashu_wc=ashu_mapper.reduceByKey(lambda ashuk,ashuv: ashuk+ashuv)
# printing by collect / pprint 
ashu_wc.pprint()

## start listener socket 
stream_sc.start() # start compute socket 
stream_sc.awaitTermination() # wait for the computation 

```

## SQL in Bigdata 

<img src="sqlb.png">

### Spark sql 

<img src="sqlb1.png">

### Hive vs spark SQL 

<img src="sphive.png">

### getting more info about spark sql data sources 

<img src="sql1.png">

### spark sql more info 

<img src="sql2.png">

### getting started with spark sql 

### Spark sql code in python 

```
#from pyspark import SparkContext
#from pyspark.streaming import StreamingContext
from pyspark.sql import SparkSession
import time 
# creating session using spar sql layer 
spark_sql1=SparkSession.builder.appName("ashu_spark_sql-example").config("some_spark_config_option","some-value").getOrCreate()
# we can load various data set of diff types like csv,json,text,xml etc
ashu_df=spark_sql1.read.json("dataset/emp.json")
# above ashu_df is a data frame and now that df is having sql like capabilities 
# to print 
#print(ashu_df.show())
# print schema of data frame 
print(ashu_df.printSchema())
# selecting particular column 
name_only=ashu_df.select("name").show()
x1=ashu_df.select(ashu_df["name"],ashu_df['email']).show()
print(x1)
time.sleep(3)
# filter ops
y1=ashu_df.filter(ashu_df['age'] > 27).show()
print(y1)
# count people by their age 
z1=ashu_df.groupby("age").count().show()
time.sleep(2)
print(z1)
# actually write SQL like query not in df condition 
# we can create temperary SQL image of df 
time.sleep(5)
ashu_df.createOrReplaceTempView("oracle")
# using sql spark session we can run queiry like sql 
final_output=spark_sql1.sql("select * from oracle")
print(final_output.show())
```

### to run we can use python / spark-submit both 



