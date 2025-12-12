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
- Merge veya rebase sırasında

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