# localhost
A simple reverse proxy config to host your development environment on your local host with HTTPS.

Have you ever worked on a project with a backend and a frontend? Once you want to experiment with things where HTTPS is required, you'll have to set up some reverse proxy with SSL handling. This is my small solution based on NginX.

## Gettings started
### Requirements
- An own (optionally wildcard) subdomain pointing to either 127.0.0.1 or your computer's IP in your home network if you want to test your app on different devices across that network
- SSL Certificate for your domains
- A computer with Docker

# 0. Clone this repository

# 1. Setup your domain
Create A-Records pointing to `127.0.0.1` or your computer's IP on a domain like `*.notebook.localhost.yourdomain.net` or `service.exampleserver.mydomain.net`.

# 2. Gather your certificates
I recommend using Let'sEncrypt with a wildcard certificate for your subdomain. If you want to automate this, checkout Cloudflare's free plan for being your nameserver, Let'sEncrypt can automatically validate your subdomains there.
You should have a `fullchain.pem` and `privkey.pem`-file at the end. Copy them into the `/certs`-directory

# 3. Configure your subdomains
Modify the `/config/default.conf`-file to your needs. Replace the example values after `server_name` with your desired domain.
Also, update the `location`-blocks in the file. The example is setup to use an application on port 8000 on the Docker host (not necessarily a container, if your app runs in a container make sure to port-forward it in Docker) when a request starts with `/api`, otherwise it serves what an app on port 5173 responds.

# 4. Start the container
Run `docker compose up -d` in the root directory of this repository.

Have fun 🎉
