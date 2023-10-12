# mininet
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
