# Linux capabilities 

(``man capabilities``)<br/>

Mysql
---
The process mysqld does not seem to need any linux capabilities. The entrypoint, on the other hand, does, because, among other things, it downgrades to the mysql user, and for that it uses the SETUID and SETGID capabilities.

The only reason DAC_READ_SEARCH is added is to allow the entrypoint to search under /var/lib/mysql, so that it does not error out, but it does not allow it to make any actual changes.

The entrypoint tries to change the owner of all the folders and files recursively to mysql:
https://github.com/docker-library/mariadb/blob/master/10.5/docker-entrypoint.sh#L146

Without the CHOWN capability, this is going to return an error anyway if any of the files are not already owned by mysql. So in order to avoid having to grant additional capabilities, the permissions need to be set beforehand in case the database is imported/copied from somewhere else.

Nextcloud Application
---
Because Nextcloud runs an rsync the first time and changes the owner of files, it needs additional capabilities, such as DAC_OVERRIDE, CHOWN, besides SETGID and SETUID:<br/>
https://github.com/nextcloud/docker/blob/master/18.0/apache/entrypoint.sh#L100-L106
