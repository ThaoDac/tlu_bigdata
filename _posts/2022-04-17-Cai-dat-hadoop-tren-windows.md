---
layout: post
title: Hướng dẫn cài đặt Hadoop 3.3.0 trên Windows
categories: hadoop
---

## Cài đặt JDK bản 1.8 (bắt buộc)
### Bước 1: Tải bộ cài
- Link: [https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html). Chọn phiên bản dành cho **Windows x64**.

![Tải bộ cài JDK 8](../../../../assets/images/bo-cai-jdk-8.png)

- Tick vào checkbox và bấm nút **Download**

![Tải bộ cài JDK 8](../../../../assets/images/accept-download-jdk.png)

- Cần thực hiện đăng nhập tài khoản trước khi tải xuống, nếu chưa có tài khoản bấm nút **Create Account** để tạo. Sau khi đăng nhập thành công, bộ cài sẽ tự động được tải xuống.

![Tải bộ cài JDK 8](../../../../assets/images/login-oracle.png)

## Bước 2: Cài đặt

- Double click vào file cài đặt vừa tải xuống.

![Cài đặt JDK 8](../../../../assets/images/double-click-jdk.png)

- Bấm **Next**

![Cài đặt JDK 8](../../../../assets/images/next-jdk.png)

- Bấm **Change** để thay đổi đường dẫn lưu.

![Cài đặt JDK 8](../../../../assets/images/next-jdk2.png)

- Chọn thư mục để lưu JDK. ***Lưu ý: đường dẫn không có dấu và không có khoảng trắng.***

![Cài đặt JDK 8](../../../../assets/images/change-path-jdk2.png)

- Tiếp tục bấm **Next**.

![Cài đặt JDK 8](../../../../assets/images/next-jdk2.png)
![Cài đặt JDK 8](../../../../assets/images/jdk-progress.png)

- Bấm **OK**.

![Cài đặt JDK 8](../../../../assets/images/jdk-ok.png)

- Bấm **Next**.

![Cài đặt JDK 8](../../../../assets/images/next-jdk3.png)
![Cài đặt JDK 8](../../../../assets/images/jdk-progress2.png)

- Hoàn tất cài đặt JDK 1.8, bấm **Cancel** để thoát.

![Cài đặt JDK 8](../../../../assets/images/jdk-finish.png)

## Bước 3: Thiết lập biến môi trường JDK

- Search từ khóa **environment** ở thanh Taskbar, chọn mục **Edit environment variables for your account**.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-search.png)

- Bấm **Environment Variables...**.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-env-var.png)

- Bấm **New**.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-new1.png)

- Nhập **Variable Name: JAVA_HOME** và **Variable Value** là đường dẫn lưu folder JDK **C:\Java\jdk1.8.0_202**

![Cài đặt JDK 8](../../../../assets/images/env-jdk-new-popup.png)

- Tiếp tục làm tương tự với **System Variables**.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-new2.png)
![Cài đặt JDK 8](../../../../assets/images/env-jdk-new-popup2.png)

- Chọn **Path** và bấm **Edit** của phần **User Variables**

![Cài đặt JDK 8](../../../../assets/images/env-jdk-path.png)

- Bấm **New** và nhập **%JAVA_HOME%\bin**

![Cài đặt JDK 8](../../../../assets/images/env-jdk-new-path-java.png)

- Làm tương tự với **System Variables**.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-path2.png)
![Cài đặt JDK 8](../../../../assets/images/env-jdk-new-path-java2.png)

- Vào **cmd** gõ **java -version**, nếu kết quả trả về như ảnh thì quá trình thiết lập môi trường thành công.

![Cài đặt JDK 8](../../../../assets/images/env-jdk-check.png)

## Cài đặt Hadoop
### Bước 1: Tải Hadoop 3.3.0

