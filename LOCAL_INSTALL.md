# Run Chat UI Locally

1. Get mongo DB
```shell
 docker run --rm -d -p 27017:27017 --name mongo-chatui mongo:latest
```
2. Install libraries for websearch

```shell
brew install playwright
playwright install
playwright install-deps

```
Typically, `install-dep` does not install anything.

Inside  the project folder run
```shell
npx playwright install
npx playwright install-dep
npm install --verbose
```


Generating long lived tokens with slipctl
```shell
poetry add pyjks
poetry add pyjwt
poetry add cryptography
```

Put the keystore `keystore2.jks` to the root folder of the `slipctl` project.
Set the password line 69 `src/slipctl/keycloak/signed_jwt.py`

```python
def get_certs(jwks_fp="keystore2.jks", password="xxxx"):
```
Run  
```shell
 python src/slipctl/keycloak/signed_jwt.py
```

Copy the token and set it for each model  `.env.local` for all models `MODELS` and `TEXT_EMBEDDING_MODELS`  
`endpoints` 


### Single Token Definition Run

Modify Line 18 
[endpointTgi.ts](src%2Flib%2Fserver%2Fendpoints%2Ftgi%2FendpointTgi.ts)
to 
```javascript
	authorization: z.string().default(env.SLIP_ACCESS_TOKEN)
```
remove the `authorization` property from eac model in the  `.env`
## NPM
```shell
npm run dev 
```

```shell
npm run dev  --env-file=.env.token  --env-file=.env.local 
```
## PM2 

```shell
  pm2 start npm --name "chat-ui" -- run "dev" 
```

With env. Not Working
```shell
  pm2 start npm --name "chat-ui" -- run "dev" \
  --env ".env.token"
```
Other commands 
```shell
  pm2 delete  "chat-ui"
  pm2 logs "chat-ui"
  pm2 monit
  

```

Restart with Cron
https://pm2.keymetrics.io/docs/usage/restart-strategies/