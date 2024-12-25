# 文件读取
```python
from pyspark.sql import SparkSession

# 初始化SparkSession
spark = SparkSession.builder \
.appName("ReadTextFromS3") \
.config("spark.hadoop.fs.s3a.access.key", "your-access-key") \
.config("spark.hadoop.fs.s3a.secret.key", "your-secret-key") \
.config("spark.hadoop.fs.s3a.endpoint", "s3.amazonaws.com") \
.getOrCreate()

# S3文件路径
s3_file_path = "s3a://your-bucket-name/path/to/your/file.txt"

# 读取S3上的文本文件
text_rdd = spark.sparkContext.textFile(s3_file_path)

# 将RDD转换为一个普通的Python列表，并返回文本内容
text_content = text_rdd.collect()

# 打印结果
for line in text_content:
    print(line)

# 如果需要返回文本字符串
full_text = "\n".join(text_content)
print(full_text)

# 关闭Spark会话
spark.stop()

```

