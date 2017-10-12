Digipulse Larva Release
-----------------------
This guide will cover the necessary information on how to setup and test the Digipulse Alpha version, codename *Larva*.



Alpha release terms, conditions and meaning
-------------------------------------------
This release is published as *alpha release*. This describes the development status as the first complete public version of our application, wich could be unstable, but is useful to show what the product will do to the initial investors and contributors of Digipulse. Bugs could still occur, and no warranty is given on any of the published code.

To avoid flooding the network, the *larva release* will be limited to the following specs:

  - 100Mb file size limited.
  - No custom dead man switches.
  - All files will be released after 30 minutes.
  - Nodes will not be payed during the *alpha stage* but can share their free space to provide network stability
  - The backend code of our core application will not be disclosed until the ***drone release*** to prevent copycats.

The alpha version will allow you to execute and perform following actions:

  - Join the network as `dpg-node` and share their drives on the network.
  - Create a personal `vault`, store files inside it and make it inheritable.
  - Dead man swith is only available directly to the inheritor's email address during *alpha stage*.



  

Join the network as node
------------------------
During the alpha version, the `dgp-node` application will only run in commandline version. The graphical version will be released during the *drone release*.

Make sure you have the following prerequisites installed:

* Git
* Node.js LTS (6.11.x)
* NPM
* Python 2.7
* GCC/G++/Make

### Node.js + NPM

#### GNU+Linux & Mac OSX

```
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
```

Close your shell and open an new one. Now that you can call the `nvm` program,
install Node.js (which comes with NPM):

```
nvm install --lts
```

#### Windows

Download [Node.js LTS](https://nodejs.org/en/download/) for Windows, launch the
installer and follow the setup instructions. Restart your PC, then test it from
the command prompt:

```
node --version
npm --version
```

### Build Dependencies

#### GNU+Linux

Debian based (like Ubuntu)
```
apt install git python build-essential
```

#### Mac OSX

```
xcode-select --install
```


#### Windows

```
npm install --global windows-build-tools
```

Once build dependencies have been installed for your platform, install the
package globally using Node Package Manager:

```
npm install --global dgpnode-daemon
```


## Usage (CLI)

Once installed, you will have access to the `dgpnode` program, so start by
asking it for some help.

```
dgpnode --help

  Usage: dgpnode [options] [command]


  Commands:

    start       start a node
    stop        stop a node
    restart     restart a node
    status      check status of node(s)
    logs        tail the logs for a node
    create      create a new configuration
    destroy     kills the node
    killall     kills all shares and stops the daemon
    daemon      starts the daemon
    help [cmd]  display help for [cmd]

  Options:

    -h, --help     output usage information
    -V, --version  output the version number
```

You can also get more detailed help for a specific command.

```
dgpnode help create

  Usage: dgpnode-create [options]

  generates a new share configuration

  Options:

    -h, --help                 output usage information
    --storj <addr>             specify the STORJ address (required)
    --key <privkey>            specify the private key
    --storage <path>           specify the storage path
    --size <maxsize>           specify share size (ex: 10GB, 1TB)
    --rpcport <port>           specify the rpc port number
    --rpcaddress <addr>        specify the rpc address
    --maxtunnels <tunnels>     specify the max tunnels
    --tunnelportmin <port>     specify min gateway port
    --tunnelportmax <port>     specify max gateway port
    --manualforwarding         do not use nat traversal strategies
    --logdir <path>            specify the log directory
    --noedit                   do not open generated config in editor
    -o, --outfile <writepath>  write config to path
```

## Configuring the Daemon

The Storj Share daemon loads configuration from anywhere the
[rc](https://www.npmjs.com/package/rc) package can read it. The first time you
run the daemon, it will create a directory in `$HOME/.config/dgpnode`, so
the simplest way to change the daemon's behavior is to create a file at
`$HOME/.config/dgpnode/config` containing the following:

```json
{
  "daemonRpcPort": 45015,
  "daemonRpcAddress": "127.0.0.1",
  "daemonLogFilePath": "",
  "daemonLogVerbosity": 3
}
```

Modify these parameters to your liking, see `example/daemon.config.json` for
detailed explanation of these properties.

## Debugging the Daemon

The daemon logs activity to the configured log file, which by default is
`$HOME/.config/dgpnode/logs/daemon.log`. However if you find yourself
needing to frequently restart the daemon and check the logs during
development, you can run the daemon as a foreground process for a tighter
feedback loop.

```
dgpnode killall
dgpnode daemon --foreground
```



## License

Digipulse dgp-node for distrubuting data on the Digipulse network.  
Copyright (C) 2017 Digipulse

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see http://www.gnu.org/licenses/.
