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
