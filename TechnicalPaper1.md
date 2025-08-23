# How Does a Browser Render HTML, CSS, and JavaScript?

Firstly, browser rendering is part of the **inner engineering side** of a browser. Many people think that writing a simple `<h1>` or `<p>` tag in an HTML file and opening it in a browser is the entire process. That idea is not completely wrong, but it misses the deeper truth.  

HTML itself is not a powerful programming language, and in fact, there is debate about whether it should be called a “programming language” at all. HTML is more like a **markup language** that describes structure. The actual work of rendering is done by complex browser engines, which are mostly written in **C++**. Modern browsers are no longer just small pieces of software; they have become full-blown systems, almost like operating systems themselves.  

---

## Behind the Scenes of a Browser

A browser has multiple important components:

- **Data Layer** → Stores cookies, local storage, and sometimes cached JavaScript.  
- **UI Layer** → The interface where users interact, see visuals, videos, images, and formatted text.  
- **Browser Engine** → Different for each browser (e.g., Blink for Chrome, WebKit for Safari), but the core logic remains the same.  
- **Rendering Engine** → Converts HTML, CSS, and JS into pixels. Responsible for creating the DOM, CSSOM, and the render tree.  
- **JavaScript Engine** → Executes JavaScript code. Chrome uses V8, Firefox uses SpiderMonkey.  
- **Network Layer** → Handles requests, responses, and communication with servers.  
- **Timers/Other Services** → Provide background tasks like scheduling events or running async scripts.  

Together, these parts make the browser far more than just a viewer of web pages. It is a powerful runtime environment.  

---

## The Rendering Mechanism

### 1. HTML Processing
- The browser’s job is to display your data and allow interaction.  
- File received = raw bytes (data).  
- **Step 1: Character Encoding** → Raw bytes are converted into characters (default: UTF-8).  
- **Step 2: Tokenization** → Characters are broken into tokens (e.g., `<h1>`, `<p>`).  
- **Step 3: Object Creation** → Tokens are converted into objects.  
- **Step 4: Relationship Building** → Defines parent-child and sibling hierarchy.  
- **Step 5: Nodes Creation** → Objects become nodes → forms the DOM (Document Object Model).  

### 2. CSS Processing
- Similar steps occur:  
  Raw data → Characters → Tokens → Objects → Relationships → **CSSOM (CSS Object Model)**.  

### 3. Render Tree Creation
- DOM + CSSOM are combined to form the Render Tree.  
- Render Tree contains only visible nodes.  
- Browser engine runs **Layout** → calculates size & position of elements.  
- **Painting** → applies styles, colors, fonts, and images.  
- **Compositing** → merges layers into the final UI displayed on screen.  

### 4. JavaScript Execution
- When JavaScript is encountered:  
  - Browser **pauses** DOM and CSSOM construction.  
  - Priority is given to executing JS.  
  - If CSSOM is not ready → **JS execution is blocked until CSSOM is complete**.
- Reason: JavaScript may query styles or modify elements → browser ensures consistency before continuing rendering.  

---

## Summary
A browser is not just a simple program but a **system with multiple engines** (rendering, JS, network). Rendering works by parsing HTML into the DOM, parsing CSS into the CSSOM, merging them into a render tree, then performing layout, painting, and compositing. JavaScript adds dynamic power but must be used carefully to avoid performance issues.  

---

## References
- [YouTube Video – How does a browser work? | Engineering Side](https://youtu.be/5rLFYtXHo9s?si=7pFf6fu0RHbdnK90)  
- [MDN Web Docs – How browsers load websites](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_browsers_load_websites)
- [ChatGPT Conversation – Browser Rendering Explanation](https://chat.openai.com/)
