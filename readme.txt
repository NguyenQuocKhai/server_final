STEP 1: Download and Activate Virtual Environment
sudo apt-get install -y python3-venv
python3 -m venv /home/venv
source /home/venv/bin/activate

STEP 2: Install, setup jadx and java
sudo apt-get install -y openjdk-17-jdk
Download jadx 1.3.0 ở https://github.com/skylot/jadx/releases?page=2
mkdir jadx
mv jadx-1.3.0.zip jadx
cd jadx
unzip jadx-1.3.0.zip
rm jadx-1.3.0.zip
sudo ln -s $(pwd)/bin/jadx /usr/local/bin/jadx
sudo ln -s $(pwd)/bin/jadx-gui /usr/local/bin/jadx-gui

STEP 3: Install SDK
mkdir -p $HOME/Android/Sdk/cmdline-tools/latest
cd $HOME/Android/Sdk/cmdline-tools/latest
wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -O commandlinetools.zip
unzip commandlinetools.zip
rm commandlinetools.zip
mv cmdline-tools/* .
rm -r cmdline-tools/
nano ~/.bashrc
# add lines into file .bashrc
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/build-tools/34.0.0
####################
source ~/.bashrc
sdkmanager --sdk_root=$ANDROID_HOME "build-tools;34.0.0"

STEP 4: Run the file requirement.sh inside folder code_static
./requirement.sh

STEP 5: Create a directory called "uploads" inside the folder "server_final"
cd server_final
mkdir uploads

STEP 6: Run file server apache2, nodejs, and file monitor.sh
sudo systemctl start apache2
node server.js (inside directory "server")
./monitor.sh (inside directory "scan")
