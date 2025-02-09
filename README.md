# HydraDX API

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](#license)

HydraDX API is an open-source RESTful service that provides easy access to **HydraDX** network data and analytics. HydraDX is a next-generation DeFi protocol on Polkadot, featuring the **Omnipool** – a single, unified liquidity pool that holds all assets for efficient, frictionless trading. The HydraDX API aggregates on-chain data (from the HydraDX Omnipool and blockchain) and off-chain data (like token prices) into convenient endpoints. This makes it simple for developers and analysts to retrieve information such as pool liquidity, token prices, total value locked (TVL), trading volumes, and more, without directly interacting with the blockchain.

## Features

- **Omnipool Data Endpoints:** Query the state of the HydraDX Omnipool, including details of all assets in the pool (reserves, prices, weights, etc.) and pool parameters.
- **Historical Stats:** Retrieve aggregated network statistics such as total value locked (TVL) and trading volume over various time frames. The API uses a Subsquid indexer and database to provide historical data for charting and analysis.
- **Market Data Integration:** Get integrated market data (e.g., token prices, pair information) from external sources like CoinGecko and CoinMarketCap, combined with on-chain data for a complete view.
- **High Performance:** Utilizes caching (Redis) to rapidly serve frequent requests and reduce load on the underlying data sources. Real-time data is fetched via Polkadot RPC, and historical data is served from a database for efficiency.
- **OpenAPI Documentation:** Includes interactive API docs via Swagger UI, so you can explore and test endpoints directly from your browser (available once the server is running, at the `/docs` path).

## Built With

HydraDX API is built with the following technologies and libraries:

- **[Fastify](https://www.fastify.io)** – A fast Node.js web framework, used here to build the REST API server and routes.
- **[Polkadot.js API](https://polkadot.js.org)** – For communicating with the HydraDX blockchain node (RPC calls to query on-chain state in real time).
- **[Subsquid](https://docs.subsquid.io)** – A blockchain indexing framework. It powers a backend indexer (with a PostgreSQL database) that stores HydraDX on-chain events and data, enabling efficient queries for historical data.
- **[Redis](https://redis.io)** – An in-memory data store used as a caching layer to speed up repeated queries and reduce latency.

## Installation and Setup

Before running the HydraDX API locally, ensure you have the following prerequisites installed and configured:

- **Node.js** – Recommended Node version 16 or newer (the project is tested with Node.js v16+).
- **npm** – Comes with Node.js (or use **yarn** if you prefer).
- **PostgreSQL** – A PostgreSQL database is required to store indexed blockchain data (as produced by Subsquid). You should have a Postgres instance running and accessible.
- **Redis** – (Optional but recommended) for caching. Install and run a Redis server locally if you want caching enabled.

### Steps to install and run locally

1. **Clone the Repository:**  
   ```bash
   git clone https://github.com/galacticcouncil/HydraDX-api.git
   cd HydraDX-api
   ```

2. **Install Dependencies:**  
   ```bash
   npm install
   ``` 

3. **Database Setup:**  
   Ensure your PostgreSQL database is running and create a database for the HydraDX indexer.

4. **Redis Setup (Optional):**  
   Start Redis to enable caching.

5. **Run the API in Development Mode:**  
   ```bash
   npm run app-dev
   ```

6. **Run the API in Production Mode:**  
   ```bash
   npm run app
   ```

7. **Run via Docker:**  
   ```bash
   docker build -t hydradx-api .
   docker run -d -p 3000:3000 --name hydradx-api-instance hydradx-api
   ```

## API Usage

Once running, you can interact with the API via:

- **Swagger UI Documentation:** `http://localhost:3000/docs`
- **Example Endpoints:**
  - `GET /omnipool/assets` – Retrieves Omnipool asset list.
  - `GET /stats/tvl` – Retrieves total value locked (TVL).
  - `GET /stats/volume?period=24h` – Retrieves trading volume over 24h.
  - `GET /asset/HDX/price` – Retrieves price data for HDX.

## Contributing

Contributions are welcome! Follow these steps to contribute:

1. **Fork the repository** and create a new branch for your feature.
2. **Follow the coding style** (run `npm run format` before committing).
3. **Submit a Pull Request** with a clear description of changes.

## License

This project is licensed under the **Apache License 2.0**.

```
SPDX-License-Identifier: Apache-2.0
```

© 2025 Galactic Council and HydraDX contributors. All rights reserved.
