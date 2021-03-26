# Common Commands in Terminal #

## Create a single node for the database ##
```zsh
cockroach start-single-node --insecure --listen-addr=localhost:26257 --http-addr=localhost:8080
    --insecure (no encryption or authentication)
    --listen-addr=localhost:26257
    --http-addr=localhost:8080
```
## Start the instance already created in the system ##
```zsh
cockroach start --insecure
```
## Load database XXX ##
```zsh
cockroach workload init XXX
```
## Enter SQL Shell mode ##
```zsh
cockroach sql --insecure
```  
##  ##
```zsh
cockroach start --insecure --store=node1 --listen-addr=localhost:26257 --http-addr=localhost:8080 --join=localhost:26257,localhost:26258,localhost:26259 --background
    --insecure 
    --store=node1 
    --listen-addr=localhost:26257 
    --http-addr=localhost:8080 
    --join=localhost:26257,localhost:26258,localhost:26259 
    --background
```
##  ##
```zsh
cockroach start --insecure --store=node2 --listen-addr=localhost:26258 --http-addr=localhost:8081 --join=localhost:26257,localhost:26258,localhost:26259 --background
cockroach start --insecure --store=node3 --listen-addr=localhost:26259 --http-addr=localhost:8082 --join=localhost:26257,localhost:26258,localhost:26259 --background
cockroach init --insecure --host=localhost:26257
cockroach workload init movr
```