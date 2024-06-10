# µIDS
A simple Python-based network signature intrusion detection system.

## Required Packages
- `scapy`
- `netifaces`

## Installation and Testing
Clone the repository and set up a virtual environment:

```bash
git clone https://github.com/dreizehnutters/-IDS.git
cd '-IDS'
pipx install -r requirements.txt
sudo python3 main.py <INTERFACE> default.rules
```
Replace `<INTERFACE>` with your network interface, e.g., `wlp4s0`.

## Rules
Rules are defined in default.rules and eval.rules.

### Rule Structure

```python
PROTO [!]IP|any:[!]PORT(RANGE)|any <>|-> [!]IP|any:[!]PORT(RANGE)|any *PAYLOAD
```

### Example
```python
ICMP 192.168.178.22:any -> 1.1.1.1:[500-510] * # -IDS
```

### Explanation
+ `PROTO`: The protocol (e.g., ICMP, TCP, UDP).
+ `[!]IP|any`: Source IP address (use ! for negation, any for any IP).
+ `[!]PORT(RANGE)|any`: Source port (use ! for negation, specify range with [min-max], any for any port).
+ `<>|->`: Direction of traffic (<> for bidirectional, -> for unidirectional).
+ `[!]IP|any`: Destination IP address.
+ `[!]PORT(RANGE)|any`: Destination port.
+ `*PAYLOAD`: Payload pattern.
+ Comments in rules are indicated with #.