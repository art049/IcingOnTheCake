# IcingOnTheCake

A Private Ethereum Testnet with Blockscout explorer easily deployable with docker-compose

## Requirements

- Install [Docker](https://docs.docker.com/get-docker/)
- Install [docker-compose](https://docs.docker.com/compose/install/)

## Running locally (with a blockscout build made by Demos Labs)

Clone the repository:

```sh
git clone git@github.com:DemosLabs/IcingOnTheCake.git
```

Pull the docker-compose containers

```sh
docker-compose pull
```

Run the docker-compose project

```sh
docker-compose up
```

## Running locally (with a local blockscout build)

Clone the repository with the submodules:

```shell
git clone git@github.com:DemosLabs/IcingOnTheCake.git --recursive
```

Build the docker-compose project

```shell
docker-compose build
```

Run the docker-compose project

```shell
docker-compose up
```

### Local Settings

| Syntax         | Description     |
| -------------- | --------------- |
| JSON-RPC URL   | localhost:8545  |
| Block Explorer | localhost:26000 |
| Chain ID       | 1337            |

## Running with HTTPS and Basic Auth (using docker-compose and Traefik)

Clone the repository:

```shell
git clone git@github.com:DemosLabs/IcingOnTheCake.git
```

Pull the docker-compose containers

```shell
docker-compose pull
```

Make sure the domain you want to use have proper A Records (for the subdomains `rpc` and `explorer`) pointing to the machine you wish to deploy the chain from.

Configure your web environment:

- Copy `.env.example` to `.env`
- Fill `ACME_EMAIL` to get reminders in the case your certificates are about to expire (it doesn't happen often since Traefik handle this automatically)
- Fill `HOST` with the base domain you want to expose the services on.
- Generate a Basic Authentication secret:

  ```shell
  echo $(htpasswd -nb USERNAME PASSWORD) | sed -e s/\\$/\\$\\$/g

  ```

Launch the docker compose project including the Traefik definitions:

```shell
docker-compose -f docker-compose.yml \
               -f docker-compose.traefik.yml \
               -f docker-compose.traefik-config.yml \
               up -d
```

After giving some minutes to Traefik for it to do its magic, the RPC and the Explorer will be available over HTTPS with a Basic Authentication.

### Traefik Settings

| Syntax         | Description                  |
| -------------- | ---------------------------- |
| JSON-RPC URL   | https://rpc.example.com      |
| Block Explorer | https://explorer.example.com |
| Chain ID       | 1337                         |

> You can use the RPC with an incline authentication string (useful with Metamask for example)
> `https://user:password@rpc.example.com`

## Accounts with funds

Addresses derived from the mnemonic `test test test test test test test test test test test junk` are funded with 100 ETH.

| Address                                    | Private Key                                                        |
| ------------------------------------------ | ------------------------------------------------------------------ |
| 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 | 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 |
| 0x70997970C51812dc3A010C7d01b50e0d17dc79C8 | 0x59c6995e998f97a5a0044966f0945389dc9e86dae88c7a8412f4603b6b78690d |
| 0x3C44CdDdB6a900fa2b585dd299e03d12FA4293BC | 0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a |
| 0x90F79bf6EB2c4f870365E785982E1f101E93b906 | 0x7c852118294e51e653712a81e05800f419141751be58f605c371e15141b007a6 |
| 0x15d34AAf54267DB7D7c367839AAf71A00a2C6A65 | 0x47e179ec197488593b187f80a00eb0da91f1b9d0b13f8733639f19c30a34926a |
| 0x9965507D1a55bcC2695C58ba16FB37d819B0A4dc | 0x8b3a350cf5c34c9194ca85829a2df0ec3153be0318b5e2d3348e872092edffba |
| 0x976EA74026E726554dB657fA54763abd0C3a0aa9 | 0x92db14e403b83dfe3df233f83dfa3a0d7096f21ca9b0d6d6b8d88b2b4ec1564e |
| 0x14dC79964da2C08b23698B3D3cc7Ca32193d9955 | 0x4bbbf85ce3377467afe5d46f804f221813b2bb87f24d81f60f1fcdbf7cbf4356 |
| 0x23618e81E3f5cdF7f54C3d65f7FBc0aBf5B21E8f | 0xdbda1821b80551c9d65939329250298aa3472ba22feea921c0cf5d620ea67b97 |
| 0xa0Ee7A142d267C1f36714E4a8F75612F20a79720 | 0x2a871d0798f97d79848a013d4936a73bf4cc922c825d33c1cf7073dff6d409c6 |
