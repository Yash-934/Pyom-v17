# GitHub par Code aur APK Kaise Publish Kare

Is guide me aapko samjhaya jayega ki aap apne code aur `app-release.apk` file ko GitHub par kaise publish kar sakte hain. Iske liye alag-alag methods hain.

---

## Method 0: Naya Project GitHub par Kaise Daalein (Shuru se)

Agar aapke paas ek project hai jo aapke computer par hai, lekin GitHub par nahi hai, to use shuru se GitHub par daalne ke liye ye steps follow karein.

### Step 1: GitHub par ek nayi (khaali) Repository Banayein

1.  Apne GitHub account me login karein.
2.  Upar-right corner me `+` icon par click karein aur `New repository` chunein.
3.  Repository ko ek naam dein (jaise `My-Awesome-App`).
4.  Use `Public` ya `Private` set karein.
5.  **Important:** `Add a README file`, `Add .gitignore`, aur `Choose a license` ko **un-check** (khaali) chhod dein.
6.  `Create repository` par click karein.

Ab aapko ek page dikhega jisme kuch commands honge. Wahan se aapko HTTPS URL copy karna hai. Wo kuch aisa dikhega:
`https://github.com/YourUsername/Your-Repo-Name.git`

### Step 2: Apne Local Project me Git Shuru Karein

Apne project ke root folder me terminal open karein aur ye commands chalayein:

```bash
# Folder ko ek Git repository banata hai
git init

# Sabhi files ko pehli baar commit ke liye add karta hai
git add .

# Pehla commit banata hai
git commit -m "Initial commit"
```

### Step 3: Local Repository ko GitHub se Jodein

Ab aapko apne local project ko batana hai ki use code kahan bhejna hai. Iske liye `git remote add` command ka istemal hota hai.

```bash
# GitHub se copy kiya hua URL yahan paste karein
git remote add origin https://github.com/YourUsername/Your-Repo-Name.git
```

### Step 4: Apne Code ko GitHub par Push Karein

Aakhri step me, apne local code ko GitHub par push karein. `-u` flag pehli baar ke liye zaroori hai, taaki aapka local `main` branch, remote `main` branch se jud jaye.

```bash
git push -u origin main
```

Iske baad, aapka poora project GitHub par upload ho jayega!

---

## Method 1: Normal Code Push Karna (Roz ke kaam ke liye)

Ek baar project GitHub par aa jaye, to uske baad koi bhi badlav push karne ke liye ye commands istemal hote hain:

### Step 1: Badlav ko Staging me Add Kare
```bash
git add .
```

### Step 2: Badlav ko Commit Kare
```bash
git commit -m "Aapke badlav ka chota sa description"
```
*Jaise: `git commit -m "User login screen banaya"`*

### Step 3: Commits ko GitHub par Push Kare
```bash
git push
```

---

## Method 2: APK File ko Force Push Karna (Not Recommended)

`app-release.apk` jaisi badi files ko seedhe Git repository me push karna **acchi practice nahi maani jaati hai**. Isse repository ka size badh jaata hai. Lekin agar aapko turant file share karni hai, to yah ek quick solution hai.

### Step 1: APK File ko Force-Add Kare
```bash
git add -f build/app/outputs/flutter-apk/app-release.apk
```

### Step 2: APK ko Commit aur Push Kare
```bash
git commit -m "Release APK add kiya"
git push
```

**Zaroori Suchna:** Iska istemal sirf temporary zaroorat ke liye karein. **Permanent solution ke liye Method 3 ka istemal karein.**

---

## Method 3: Version Release Banana (Recommended for APK)

Yahi APK ya kisi bhi software ko release karne ka sabse professional aur sahi tareeka hai. Isse aapki Git history saaf rehti hai.

### Step 0: GitHub CLI me Login Karna (Sirf ek baar)
Release banane ke liye hum `gh` (GitHub CLI) tool ka istemal karte hain. Ise pehli baar istemal karne se pehle aapko login karna hoga.

```bash
gh auth login
```
Iske baad diye gaye steps follow karke browser me authentication poora karein.

### Step 1: Naya Git Tag Banana
```bash
git tag -a v1.0 -m "Version 1.0: Initial Release"
```

### Step 2: Tag ko GitHub par Push Karna
```bash
git push origin v1.0
```

### Step 3: GitHub Release Banana aur APK Upload Karna
```bash
gh release create v1.0 build/app/outputs/flutter-apk/app-release.apk -t "Version 1.0" -n "Release notes yahan likhein."
```
Is command ke baad, aapko ek link milega jahan se koi bhi aapka APK download kar sakta hai.
