# Survive Game

**A simple Android survival game based on a national ID number.**  
Enter your 9-digit ID, follow the correct steps, and see if you survive and reach your destination city!

---

## Gameplay Overview

- The user enters a 9-digit ID number.
- The app converts each digit to a direction using `digit % 4`.
- The player must click the corresponding arrows in the correct sequence:
  - `0` = left  
  - `1` = right  
  - `2` = up  
  - `3` = down
- When finished:
  - If all steps are correct → `Toast: "Survived in [City]"`
  - If a mistake is made → `Toast: "You Failed"`

---

## How the City is Determined

The app fetches a list of cities from:

```
https://pastebin.com/raw/T67TVJG9
```

The city is selected based on the 8th digit of the ID:

```java
state = data.split(",")[Integer.parseInt(id.charAt(7) + "")];
```

---

## Example Result

- ID entered: `111111111`
- Calculated steps: `1 1 1 1 1 1 1 1 1` → must press **right** 9 times  
- 8th digit: `1` → second city in the list → **Texas**
- Toast displayed:  
  `Survived in Texas`

---

## Bugs Fixed During the Process

### 1. Toast duration 

**Before:**
```java
Toast.makeText(this, "Survived in " + state, 1).show();
```

**After:**
```java
Toast.makeText(this, "Survived in " + state, Toast.LENGTH_LONG).show();
```

### 2. URL contained hidden zero-width characters

**Before (broken URL):**
```
https://pastebin.com/raw/%E2%80%8C%E2%80%8C%E2%80%8CT67TVJG9
```

**After (fixed):**
```
https://pastebin.com/raw/T67TVJG9
```

**Explanation:**  
The original URL included invisible RTL characters that silently broke the fetch request.  
Fix: manually typed the correct URL into `strings.xml`.

---

## Work Summary

- Decompiled APK using [Java Decompilers](http://www.javadecompilers.com/) to access the source code
- Found activities in folders and required files (`R.string.url`, `ic_*.xml`, etc.)
- Reconstructed source code manually in Android Studio
- Fixed logic bugs and UI issues
- Rebuilt manifest and layout structure
- Verified correct behavior with working example ID

---

## How to Run

1. Open the project in Android Studio
2. Run on a device or emulator
3. Enter a 9-digit ID (e.g., `111111111`)
4. Follow the steps in order to survive
5. If successful, the app will show a success toast with the city name

---

## Screenshots


https://github.com/user-attachments/assets/e62bc7e8-fee1-43da-93f9-9048b675c321



---

## Author

Reverse engineering project  
By: Gal Yaish
