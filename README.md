# Big-data
various concepts and codes related to Big data

#Mapreduce in Hadoop

Mapper Code:
public static class Map extends Mapper<LongWritable,Text,Text,IntWritable>
public void map(LongWritable key,Text value,Context context) throws IOException,InterruptedException{

String line=value.ToString();
String Tokenizer tokenizer=new StringTokenizer(line);
while(tokenizer.hasMoreTokens()){
value.set(tokenizer.nextToken());
context.write(value,new Intwritable(1));
}

Reducer Code:
public static class Reduce extends Reducer<Text,Intwritable,Text,Intwritable>
{
public static void reduce(Text key,Iterable<Intwritable> values,Context context) throws IOException,InterruptedException{

int sum=0;
for(IntWritable x:values)
{
sum+=x.get();
}
context.write(key,new Intwritable(sum));
}
}

Driver Code:
Configuration conf=new Configuration();
Job job=new Job(conf,"Word count program");
job.setJarByClass(WordCount.class);
job.setMapperClass(Map.class);
job.setReducerClass(Reduce.class);
job.setOutputKeyClass(Text.class);

job.setOutputValueClass(IntWritable.class);
job.setInputFormatClass(TextInputFormat.class);
job.setOutputFormatClass(TextOutputFormat.class);
path outputPath=new Path(args[1]);

//setting up configuration for input and output path
FileInputFormat.addInputPath(job,new Path(args[0]));
FileOutputFormat.setOutputPath(job,new Path(args[1]);
