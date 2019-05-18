# GossipProtocol
GossipProtocol for Bitcoin + Hierarchy Derived Wallet with keys

Based on Boost::Asio this protocol established quick and efficient
connection management between nodes, so they can then share and send
messages(containing any data you want, using Boost::Serialization) 
among all nodes in a short time.

First of all MainNode on port 12345 is created. Then every other 
node connects to MainNode to become "friends" with it. Every node
can have only 6 friends, if a new request have been sent and friend
list is full, then requested node gives other node his friend list,
so now it can request them for friendship. With such an easy way 
all nodes can connect together in a very short time.

This protocol is multithreaded. Uses following threads:

-void run_connection_process()
        creates threads for other processes 
        and connects to all pending connections
        
-process_new_accept(boost::asio::yield_context yield)
        maintains all incoming connection requests and accepts them
	
-process_new_message()
        maintains all incoming messages and answers to them
	
-run_disconnection_process()
        from time to time disconnects random friend
	      used to prevent states when new node can't connect to anybody

-run_supporting_process()
        from time to time searches for unused conenctions and removes them
        and asks for someone to send friends if has not enough( 1 or 2 )

/**********************************************************************/

Hierarchy Derived Wallet + Keys

This repository contains HDWallet class, which uses asynchronous cryptography
in order to Encrypt and Decrypt messages and parse them through network.
This class uses Secp251k1 and OpenSSL crypto libraries and Boost::Serialization
to parse Public and Private Keys through network.
