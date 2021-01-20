# Common Commands in Terminal #

## Crea un unico nodo para la base de datos ##
cockroach start-single-node --insecure --listen-addr=localhost:26257 --http-addr=localhost:8080
    --insecure (no encryption or authentication)
    --listen-addr=localhost:26257
    --http-addr=localhost:8080

## Arranca la instancia ya creada en el sistema ##
cockroach start --insecure

## Carga la base de datos XXX ##
cockroach workload init XXX

## Ingresa al modo SQL Shell ##
cockroach sql --insecure
        
##  ##
cockroach start --insecure --store=node1 --listen-addr=localhost:26257 --http-addr=localhost:8080 --join=localhost:26257,localhost:26258,localhost:26259 --background
    --insecure 
    --store=node1 
    --listen-addr=localhost:26257 
    --http-addr=localhost:8080 
    --join=localhost:26257,localhost:26258,localhost:26259 
    --background

cockroach start --insecure --store=node2 --listen-addr=localhost:26258 --http-addr=localhost:8081 --join=localhost:26257,localhost:26258,localhost:26259 --background
cockroach start --insecure --store=node3 --listen-addr=localhost:26259 --http-addr=localhost:8082 --join=localhost:26257,localhost:26258,localhost:26259 --background
cockroach init --insecure --host=localhost:26257
cockroach workload init movr