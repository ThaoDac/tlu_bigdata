---
layout: post
title: MapReduce - Lập trình chương trình WordCount
categories: hadoop
---

## I. Thử nghiêm với hàm mẫu WordCount của Hadoop

Trong thư mục **C:\hadoop-3.3.0\share\hadoop\mapreduce** Hadoop đã có sẵn chương trình MapReduce **hadoop-mapreduce-examples-3.3.0.jar**. Ta sẽ thử nghiệm bài toán đếm từ bằng cách tạo ra file text chứa dữ liệu và đầu ra mong muốn là các cặp **[từ: số lượng xuất hiện]**

### Bước 1: Tạo file data.txt

Nội dung của file data.txt là:

```
Bus Car bus
car train car
bus car train
bus TRAIN BUS
buS caR CAR
car BUS TRAIN
```

### Bước 2: Tạo thư mục input tại hdfs và lưu file data.txt

Tạo thư mục **input** trong hdfs với câu lệnh:
```
hdfs dfs -mkdir /input
```

Đẩy file **data.txt** vào folder **input** vừa tạo:
```
hdfs dfs -put "C:\input\data.txt" /input
```

>Lưu ý: Thay "C:\input\data.txt" bằng nơi lưu trữ file trong máy

Vào trang quản lý NameNode [http://localhost:9870/](http://localhost:9870/) để kiểm tra file 

![MapReduce](../../../../assets/images/browser-file-hdfs.png)

![MapReduce](../../../../assets/images/folder-input-created.png)

![MapReduce](../../../../assets/images/data-saved.png)

### Bước 3: Chạy chương trình MapReduce và xem kết quả

Chương trình mẫu MapReduce của Hadoop nằm tại **C:\hadoop-3.3.0\share\hadoop\mapreduce\hadoop-mapreduce-examples-3.3.0.jar**. Ta sẽ thử nghiệm đầu vào chương trình là file **data.txt** và kết quả sẽ được lưu tại folder **/output**, lệnh thực hiện"

```
hadoop jar "C:\hadoop-3.3.0\share\hadoop\mapreduce\hadoop-mapreduce-examples-3.3.0.jar" wordcount /input/data.txt /output
```

![MapReduce](../../../../assets/images/run-sample-mapreduce.png)

Xem kết quả thu được:

![MapReduce](../../../../assets/images/show-result-mr.png)

![MapReduce](../../../../assets/images/show-result-mr2.png)

![MapReduce](../../../../assets/images/show-result-mr3.png)

![MapReduce](../../../../assets/images/show-result-mr4.png)


Hoặc dùng lệnh cmd:

```
hdfs dfs -cat /output/part-r-00000
```

>Lưu ý: thay /output/part-r-00000 thành đường dẫn file muốn xem

![MapReduce](../../../../assets/images/show-result-mr5.png)

Như vậy ta đã chạy thành công chương trình mẫu MapReduce của Hadoop cung cấp.

## II. Lập trình chương trình WordCount bằng Eclipse
### Bước 1: Tạo project

Mở chương trình Eclipse. Chọn **workspace** (nên để mặc định)

![MapReduce](../../../../assets/images/create-wordcount-eclipse.png)

Tạo project Java, chọn **File > New > Java Project**

![MapReduce](../../../../assets/images/create-wordcount-eclipse2.png)

Đặt tên project là **WordCount** và chọn môi trường là **JavaSE-1.8**. Xong ấn **Finish**.

![MapReduce](../../../../assets/images/create-wordcount-eclipse3.png)

### Bước 2: Thêm thư viện cần thiết để chạy MapReduce

Chuột phải vào project **WordCount** chọn **Properties**

![MapReduce](../../../../assets/images/add-lib-mr.png)

Chọn **Java Build Path**, chọn tab **Libraries** và bấm **Add External JARs**

![MapReduce](../../../../assets/images/add-lib-mr2.png)

Chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\client** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr3.png)

Tương tự chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\common** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr4.png)

Chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\common\lib** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr5.png)

Chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\hdfs** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr6.png)

Chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\mapreduce** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr7.png)

Chọn tất cả file trong thư mục **C:\hadoop-3.3.0\share\hadoop\yarn** và ấn **Open**

![MapReduce](../../../../assets/images/add-lib-mr8.png)

Ấn **Apply and Close**

![MapReduce](../../../../assets/images/add-lib-mr9.png)

