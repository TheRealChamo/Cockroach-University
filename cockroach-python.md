connect db cloud con mac
cockroach sql --url 'postgres://dbadmin@orange-lynx-8j4.gcp-us-east4.cockroachlabs.cloud:26257/defaultdb?sslmode=verify-full&sslrootcert=/Users/midiaz/Downloads/orange-lynx-ca.crt'


verifi tables
SHOW TABLES FROM movr

cockroach sql --url 'postgres://dbadmin@orange-lynx-8j4.gcp-us-east4.cockroachlabs.cloud:26257/movr?sslmode=verify-full&sslrootcert=/Users/midiaz/Downloads/orange-lynx-ca.crt'


> CREATE USER app_user WITH PASSWORD 'Cockroach2020!';
> GRANT SELECT, INSERT, UPDATE, DELETE ON DATABASE movr TO app_user;
> REVOKE SELECT ON DATABASE movr FROM reports_user;


GRANT CREATE, DROP, GRANT, SELECT, INSERT, UPDATE, DELETE ON TABLE movr.* TO app_user;

IMPORT
TABLE
    vehicles (
        id
            UUID PRIMARY KEY,
        last_longitude
            FLOAT8 NOT NULL,
        last_ñatitude
            FLOAT8 NOT NULL,
        battery
            INT8 NOT NULL,
        last_checkin
            TIMESTAMP NOT NULL,
        in_use
            BOOL NOT NULL,
        vehicle_type
            STRING NOT NULL
    )
CSV
    DATA (
        'https://cockroach-university-public.s3.amazonaws.com/10000vehicles.csv'
    )
WITH
    delimiter = '|';

Dependency 

Instructions / Terminal Commands

Brew

$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"


From  https://brew.sh/

Python 3

From  https://docs.python-guide.org/starting/install3/osx/  


$ echo 'export PATH="/usr/local/opt/python/libexec/bin:$PATH"' >> ~/.profile

 

$ source ~/.profile


$ brew install python

PIP

$ sudo easy_install pip

Docopt

$ pip3 install docopt

Flask

$ pip3 install flask

flask-bootstrap

$ pip3 install flask-bootstrap

flask-login

$ pip3 install flask-login

sqlalchemy

$ pip3 install sqlalchemy

sqlalchemy-cockroachdb driver

$ pip3 install sqlalchemy-cockroachdb

Psycopg2

$ pip3 install psycopg2-binary

Geopy

$ pip3 install geopy

Dotenv

$ pip3 install python-dotenv

Flask-wtf

$ pip3 install flask-wtf

Install pip en Python3

python3 -m pip install -U pip