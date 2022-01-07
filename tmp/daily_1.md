+ TODO: 记录安装postgresql时的错误  <09-12-21, Redari-Es> +

在我配置psql时，出现了一个动态连接库文件的错误，其结果导致了我的sudo无法使用，
最后是根据live里的系统的动态库更改过来的
导致的原因可能是更新导致，旧连接被覆盖掉了
libldap
libldbr

