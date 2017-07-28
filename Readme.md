# Fix Instruction for Realtek rtl8723be (Weak Signal / Automatic Disconnection)

The problem is caused becuase the default drivers are looking for the connection on the wrong antenna on the network card.

Open Teminal and Execute the following code:

```
git clone https://github.com/technosap/rtlwifi_new
cd rtlwifi_new/
make clean
make
sudo make install
sudo modprobe -rv rtl8723be
```

Next, you have to reload the drivers with the correct antenna selection by adding an argument ant_sel which ranges from 0 to 5. Try with each value and check if the connection is working. If not remake and reinstall and try with a different value of ant_sel. My issue was fixed with ant_sel=2.

```
sudo modprobe -v rtl8723be ant_sel=2
```

Finally run the following command with your working value of ant_sel to make changes permanent. Remember to repeat the entire process after every kernel update. Note this is a temporary fix until a permanent solution is provided by ubuntu.

```
echo "options rtl8723be ant_sel=2" | sudo tee /etc/modeprobe.d/rtl8723be.conf
```


Note: The original drivers are by lwfinger: https://github.com/lwfinger/rtlwifi_new
