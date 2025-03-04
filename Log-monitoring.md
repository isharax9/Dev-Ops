### **1. Locate Log Files**

Most system and service logs are stored in the `/var/log/` directory. Common logs include:

- **System logs**: `/var/log/syslog` (Debian/Ubuntu) or `/var/log/messages` (RHEL/CentOS)
- **Authentication logs**: `/var/log/auth.log` (Debian/Ubuntu) or `/var/log/secure` (RHEL/CentOS)
- **Boot logs**: `/var/log/boot.log`
- **Kernel logs**: `/var/log/dmesg` (or use `dmesg` command)
- **Service-specific logs** (e.g., `/var/log/nginx/`, `/var/log/apache2/`, `/var/log/mysql/`)

---

### **2. Use Command-Line Tools**

### **Basic Tools**

- **`cat`**: View the entire log file (not ideal for large files).
    
    ```
    cat /var/log/syslog
    ```
    
- **`less`**: Scroll through logs interactively (press `q` to quit).
    
    ```
    less /var/log/auth.log
    ```
    
- **`tail`**: View the end of a log (default: last 10 lines).
    
    ```
    tail /var/log/syslog
    # Monitor logs in real-time:
    tail -f /var/log/syslog
    ```
    
- **`grep`**: Filter logs for specific keywords (e.g., "error").
    
    ```
    grep -i "error" /var/log/syslog
    ```
    

### **Advanced Tools**

- **`journalctl`**: For systems using `systemd` (views logs from the journal).
    
    ```
    journalctl -u nginx.service   # Logs for a specific service
    journalctl -f                 # Follow logs in real-time
    journalctl --since "2024-01-01" --until "2024-01-02"
    ```
    
- **`multilog`**: For daemontools-based services.
- **`logrotate`**: Manage log rotation (not for viewing, but useful for maintenance).

---

### **3. Examples**

### **Check Authentication Failures**

```
grep "Failed password" /var/log/auth.log
```

### **Monitor Apache Errors in Real-Time**

```
tail -f /var/log/apache2/error.log
```

### **View Systemd Service Logs**

```
journalctl -u sshd --since "10 minutes ago"
```

---

### **4. GUI Tools (Optional)**

- **GNOME Logs**: A graphical log viewer for desktop environments.
- **Logwatch**/**GoAccess**: Generate summarized log reports.

---

### **5. Security & Permissions**

- Use `sudo` if you lack permission to view logs:
    
    ```
    sudo less /var/log/secure
    ```
    
- Logs may be compressed (e.g., `.gz`) after rotation. Use `zcat` or `zgrep`:
    
    ```
    zcat /var/log/syslog.1.gz
    ```
    

---

### **6. Troubleshooting Tips**

- **Check timestamps**: Correlate events with the server’s time zone.
- **Look for patterns**: Errors, warnings, or repeated failures.
- **Correlate multiple logs**: Cross-reference `/var/log/syslog`, `auth.log`, and service-specific logs.

---

### **7. Log Management**

- Use tools like **Logrotate** to prevent logs from consuming disk space.
- For centralized logging, consider **ELK Stack** (Elasticsearch, Logstash, Kibana) or **Graylog**.

---

By mastering these tools, you can efficiently diagnose server issues, monitor activity, and maintain system health.