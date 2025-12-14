---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

# **Git/Github ve Açık Kaynak Yazılım**

--- 

# Neden Git?

Git kullanmadan ekip çalışması yaptınız mı?
- Adları ‘final’, ‘final2’, ‘final_son_bu’, ‘final_son_son’ olan dosyalar
- Hiç bir dosyanın önceki haline geri dönme ihtiyacınız oldu mu?

---

# Neden Git?

Git kullanmadan ekip çalışması yaptınız mı?
- Adları ‘final’, ‘final2’, ‘final_son_bu’, ‘final_son_son’ olan dosyalar
- Hiç bir dosyanın önceki haline geri dönme ihtiyacınız oldu mu?


Git ve diğer versiyon kontrol sistemleri bu sorunlara çözüm bulmak amacıyla oluşturulmuştur.

---

# Git kurulumu

[https://git-scm.com/install](https://git-scm.com/install)
![gitss](./assets/gitss.png)

---

# Repository

Bir projenin tüm dosyalarının, geçmiş kayıtlarının (commit'lerin) ve ayarlarının saklandığı yerdir. 

- Mevcut bir klasörde repo oluşturmak için:
```bash
git init
```

- Bir repoyu bilgisayara klonlamak için:
```bash
git clone https://github.com/apache/superset.git
```

---

# Repository

- Git sadece dosyalar üzerinde çalışır. İçi boş bir klasör git için bir şey ifade etmez.
- Repo klasöründe `.gitignore` isimli bir dosya oluşturarak bazı dosyaları göz ardı edebilirsiniz.

```
node_modules
.env
.venv
```

---

# Commit

Yaptığınız değişikliklerin kaydedilmiş bir anlık görüntüsü. Checkpoint ya da kayıtlı oyun gibi düşünebilirsiniz.

```bash
git commit -m "Commit mesajı"
```

---

# Branch

Belirli bir commiti işaret eden küçük bir işaretçidir. Her yeni commit ile ileri taşınır.

- Yeni bir branch oluşturmak için:
```bash
git branch msyavuz/feat/implement-sync
```

- Branch silme

```bash
git branch -d msyavuz/feat/implement-sync
```

---
![Branch visual](./assets/branch-example.png)

---

# Merge

İki branch'i birleştirmenin en yaygın yolu. Yeni bir "merge commit" oluşturur.

```bash
git checkout main
git merge feature-branch
```

**Özellikleri:**
- Tüm geçmiş korunur
- Merge commit ile kim, ne zaman birleştirdi görülür
- Branch yapısı karmaşık olabilir

---

# Merge Örneği

```
main:     A---B---C---F (merge commit)
               \     /
feature:        D---E
```

Feature branch'teki D ve E commit'leri main'e merge edildiğinde F merge commit'i oluşur.

---

# Rebase

Branch'inizi başka bir branch'in üzerine "yeniden temellendirir". Commit'leri yeniden yazar.

```bash
git checkout feature-branch
git rebase main
```

**Özellikleri:**
- Temiz, lineer geçmiş
- Merge commit yok
- Public branch'lerde tehlikeli!

---

# Rebase Örneği - Önce

```
main:     A---B---C
               \
feature:        D---E
```

---

# Rebase Örneği - Sonra

```
main:     A---B---C
                   \
feature:            D'---E'
```

D ve E commit'leri C'nin üzerine yeniden yazılır (D' ve E' olur).

---

# Merge vs Rebase - Ne Zaman Merge?

- Public/paylaşılan branch'lerde
- Geçmişi korumak istediğinizde
- Takım çalışmalarında güvenli seçenek

---

# Merge vs Rebase - Ne Zaman Rebase?

- Local feature branch'lerde
- Temiz geçmiş istediğinizde
- Push etmeden önce main ile senkronize olurken

---

# Interactive Rebase

Rebase yaparken her commiti editleyerek devam etmenizi sağlar

```bash
git rebase -i HEAD~3  # Son 3 commit'i düzenle
```

Seçenekler:
- **pick**: Commit'i koru
- **reword**: Commit mesajını değiştir
- **squash**: Önceki commit ile birleştir
- **drop**: Commit'i sil

---

# Merge Conflict Nedir?

Git aynı dosyanın aynı bölümünde farklı değişiklikler olduğunda otomatik birleştirme yapamaz.

**Ne zaman oluşur:**
- İki branch aynı satırı değiştirdiğinde
- Bir branch dosyayı silerken diğeri düzenlediğinde

---

# Conflict İşaretleri

```diff
<<<<<<< HEAD
console.log("Main branch kodu");
=======
console.log("Feature branch kodu");
>>>>>>> feature-branch
```

- `<<<<<<< HEAD`: Mevcut branch'teki kod
- `=======`: Ayırıcı
- `>>>>>>> feature-branch`: Merge edilen branch'teki kod

---

# Conflict Çözme - Adım 1 & 2

1. **Conflict'li dosyaları bul:**
```bash
git status
```

2. **Dosyaları düzenle** - İşaretleri kaldır, doğru kodu bırak

---

# Conflict Çözme - Adım 3 & 4

3. **Değişiklikleri ekle:**
```bash
git add dosya.txt
```

4. **Merge'ü tamamla:**
```bash
git commit
```

---

# Conflict Çözme İpuçları

- **Takım arkadaşınızla konuşun** - Hangi kod kalmalı?
- **Test edin** - Çözüm sonrası kod çalışıyor mu?
- **IDE araçlarını kullanın** - VS Code, IntelliJ conflict çözme araçları
- **git mergetool** - Görsel araçlar için

```bash
git mergetool
```

---

# Conflict'i İptal Etme

Merge'ü iptal etmek için:
```bash
git merge --abort
```

Rebase'i iptal etmek için:
```bash
git rebase --abort
```

Bu komutlar conflict öncesi duruma döndürür.

---

# Günlük Git İş Akışı

```bash
git status                   # Değişiklikleri kontrol et
git add .                    # Tüm değişiklikleri ekle  
git commit -m "Açıklama"     # Commit yap
git push origin main         # Remote'a gönder
```

---

# Git Add Detayları

```bash
git add dosya.txt            # Tek dosya ekle
git add .                    # Tüm değişiklikleri ekle
```

**Staging Area:** Commit öncesi değişikliklerin bekletildiği alan

---


# Git Stash

Değişiklikleri geçici olarak kaydet.

```bash
git stash                    # Değişiklikleri sakla
git stash list               # Stash listesi
git stash pop                # Son stash'i geri al
git stash apply              # Stash'i uygula (silme)
```

---

# Stash Kullanım Senaryoları

- **Acil bug fix:** Üzerinde çalıştığın feature'ı stashle
- **Branch değiştirme:** Commit'siz geçiş için
- **Deney:** Değişiklikleri geçici sakla

```bash
git stash save "WIP: login feature"
git stash drop stash@{0}    # Belirli stash'i sil
```

---

# Git Reset

Commit'leri geri al.

```bash
git reset --soft HEAD~1      # Son commit'i geri al (değişiklikler staged)
git reset --mixed HEAD~1     # Son commit'i geri al (unstaged)
git reset --hard HEAD~1      # Son commit'i tamamen sil
```

⚠️ **Dikkat:** `--hard` değişiklikleri kalıcı siler!

---

# Git Revert

Güvenli geri alma - yeni commit oluşturur.

```bash
git revert HEAD              # Son commit'i geri al
git revert <commit-hash>     # Belirli commit'i geri al
```

**Reset vs Revert:**
- Reset: Geçmişi değiştirir
- Revert: Geçmişi korur, yeni commit ekler

---

# Kayıp Commit'leri Kurtar

```bash
git reflog                   # Tüm HEAD hareketleri
git checkout <hash>          # Kayıp commit'e git
git cherry-pick <hash>       # Tek commit'i al
```

**Reflog:** Git'in geri dönüş sigortası

---

# Git Log ve Geçmiş

```bash
git log --oneline            # Özet görünüm
git log --graph --all        # Görsel branch yapısı
git log -p                   # Değişikliklerle birlikte
git blame dosya.txt          # Satır bazlı tarih
```

---

# Remote Repository

Uzak sunucudaki (GitHub, GitLab) Git repository'si.

```bash
git remote -v                # Remote'ları listele
git remote add origin URL    # Yeni remote ekle
```

---

# Fetch, Pull, Push

```bash
git fetch origin             # Değişiklikleri indir (birleştirme)
git pull origin main         # Fetch + Merge
git push origin main         # Commit'leri gönder
```

**İpucu:** Pull = Fetch + Merge

---

# Birden Fazla Remote

```bash
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git merge upstream/main
```

Fork edilmiş projelerle çalışırken kullanışlı.

---

# GitHub Nedir?

- **Git != GitHub**
- Git repository'lerini barındıran web servisi
- Sosyal kodlama platformu
- Microsoft'a ait (2018'den beri)

**Alternatifleri:** GitLab, Bitbucket, Gitea

---

# GitHub Özellikleri

- **Repository hosting**
- **Issues & Projects:** Proje yönetimi
- **Pull Requests:** Kod inceleme ve birleştirme
- **Actions:** CI/CD otomasyonu
- **Pages:** Statik site hosting
- **Gists:** Kod parçacıklarını paylaş

---

# README.md

Projenizin vitrini - ilk bakışta görülen dosya.

**Şunları içermeli:**
- Proje açıklaması
- Kurulum adımları
- Kullanım örnekleri
- Katkıda bulunma rehberi
- Lisans bilgisi

---

# GitHub - Fork ve Clone

**Fork:** Başka birinin projesini kendi hesabınıza kopyalama
**Clone:** Repository'yi bilgisayarınıza indirme

```bash
# Fork'u clone'la
git clone https://github.com/sizin-kullanici/proje.git
```

---

# Pull Request (PR)

Değişikliklerinizi orijinal projeye ekleme talebi.

**Adımlar:**
1. Fork yap
2. Branch oluştur
3. Değişiklik yap ve commit at
4. Push et
5. GitHub'da PR aç

---

# İyi PR Pratikleri

- **Açıklayıcı başlık ve açıklama**
- **Küçük, odaklı değişiklikler**
- **Test edilmiş kod**
- **Code review'a açık ol**
- **Proje kurallarına uy** (CONTRIBUTING.md)

---

# GitHub Issues

Hata bildirimi ve özellik istekleri için.

- Bug report
- Feature request
- Discussion
- Task tracking

**İpucu:** Issue numarasını issue için açtığın pr'a ekle: `fixes: #42`

---

# GitHub Actions

Otomatik iş akışları (CI/CD).

```yaml
name: Test
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: npm test
```

Her push'ta testler otomatik çalışır.

---

# Açık Kaynak'a Katkı

1. **İlgi alanında proje bul**
2. **Issues'ları incele** (good first issue)
3. **Fork et ve clone'la**
4. **Değişiklik yap**
5. **PR gönder**
6. **Geri bildirime açık ol**

---

# İyi Katkıda Bulunma Pratikleri

- **CONTRIBUTING.md oku**
- **Küçük başla** (typo, dokümantasyon)
- **Issue aç/sor** önce
- **Test yaz**
- **Commit mesajları kurallara uy**
- **Sabırlı ol** - review zaman alabilir

---

# Lisanslar

**Popüler açık kaynak lisansları:**

- **MIT:** En esnek, ticari kullanıma izin
- **Apache 2.0:** Patent korumalı
- **GPL:** Türevler de açık kaynak olmalı
- **BSD:** MIT benzeri, basit

Lisanssız = Tüm haklar saklı (kullanılamaz!)

---

# Teşekkürler!

**Sorularınız için:**
- GitHub: @msyavuz
- E-posta: salih.yavuz@proton.me

**Faydalı Kaynaklar:**
- [Pro Git Book](https://git-scm.com/book)
- [GitHub Docs](https://docs.github.com)

İyi kodlamalar! 🚀
