<h1 align="center">Hi 👋, I'm Rochak Prajapati</h1>
<h3 align="center">B.Tech (CSE) 5th Sem | Java Developer (Core + OOPs) | DSA Enthusiast | Aspiring Software Engineer</h3>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=rochak0001&label=Profile%20Views&color=0e75b6&style=flat" alt="rochak0001" />
</p>

---

### 👨‍💻 About Me  

- 🎓 Pursuing **B.Tech in Computer Science Engineering (5th Semester)**  
- ☕ Skilled in **Core Java and OOPs**  
- 💻 Focused on **Data Structures & Algorithms (DSA)**  
- 🧩 Solving problems on **LeetCode** & **GFG**  
- 🌱 Exploring **Backend Development** (Spring Boot, APIs)  
- 💬 Ask me about **Java, DSA, and Problem Solving**  
- ⚡ Fun fact: *I love turning logic into working code!*  

---

### 💻 Languages and Tools  

<p align="center">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white"/>
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"/>
  <img src="https://img.shields.io/badge/VS%20Code-0078D4?style=for-the-badge&logo=visualstudiocode&logoColor=white"/>
  <img src="https://img.shields.io/badge/IntelliJ%20IDEA-000000?style=for-the-badge&logo=intellijidea&logoColor=white"/>
</p>

---

### 🌐 Languages I Speak  

<p align="center">
  <img src="https://img.shields.io/badge/English-Fluent-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Hindi-Native-orange?style=for-the-badge"/>
</p>

---

### 🧠 My Focus

> “I believe mastering Data Structures and Algorithms builds the foundation of great software engineering.”

📈 Currently:
- 🔹 Solving problems on **LeetCode** and **GFG**
- 🔹 Revising **Striver’s DSA Sheet**
- 🔹 Learning **System Design Basics**
- 🔹 Working on small **Java + DSA Projects**

---

### 💡 Coding Animation  

<p align="center">
  <img src="https://media.giphy.com/media/qgQUggAC3Pfv687qPC/giphy.gif" width="400" alt="coding gif"/>
</p>

---

### ⚙️ Java & DSA Visualization Concepts  

> 💡 *Here’s a fun concept I’ve been working on — a visualization idea combining **Java Core**, **OOPs**, and **DSA** through animations and code logic.*

```js
// Java Core: Typing animation
const javaCode = `public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}`;
let index = 0;
function startTyping() {
    const display = document.getElementById('code-display');
    display.textContent = '';
    index = 0;
    const interval = setInterval(() => {
        display.textContent += javaCode[index];
        index++;
        if (index >= javaCode.length) clearInterval(interval);
    }, 100);
}

// OOPs: Simple diagram animation
function showOOPs() {
    const diagram = document.getElementById('oops-diagram');
    diagram.innerHTML = '<p>Class Animal</p><p>↓ Inheritance</p><p>Class Dog (Polymorphism)</p>';
    setTimeout(() => {
        diagram.innerHTML += '<p>Object created: Dog d = new Dog();</p>';
    }, 2000);
}

// DSA: Bubble Sort visualization
function runBubbleSort() {
    const viz = document.getElementById('sort-viz');
    let arr = [64, 34, 25, 12, 22, 11, 90];
    viz.innerHTML = arr.map(h => `<div class="bar" style="height:${h*3}px"></div>`).join('');
    bubbleSort(arr);
}

async function bubbleSort(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
                updateBars(arr);
                await sleep(500);
            }
        }
    }
}

function updateBars(arr) {
    const bars = document.querySelectorAll('.bar');
    bars.forEach((bar, i) => bar.style.height = `${arr[i]*3}px`);
}

function sleep(ms) { return new Promise(resolve => setTimeout(resolve, ms)); }

// DSA: Binary Tree growth
function growTree() {
    const viz = document.getElementById('tree-viz');
    viz.innerHTML = '<div class="node">50</div>';
    setTimeout(() => viz.innerHTML += '<div class="node">30</div><div class="node">70</div>', 1000);
    setTimeout(() => viz.innerHTML += '<div class="node">20</div><div class="node">40</div><div class="node">60</div><div class="node">80</div>', 2000);
}

// Software Dev: Debug and Deploy
function debugAndDeploy() {
    const dev = document.getElementById('debug-deploy');
    dev.innerHTML = '<p>Debugging: Error found!</p>';
    setTimeout(() => dev.innerHTML = '<p>Fixed! Deploying to cloud...</p>', 2000);
    setTimeout(() => dev.innerHTML += '<p>✅ Deployed! Software Engineer Badge Earned.</p>', 4000);
}


