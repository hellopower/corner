.. _index_not_find_problem:

Hive出现Index not found for分析[未完]
=========================================================

报错场
^^^^^^^^^^^^^^^^^^^^^

先看错误日志::

  Total jobs = 4
  Launching Job 1 out of 4
  Launching Job 2 out of 4
  Number of reduce tasks not specified. Estimated from input data size: 7
  In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
  In order to limit the maximum number of reducers:
  set hive.exec.reducers.max=<number>
  In order to set a constant number of reducers:
  set mapreduce.job.reduces=<number>
  Number of reduce tasks not specified. Estimated from input data size: 473
  In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
  In order to limit the maximum number of reducers:厅
  set hive.exec.reducers.max=<number>
  In order to set a constant number of reducers:
  set mapreduce.job.reduces=<number>
  java.io.IOException: Index not found for hdfs://ns1/user/dd_edw/gdm.db/gdm_m03_item_sku_da/dt=2016-11-16/000829_0.lzo
  at com.hadoop.mapred.DeprecatedLzoTextInputFormat.getSplits(DeprecatedLzoTextInputFormat.java:137)
  at org.apache.hadoop.hive.ql.io.HiveInputFormat.addSplitsForGroup(HiveInputFormat.java:305)
  at org.apache.hadoop.hive.ql.io.HiveInputFormat.getSplits(HiveInputFormat.java:407)
  at org.apache.hadoop.hive.ql.io.CombineHiveInputFormat.getCombineSplits(CombineHiveInputFormat.java:408)
  at org.apache.hadoop.hive.ql.io.CombineHiveInputFormat.getSplits(CombineHiveInputFormat.java:571)
  at org.apache.hadoop.mapreduce.JobSubmitter.writeOldSplits(JobSubmitter.java:363)
  at org.apache.hadoop.mapreduce.JobSubmitter.writeSplits(JobSubmitter.java:355)
  at org.apache.hadoop.mapreduce.JobSubmitter.submitJobInternal(JobSubmitter.java:231)
  at org.apache.hadoop.mapreduce.Job$10.run(Job.java:1290)
  at org.apache.hadoop.mapreduce.Job$10.run(Job.java:1287)
  at java.security.AccessController.doPrivileged(Native Method)
  at javax.security.auth.Subject.doAs(Subject.java:415)
  at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1657)
  at org.apache.hadoop.mapreduce.Job.submit(Job.java:1287)
  at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:575)
  at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:570)
  at java.security.AccessController.doPrivileged(Native Method)
  at javax.security.auth.Subject.doAs(Subject.java:415)
  at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1657)
  at org.apache.hadoop.mapred.JobClient.submitJobInternal(JobClient.java:570)
  at org.apache.hadoop.mapred.JobClient.submitJob(JobClient.java:561)
  at org.apache.hadoop.hive.ql.exec.mr.ExecDriver.execute(ExecDriver.java:435)
  at org.apache.hadoop.hive.ql.exec.mr.MapRedTask.execute(MapRedTask.java:137)
  at org.apache.hadoop.hive.ql.exec.Task.executeTask(Task.java:160)
  at org.apache.hadoop.hive.ql.exec.TaskRunner.runSequential(TaskRunner.java:89)
  at org.apache.hadoop.hive.ql.exec.TaskRunner.run(TaskRunner.java:75)
  Job Submission failed with exception 'java.io.IOException(Index not found for hdfs://ns1/user/dd_edw/gdm.db/gdm_m03_item_sku_da/dt=2016-11-16/000829_0.lzo)'
  Starting Job = job_1475151627062_1233540, Tracking URL = http://rm:50320/proxy/application_1475151627062_1233540/
  Kill Command = /software/servers/hadoop-2.7.1/bin/hadoop job  -kill job_1475151627062_1233540
  FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.mr.MapRedTask
  Hadoop job information for Stage-1: number of mappers: 0; number of reducers: 0
  killing job with: job_1475151627062_1233540

问题可能原因
------------------

