# [2025-06-05] ramips: mt7621: 采用 mt76 替代 mtwifi
- 切换前的commit:
https://github.com/coolsnowwolf/lede/tree/ec104e953b4967fedc0d7694aa0757048ed45638

- 恩山分享测试的commit:
https://github.com/coolsnowwolf/lede/tree/a8fa2567a15eb5ae4b91b115165c4a8efc81f75c
- 帖子:
https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8325659&highlight=AC2100



- image(MTWIFI)
```
define Device/xiaomi_mi-router-ac2100
  $(Device/xiaomi_nand_separate)
  DEVICE_MODEL := Mi Router AC2100
  IMAGE_SIZE := 120320k
  DEVICE_PACKAGES += kmod-mt7603e kmod-mt7615d luci-app-mtwifi \
	-wpad-openssl
endef
TARGET_DEVICES += xiaomi_mi-router-ac2100
```

- WiFi在断电重启后不能自动开启,添加本地启动脚本:
```
ifconfig rai0 up
ifconfig ra0 up
brctl addif br-lan rai0
brctl addif br-lan ra0
```