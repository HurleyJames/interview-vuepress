# SQL约束

* 空值约束`not null`：用于控制字段内容一定不为空
* 唯一约束`unique`：控制字段不能重复，一个表中可以多个`unique`约束
* 主键约束`primary key`：用于控制字段内容不能重复，但是每个表中只能出现一个
* 外键约束`foreign key`：用于与另一张表相关联，是能确认另一张表记录的字段，用于保持数据的一致性
* 检查约束`check`：用于控制字段的值范围
* 默认值约束`default`：用于向列中插入默认值。如果没有规定其它的值，那么会将默认值添加到所有的新纪录