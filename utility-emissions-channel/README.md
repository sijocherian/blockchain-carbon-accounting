# utility-emissions-channel

This project implements the [Utility Emissions Channel](https://wiki.hyperledger.org/display/CASIG/Utility+Emissions+Channel) use case.

Running the Code
================

First, install [minifabric](https://github.com/litong01/minifabric).  If you're new to minifabric, these [training videos](https://www.youtube.com/playlist?list=PL0MZ85B_96CExhq0YdHLPS5cmSBvSmwyO) are very helpful for getting familiar with it.

Then, copy minifab to your ``bin/`` directory, so you can run it from this directory.  Use minifabric to set up your network and channels:

    $ minifab up -o auditor1.com
    $ minifab create -c utilityemissions
    $ minifab join

You can then check the status of your network with

    $ minifab stats

See all your docker contains

    $ docker ps

This will create your channel configuration file in ``./vars/utilityemissions_config.json``

    $ minifab channelquery

Next install the chaincode.  You can start with the Node.js chaincode.  Go to the ``minifabric`` directory and follow these steps:

    $ mkdir vars/chaincode/emissions/node
    $ cp -r ~/hyperledger/blockchain-carbon-accounting/utility-emissions-channel/chaincode/node vars/chaincode/emissions/node
    $ ./minifab install -n emissions -l node
    $ ./minifab approve -n emissions
    $ ./minifab commit -n emissions

This doesn't work yet::

    $ ./minifab initialize
    $ ./minifab invoke -p '"recordEmissions", "BigUtility", "MyCompany", "2020-06-01", "2020-06-30", "15000", "KWH"'
  