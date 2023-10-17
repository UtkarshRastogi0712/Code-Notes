#C 
### Process:
_Server:_ 
1. Create socket
2. Bind to address
3. Listen for connections
4. Accept connection
5. Send/Receive data 
6. Close connection

_Client:_
1. Create socket
2. Connect to address
3. Send/Receive data
4. Close connection

### Components:

#### Includes:
```C
#include <stdio.h> //Standard input output
#include <stdlib.h> //Standard library functions
#includes <sys/types.h> //System data types and 
#include <sys/socket.h> //Socket functionality
#include <netinet/in.h> //Address information
```

#### Socket:
Socket is identified by a file descriptor in the File Descriptor Table (FDT) in UNIX pointing to a structure in memory. Identified by an integer.
```C
//int socket_descriptor = socket(protocol_famil, protocol type/semantic, protocol)
int socket_descriptor = socket(AF_INET, SOCK_STREAM, 0);
//AF_INET is for internet, SOCK_STREAM for TCP, and default 0 for protcol as TCP and internet are enough
```
>Families:
>- AF_INET: IPv4
>- AF_INET6: IPv6
>- PF_INET: Same as AF_INET

>Communication protocols:
>- SOCK_STREAM: TCP/stream socket (connection oriented)
>- SOCK_DGRAM: UDP/datagram socket (connectionless)
>- SOCK_RAW: raw socket
>- SOCK_SEQPACKET: sequenced packet socket
>- SOCK_RDM: reliable delivery messaged socket

#### Socket address:
```C
struct sockaddr_in server_address;
server_address.sin_family = AF_INET;
server_address.sin_port = htons(8080);
server_address.sin_addr.s_addr = IN_ADDRANY; //any internet address 
```

#### Connect:
```C
//int connection = connect(socket, address_struct, address_struct_size)
int connection = connect(socket_descriptor, (struct sockaddr*)&serveraddress, sizeof(serveraddress));
if(connect == -1){
printf("Error");
}
```

### Related functions:
#### Byte Ordering:
Fixes the byte ordering disparity between host and network. (Little and Big Endian)
- htons() : host to network short (16 bits)
- htonl() : host to network long (32 bits)
- ntohs() : host to network short(16 bits)
- ntohl() : host to network long (32 bits)