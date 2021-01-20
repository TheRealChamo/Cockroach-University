## Commands Usage ##

|Commands	                                |Description|
|--                                         |--|
|`cockroach start`	                        |Start a node as part of a multi-node cluster.|
|`cockroach init`	                        |Initialize a multi-node cluster.|
|`cockroach start-single-node`	            |Start a single-node cluster.|
|`cockroach cert`	                        |Create CA, node, and client certificates.|
|`cockroach quit`	                        |Temporarily stop a node or permanently remove a node.|
|`cockroach sql`	                        |Use the built-in SQL client.|
|`cockroach sqlfmt`	                        |Reformat SQL queries for enhanced clarity.|
|`cockroach node`	                        |List node IDs, show their status, decommission nodes for removal, or recommission nodes.|
|`cockroach dump`	                        |Deprecated. Use one of the following instead:
                                                - To back up your data, take a full backup.
                                                - To export your data in plaintext format, use EXPORT.
                                                - To view table schema in plaintext, use SHOW CREATE TABLE.|
|`cockroach demo`	                        |Start a temporary, in-memory CockroachDB cluster, and open an interactive SQL shell to it.|
|`cockroach gen`	                        |Generate manpages, a bash completion file, example SQL data, or an HAProxy configuration file for a running cluster.|
|`cockroach version`	                    |Output CockroachDB version details.|
|`cockroach debug ballast`	                |Create a large, unused file in a node's storage directory that you can delete if the node runs out of disk space.|
|`cockroach debug encryption-active-key`	|View the encryption algorithm and store key.|
|`cockroach debug zip`	                    |Generate a .zip file that can help Cockroach Labs troubleshoot issues with your cluster.|
|`cockroach debug merge-logs`	            |Merge multiple log files from different machines into a single stream.|
|`cockroach workload`	                    |Run a built-in load generator against a cluster.|
|`cockroach nodelocal upload`	            |Upload a file to the externalIODir on a node's local file system.|
|`cockroach userfile upload`	            |New in v20.2: Upload a file to the user-scoped file storage.|
|`cockroach userfile list`	                |New in v20.2: List the files stored in the user-scoped file storage.|
|`cockroach userfile delete`	            |New in v20.2: Deletes the files stored in the user-scoped file storage.|