### Bước 3: Tạo class xử lý tác vụ MapReduce

Double click vào project **WordCount**, chuột phải vào **src** và chọn **New > Class**

![MapReduce](../../../../assets/images/create-class-mr.png)

Tạo class để xử lý nhiệm vụ **Map**, đặt tên là **WordCountMapper**

![MapReduce](../../../../assets/images/create-class-mr2.png)

Nội dung bên trong file **WordCountMapper.java**:

```java
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.io.LongWritable;

public class WordCountMapper extends Mapper <LongWritable, Text, Text, IntWritable>
{
  private Text wordToken = new Text();
  public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException
  {
    StringTokenizer tokens = new StringTokenizer(value.toString()); //Dividing String into tokens
    while (tokens.hasMoreTokens())
    {
      wordToken.set(tokens.nextToken());
      context.write(wordToken, new IntWritable(1));
    }
  }
}
```

Tương tự tạo class xử lý nhiệm vụ **Reduce**, đặt tên là **WordCountReducer**:

```java
import java.io.IOException;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Reducer;

public class WordCountReducer extends Reducer <Text, IntWritable, Text, IntWritable>
{
  private IntWritable count = new IntWritable();
  public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException
  {
    int valueSum = 0;
    for (IntWritable val : values)
    {
      valueSum += val.get();
    }
    count.set(valueSum);
    context.write(key, count);
  }
}
```

Và tạo class **WordCount** chứa hàm **main** để khởi chạy chương trình:

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount
{
  public static void main(String[] args) throws Exception
  {
    Configuration conf = new Configuration();
    String[] pathArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (pathArgs.length < 2)
    {
      System.err.println("MR Project Usage: wordcount <input-path> [...] <output-path>");
      System.exit(2);
    }
    Job wcJob = Job.getInstance(conf, "MapReduce WordCount");
    wcJob.setJarByClass(WordCount.class);
    wcJob.setMapperClass(WordCountMapper.class);
    wcJob.setCombinerClass(WordCountReducer.class);
    wcJob.setReducerClass(WordCountReducer.class);
    wcJob.setOutputKeyClass(Text.class);
    wcJob.setOutputValueClass(IntWritable.class);
    for (int i = 0; i < pathArgs.length - 1; ++i)
    {
      FileInputFormat.addInputPath(wcJob, new Path(pathArgs[i]));
    }
    FileOutputFormat.setOutputPath(wcJob, new Path(pathArgs[pathArgs.length - 1]));
    System.exit(wcJob.waitForCompletion(true) ? 0 : 1);
  }
}
```

![MapReduce](../../../../assets/images/create-class-mr3.png)

### Bước 4: Tạo file JAR

Chuột phải vào project **WordCount** chọn **Export**

![MapReduce](../../../../assets/images/build-jar-mr.png)

Chọn **Java > JAR File** rồi bấm **Next**

![MapReduce](../../../../assets/images/build-jar-mr2.png)

Chọn đường dẫn lưu file JAR và bấm **Next**

![MapReduce](../../../../assets/images/build-jar-mr3.png)

Bấm **Next**

![MapReduce](../../../../assets/images/build-jar-mr4.png)

Bấm **Browser** để chọn file **main**

![MapReduce](../../../../assets/images/build-jar-mr5.png)

Chọn **WordCount** và bấm **OK**

![MapReduce](../../../../assets/images/build-jar-mr6.png)

Bấm **Finish** để thực hiện quá trình **Export**

![MapReduce](../../../../assets/images/build-jar-mr7.png)

Vào thư mục chứa lưu file JAR vừa tạo và kiểm tra kết quả

![MapReduce](../../../../assets/images/build-jar-mr8.png)

Thử nghiệm trên file dữ liệu **data.txt** đã tạo ở trên, và kết quả thu được lưu tại thư mục **r_output**. Chạy lệnh sau:

```
hadoop jar "C:\jar\WordCount.jar" /input/data.txt /r_output
```
>Lưu ý: Thay "C:\jar\WordCount.jar" bằng đường dẫn chứa file JAR ở trên máy

![MapReduce](../../../../assets/images/run-own-mapreduce.png)

![MapReduce](../../../../assets/images/result-own-mr.png)

![MapReduce](../../../../assets/images/result-own-mr2.png)

![MapReduce](../../../../assets/images/result-own-mr3.png)
