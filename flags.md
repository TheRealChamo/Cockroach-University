## Flags ##

### General ###

General
|Flag|Description|
`--attrs`	Arbitrary strings, separated by colons, specifying node capability, which might include specialized hardware or number of cores, for example:

--attrs=ram:64gb

These can be used to influence the location of data replicas. See Configure Replication Zones for full details.
--background	Set this to start the node in the background. This is better than appending & to the command because control is returned to the shell only once the node is ready to accept requests.

Note: --background is suitable for writing automated test suites or maintenance procedures that need a temporary server process running in the background. It is not intended to be used to start a long-running server, because it does not fully detach from the controlling terminal. Consider using a service manager or a tool like daemon(8) instead.
--cache	The total size for caches, shared evenly if there are multiple storage devices. This can be a percentage (notated as a decimal or with %) or any bytes-based unit, for example:

--cache=.25
--cache=25%
--cache=1000000000 ----> 1000000000 bytes
--cache=1GB ----> 1000000000 bytes
--cache=1GiB ----> 1073741824 bytes

Note: If you use the % notation, you might need to escape the % sign, for instance, while configuring CockroachDB through systemd service files. For this reason, it's recommended to use the decimal notation instead.

Default: 128MiB

The default cache size is reasonable for local development clusters. For production deployments, this should be increased to 25% or higher. Increasing the cache size will generally improve the node's read performance. See Recommended Production Settings for more details.
--cluster-name	A string that specifies a cluster name. This is used together with --join to ensure that all newly created nodes join the intended cluster when you are running multiple clusters.

Note: If this is set, cockroach init, cockroach node decommission, cockroach node recommission, and the cockroach debug commands must specify either --cluster-name or --disable-cluster-name-verification in order to work.
--disable-cluster-name-verification	On clusters for which a cluster name has been set, this flag paired with --cluster-name disables the cluster name check for the command. This is necessary on existing clusters, when setting a cluster name or changing the cluster name: Perform a rolling restart of all nodes and include both the new --cluster-name value and --disable-cluster-name-verification, then a second rolling restart with --cluster-name and without --disable-cluster-name-verification.
--external-io-dir	The path of the external IO directory with which the local file access paths are prefixed while performing backup and restore operations using local node directories or NFS drives. If set to disabled, backups and restores using local node directories and NFS drives, as well as cockroach nodelocal upload, are disabled.

Default: extern subdirectory of the first configured store.

To set the --external-io-dir flag to the locations you want to use without needing to restart nodes, create symlinks to the desired locations from within the extern directory.
--listening-url-file	The file to which the node's SQL connection URL will be written as soon as the node is ready to accept connections, in addition to being printed to the standard output. When --background is used, this happens before the process detaches from the terminal.

This is particularly helpful in identifying the node's port when an unused port is assigned automatically (--port=0).
--locality	Arbitrary key-value pairs that describe the location of the node. Locality might include country, region, availability zone, etc. For more details, see Locality below.
--max-disk-temp-storage	The maximum on-disk storage capacity available to store temporary data for SQL queries that exceed the memory budget (see --max-sql-memory). This ensures that JOINs, sorts, and other memory-intensive SQL operations are able to spill intermediate results to disk. This can be a percentage (notated as a decimal or with %) or any bytes-based unit (e.g., .25, 25%, 500GB, 1TB, 1TiB).

Note: If you use the % notation, you might need to escape the % sign, for instance, while configuring CockroachDB through systemd service files. For this reason, it's recommended to use the decimal notation instead. Also, if expressed as a percentage, this value is interpreted relative to the size of the first store. However, the temporary space usage is never counted towards any store usage; therefore, when setting this value, it's important to ensure that the size of this temporary storage plus the size of the first store doesn't exceed the capacity of the storage device.

The temporary files are located in the path specified by the --temp-dir flag, or in the subdirectory of the first store (see --store) by default.

Default: 32GiB
--max-offset	The maximum allowed clock offset for the cluster. If observed clock offsets exceed this limit, servers will crash to minimize the likelihood of reading inconsistent data. Increasing this value will increase the time to recovery of failures as well as the frequency of uncertainty-based read restarts.

