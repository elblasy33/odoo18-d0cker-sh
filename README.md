

---

# 🚀 Odoo Docker SH

## 🧩 Quick Install

Install **Odoo 15** effortlessly with a single command.

> **Supports multiple Odoo instances on a single server**

### 📦 Prerequisites

* Install [Docker](https://docs.docker.com/get-docker/)
* Install [Docker Compose](https://docs.docker.com/compose/install/)

### 🛠️ Installation

To set up the first Odoo instance:

```bash
curl -s https://raw.githubusercontent.com/elblasy33/odoo18-d0cker-sh/main/run.sh | sudo bash -s odoo-18-one 10018 20018
```



Access Odoo at: `http://localhost:10018`
Default master password: `Elblasy2022@1234`

To set up another Odoo instance:

```bash
curl -s https://raw.githubusercontent.com/elblasy33/odoo18-d0cker-sh/main/run.sh | sudo bash -s odoo18-two 11018 21018
```



Access Odoo at: `http://localhost:11018`
Default master password: `Elblasy2022@1234`

### 📝 Parameters

* First argument (`odoo-18-one`): Deployment folder name
* Second argument (`10018`): Odoo port
* Third argument (`20018`): Live chat port

> **Note:** If `curl` is not installed, you can install it using:

```bash
sudo apt-get install curl  # For Debian/Ubuntu
sudo yum install curl      # For CentOS/RHEL:contentReference[oaicite:52]{index=52}
```



---

## ⚙️ Usage

### ▶️ Starting the Container

```bash
docker-compose up
```



Then, open `http://localhost:10018` to access Odoo 15.

> To start the server with a different port, modify the `docker-compose.yml` file:

```yaml
ports:
  - "10018:8069"
```



### 🧳 Detached Mode

Run Odoo in detached mode to keep it running after closing the terminal:

```bash
docker-compose up -d
```



### 🔐 Permissions

If you encounter permission issues, adjust folder permissions:

```bash
git clone https://github.com/elblasy33/odoo15-d0cker-sh.git
sudo chmod -R 777 addons
sudo chmod -R 777 etc
mkdir -p postgresql
sudo chmod -R 777 postgresql
```



### 📈 Increase File Watch Limit (Optional)

To avoid errors when running multiple Odoo instances:

```bash
if grep -qF "fs.inotify.max_user_watches" /etc/sysctl.conf; then
  echo $(grep -F "fs.inotify.max_user_watches" /etc/sysctl.conf)
else
  echo "fs.inotify.max_user_watches = 524288" | sudo tee -a /etc/sysctl.conf
fi
sudo sysctl -p  # Apply new config immediately
```



---

## 🧩 Custom Addons

Place your custom addons in the `addons/` directory.

---

## 🛠️ Configuration & Logs

* To modify Odoo configurations, edit: `etc/odoo.conf`
* Log file location: `etc/odoo-server.log`
* Default database password (`admin_passwd`): `Elblasy2022@1234`

  * It's recommended to change this password in the `etc/odoo.conf` file.

---

## 🐳 Docker Commands

* **Run Odoo:**

  ```bash
  docker-compose up -d
  ```



* **Restart Odoo:**

  ```bash
  docker-compose restart
  ```



* **Stop Odoo:**

  ```bash
  docker-compose down
  ```



---

## 💬 Live Chat Configuration

In the `docker-compose.yml` file, port `20015` is exposed for live chat functionality.

To configure **nginx** for live chat in a production environment:

```nginx
server {
    # ...
    location /longpolling/ {
        proxy_pass http://0.0.0.0:20015/longpolling/;
    }
    # ...
}
```



---

## 📦 Docker Images

* Odoo: `odoo:15.0`
* PostgreSQL: `postgres:14`

---

## 📸 Screenshots

Welcome Screen:

![Welcome Screen](screenshots/odoo-15-welcome-screenshot.png)

Apps Dashboard:

![Apps Dashboard](screenshots/odoo-15-apps-screenshot.png)

---

Feel free to copy and paste this updated `README.md` into your GitHub repository. If you need further customization or assistance, don't hesitate to ask!
