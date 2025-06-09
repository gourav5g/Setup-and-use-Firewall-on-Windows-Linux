# Setup-and-use-Firewall-on-Windows-Linux
Setup of Firewall
# Task 4

---

## 🔧 TASK 4: Setup and Use a Firewall on Windows/Linux

### ✅ Objective:

Configure and test basic firewall rules to allow or block network traffic using either:

- **Windows Firewall** (on Windows)
- **Uncomplicated Firewall (UFW)** (on Linux)

---

## 🛡️ PART A: WINDOWS FIREWALL CONFIGURATION

### 1. Open Windows Firewall Advanced Settings

- Press `Win + R`, type `wf.msc`, and press Enter.
- You’ll see **Inbound Rules**, **Outbound Rules**, and **Connection Security Rules**.

### 2. List Current Inbound Rules

- Go to **Inbound Rules**.
- Scroll through the list to see active rules.

### 3. Add Rule to Block Inbound Traffic on Port 23 (Telnet)

- Click **New Rule** in the right pane.
- Choose **Port** → Next.
- Select **TCP** → Specific local ports: `23` → Next.
- Choose **Block the connection** → Next.
- Apply to all profiles (Domain, Private, Public) → Next.
- Name the rule: `Block Telnet (Port 23)` → Finish.

### 4. Test the Rule

Use PowerShell/CMD to try connecting to port 23 locally:

```bash
telnet localhost 23

```

> If blocked, you'll get a "connection refused" message.
> 

### 5. Allow SSH (Optional if Testing Remotely)

If you're using SSH to access the machine, ensure port 22 is allowed:

- Create a new rule like above, but choose **Allow the connection** and set port `22`.

### 6. Remove the Block Rule

- Go back to **Inbound Rules**.
- Right-click `Block Telnet (Port 23)` → Delete.

### 7. Document GUI Steps Used

Take screenshots of:

- The **Inbound Rules** list before and after adding the rule.
- The **Rule Properties** window showing the settings for blocking port 23.

---

## 🔐 PART B: LINUX UFW CONFIGURATION

### 1. Open Terminal and Check UFW Status

```bash
sudo ufw status verbose

```

### 2. List Current Rules

```bash
sudo ufw status numbered

```

### 3. Add Rule to Block Inbound on Port 23

```bash
sudo ufw deny 23/tcp

```

### 4. Test the Rule

From another machine or same system:

```bash
nc -zv <your-ip> 23

```

Or:

```bash
telnet <your-ip> 23

```

> Should time out or be denied.
> 

### 5. Allow SSH (Port 22)

```bash
sudo ufw allow 22/tcp

```

### 6. Remove the Rule

```bash
sudo ufw delete deny 23/tcp

```

### 7. Document Commands Used

Save output of:

```bash
sudo ufw status verbose

```

Take screenshot of terminal commands and outputs.

---

## 📁 DELIVERABLES

### For Submission:

1. **Screenshots**:
    - Before and after adding the block rule.
    - Output of `ufw status` or Windows Firewall inbound rules.
2. **Commands/Steps Used**:
    - Include exact CLI commands or GUI navigation steps.
3. **Test Results**:
    - Show failed attempts to connect to port 23 after blocking.
4. **Summary of How Firewalls Filter Traffic** (see below).

---

## 📚 INTERVIEW QUESTIONS & ANSWERS

### 1. **What is a firewall?**

A **firewall** is a network security device that monitors and filters incoming and outgoing network traffic based on predefined security rules. It acts as a barrier between trusted internal networks and untrusted external networks (like the Internet).

---

### 2. **Difference between stateful and stateless firewall?**

- **Stateful**: Tracks the state of active connections and makes decisions based on context (e.g., allowing return traffic).
- * Stateless**: Filters packets individually without considering the context or connection state.

---

### 3. **What are inbound and outbound rules?**

- **Inbound Rules**: Control traffic coming **into** your system from external sources.
- **Outbound Rules**: Control traffic going **out** from your system to external destinations.

---

### 4. **How does UFW simplify firewall management?**

UFW (Uncomplicated Firewall) provides a **user-friendly interface** to manage `iptables` in Linux. It allows users to define rules with simple commands (e.g., `allow`, `deny`, `limit`) without dealing with complex `iptables` syntax.

---

### 5. **Why block port 23 (Telnet)?**

Telnet sends data in **plaintext** (no encryption), making it vulnerable to eavesdropping. Blocking port 23 prevents insecure remote access and encourages use of secure alternatives like SSH (port 22).

---

### 6. **What are common firewall mistakes?**

- Allowing too much traffic (overly permissive rules).
- Not testing rules before deployment.
- Misconfigured default policies (e.g., allowing all instead of denying all).
- Forgetting to log or monitor traffic.
- Leaving unnecessary services exposed.

---

### 7. **How does a firewall improve network security?**

A firewall improves security by:

- Preventing unauthorized access.
- Filtering malicious traffic.
- Enforcing access control policies.
- Providing visibility into network activity.
- Mitigating DDoS and intrusion attempts.

---

### 8. **What is NAT in firewalls?**

NAT (Network Address Translation) allows multiple devices on a private network to share a single public IP address. In firewalls, NAT hides internal IPs from the outside world, enhancing privacy and security.

---

## 📝 SUMMARY: How Firewalls Filter Traffic

Firewalls filter traffic by:

- Inspecting packet headers (source/destination IP, port, protocol).
- Comparing against defined **rules** (allow/deny/block).
- Applying **default policies** (e.g., deny all unless allowed).
- Using **stateful inspection** to track ongoing sessions.
- Controlling **inbound** and **outbound** traffic separately.