Note that this value must be the same on all nodes in the cluster and cannot be changed with a rolling upgrade. In order to change it, first stop every node in the cluster. Then once the entire cluster is offline, restart each node with the new value.

Default: 500ms
--max-sql-memory	The maximum in-memory storage capacity available to store temporary data for SQL queries, including prepared queries and intermediate data rows during query execution. This can be a percentage (notated as a decimal or with %) or any bytes-based unit, for example:

--max-sql-memory=.25
--max-sql-memory=25%
--max-sql-memory=10000000000 ----> 1000000000 bytes
--max-sql-memory=1GB ----> 1000000000 bytes
--max-sql-memory=1GiB ----> 1073741824 bytes

The temporary files are located in the path specified by the --temp-dir flag, or in the subdirectory of the first store (see --store) by default.

Note: If you use the % notation, you might need to escape the % sign, for instance, while configuring CockroachDB through systemd service files. For this reason, it's recommended to use the decimal notation instead.

Default: 25%

The default SQL memory size is suitable for production deployments but can be raised to increase the number of simultaneous client connections the node allows as well as the node's capacity for in-memory processing of rows when using ORDER BY, GROUP BY, DISTINCT, joins, and window functions. For local development clusters with memory-intensive workloads, reduce this value to, for example, 128MiB to prevent out of memory errors.
--pid-file	The file to which the node's process ID will be written as soon as the node is ready to accept connections. When --background is used, this happens before the process detaches from the terminal. When this flag is not set, the process ID is not written to file.
--store
-s	The file path to a storage device and, optionally, store attributes and maximum size. When using multiple storage devices for a node, this flag must be specified separately for each device, for example:

--store=/mnt/ssd01 --store=/mnt/ssd02

For more details, see Store below.
--spatial-libs	New in v20.2: The location on disk where CockroachDB looks for spatial libraries.

Defaults:
/usr/local/lib/cockroach
A lib subdirectory of the CockroachDB binary's current directory.

--temp-dir	The path of the node's temporary store directory. On node start up, the location for the temporary files is printed to the standard output.

Default: Subdirectory of the first store

### Networking ###

Flag	Description
--listen-addr	The IP address/hostname and port to listen on for connections from other nodes and clients. For IPv6, use the notation [...], e.g., [::1] or [fe80::f6f2:::].

This flag's effect depends on how it is used in combination with --advertise-addr. For example, the node will also advertise itself to other nodes using this value if --advertise-addr is not specified. For more details, see Networking.

Default: Listen on all IP addresses on port 26257; if --advertise-addr is not specified, also advertise the node's canonical hostname to other nodes
--advertise-addr	The IP address/hostname and port to tell other nodes to use. If using a hostname, it must be resolvable from all nodes. If using an IP address, it must be routable from all nodes; for IPv6, use the notation [...], e.g., [::1] or [fe80::f6f2:::].

This flag's effect depends on how it is used in combination with --listen-addr. For example, if the port number is different than the one used in --listen-addr, port forwarding is required. For more details, see Networking.

Default: The value of --listen-addr; if --listen-addr is not specified, advertises the node's canonical hostname and port 26257
--http-addr	The IP address/hostname and port to listen on for DB Console HTTP requests. For IPv6, use the notation [...], e.g., [::1]:8080 or [fe80::f6f2:::]:8080.

Default: Listen on the address part of --listen-addr on port 8080
--locality-advertise-addr	The IP address/hostname and port to tell other nodes in specific localities to use. This flag is useful when running a cluster across multiple networks, where nodes in a given network have access to a private or local interface while nodes outside the network do not. In this case, you can use --locality-advertise-addr to tell nodes within the same network to prefer the private or local address to improve performance and use --advertise-addr to tell nodes outside the network to use another address that is reachable from them.

This flag relies on nodes being started with the --locality flag and uses the locality@address notation, for example:

--locality-advertise-addr=region=us-west@10.0.0.0:26257

