# WordCount example application 
##### This example uses the [CDH-5 Docker image](https://registry.hub.docker.com/u/chalimartines/cdh5-pseudo-distributed/) contributed by [chalimartines](https://hub.docker.com/u/chalimartines/):

## **Pre-requisites**:

#### **Install docker**: 
[Docker Installation](https://docs.docker.com/installation/)

#### **Download modified(double count "cloudera") WordCount**: 
[WordCount.Java](https://github.com/ksriraman/cdh5-wc-docker/blob/master/root/WordCount.java)

## **Execution**:

#### **Pull Docker image**:
```docker pull karthicks/cdh5-docker```

### **Run image in background and mount wordCount.java**:
```docker run -i -t -v /root/WordCount.java:/root/WordCount.java --name cdh_wc7 -d -p 9020:9020 -p 60070:60070 -p 60010:60010 -p 60020:60020 -p 60075:60075 -p 9030:9030 -p 9031:9031 -p 9032:9032 -p 9033:9033 -p 9088:9088 -p 9040:9040 -p 9042:9042 -p 10021:10021 -p 19889:19889 -p 11001:11001 karthicks/cdh5-docker:v2```

#### **Enter docker bash shell (Replace CONTAINERID from above output)**:
```docker exec -i -t CONTAINERID bash -l```

#### **Run WordCount application**:
```hadoop jar word_count.jar org.myorg.WordCount /user/cloudera/wordcount/input /user/cloudera/wordcount/output```

#### **If needed, recompile the WordCount class**:
```mkdir -p build
 	javac -cp /usr/lib/hadoop/*:/usr/lib/hadoop-mapreduce/* WordCount.java -d build -Xlint```
 
#### **If needed, recreate JAR**:
```jar -cvf word_count.jar -C build/ .```
