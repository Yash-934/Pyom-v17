
# GitHub par Code aur APK Kaise Publish Kare

Is guide me aapko samjhaya jayega ki aap apne code aur `app-release.apk` file ko GitHub par kaise publish kar sakte hain. Iske liye 3 tareeke hain.

---

## Method 1: Normal Code Push Karna (Roz ke kaam ke liye)

Jab bhi aap apne code me koi badlav karte hain (jaise ki `lib/main.dart` me kuch change karna), to use GitHub par push karne ke liye ye standard commands hain:

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
In teen commands se aapka code aapki GitHub repository me update ho jayega.

---

## Method 2: APK File ko Force Push Karna (Not Recommended)

`app-release.apk` jaisi badi files ko seedhe Git repository me push karna **acchi practice nahi maani jaati hai**. Isse repository ka size badh jaata hai. Lekin agar aapko turant file share karni hai, to yah ek quick solution hai.

### Samasya: `.gitignore` file
Aapke project me ek `.gitignore` file hai jo `build` folder ko ignore karti hai. Isi vajah se `git add` command ispar kaam nahi karta.

### Samadhan: Force Add (`-f` flag)
Is samasya ko bypass karne ke liye, hum `git add` command ke saath `-f` (force) flag ka istemal kar sakte hain.

#### Step 1: APK File ko Force-Add Kare
```bash
git add -f build/app/outputs/flutter-apk/app-release.apk
```

#### Step 2: APK ko Commit aur Push Kare
```bash
git commit -m "Release APK add kiya"
git push
```

**Zaroori Suchna:** Iska istemal sirf temporary zaroorat ke liye karein. **Permanent solution ke liye Method 3 ka istemal karein.**

---

## Method 3: Version Release Banana (Recommended for APK)

Yahi APK ya kisi bhi software ko release karne ka sabse professional aur sahi tareeka hai. Isse aapki Git history saaf rehti hai aur koi bhi user aasani se alag-alag version download kar sakta hai.

Iske liye hum **Git Tags** aur **GitHub Releases** ka istemal karte hain.

### Step 0: GitHub CLI me Login Karna (Sirf ek baar)
Release banane ke liye hum `gh` (GitHub CLI) tool ka istemal karte hain. Ise pehli baar istemal karne se pehle aapko login karna hoga.

```bash
gh auth login
```

Is command ko chalane ke baad, aapse kuch sawal pooche jayenge:
1.  `What account do you want to log into?` -> `GitHub.com` chunein.
2.  `What is your preferred protocol for Git operations?` -> `HTTPS` chunein.
3.  `Authenticate Git with your GitHub credentials?` -> `Y` (Yes) chunein.
4.  `How would you like to authenticate?` -> `Login with a web browser` chunein.

Iske baad, aapko ek one-time code milega aur ek link open hogi. Us code ko browser me paste karke authentication poora karein.

### Step 1: Naya Git Tag Banana
Pehle, hum apne code ke current state ko ek version number (jaise `v1.0`) se "tag" karenge. Yah aapke project ka ek permanent snapshot bana deta hai.

```bash
git tag -a v1.0 -m "Version 1.0: Initial Release"
```
*Aap `v1.0` ki jagah `v1.1` ya koi aur naya version number de sakte hain. Message me us version ke baare me likhein.*

### Step 2: Tag ko GitHub par Push Karna
Ab is tag ko aapki GitHub repository me push karna hoga.
```bash
git push origin v1.0
```
*(Yahan bhi `v1.0` ki jagah aapka naya tag name aayega)*

### Step 3: GitHub Release Banana aur APK Upload Karna
Login aur Tag push hone ke baad, aap is command se ek naya release bana sakte hain aur apni `app-release.apk` file uske saath "Asset" ke roop me jod sakte hain.

```bash
gh release create v1.0 build/app/outputs/flutter-apk/app-release.apk -t "Version 1.0" -n "Is release me kya khaas hai, uska description yahan likhein."
```

*   `v1.0`: Aapka tag name.
*   `build/app/outputs/flutter-apk/app-release.apk`: Aapki APK file ka path.
*   `-t`: Release ka Title.
*   `-n`: Release ke notes ya description.

Is command ke chalne ke baad, aapko ek link milega. Us link par jaakar koi bhi `app-release.apk` ko **Assets** section se download kar sakta hai.
