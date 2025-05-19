## 🇺🇸/🇫🇷 Correction des erreurs `locale` (Perl, apt, etc.) sous Debian/Proxmox

### 📌 Symptôme

Erreurs comme :

```
perl: warning: Setting locale failed.
locale: Cannot set LC_CTYPE to default locale: No such file or directory
```

---

## ✅ Solution — Locale en anglais (`en_US.UTF-8`)

### 1. Générer la locale

```bash
dpkg-reconfigure locales
```

✔️ Active : `en_US.UTF-8 UTF-8`
✔️ Choisis comme **par défaut** : `en_US.UTF-8`

---

### 2. Exporter manuellement dans la session actuelle

```bash
export LANG=en_US.UTF-8
export LANGUAGE=en_US
export LC_ALL=en_US.UTF-8
```

Vérifie :

```bash
locale
```

Doit afficher uniquement `en_US.UTF-8` partout.

---

### 3. Rendre la configuration persistante

Édite le fichier `/etc/environment` :

```bash
nano /etc/environment
```

Et mets :

```
LANG=en_US.UTF-8
LANGUAGE=en_US
LC_ALL=en_US.UTF-8
```

Recharge (ou reboot) :

```bash
source /etc/environment
```

---

## 🇫🇷 Option : passer le système en français (`fr_FR.UTF-8`)

### 1. Activer la locale française

```bash
dpkg-reconfigure locales
```

✔️ Active :

* `en_US.UTF-8 UTF-8`
* `fr_FR.UTF-8 UTF-8`

✔️ Choisis : `fr_FR.UTF-8` comme locale par défaut

---

### 2. Modifier `/etc/environment` :

```bash
nano /etc/environment
```

Remplace par :

```
LANG=fr_FR.UTF-8
LANGUAGE=fr_FR
LC_ALL=fr_FR.UTF-8
```

---

### 3. Recharger la configuration :

```bash
source /etc/environment
```

ou

```bash
reboot
```

---

## 🔪 Vérification finale

```bash
locale
```

Et test :

```bash
perl -e ""
```

⚠️ Plus aucune erreur ne doit s’afficher.