See the example below for more details.
--sql-addr	The IP address/hostname and port to listen on for SQL connections from clients. For IPv6, use the notation [...], e.g., [::1] or [fe80::f6f2:::].

This flag's effect depends on how it is used in combination with --advertise-sql-addr. For example, the node will also advertise itself to clients using this value if --advertise-sql-addr is not specified.

Default: The value of --listen-addr; if --listen-addr is not specified, advertises the node's canonical hostname and port 26257

For an example, see Start a cluster with separate RPC and SQL networks
--advertise-sql-addr	The IP address/hostname and port to tell clients to use. If using a hostname, it must be resolvable from all nodes. If using an IP address, it must be routable from all nodes; for IPv6, use the notation [...], e.g., [::1] or [fe80::f6f2:::].

This flag's effect depends on how it is used in combination with --sql-addr. For example, if the port number is different than the one used in --sql-addr, port forwarding is required.

Default: The value of --sql-addr; if --sql-addr is not specified, advertises the value of --listen-addr
--join
-j	The host addresses that connect nodes to the cluster and distribute the rest of the node addresses. These can be IP addresses or DNS aliases of nodes.

When starting a cluster in a single region, specify the addresses of 3-5 initial nodes. When starting a cluster in multiple regions, specify more than 1 address per region, and select nodes that are spread across failure domains. Then run the cockroach init command against any of these nodes to complete cluster startup. See the example below for more details.

Use the same --join list for all nodes to ensure that the cluster can stabilize. Do not list every node in the cluster, because this increases the time for a new cluster to stabilize. Note that these are best practices; it is not required to restart an existing node to update its --join flag.

cockroach start must be run with the --join flag. To start a single-node cluster, use cockroach start-single-node instead.
--socket-dir	The directory path on which to listen for Unix domain socket connections from clients installed on the same Unix-based machine. For an example, see Connect to a cluster listening for Unix domain socket connections.
--advertise-host	Deprecated. Use --advertise-addr instead.
--host	Deprecated. Use --listen-addr instead.
--port
-p	Deprecated. Specify port in --advertise-addr and/or --listen-addr instead.
--http-host	Deprecated. Use --http-addr instead.
--http-port	Deprecated. Specify port in --http-addr instead.

### Security ###

Flag	Description
--certs-dir	The path to the certificate directory. The directory must contain valid certificates if running in secure mode.

Default: ${HOME}/.cockroach-certs/
--insecure	Note: The --insecure flag is intended for non-production testing only. It will be deprecated and replaced with new secure options in v21.1.

Run in insecure mode. If this flag is not set, the --certs-dir flag must point to valid certificates.

Note the following risks: An insecure cluster is open to any client that can access any node's IP addresses; any user, even root, can log in without providing a password; any user, connecting as root, can read or write any data in your cluster; and there is no network encryption or authentication, and thus no confidentiality.

Default: false
--accept-sql-without-tls	This experimental flag allows you to connect to the cluster using a SQL user's password without validating the client's certificate. When connecting using the built-in SQL client, use the --insecure flag with the cockroach sql command.
--cert-principal-map	A comma-separated list of cert-principal:db-principal mappings used to map the certificate principals to IP addresses, DNS names, and SQL users. This allows the use of certificates generated by Certificate Authorities that place restrictions on the contents of the commonName field. For usage information, see Create Security Certificates using Openssl.
--enterprise-encryption	This optional flag specifies the encryption options for one of the stores on the node. If multiple stores exist, the flag must be specified for each store.

This flag takes a number of options. For a complete list of options, and usage instructions, see Encryption at Rest.

Note that this is an enterprise feature.
--external-io-disable-http	This optional flag disables external HTTP(S) access (as well as custom HTTP(S) endpoints) when performing bulk operations (e.g, BACKUP, IMPORT, etc.). This can be used in environments where you cannot run a full proxy server.

If you want to run a proxy server, you can start CockroachDB while specifying the HTTP(S)_PROXY environment variable.
--external-io-disable-implicit-credentials	This optional flag disables the use of implicit credentials when accessing external cloud storage services for bulk operations (e.g, BACKUP, IMPORT, etc.).