
# Git  Serftifica Tanımlaması
```
$ git config --global http.sslCAInfo sertifika_adı
```

# SSH Key Bağlantısı
```
ssh-keygen -t ed25519
```
çıkan seçenekleri boş bırak enter tuşuna basarak

açık anahtarını aşağıdaki komut ile gör 

```
cat .ssh/id_ed25519.pub
```

git kullanıcı profili yanındaki ayarlardan ssh key kısmına girip çıkan anahtarı yapışıtırp ekleyin.
