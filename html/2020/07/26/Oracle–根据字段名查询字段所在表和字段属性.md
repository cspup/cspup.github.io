# Oracle–根据字段名查询字段所在表和字段属性
```SQL
--根据字段名查找对应的表和注释
select concat(concat(a.owner, '.'), a.table_name) 表名,
       a.column_name 字段名,
       a.data_type 字段类型,
       a.data_length 字段长度,
       b.comments 字段描述
  from dba_tab_columns a, dba_col_comments b
 where a.OWNER = b.owner
   and a.TABLE_NAME = b.table_name
   and a.COLUMN_NAME = b.column_name
   and b.column_name like upper('字段名');
```