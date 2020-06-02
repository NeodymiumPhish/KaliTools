# Nmap

Table of Contents
=================

 * [Target can be in almost any format:](#target-can-be-in-almost-any-format)
 * [Selecting port](#selecting-port)
 * [Scan Types](#scan-types)
 * [Service and OS Detection Flags](#service-and-os-detection-flags)
 * [Nmap Scripting Engine (NSE)](#nmap-scripting-engine-nse)
 * [Nmap Output](#nmap-output)


# Nmap "Network Mapper"

` nmap [Options] {Target}`

### Target can be in almost any format:

`sub.domain.com; domain.com/24; 192.168.1.1; 192.168.1.0-255; 192.168.1.0/24; `

`-iL <filename>` - reference a list of targets

`--exclude <targets>` or `--excludefile <filename>` to ignore host(s)

### Selecting port

To specify one or more ports for scanning, simply use `-p` and then the port(s)

```bash
nmap -p 3389 192.168.1.1
nmap -p 22-100 192.168.1.1
nmap -p 22,135,445,3389 192.168.1.1
```

The "fast" port scan option selects the 100 most common ports

```bash
nmap -F 192.168.1.1
```

For all ports, use `-p-` to scan all 65535 ports

```bash
nmap -p- 192.168.1.1
```



### Scan Types

Nmap (when run with `sudo`) can also scan using multiple methodologies.  For example, nmap can conduct a full TCP handshake using `-sT` or just scan UDP ports with `-sU`.  By default, nmap will conduct a TCP SYN scan `-sS` if nothing is specified.

```bash
nmap -sT 192.168.1.1	# TCP Connect
nmap -sS 192.168.1.1	# TCP SYN
nmap -sU 192.168.1.1	# UDP scan
```



### Service and OS Detection Flags

Nmap keeps definitions of services and operating systems and uses these definitions to identify which services and systems are running on target ports.  This includes the ability to identify which version of some services are running.

```bash
nmap -A 192.168.1.1		# Detects Operating System and all Services
nmap -sV 192.168.1.1	# Detects all software and version numbers 
```



### Nmap Scripting Engine (NSE)

Nmap also has the ability to run scripts using it's very simple NSE.  By default, nmap is updated will a great selection of scripts that can be run directly via nmap by simply calling their name.  

nmap's script flag can accept individual scripts from it's library in `/usr/share/nmap/scripts/` or providing just the name of a category will run all scripts that fall within that category.

```bash
nmap -sV --script smb-vuln-ms17-010 192.168.1.1		# Scans for all service versions and the checks for the EternalBlue vulnerability
nmap -sV --script vuln 192.168.1.1					# Runs all of the vulnerability nmap scripts
nmap --script ~/custom_script.nse 192.168.1.1		# Runs custom NSE script file
nmap --script asn-query,whois 192.168.1.1			# Runs lookups against the IP address
```



### Nmap Output

Nmap understands that you may want to run scans and review the results for further information later.  As such, there are multiple options for outputting the results.

```bash
nmap -oX <file_name>.xml target.com			# Outputs results to an XML
nmap -oN <file_name>.txt target.com			# Outputs results to a txt file
nmap -oG <file_name>.txt target.com			# Outputs as txt file that's easy to grep
nmap -oA <file_name> target.com				# Outputs in all formats
```

