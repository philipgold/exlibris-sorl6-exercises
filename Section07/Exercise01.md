# Exercise 01 - Managing backups
 
1. Add new `demobackup` collection

Open up the terminal and hit:

```bash
solr create -c demobackup -e techproducts
```
 
2. Run backup command:
```bash
http://localhost:8984/solr/demobackup/replication?command=backup&name=mybackup
```

3. Check current status of the backup operation
   
`http://localhost:8984/solr/demobackup/replication?command=details&wt=xml` 

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
    <lst name="responseHeader">
        <int name="status">0</int>
        <int name="QTime">1</int>
    </lst>
    <lst name="details">
        <str name="indexSize">71 bytes</str>
        <str name="indexPath">C:\solr\solr-6.6.6\example\techproducts\solr\demobackup\data\index/</str>
        <arr name="commits">
            <lst>
                <long name="indexVersion">0</long>
                <long name="generation">1</long>
                <arr name="filelist">
                    <str>segments_1</str>
                </arr>
            </lst>
        </arr>
        <str name="isMaster">true</str>
        <str name="isSlave">false</str>
        <long name="indexVersion">0</long>
        <long name="generation">1</long>
        <lst name="master">
            <arr name="replicateAfter">
                <str>commit</str>
            </arr>
            <str name="replicationEnabled">true</str>
        </lst>
        <lst name="backup">
            <str name="startTime">Tue Jun 25 20:55:03 UTC 2019</str>
            <int name="fileCount">1</int>
            <str name="status">success</str>
            <str name="snapshotCompletedAt">Tue Jun 25 20:55:03 UTC 2019</str>
            <str name="snapshotName">mybackup</str>
        </lst>
    </lst>
</response>
```

4. Restore backup previously created

```bash
http://localhost:8984/solr/demobackup/replication?command=restore&name=mybackup
``` 
will restore the index snapshot named demobackup in the current core

Response:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
    <lst name="responseHeader">
        <int name="status">0</int>
        <int name="QTime">2</int>
    </lst>
    <str name="status">OK</str>
</response>
```

5. Check the restore status: 
`http://localhost:8984/solr/demobackup/replication?command=restorestatus&wt=xml`
The output of the API will be as follows: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
    <lst name="responseHeader">
        <int name="status">0</int>
        <int name="QTime">0</int>
    </lst>
    <lst name="restorestatus">
        <str name="snapshotName">snapshot.mybackup</str>
        <str name="status">success</str>
    </lst>
</response>
```

Can create, restore, and list snapshots of the index using APIs.  

6. Create snapshot   
`http://localhost:8984/solr/admin/cores?action=CREATESNAPSHOT&core=demobackup&commitName=commit1`

7. List snapshot   

`http://localhost:8984/solr/admin/cores?action=LISTSNAPSHOTS&core=demobackup&commitName=commit1`


8. Delete snapshot   

`http://localhost:8984/solr/admin/cores?action=DELETESNAPSHOT&core=demobackup&commitName=commit1` 
