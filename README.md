# MaxCluster MCP Server

> **Spin up complete Magento 2 environments in 60 seconds** ⚡

Model Context Protocol (MCP) server for MaxCluster infrastructure management. Control NGINX, Apache, PHP, MySQL, Redis, RabbitMQ, and Elasticsearch/OpenSearch through AI agents or directly via MCP clients.

## ✨ Key Features

- **🎯 One-Command Magento 2 Setup** - Complete infrastructure provisioning with `magento_prepare_environment`
- **🤖 AI-Powered Operations** - Natural language server control via Claude and other AI agents
- **🔧 44 Management Tools** - Comprehensive control over all Magento 2 infrastructure components
- **📋 Ready-to-Use Configs** - Auto-generated `app/etc/env.php` configurations
- **🔒 Secure by Default** - Auto-generated passwords, no credential storage

## 🚀 Quick Start

### Prerequisites

- Node.js 20+
- MaxCluster account with Personal Access Token (PAT)
- MCP-compatible client (Claude Desktop, etc.)

### Installation

#### Option 1: NPX (Recommended)

```bash
# Run directly with npx
npx maxcluster-mcp-server
```

#### Option 2: Claude Code (One-liner)

```bash
claude mcp add maxcluster-mcp-server --env MAXCLUSTER_PAT=your_token_here -- npx -y maxcluster-mcp-server
```

#### Option 3: Manual Installation

```bash
# Clone the repository
git clone https://github.com/run-as-root/maxcluster-mcp.git
cd maxcluster-mcp

# Install dependencies
npm install

# Build the server
npm run build
```

### Configuration

