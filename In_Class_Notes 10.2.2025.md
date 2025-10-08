# Binary and Networking Basics
### Private IP Address Ranges (RFC 1918)

| Range                             | CIDR  | Common Usage              |
| --------------------------------- | ----- | ------------------------- |
| `192.168.0.0` – `192.168.255.255` | `/16` | Home & small networks     |
| `172.16.0.0` – `172.31.255.255`   | `/12` | Mid-size private networks |
| `10.0.0.0` – `10.255.255.255`     | `/8`  | Large enterprise networks |

These addresses are not routable on the public internet and are used internally.
### Binary
- **Binary** is **Base-2** (only `0` and `1`)
- Each bit is a **switch** for a power of 2
- A full **byte** = 8 bits. Max value for a byte is **255**
- IPv4 Address = 32 bits = 4 bytes = 4 "octets" (e.g., `192.168.10.5`)
---
### Byte Breakdown Table (Each Bit's Value)
Use these bit switches to decode values that are encoded in 8-bit binary (IP addresses, subnet masks, permissions, etc.)

| Bit Position | 2⁷  | 2⁶  | 2⁵  | 2⁴  | 2³  | 2²  | 2¹  | 2⁰  |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| Value (On)   | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| Bit Switches |     |     |     |     |     |     |     |     |
| **Total**    |     |     |     |     |     |     |     |     |
**How to Use It**
- Read bit positions **left to right**
- For each bit, write a `1` (on) or `0` (off) in the "Bit Switches" row.
- A bit set to `1` means **“switch on”**—add the corresponding value.
- A bit set to `0` means the value is ignored.
- All on values (Total) should equal the encoded number.
- The row of bit switches is the **binary representation** of that number.

---
### Convert IP to Binary: `192.168.10.5`

| Octet | Decimal | Binary     |
| ----- | ------- | ---------- |
| 1     | 192     | `11000000` |
| 2     | 168     | `10101000` |
| 3     | 10      | `00001010` |
| 4     | 5       | `00000101` |

**Binary Form:** `11000000.10101000.00001010.00000101`

---

### Convert Subnet Mask to CIDR

### Steps:

1. Convert each octet to binary.
    - e.g. `255.255.255.224` = `11111111.11111111.11111111.11100000`
2. Count all `1`s → `8 + 8 + 8 + 3 = 27`
3. Result: **CIDR notation** = `/27`

CIDR = how many bits are reserved for **network ID**, rest are for **host IDs**.

---
### Transforming  IP Address (Bytes) to Bits: `192.168.10.5`

#### **Octet 1: 192**

| Bit Position | 2⁷  | 2⁶  | 2⁵  | 2⁴  | 2³  | 2²  | 2¹  | 2⁰  |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| Value (On)   | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| Bit Switches | 1   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| **Total**    | 192 |     |     |     |     |     |     |     |
`11000000`

#### **Octet 2: 168**

| Bit Position | 2⁷  | 2⁶  | 2⁵  | 2⁴  | 2³  | 2²  | 2¹  | 2⁰  |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| Value (On)   | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| Bit Switches | 1   | 0   | 1   | 0   | 1   | 0   | 0   | 0   |
| **Total**    | 168 |     |     |     |     |     |     |     |
`10101000`

#### **Octet 3: 10**

| Bit Position | 2⁷  | 2⁶  | 2⁵  | 2⁴  | 2³  | 2²  | 2¹  | 2⁰  |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| Value (On)   | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| Bit Switches | 0   | 0   | 0   | 0   | 1   | 0   | 1   | 0   |
| **Total**    | 10  |     |     |     |     |     |     |     |
`00001010`
#### **Octet 4: 5**

| Bit Position | 2⁷  | 2⁶  | 2⁵  | 2⁴  | 2³  | 2²  | 2¹  | 2⁰  |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| Value (On)   | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| Bit Switches | 0   | 0   | 0   | 0   | 0   | 1   | 0   | 1   |
| **Total**    |     |     |     |     |     |     |     |     |
`00000101`