- Truy cập link [https://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz](https://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz) file nén Hadoop 3.3.0 sẽ tự động được tải xuống

- Bấm chuột phải vào file **hadoop-3.3.0.taz.gz** và bấm **Extract files...**

![Cài đặt JDK 8](../../../../assets/images/hadoop-extract.png)

- Chọn ổ **C** và bấm **OK**

![Cài đặt JDK 8](../../../../assets/images/hadoop-C.png)

- Mở ổ **C** sẽ thấy thư mục **hadoop-3.3.0**

![Cài đặt JDK 8](../../../../assets/images/hadoop-C2.png)

### Bước 2: Thiết lập biến môi trường cho Hadoop

- Làm tương tự thiết lập biến môi trường cho JDK. Với **Variable Name: HADOOP_HOME** và **Variable Value** là đường dẫn lưu folder Hadoop **C:\hadoop-3.3.0**

![Cài đặt JDK 8](../../../../assets/images/hadoop-env.png)

- Thêm 2 giá trị **%HADOOP_HOME%\bin** và **%HADOOP_HOME%\sbin** vào biến **Path** của phần **User Variables**

![Cài đặt JDK 8](../../../../assets/images/env-jdk-path.png)
![Cài đặt JDK 8](../../../../assets/images/hadoop-path.png)

- Tương tự thêm vào biến **Path** của phần **System Variables**

![Cài đặt JDK 8](../../../../assets/images/env-jdk-path2.png)
![Cài đặt JDK 8](../../../../assets/images/hadoop-path.png)

- Vào **cmd** gõ **hadoop version**, nếu kết quả trả về như ảnh thì quá trình thiết lập môi trường thành công.

![Cài đặt JDK 8](../../../../assets/images/hadoop-check.png)

### Bước 3: Cấu hình các tập tin cho Hadoop

- Truy cập thư mục **C:\hadoop-3.3.0\etc\hadoop**

- Cấu hình core-site.xml như dưới đây:

```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>
```

- Cấu hình mapred-site.xml như dưới đây:

```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>
```

- Tạo thư mục **data** trong **C:\hadoop-3.3.0**

- Tạo thư mục con **datanode** trong **C:\hadoop-3.3.0\data**

- Tạo thư mục con **namenode** trong **C:\hadoop-3.3.0\data**

- Sau đó cấu hình hdfs-site.xml như sau:

```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>/hadoop-3.3.0/data/namenode</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/hadoop-3.3.0/data/datanode</value>
  </property>
</configuration>
```

- Cấu hình yarn-site.xml như dưới đây:

```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
</configuration>
```

- Tải [apache-hadoop-winutils](../../../../assets/files/winutils.zip)

- Giải nén sẽ thấy thư mục **bin** bên trong. Chép đè thư mục bin này vào thư mục **C:\hadoop-3.3.0\bin**

![Cài đặt Hadoop](../../../../assets/images/hadoop-extract-winutils.png)

- Sau đó format lại namenode và datanode, mở command line lên, gõ 2 lệnh sau (Bước format này chỉ cần làm 1 lần):

```
hdfs namenode –format
```

```
hdfs datanode -format
```

- Tiếp theo sao chép file: **C:\hadoop-3.3.0\share\hadoop\yarn\timelineservice\ hadoop-yarn-servertimelineservice-3.3.0.jar** vào **C:\hadoop-3.3.0\share\hadoop\yarn\hadoop-yarn-server-timelineservice-3.3.0.jar**

- Quá trình cài đặt Hadoop đã hoàn tất, để chạy Hadoop di chuyển tới thư mục **C:\hadoop-3.3.0\sbin**. Gõ lệnh:

```
start-all
```

- 4 ứng dụng sẽ được chạy và phải đảm bảo các ứng dụng không bị kết thúc:

![Cài đặt JDK 8](../../../../assets/images/hadoop-cmd-check.png)

>NOTE: Trường hợp bị lỗi hãy chạy lên trên cmd bằng quyền Administrator

- Yarn web page: **http://localhost:8088/**
![Cài đặt JDK 8](../../../../assets/images/hadoop-8088.png)

- Name node web page: **http://localhost:9870/**
![Cài đặt JDK 8](../../../../assets/images/hadoop-9879.png)

- Data node web page: **http://localhost:9864/**
![Cài đặt JDK 8](../../../../assets/images/hadoop-9884.png)