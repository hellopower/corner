.. _lzotble_read_text:

lzo的表读取text数据问题
=================================

描述  
--------------------

在Hive中创建一个表，指定格式为DeprecatedLzoTextInputFormat,但在表的Location下保存的是text文件，当使用::

  select * from lzo_table 

以上SQL查询结果不空。

使用::

  select count(1) from lz_table

以上SQL结果不为空。

原因
-----------

* select * from lzo_table

在这种情况下，hive不会提交mapredce任务，而是直接走fetchTask把数据直接读出,用的是DeprecatedLzoTextInputFormat,而DeprecatedLzoTextInputFormat会对非lzo的文件进行过滤，通过参数set lzo.text.input.format.ignore.nonlzo=true控制

::

    boolean ignoreNonLzo = LzoInputFormatCommon.getIgnoreNonLzoProperty(conf);

    Iterator<FileStatus> it = files.iterator();
    while (it.hasNext()) {
      FileStatus fileStatus = it.next();
      Path file = fileStatus.getPath();

      if (!LzoInputFormatCommon.isLzoFile(file.toString())) {
        // Get rid of non-LZO files, unless the conf explicitly tells us to
        // keep them.
        // However, always skip over files that end with ".lzo.index", since
        // they are not part of the input.
        if (ignoreNonLzo || LzoInputFormatCommon.isLzoIndexFile(file.toString())) {
          it.remove();
        }
      }

* select count(1) from lz_table

Hive生成MapReduce，这个时候hive使用的是org.apache.hadoop.hive.ql.io.CombineHiveInputFormat没有对非lzo的文件进行过滤，所以可以正常查询数据。
