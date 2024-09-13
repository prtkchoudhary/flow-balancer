

# Flow Balancer - Scalable Load Balancer in Go

## Overview

**Flow Balancer** is a high-performance, scalable load balancer built in **Go**, designed to distribute traffic across multiple servers using a variety of load-balancing algorithms. These algorithms include:

- **Round Robin**
- **Weighted Round Robin**
- **Least Connections**
- **Weighted Least Connections**

The load balancer is designed to ensure efficient traffic management, ensuring that requests are routed to healthy servers. It also features **real-time health checks** to ensure traffic is directed only to active servers. Additionally, **comprehensive logging** is built into the system, offering different logging levels (info, warning, error) to track redirection patterns, server health, and traffic statistics.

## Features

- **Multiple Load Balancing Algorithms**: Choose between Round Robin, Weighted Round Robin, Least Connections, and Weighted Least Connections.
- **Health Checks**: Automatic server health monitoring to ensure traffic is only routed to live servers.
- **Advanced Logging**: Built-in logging with support for different log levels (info, warning, error).
- **Scalability**: Designed to handle large traffic loads with efficient distribution across servers.

## Table of Contents

1. [Installation](#installation)
2. [Setting Up Python Servers](#setting-up-python-servers)
3. [Running Flow Balancer](#running-flow-balancer)
4. [Configuration](#configuration)
5. [Contributing](#contributing)
6. [License](#license)

## Installation

To get started with **Flow Balancer**, follow these steps:

### Prerequisites

- **Go** (version 1.16 or above)
- **Python** (version 3.x for setting up backend servers)
- A terminal or command line interface

### Clone the Repository

```bash
git clone https://github.com/prtkchoudhary/flow-balancer.git
cd flow-balancer
```

### Build the Project

Make sure you have Go installed. You can install Go from the official [Go Installation Page](https://golang.org/doc/install).

1. Navigate to the project directory.
2. Build the Go project:

```bash
go build -o flow-balancer main.go
```

This will generate the `flow-balancer` binary in the project directory.

## Setting Up Python Servers

To test the load balancer, we'll set up five simple HTTP servers using Python's built-in HTTP server. Each server will run on a different port and will respond with its unique identifier, which allows us to see which server is receiving the traffic.

1. Open a terminal window and run the following commands to start five Python servers:

```bash
# Server 1
python -m http.server 8081 --bind 127.0.0.1

# Server 2
python -m http.server 8082 --bind 127.0.0.1

# Server 3
python -m http.server 8083 --bind 127.0.0.1

# Server 4
python -m http.server 8084 --bind 127.0.0.1

# Server 5
python -m http.server 8085 --bind 127.0.0.1
```

Each of these servers will be accessible locally on `localhost` with their respective ports. 

To confirm they are running, you can open a browser and go to:

- http://localhost:8081
- http://localhost:8082
- http://localhost:8083
- http://localhost:8084
- http://localhost:8085

You should see a simple "Directory listing" page for each server.

## Running Flow Balancer

Once your servers are up and running, you can launch **Flow Balancer** and start distributing traffic.

1. Open a new terminal window.
2. Run the **flow-balancer** load balancer by executing the following command:

```bash
./flow-balancer
```

### Default Configuration

By default, **Flow Balancer** will distribute traffic across the servers on `localhost`:

- http://localhost:8081
- http://localhost:8082
- http://localhost:8083
- http://localhost:8084
- http://localhost:8085

The load balancer uses the **Round Robin** algorithm by default, but you can change this in the configuration file (explained below).

### Testing the Load Balancer

You can test the load balancer by opening a browser or using a tool like `curl`:

```bash
curl http://localhost:8000
```

This will send requests to the load balancer, which will distribute them across the five Python servers. Each response should indicate which server handled the request.

## Configuration

You can configure **Flow Balancer** by editing the `config.yaml` file. This file allows you to:

- **Add or remove servers**: Specify the backend servers for load balancing.
- **Change the load-balancing algorithm**: Choose between Round Robin, Weighted Round Robin, Least Connections, and Weighted Least Connections.
- **Configure health checks**: Set the frequency of health checks and the timeout period.
- **Adjust logging levels**: Set the log level to `info`, `warning`, or `error`.

### Example `config.yaml`:

```yaml
servers:
  - address: "http://localhost:8081"
  - address: "http://localhost:8082"
  - address: "http://localhost:8083"
  - address: "http://localhost:8084"
  - address: "http://localhost:8085"

load_balancing_algorithm: "round_robin"

health_check:
  interval: 5  # in seconds
  timeout: 2   # in seconds

logging:
  level: "info"
```

After editing the configuration file, restart the load balancer for the changes to take effect:

```bash
./flow-balancer
```

## Contributing

We welcome contributions! If you'd like to improve **Flow Balancer**, feel free to fork the repository and submit a pull request.

1. Fork the project
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a pull request

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

This README should provide a solid introduction to your project and help users set up and run the load balancer easily. Let me know if you need any more details or modifications!
