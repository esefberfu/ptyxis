# Container tabanlı geliştirme

Bu fork, Ptyxis'i host sistemini kirletmeden derlemek için container tabanlı
bir build ortamı içerir. Derleme container içinde yapılır; çalıştırma host'ta.

## Gereksinimler

- `docker`
- `git`

## Kullanım

```bash
./dev build-image   # build image'ini oluştur (ilk kez / Dockerfile değişince)
./dev setup         # meson setup (prefix=build/install, development=true)
./dev run           # derle + kur, sonra HOST'ta çalıştır
```

Geliştirme sürümü `org.gnome.Ptyxis.Devel` app-id'siyle çalışır, böylece
sistemde kurulu Ptyxis ile yan yana açılabilir.

Diğer komutlar: `./dev compile`, `./dev install`, `./dev test`, `./dev shell`,
`./dev clean`. Sistemdekini değiştirecek release build için: `./dev release`.

## Bu fork'taki özellik

**Copy on Select** — Tercihler → Behavior → Clipboard altından açılır. Açıkken,
terminalde metin seçer seçmez otomatik olarak panoya kopyalanır.
