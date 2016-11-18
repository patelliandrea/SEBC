## Grant `scm` only from CM node
```
grant all on scm.* TO 'cloudera-scm'@'ip-172-30-2-4.eu-central-1.compute.internal' IDENTIFIED BY 'cloudera-scm';
```