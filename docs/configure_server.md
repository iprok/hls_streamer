# ⚙️ Configuring the Server

## 1. Connect to the Server

SSH into your target server:

```bash
ssh root@your.server.ip
```

## 2. Install Required Tools

Update package lists and install basic tools:

```bash
apt-get update
apt-get install -y ansible git mc
```

## 3. Get the Role

Choose one of the following options:

### Option A – Clone from GitHub

```bash
git clone https://github.com/iprok/hls_streamer.git
cd hls_streamer
```

### Option B – Extract from Archive

If you have the `hls_streamer.tar.gz` archive:

```bash
tar -xzf hls_streamer.tar.gz
cd hls_streamer
```

## 4. Edit Inventory File

Open the `hosts` file (located in the root of the role directory) using your preferred editor:

```bash
mcedit hosts
```

Edit it to look like this:

```ini
[webservers]
localhost ansible_connection=local

[webservers:vars]
domain_name=stream.example.com
email=admin@example.com
webroot_path=/var/www/html
enable_ipv6=true
```

- `domain_name` — the domain name to serve content from
- `email` — the email address used for Let's Encrypt

Save the file and exit.

---

# 🚀 Running the Playbook

## 1. Run the Playbook

Execute the following command **from inside the `hls_streamer` directory**:

```bash
ansible-playbook -i hosts site.yml
```

This will:

- Ensure Python is installed on the system (if not already present)
- Install NGINX from the official vendor repository
- Set up a minimal HTTP configuration for Let's Encrypt verification
- Obtain an SSL certificate using Certbot and the webroot method
- Deploy a simple HTTPS configuration to serve static content from `/var/www/hls/`
