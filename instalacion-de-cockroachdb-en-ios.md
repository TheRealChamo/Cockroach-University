# Instalación de CockroachDB en iOS

## Download the binary ##

* Download the [CockroachDB archive](https://binaries.cockroachdb.com/cockroach-v20.2.3.darwin-10.9-amd64.tgz) for OS X and the supporting libraries that are used to provide [spatial features](https://www.cockroachlabs.com/docs/v20.2/spatial-features), and extract the binary:

```zsh
curl https://binaries.cockroachdb.com/cockroach-v20.2.3.darwin-10.9-amd64.tgz | tar -xJ
```

* Copy the binary into your PATH so you can execute [cockroach commands](https://www.cockroachlabs.com/docs/v20.2/cockroach-commands) from any shell:

```zsh
cp -i cockroach-v20.2.3.darwin-10.9-amd64/cockroach /usr/local/bin/
```

If you get a permissions error, prefix the command with sudo.