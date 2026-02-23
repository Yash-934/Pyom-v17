# GitHub par Code aur APK Kaise Push Kare

Is guide me aapko samjhaya jayega ki aap apne code aur `app-release.apk` file ko GitHub par kaise push kar sakte hain.

## 1. Normal Code Push Karna

Jab bhi aap apne code me koi badlav karte hain (jaise ki `lib/main.dart` me kuch change karna), to use GitHub par push karne ke liye ye standard commands hain:

### Step 1: Badlav ko Staging me Add Kare

Sabse pehle, aapko Git ko batana hota hai ki aap kaun si files ke badlav ko commit karna chahte hain. Aap ek-ek file ka naam de sakte hain ya `.` istemal karke sabhi modified files ko add kar sakte hain.

```bash
git add .
```

### Step 2: Badlav ko Commit Kare

Ab in badlavon ko ek message ke saath commit karein. Message me yah likhna accha rehta hai ki aapne kya changes kiye hain.

```bash
git commit -m "Aapke badlav ka chota sa description"
```
*Jaise: `git commit -m "User login screen banaya"`*

### Step 3: Commits ko GitHub par Push Kare

Aakhri step me, apne local commits ko GitHub server par bhej de.

```bash
git push
```

In teen commands se aapka code aapki GitHub repository me update ho jayega.

---

## 2. APK File Push Karna (Special Case)

`app-release.apk` jaisi badi files ko Git repository me push karna normal practice nahi hai, lekin agar aapko yah karna zaroori hai, to niche diye gaye tarike se kar sakte hain.

### Samasya: `.gitignore` file

Aapke project me ek `.gitignore` naam ki file hai. Is file me un sabhi files aur folders ke naam likhe hote hain jinhe Git ko ignore karna chahiye. `build` folder bhi is list me shamil hota hai, kyunki isme temporary aur badi-badi generated files hoti hain.

Isi vajah se, jab aap normal `git add` command se APK ko add karne ki koshish karte hain, to Git use ignore kar deta hai aur ek error dikhata hai.

### Samadhan: Force Add (`-f` flag)

Is samasya ko bypass karne ke liye, hum `git add` command ke saath `-f` (force) flag ka istemal kar sakte hain. Yah Git ko majboor karta hai ki woh `.gitignore` me likhi hui file ko bhi add kar le.

### Step 1: APK File ko Force-Add Kare

Apni `app-release.apk` file ko force ke saath staging me add karein.

```bash
git add -f build/app/outputs/flutter-apk/app-release.apk
```

### Step 2: APK ko Commit Kare

APK file ke liye ek alag commit banayein.

```bash
git commit -m "Release APK add kiya"
```

### Step 3: Commit ko Push Kare

Aakhri me, is commit ko GitHub par push kar de.

```bash
git push
```

**Zaroori Suchna (Important Note):** Badi files (jaise APK, video, zip) ko Git me baar-baar push karne se aapki repository ka size bahut zyada badh sakta hai aur use clone karne me bahut time lag sakta hai. Yah tarika sirf zaroorat padne par hi istemal karein. Behtar tarika `Git LFS` (Large File Storage) ya fir APK ko release assets ke taur par GitHub par upload karna hota hai.
