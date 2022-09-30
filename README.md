![image](https://user-images.githubusercontent.com/65338121/193364133-24f2da72-e8bb-4ff3-b979-461c8aa6ef7e.png)
#  TERP node qurulum rəhbəri 
Digər normal Cosmos proyektləri kimidir. 
# Minimum server istəyi
* 3x GPU
* 4GB RAM
* 80GB Disk

# Məsləhət olunan server istəyi
* 4x CP
* 8GB RAM
* 200 GB Dİsk

# Tək script istifadə edərək node qurulması. Sonra sizdən node adı istəyəcək. Yazıb bir yerə qeyd edin.
```bash
wget -O TERP.sh https://github.com/drkhayal/test.wiki.git && chmod +x TERP.sh && ./TERP.sh
```
# Qurulum sonrası addımlar.
Doğrulayıcının sinxron olduğundan əmin olmaq lazımdır. False yazarsa olmuş sayılır.
```bash
terpd status 2>&1 | jq .SyncInfo
```
#Cüzdan yaratma
Yeni cüzdan yaratdıqdan sonra mnemonici yadda saxlayın.
```bash
terpd keys add $TERP_WALLET
```
# Aktiv cüzdanınızı istifadə etmək üçün
```bash
terpd keys add $TERP_WALLET --recover
```
# Cüzdan adresi əlavə edin.
```bash
TERP_WALLET_ADDRESS=$(terpd keys show $TERP_WALLET -a)
TERP_VALOPER_ADDRESS=$(terpd keys show $TERP_WALLET --bech val -a)
echo 'export TERP_WALLET_ADDRESS='${TERP_WALLET_ADDRESS} >> $HOME/.bash_profile
echo 'export TERP_VALOPER_ADDRESS='${TERP_VALOPER_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```
# Doğrulayıcı yaratma
```bash
terpd tx staking create-validator \
  --amount 1999000uterpx \
  --from $TERP_WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(terpd tendermint show-validator) \
  --moniker $TERP_NODENAME \
  --chain-id $TERP_ID \
  --fees 250uterpx
```
# Lazım ola biləcək komandalar
 
# Logları kontrol etmə
```bash
journalctl -fu terpd -o cat
```
# Servisi başlad
```bash
systemctl start terpd
```
# Servisi dayandır
```bash
systemctl stop terpd
```
# Servisi restart et
```bash
systemctl restart terpd
```









