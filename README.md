# Clickjacking & Reverse Tapnapping PoC

This repository contains a proof of concept (PoC) demonstrating **Clickjacking** and **Reverse Tapnapping** attacks. These attacks exploit vulnerabilities in how user interactions are handled by web browsers, particularly on mobile devices and desktop environments.

## Table of Contents
- [What is Clickjacking?](#what-is-clickjacking)
- [What is Reverse Tapnapping?](#what-is-reverse-tapnapping)
- [How to Run the PoC](#how-to-run-the-poc)
- [Demonstration](#demonstration)
- [Prevention](#prevention)
- [License](#license)

## What is Clickjacking?

Clickjacking, also known as UI redress attack, occurs when a malicious website places an invisible or disguised element (such as a button or iframe) over a legitimate user interface element. The attacker tricks users into clicking on this hidden element, resulting in unintended actions, like changing settings, initiating transactions, or even disclosing personal information.

### Example:
In this PoC (`poc_clickjacking.html`), the page is loaded inside an iframe to test whether the web application can be run within the frame. If it can, an overlay can be placed over the iframe.

## What is Reverse Tapnapping?

**Reverse Tapnapping** is a variation of tapnapping where an attacker uses a visible `<a href>` link, but when the user clicks on it, instead of navigating to the expected page, the original page containing the link gets redirected to another location. 

The user thinks they are clicking a normal link, but the click causes the page they are on (rather than the link target) to redirect. This is particularly deceptive, as it can cause confusion or trigger unintended actions without the user's knowledge.

### Example:
In this PoC (`poc_tabnabbing_tab1.html` and `poc_tabnabbing_tab2.html`), you can test how browser handles this type of attack with different atributes inside the `rel`.

## Prevention

To prevent clickjacking and reverse tapnapping attacks, the following strategies can be used:

1. **X-Frame-Options HTTP Header**: This header prevents your site from being embedded inside an iframe on malicious websites. Options include:
   - `X-Frame-Options: DENY` — Prevents all domains from framing your content.
   - `X-Frame-Options: SAMEORIGIN` — Allows only the same origin to frame your content.

2. **Content Security Policy (CSP)**: Use the `frame-ancestors` directive to control which domains can embed your content in frames.
   `Content-Security-Policy: frame-ancestors 'self';`

3. **JavaScript Defense**: You can use JavaScript to detect if your site is being loaded in an iframe and prevent certain interactions.

   `if (top !== self) { top.location = self.location; }`

4. **UI Design Best Practices**: Ensure critical actions are not buried within iframes or invisible elements, and use clear UI indications for interactive elements.

5. **Edit `rel`**: add `rel="noopener noreferrer"`

## Default Values (based on ChatGPT)
### **Google Chrome:**
- **Version 88 and later** automatically add `rel="noopener noreferrer"` to links with `target="_blank"`.

### **Mozilla Firefox:**
- **Version 85 and later** automatically add `rel="noopener noreferrer"` to links with `target="_blank"`, meaning Firefox adds both `noopener` for security and `noreferrer` to prevent sending referrer information.

### **Microsoft Edge:**
- **Version 88 and later** automatically add `rel="noopener noreferrer"` to links with `target="_blank"`.

### **Safari:**
- **Version 14 and later** automatically add `rel="noopener noreferrer"` to links with `target="_blank"`.

### **Opera:**
- **Version 74 and later** automatically add `rel="noopener noreferrer"` to links with `target="_blank"`.

## Disclaimer
> **Note:** Please use this PoC for educational purposes only. It is designed to demonstrate how these attacks work, but it should never be used for malicious intent.
