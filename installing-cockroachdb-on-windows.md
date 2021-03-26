# Installing CockroachDB on Windows #

## Download the executable ##

* Download and extract the [CockroachDB v20.2.3](https://binaries.cockroachdb.com/cockroach-v20.2.3.windows-6.2-amd64.zip) archive for Windows.

* To ensure that CockroachDB can use location-based names as time zone identifiers, download Go's official [zoneinfo.zip](https://github.com/golang/go/raw/master/lib/time/zoneinfo.zip) and [set the `ZONEINFO` environment variable](https://www.techjunkie.com/environment-variables-windows-10/) to point to the zip file.

* Open PowerShell, navigate to the directory containing the executable, and make sure it works:

```powershell
PS C:\cockroach-v20.2.3.windows-6.2-amd64> .\cockroach.exe version
```