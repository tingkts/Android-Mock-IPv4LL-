add mock/lite IPv4LL mechanism to android ethernet-service



<u>Rough concept of IPv4LL</u>:

		IP: 		  169.254.*.*
		Broadcast: 	  169.254.255.255
		Mask:		  255.255.0.0
		DNS, Gateway  null
	
		or
		
		IP:			  169.254.*.*/16


​		

<u>Codebase of ethernet-service related</u>:

- client side manager @ client app process

```
        frameworks/base/core/java/android/net/
            ConnectivityManager.java		
            EthernetManager.java		
            DhcpInfo.aidl	
            DhcpInfo.java	
            DhcpResults.aidl
            DhcpResults.java	
```

- server service @ system_server	

            frameworks/base/services/core/java/com/android/server/
                ConnectivityService.java	
    
            frameworks/base/services/core/java/com/android/server/net/
                IpConfigStore.java
    
            frameworks/base/services/net/java/android/net/dhcp/
                DhcpClient.java
    
            frameworks/base/services/net/java/android/net/ip/
                IpClient.java

- server side service @ ethernet-service

  ```
  
      frameworks/opt/net/ethernet/java/com/android/server/ethernet/
          EthernetConfigStore.java
          EthernetNetworkFactory.java
          EthernetService.java
          EthernetServiceImpl.java
          EthernetTracker.java
      
      
      
  ```

<u>Related process/file</u>:

```
    process: 
        netd
        system_server

    file:	
        /data/misc/ethernet/ipconfig.txt //static ip storage place
        
        
        
```

<u>Patch</u>:

```
	frameworks/opt/net/ethernet
```


<u> To-Do</u>:

- Use random number algorithm to generate the last two code address of IPv4LL.
- Add ARP check to avoid IP conflicts.