#### Final Result:

```
Binary:  11000000.10101000.00001010.00000101
Decimal:   192      .   168     .   10     .   5
```

#### Study References
- Binary Game (Cisco): [Binary Practice Game](https://learningcontent.cisco.com/games/binary/index.html)
- IPv4 Addressing: [IANA Private Address Space](https://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml)
- Subnetting: [AWS Subnet Basics](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
- CIDR Notation: [Wikipedia - CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)

### Steps to Convert  Subnet Mask to CIDR Block
1. **Write the subnet mask in binary**
    - Example:  
        `255.255.255.224` =  
        `11111111.11111111.11111111.11100000`
2. **Count all the 1s**
    - `8 + 8 + 8 + 3 = 27`
3. **CIDR suffix = Number of 1s**
    - So:  
        `255.255.255.224` → **`/27`**

Think of the subnet mask as a **ruler**. The number of `1`s in the mask (CIDR) tells you how much of the IP is **reserved for the network**, and how much is left for **hosts**.

### CIDR BLOCKS
**CIDR** = _Classless Inter-Domain Routing_
 **`/X` locks the first `X` bits as the network.**  
 The remaining `32 - X` bits are used for hosts.
 - Network bits (fixed): identify the subnet
 - Host bits (variable): identify IP addresses (assigned to devices) within that subnet

#### Which Parts of the IP Can Change?

| CIDR  | Fixed Bits | Variable Bits | Octets that can change |
| ----- | ---------- | ------------- | ---------------------- |
| `/8`  | First 8    | Last 24       | **2nd, 3rd, 4th**      |
| `/16` | First 16   | Last 16       | **3rd, 4th**           |
| `/24` | First 24   | Last 8        | **4th only**           |
| `/32` | All 32     | None          | **Exactly 1 IP**       |


**AWS Reserves 5 IPs in Each subnet:**

| Last Octet | IP Offset                  | Reserved For                       |
| ---------- | -------------------------- | ---------------------------------- |
| `.0`       | 0                          | Network Address (not assignable)   |
| `.1`       | 1                          | VPC Router (gateway)               |
| `.2`       | 2                          | DNS (Amazon DNS)                   |
| `.3`       | 3                          | Reserved for future use            |
| `.last IP` | Varies (CIDR /24 = `.255`) | Broadcast Address (not assignable) |

#### Calculating IP Availability
##### Available IPs = 2^(32 - CIDR) - 5
**`10.0.0.0/21`**
- CIDR = 21
- Total IPs: `2^(32 - 21)` = 2048
- Available IPs: `2048 - 5` = **2043**

**`192.168.10.0/29`**
- CIDR = 29
- Total IPs: `2^(32 - 29)` = 8
- Available IPs: `8 - 5` = **3**

**`172.16.0.0/19`**
- CIDR = 19
- Total IPs: `2^(32 - 19)` = 8192
- Available IPs: `8192 - 5` = **8187**

#### CIDR Chart for Total IPs

| CIDR | Total IPs | Available IPs (AWS) | Common Use Case                                   |
| ---- | --------- | ------------------- | ------------------------------------------------- |
| /32  | 1         | 0                   | Not valid for subnets                             |
| /31  | 2         | 0                   | Not valid for subnets                             |
| /30  | 4         | 0                   | Not valid for subnets                             |
| /29  | 8         | 3                   | Barely usable.                                    |
| /28  | 16        | 11                  | Tiny test environments or NAT gateway savings.    |
| /27  | 32        | 27                  | Small app subnet (1–2 EC2 tiers + NAT gateway)    |
| /26  | 64        | 59                  | Mid-size subnet for EC2 auto scaling groups       |
| /25  | 128       | 123                 | Larger subnet for DBs, ECS services, or growth    |
| /24  | 256       | 251                 | Standard-sized subnet for public/private zones    |
| /23  | 512       | 507                 | Medium-sized VPCs or multi-tier subnet groupings  |
| /22  | 1024      | 1019                | Growing applications with multiple AZ deployments |
| /21  | 2048      | 2043                | Large ECS/EKS clusters                            |
| /20  | 4096      | 4091                | Enterprise-scale workloads                        |
| /19  | 8192      | 8187                | Large-scale services or migration buffers         |
| /18  | 16384     | 16379               | Very large enterprise subnets                     |
| /17  | 32768     | 32763               | Massive regional workloads                        |
| /16  | 65536     | 65531               | **Entire VPC CIDR block (typical AWS maximum)**   |
|      |           |                     |                                                   |
> You can quickly memorize this chart for reference. Start by listing CIDRs from /32 to /16. Then, write 1 Total IP at /32 and double each step to reach 65,536 at /16. To calculate usable IPs in AWS, subtract 5 from the total IPs.

### Route Tables in AWS VPC
A **route table** is a set of **rules (routes)** that determine how traffic is directed within a VPC.
Each route consists of:
- **Destination**: A CIDR block
- **Target**: A gateway or network interface the traffic should be routed to

#### Default Local Route

```
172.31.0.0/16 → local
```

- Automatically created when a VPC is provisioned
- Ensures that any traffic matching the VPC’s CIDR block stays within the VPC
- Enables communication between subnets inside the same VPC

#### Internet Route (IGW)

```
0.0.0.0/0 → igw-xxxxxxxx
```

- This is a catch-all route for **all external traffic**
- Directs outbound traffic that does **not** match the VPC CIDR to the **Internet Gateway (IGW)**
- Required for **public subnets** to allow access to the internet
#### Example: Route Table Behavior

##### Internal VPC Traffic
**EC2 Instance A**: `172.31.1.10` → **EC2 Instance B**: `172.31.2.55`
- Traffic matches `172.31.0.0/16`
- Routed via the `local` rule
- Traffic stays inside the VPC (no gateway used)

##### Outbound Internet Traffic
**EC2 Instance B**: `172.31.2.55` → **External IP**: `34.10.0.166`
- Traffic does **not** match the `172.31.0.0/16` CIDR
- Routed via `0.0.0.0/0 → IGW`
- Sent to the Internet Gateway for external access
### **Three-Layer VPC Architecture**
Three-Layer VPC Architecture is an enterprise-grade  architecture that is used in production for scalability, maintainability, and layered security.
- The **Presentation layer** only handles routing and entry points.
- The **Application layer** isolates compute logic.
- The **Data layer** becomes _effectively unreachable_ from outside the VPC.

>Always **PAD** your architecture with **Presentation**, **Application**, and Data **layers**. Each layer should maintain its own subnet, network boundaries, and security groups. **Pushing private resources deeper into the architecture minimizes the attack surface, strengthens isolation, and enforces least-privilege access across all tiers.**
#### **1. Presentation Layer (Public Subnet)**
- **Purpose:** Exposes only the necessary endpoints to the internet.
- **Contains:**
    - Load Balancers (e.g., Application Load Balancer)
    - Bastion Host / Jump Box (optional for admin SSH access)
- **Routing:** Has an Internet Gateway (IGW) for inbound/outbound traffic.
---
#### **2. Application Layer (Private Subnet)**
- **Purpose:** Processes logic and handles requests between the frontend and fully isolated tiers.
- **Contains:**
    - EC2 application servers
    - ECS tasks, Lambda functions, or containerized workloads
- **Routing:** No direct internet access; inbound traffic **only from the public subnet** via ALB or bastion.
    - Uses a **NAT Gateway** in the public subnet for outbound updates if needed.
---
#### **3. Data Layer (Private Subnet)**
- **Purpose:** Stores and manages data securely.
- **Contains:**
    - Databases and data stores containing sensitive or business-critical information, such as RDS, DynamoDB, or self-managed databases.
    - Includes in-memory cache services like Reids or ElastiCache that support database performance and scalability.
- **Routing:** These resources must be fully isolated from the internet. Absolutely **no route to the internet**; accessible only through the application layer via tightly controlled security groups and private routing. 
---
#### **Security Group Flow for Three-Tier Architecture**
- **Public Layer (ALB / Bastion Host):**
    - The **ALB Security Group** allows inbound HTTP/HTTPS (ports **80/443**) from the internet.
    - It allows outbound traffic to the **Application Layer Security Group** (App SG) on the required ports (e.g., **80/443**).
- **Application Layer (EC2 / App Servers):**
    - The **App Security Group** allows inbound traffic **only from the ALB SG** on web ports (**80/443**).
    - It allows outbound traffic to the **Data Layer Security Group** (DB SG) on database or cache ports (e.g., **3306** for MySQL, **6379** for Redis).
- **Data Layer (RDS / ElastiCache / Databases):**
    - The **DB Security Group** allows inbound traffic **only from the App SG** on the specific service ports.
    - No inbound access from the internet or public layer.
    - Outbound access is typically restricted or limited to internal VPC communication.
---

### VPC Subnet-Segmentation
##$# Rob’s House of VPC (10.32.0.0/16, N. Virginia)

**Public Subnets (Presentation Layer)**
10.32.1.0/24 — Public Room A — us-east-1a  
10.32.2.0/24 — Public Room B — us-east-1b  
10.32.3.0/24 — Public Room C — us-east-1c  
10.32.4.0/24 — Public Room D — us-east-1d  
10.32.5.0/24 — Public Room E — us-east-1e  
10.32.6.0/24 — Public Room F — us-east-1f

**Private Subnets (Application Layer)**
10.32.11.0/24 — Politician Room A — us-east-1a  
10.32.12.0/24 — Politician Room B — us-east-1b  
10.32.13.0/24 — Politician Room C — us-east-1c  
10.32.14.0/24 — Politician Room D — us-east-1d  
10.32.15.0/24 — Politician Room E — us-east-1e  
10.32.16.0/24 — Politician Room F — us-east-1f

**Private Subnets (Data Layer)**
10.32.21.0/24 — Yakuza Room A — us-east-1a  
10.32.22.0/24 — Yakuza Room B — us-east-1b  
10.32.23.0/24 — Yakuza Room C — us-east-1c  
10.32.24.0/24 — Yakuza Room D — us-east-1d  
10.32.25.0/24 — Yakuza Room E — us-east-1e  
10.32.26.0/24 — Yakuza Room F — us-east-1f

#### **Subnet Logic
- The **second octet** defines the **VPC** (unique per environment).
	- 10.**32**.0.0/24
- The **third octet** defines **subnet roles**:
    - Single-digit (10.**1**.0.0/24) → Public subnet — internet-facing resources.
    - Double-digit (10.32.**11**.0/24) → Private subnet — internal-only resources.
- **Private subnets should never have direct internet access** — only indirect communication via bastion hosts, NAT gateways or load balancers (ALB/NLB).
---
#### **Example: Rob’s House of VPC (10.32.0.0/16 – N. Virginia)**

| **Layer / Tier**                | **Subnet CIDR**                       | **Nickname**             | **Purpose / Access**                                    |
| ------------------------------- | ------------------------------------- | ------------------------ | ------------------------------------------------------- |
| **Presentation Layer** (Public) | 10.32.**1**.0/24 → 10.32.**6**.0/24   | “Public Rooms (A–F)”     | Public entry points (ALBs, Bastion Hosts, etc.)         |
| **Application Layer** (Private) | 10.32.**11**.0/24 → 10.32.**16**.0/24 | “Politician Rooms (A–F)” | Internal compute layer (EC2s, app servers, cache tiers) |
| **Data Layer** (Private)        | 10.32.**21**.0/24 → 10.32.**26**.0/24 | “Yakuza Rooms (A–F)”     | Databases, storage, and sensitive systems               |

---
### **Run Your VPC like an Underground Subnet Syndicate**
> “Public rooms greet the world. Politicians handle business behind closed doors. The Yakuza run the vault — nobody gets in without permission.”