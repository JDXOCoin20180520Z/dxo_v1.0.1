# DXO_ver1.0.1 VPS Setup Guide.(Author by DXO_Tacco)

## Step1. Prepare system program and Ubuntu Update.
<pre><code>
apt-get install nano unzip libzmq5 software-properties-common -y && apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev -y && apt-get install libboost-program-options-dev libboost-test-dev libboost-thread-dev -y && apt-get install libminiupnpc-dev libzmq3-dev -y && add-apt-repository ppa:bitcoin/bitcoin && apt-get update && sudo apt-get install libdb4.8-dev libdb4.8++-dev -y
</code></pre>

## Step2. Open Port.
<pre><code>
sudo ufw allow OpenSSH
sudo ufw allow 39320
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
</code></pre>

## Step3. Set Swap Drive.
<pre><code>
sudo dd if=/dev/zero of=/var/swap.img bs=2048k count=1000
sudo mkswap /var/swap.img
sudo swapon /var/swap.img

sudo chmod 0600 /var/swap.img
sudo chown root:root /var/swap.img
sudo nano /etc/fstab 
</code></pre>

Add to end of file Just Flow 1line.
<pre><code>
/var/swap.img none swap sw 0 0
</code></pre>


## Step4. Download and Unzip to Node files.
<pre><code>
wget https://github.com/dextrocoin/dextro/releases/download/2.0.2.1/dextro-v2.0.2.1-ubuntu_16.tar.gz
tar xvfz dextro-v2.0.2.1-ubuntu_16.tar.gz
</code></pre>

## Step5. Run Daemon and Set configuration.
Run Deamon once and Stop. For generating configuration files.
<pre><code>
./dextrod -daemon
./dextro-cli getinfo
./dextro-cli stop

nano .dextro/dextro.conf
</code></pre>

Insert into the configuration file.
To match your masternode configuration.
<pre><code>
rpcallowip=127.0.0.1
rpcuser=[ANY_LONG_USERNAME]
rpcpassword=[ANY_LONG_PASSWORD]
staking=1
server=1
listen=1
port=39320
masternode=1
masternodeaddr=[IP]:39320
externalip=[IP]:39320
masternodeprivkey=[Your generate Masternode private key]
</code></pre>

※ Example
<pre><code>
rpcallowip=127.0.0.1
rpcuser=93XdextroP01983231
rpcpassword=93XdextroP01983231xGoodDxo
staking=1
server=1
listen=1
port=39320
masternode=1
masternodeaddr=182.65.15.65:39320
externalip=182.65.15.65:39320
masternodeprivkey=6JueftAf8teJPMVjpygmBvrZ8h1kNiVhPxhePc1CP8gqaJPXUAR
</code></pre>

## Step7. Run Daemon and Checking Block.
<pre><code>
./dextrod -daemon
</code></pre>

※ Check the node information in real time with the command below.
<pre><code>
watch ./dextro-cli getinfo

watch ./dextro-cli  masternode status

watch ./dextro-cli  mnsync status
</code></pre>

※ Local wallet set [masternode.conf] and Restart.

※ Wait a few minutes and Open Local Wallet Console. 

※ Run to MN Start Command.

<pre><code>
masternode start-alias [MASTERNODE_ALIAS]
</code></pre>



