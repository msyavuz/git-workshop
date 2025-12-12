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
