## Hadoop 2.7.3 pseudo distributed mode and Jupyter Notebook with CentOS 6

### Build image
```
docker build -t hadoop:2.7.3 .

docker run --rm --name Hadoop -h hadoop \
	-p 8088:8088 \
	-p 8888:8888 \
	-ti hadoop:2.7.3 bash
```

### Hadoop Browser
```
http://localhost:8088
```

### Notebook access
```
jupyter notebook --ip='0.0.0.0' --no-browser

http://localhost:8888
```

## Testing..

### Create a Directory
```
hdfs dfs -mkdir /bigdata
```

### List diretory
```
hadoop fs -ls /
```

### Download a file csv
```
wget -c http://compras.dados.gov.br/contratos/v1/contratos.csv
```

### Copy file to the HDFS directory created above
```
hadoop fs -copyFromLocal contratos.csv /bigdata
```

### Read file
```
hadoop fs -cat /bigdata/contratos.csv
```
### Test word count with mapreduce
```
hadoop jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /bigdata/contratos.csv /output
```

### Read result
```
hdfs dfs -cat /output/*
```