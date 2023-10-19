# mininet
## open terminal eq
```bash
xterm s1
```
## default topo
```bash
cd ~/mininet/custom
```
## script create network with 2 sw , 2 host
```bash
from mininet.topo import Topo

class MyTopo( Topo ):
    "Simple topology example."

    def build( self ):
        "Create custom topo."

        # Add hosts and switches
        Host1 = self.addHost( 'h1' )
        Host2 = self.addHost( 'h2' )
        Host3 = self.addHost( 'h3' )
        Host4 = self.addHost( 'h4' )
        Switch1 = self.addSwitch( 's1' )
        Switch2 = self.addSwitch( 's2' )

        # Add links
        self.addLink( Host1, Switch1 )
        self.addLink( Host2, Switch1 )
        self.addLink( Host3, Switch2 )
        self.addLink( Host4, Switch2 )
        self.addLink( Switch1, Switch2 )


topos = { 'mytopo': ( lambda: MyTopo() ) }
```
## script automatisation topo au dessus
```bash
from mininet.topo import Topo

class MyTopo( Topo ):
    "Simple topology example."

    def build( self ):
        "Create custom topo."

        # Add hosts and switches
        Host1 = self.addHost( 'h1' )
        Host2 = self.addHost( 'h2' )
        Host3 = self.addHost( 'h3' )
        Host4 = self.addHost( 'h4' )
        Switch1 = self.addSwitch( 's1' )
        Switch2 = self.addSwitch( 's2' )

        # Add links
        self.addLink( Host1, Switch1 )
        self.addLink( Host2, Switch1 )
        self.addLink( Host3, Switch2 )
        self.addLink( Host4, Switch2 )
        self.addLink( Switch1, Switch2 )


topos = { 'mytopo': ( lambda: MyTopo() ) }
```
## script create network with boucle
```bash
#!/usr/bin/python

from mininet.topo import Topo
from mininet.net import Mininet
from mininet.util import dumpNodeConnections
from mininet.log import setLogLevel

class SingleSwitchTopo( Topo ):
    "Single switch connected to n hosts."
    def __init__(self, n=2, **opts):
        #initialize topology and default options
        Topo.__init__( self, **opts)
        switch = self.addSwitch('s1')

        #Python's range(n) generates 0..n-1
        for h in range(n):
                host = self.addHost('h%s' % (h + 1))
                self.addLink(host, switch)

def simpleTest():
        "create and test a simple experiment"
        topo = SingleSwitchTopo(n=4)
        net = Mininet(topo)
        net.start()
        print "Dumping host connection"
        dumpNodeConnections(net.hosts)
        print "Testing network  connectivity"
        net.pingAll()
        net.stop() 

if __name__ == '__main__':
        # Tell mininet to rint usefull information
        setLogLevel('info')
        simpleTest()
```
## execution script
```bash
sudo python  ___.py
```
# OpenDaylight
```bash
sudo apt-get install openjdk-7-jdk
```
```bash
sudo apt-get install maven
```
## extract 
```bash
tar -xzvf distribution-karaf-0.3.2-Lithium.SR2.tar.gz
```
## run karaf
```bash
cd distribution-karaf-0.3.2-Lithium.SR2/bin
```
```bash
./karaf -of13
```
# Ryu
```bash
#!/bin/bash
#echo "step 1. install tools"
sudo apt-get -y install git python-pip python-dev

#echo "step 2. install python packages"
sudo apt-get -y install python-eventlet python-routes python-webob python-paramiko

#echo "step 4. Install RYO"
sudo pip install setuptools --upgrade
cd ryu;
sudo python ./setup.py install

#echo "Setup 5.install and upgrade python package"
sudo pip install six --upgrade
sudo pip install oslo.config msgpack-python
sudo pip install eventlet --upgrade
```