Add to your MCP client configuration (e.g., `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "maxcluster": {
      "command": "npx",
      "args": ["maxcluster-mcp-server"],
      "env": {
        "MAXCLUSTER_PAT": "your_personal_access_token_here"
      }
    }
  }
}
```

### Your First Magento 2 Environment

```bash
# In your MCP client (e.g., Claude Desktop), use:
magento_prepare_environment \
  --cluster_id="C-1234" \
  --web_server="srv-a" \
  --db_server="db-a" \
  --cache_server="cache-a" \
  --queue_server="queue-a" \
  --search_server="search-a" \
  --search_engine="elasticsearch" \
  --environment_name="Demo"
```

**Result**: Complete Magento 2 infrastructure with ready-to-use configuration in ~60 seconds!

---

## 🎯 The Ultimate Tool: `magento_prepare_environment`

This tool orchestrates **6 infrastructure operations** in one call:

1. ✅ Creates MySQL database (auto-generated credentials)
2. ✅ Creates 3 Redis instances (cache, session, full-page cache)
3. ✅ Sets up RabbitMQ (vhost + user + permissions)
4. ✅ Creates Elasticsearch/OpenSearch instance
5. ✅ Generates complete `app/etc/env.php` configuration
6. ✅ Provides step-by-step Magento setup instructions

### What You Get

```
🎉 Magento 2 Demo Environment Prepared Successfully!

📊 CREATED RESOURCES:

MySQL Database:
  Database: db_rand_abc123
  Username: user_rand_xyz789
  Password: Xy9#mK2$pL4&nQ8@vB

Redis Instances:
  Default Cache:    Port 6379
  Session Storage:  Port 6380
  Full-Page Cache:  Port 6381

RabbitMQ:
  Vhost:    /magento
  Username: magento
  Password: auto_generated_secure_password

Elasticsearch:
  Port: 9200
  Heap: 2048MB

📝 COMPLETE MAGENTO 2 CONFIGURATION (app/etc/env.php):

[Complete ready-to-paste PHP configuration file]

✨ Next Steps:
1. Copy the configuration above into app/etc/env.php
2. Run: bin/magento setup:upgrade
3. Run: bin/magento setup:di:compile
4. Run: bin/magento cache:flush
5. Run: bin/magento indexer:reindex
```

**Copy. Paste. Done.** No manual configuration required.

---

## 📚 All Available Tools

### 🎭 Orchestration (2 tools)

- **`magento_environment_check`** - Health check all services (MySQL, Redis, RabbitMQ, Search, PHP, Web Server)
- **`magento_prepare_environment`** - Complete one-shot Magento 2 setup

### 🗄️ MySQL/MariaDB (5 tools)

- `mysql_status` - Get database status and list all databases
- `mysql_restart` - Restart MySQL service
- `mysql_create_database` - Create database with auto-generated credentials
- `mysql_list_databases` - List all databases with users
- `mysql_delete_database` - Delete database (DESTRUCTIVE)

### 🔴 Redis (7 tools)

- `redis_status` - Get all instances with details
- `redis_create_cache_instance` - Create cache-optimized instance (1GB, volatile-lru)
- `redis_create_session_instance` - Create session-optimized instance (512MB, persisted)
- `redis_create_fpc_instance` - Create full-page-cache instance (1GB, volatile-lru)
- `redis_start_instance` - Start instance by port
- `redis_stop_instance` - Stop instance by port
- `redis_flush_instance` - Flush all keys (FLUSHALL)

### 🐰 RabbitMQ (6 tools)

- `rabbitmq_status` - Get service status, vhosts, and users
- `rabbitmq_start` - Start RabbitMQ service
- `rabbitmq_stop` - Stop RabbitMQ service
- `rabbitmq_create_vhost` - Create virtual host
- `rabbitmq_create_user` - Create user with auto-generated password
- **`rabbitmq_setup_magento`** - Complete setup (vhost + user + permissions)

### 🔍 Elasticsearch (5 tools)

- `elasticsearch_status` - Get version, instances, heap sizes
- `elasticsearch_create_instance` - Create instance with specified heap
- `elasticsearch_start_instance` - Start instance by port
- `elasticsearch_stop_instance` - Stop instance by port
- `elasticsearch_restart_instance` - Restart instance by port

### 🔍 OpenSearch (5 tools)

- `opensearch_status` - Get version, instances, heap sizes
- `opensearch_create_instance` - Create instance with specified heap
- `opensearch_start_instance` - Start instance by port
- `opensearch_stop_instance` - Stop instance by port
- `opensearch_restart_instance` - Restart instance by port

### 🌐 Web Server (6 tools)

- `nginx_restart` - Restart NGINX
- `nginx_reload` - Reload NGINX config (graceful)
- `apache_start` - Start Apache (auto-switches from NGINX)
- `apache_restart` - Restart Apache
- `apache_reload` - Reload Apache config (graceful)
- `apache_status` - Get Apache status and configuration

### 🐘 PHP (7 tools)

- `php_status` - Get PHP versions and configuration
- `php_restart` - Restart PHP-FPM
- `php_reload` - Reload PHP-FPM (graceful)
- `php_install_version` - Install specific PHP version
- `php_uninstall_version` - Uninstall PHP version
- `php_change_cli_version` - Change default CLI version
- `php_change_composer_version` - Change Composer version

### 🛠️ Utilities (3 tools)

- `intelligent_server_operation` - Natural language operations (e.g., "restart nginx on production")
- `list_available_servers` - List configured server mappings
- `list_clusters` - List all accessible MaxCluster clusters
- `server_info` - Get detailed server hardware and network info

---

## 💡 Common Workflows

### Create Individual Services

```bash
# Create database
mysql_create_database C-1234 db-a --description="My Store"

# Create Redis instances
redis_create_cache_instance C-1234 cache-a --description="Default Cache"
redis_create_session_instance C-1234 cache-a --description="Sessions"
redis_create_fpc_instance C-1234 cache-a --description="Full Page Cache"

# Setup RabbitMQ
rabbitmq_setup_magento C-1234 queue-a \
  --vhost_name="/magento" \
  --username="magento-user"

# Create search engine
elasticsearch_create_instance C-1234 search-a \
  --heap_size_mb=2048 \
  --description="Catalog Search"
```

### Health Check Before Deployment

```bash
magento_environment_check C-1234 \
  --web_server="srv-a" \
  --db_server="db-a" \
  --cache_server="cache-a" \
  --queue_server="queue-a" \
  --search_server="search-a" \
  --search_engine="elasticsearch"
```

### Manage Services

```bash
# Restart web server
nginx_restart C-1234 srv-a

# Flush Redis cache
redis_flush_instance C-1234 cache-a --port=6379

# Restart search engine
elasticsearch_restart_instance C-1234 search-a --port=9200
```

---

## 📖 Documentation

- **[Complete User Guide](docs/MAGENTO2_COMPLETE_GUIDE.md)** - Comprehensive workflows and examples
- **[Implementation Plan](docs/IMPLEMENTATION_PLAN.md)** - Technical architecture and design
- **[API Discovery](docs/API_DISCOVERY.md)** - MaxCluster API endpoint reference
- **[MySQL Tools](docs/MYSQL_IMPLEMENTATION_SUMMARY.md)** - Database management details
- **[Redis Tools](docs/REDIS_IMPLEMENTATION_SUMMARY.md)** - Cache management details
- **[RabbitMQ Tools](docs/RABBITMQ_IMPLEMENTATION_SUMMARY.md)** - Queue management details
- **[Search Tools](docs/SEARCH_IMPLEMENTATION_SUMMARY.md)** - Elasticsearch/OpenSearch details
- **[Orchestration Tools](docs/MAGENTO_ORCHESTRATION_SUMMARY.md)** - High-level automation details

---

## 🔒 Security

### Personal Access Token

Your MaxCluster PAT is sensitive. **Never commit it to version control.**

**Recommended setup**:

```bash
# Add to your shell profile (~/.zshrc or ~/.bashrc)
export MAXCLUSTER_PAT="your_token_here"

# Or use MCP client env config
{
  "env": {
    "MAXCLUSTER_PAT": "your_token_here"
  }
}
```

### Credential Handling

- All passwords are auto-generated by MaxCluster (secure random)
- Credentials are only displayed once after creation
- **Save credentials immediately** - they cannot be retrieved later
- No credentials are stored or logged by this MCP server

---

## 🏗️ Architecture

### Technology Stack

- **TypeScript** - Type-safe implementation
- **MCP SDK** - Model Context Protocol v0.4.0
- **Axios** - HTTP client for MaxCluster API
- **Zod** - Runtime validation

### Design Principles

- **Composition over duplication** - Orchestration tools reuse individual tools
- **Type safety throughout** - Comprehensive TypeScript types
- **Consistent error handling** - Descriptive errors with context
- **Resource cleanup** - Proper cleanup on success and failure
- **Production-ready** - Comprehensive validation and logging

---

## 🤝 Contributing

Contributions are welcome! This project follows:

- Incremental changes over big rewrites
- Learning from existing code patterns
- Clear intent over clever code
- Comprehensive error handling

See individual tool implementations in `src/index.ts` for patterns to follow.

---

## 📝 License

MIT License - Copyright (c) 2025 run-as-root

See [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- Built with [Model Context Protocol](https://modelcontextprotocol.io)
- Powered by [MaxCluster](https://maxcluster.de) infrastructure
- Designed for [Magento 2](https://magento.com) deployments

---

## 📊 Project Stats

- **44 Tools** - Complete infrastructure management
- **8 Services** - NGINX, Apache, PHP, MySQL, Redis, RabbitMQ, Elasticsearch, OpenSearch
- **4800+ Lines** - Type-safe TypeScript implementation
- **Zero Dependencies** - Only MCP SDK, Axios, and Zod
- **100% Type Coverage** - Full TypeScript with strict mode

---

## 🔗 Links

- **GitHub**: [run-as-root/maxcluster-mcp](https://github.com/run-as-root/maxcluster-mcp)
- **MaxCluster**: [maxcluster.de](https://maxcluster.de)
- **MCP Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)
- **Issues**: [GitHub Issues](https://github.com/run-as-root/maxcluster-mcp/issues)

---

**From zero to production Magento 2 in one command.** 🚀
