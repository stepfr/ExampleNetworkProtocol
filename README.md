# Example Network Protocol
[![python versions](https://img.shields.io/badge/python-3.6%20%7C%203.7-blue.svg)](https://www.python.org/)
[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://github.com/stepfr/ExampleNetworkProtocol/blob/master/LICENSE)

The Example Network Protocol is an **artificial** network-based communication protocol.
It is **not designed** to be used in productional scenarios!

It comprises *peculiarities* observed in common industrial communication protocols as well as in Internet protocols.
Examples for those protocols are *Profinet IO* and *OPC UA* as well as *Ethernet* and *TCP*.

The Example Network Protocol is designed to be useful for tool developers.
Use cases taken into account are
- Protocol learning tools, 
- Protocol implementation frameworks and
- Protocol meta model design.

With the Example Network Protocol, developers have a reference protocol to design, implement and test their implementation against.
The general idea in behind is:

> *A tool that is able to handle the Example Network Protocol is able to handle every imaginable network protocol.*


## Publications

For detailed information about the Example Network Protocol, please also refer to the following publication:

**Design of an Example Network Protocol for Security Tests Targeting Industrial Automation Systems**
Steffen Pfrang, Mark Giraud, Anne Borcherding, David Meier and Jürgen Beyerer
*ICISSP Workshop ForSE 2019*

The paper will be presented at the [ICISSP Workshop ForSE 2019](https://www.icissp.org/) (23–25 February, 2019) and be available soon.
The same goes for the source code.


## Example scenarios

This repository contains an implementation of the Example Network Protocol using Python and Scapy.
Additionally, we provide network packet captures (pcaps) showing the behavior of the Example Network Protocol in the following scenarios:

* **Scenario 1:** 
In this scenario the following actions are performed by the client:
```
    1. Connect to server
    2. Create channel
    3. Create session ("Scenario1")
    4. Attach to session
    5. Send keep-alive
    6. Request random message from server
    7. Request active channels via TCP
    8. Request active channels via UDP
    9. Delete session
    10. Close channel
    11. Disconnect from server
```	
	

* **Scenario 2:** 
In this scenario the following actions are performed by the client:
```
    1. Connect to server
    2. Create channel
    3. Request active channels via TCP
    4. Request active channels via UDP
    5. Set maximum channel count to 2
    6. Close channel
    7. Wait 2 seconds
    8. Create channel
    9. Create session ("Scenario2")
    10. Attach to session
    11. Repeat 5 times:
        1. Wait 2 seconds
    	2. Send keep-alive
    12. Repeat 100 times:
    	1. Send random data to server
    	2. Request random data from server
    13. Delete session
    14. Request active channels via TCP
    15. Request active channels via UDP
    16. Close channel
    17. Disconnect from server
```


## Differences between paper and implementation

There are some minor differences between the description of the Example Network Protocol described in the paper referenced above and the current implementation state.
These differences include:
* RT communication:  
The `send_RT` function is not yet implemented. But it is possible to use UDP-based communication via the `send_udp` function. This function is used in both demonstration scenarios, as shown above.
* Implemented fields:  
The `DynamicLengthVariableRuleField` is not yet implemented.


## Requirements

* [python>=3.6](https://www.python.org/)
* [scapy>=2.4](https://scapy.net/)


## Installation

This is an example showing how to install the Example Network Protocol on Ubuntu using python-venv:

Install dependencies:
```	
    $ sudo apt install git python3 python3-venv
```
Clone project:

```
    $ git clone https://github.com/stepfr/ExampleNetworkProtocol.git
    $ cd isuproto
```
Create and activate Python venv:
```
    $ python3 -m venv venv
    $ source ./venv/bin/activate
```
Install scapy in venv:
```
    $ pip install scapy
```
Install isuproto:
```
    $ python3 setup.py install
```

## Run server & client examples

The implementation provides a sample server and client. 
After starting the server, it is waiting for a client to connect. 
After starting the client, multiple requests and state changes will be executed.
 
To perform the examples, first start server and then the client in separate terminals.

1. Activate venv and start server:
```	
    $ source ./venv/bin/activate
    $ python3 ./proto/server.py
```
2. Activate venv and start client:
```
    $ source ./venv/bin/activate
    $ python3 ./proto/client.py	
```
