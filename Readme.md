<div align="center">

# 🧠 SIP Problem Sums — Class 2

### 100 Mixed Arithmetic Word Problems

Practise addition, subtraction, multiplication, and division with a fixed set of 100 word problems. Enter your answers, check your score, reveal solutions, or print a worksheet.

<p>
  <a href="#-features"><img src="https://img.shields.io/badge/✨_Features-Explore-0b63d5?style=for-the-badge" alt="Features"></a>
  <a href="#-installation"><img src="https://img.shields.io/badge/🚀_Setup-Get_Started-2ea44f?style=for-the-badge" alt="Setup"></a>
  <a href="#-how-to-use"><img src="https://img.shields.io/badge/📘_How_to_Use-Guide-7b61ff?style=for-the-badge" alt="Usage guide"></a>
</p>

<p>
  <img src="https://img.shields.io/badge/HTML5-Structure-e34f26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/CSS3-Responsive_Design-1572b6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3">
  <img src="https://img.shields.io/badge/JavaScript-Interactive-f7df1e?style=for-the-badge&logo=javascript&logoColor=222" alt="JavaScript">
  <img src="https://img.shields.io/badge/100-Word_Problems-orange?style=for-the-badge" alt="100 word problems">
  <img src="https://img.shields.io/badge/Works_Offline-Yes-2ea44f?style=for-the-badge" alt="Works offline">
</p>

</div>

---

## 📚 Contents

- [Overview](#-overview)
- [Features](#-features)
- [Installation](#-installation)
- [How to Use](#-how-to-use)
- [Question Set](#-question-set)
- [Printing and PDF](#️-printing-and-pdf)
- [Technologies](#️-technologies)
- [Limitations](#️-limitations)

## 📖 Overview

**SIP Problem Sums — 100 Questions** is a simple, browser-based practice worksheet aimed at Class 2 / contest-style arithmetic. It contains 100 word problems covering the four basic operations: addition, subtraction, multiplication, and division.

The page runs entirely in the browser using plain HTML, CSS, and JavaScript. No server, account, or external library is required.

## ✨ Features

<table>
<tr>
<td width="50%">

### 🧮 Fixed Set of 100 Questions
- Includes 100 pre-written word problems.
- Covers addition, subtraction, multiplication, and division.
- Uses everyday contexts such as toys, food, money, books, and groups of objects.
- Randomizes the order when a new set is generated.

</td>
<td width="50%">

### ✍️ Answer Entry
- Type a numeric answer below each problem.
- Uses number inputs with mobile-friendly numeric keyboards.
- Questions are arranged in two columns on wide screens.

</td>
</tr>
<tr>
<td width="50%">

### ✅ Instant Results
- Checks all entered answers in one action.
- Shows a score out of 100.
- Highlights correct answers in green.
- Shows incorrect or unanswered questions and their correct answers in red.

</td>
<td width="50%">

### 💡 Solutions and Printing
- Reveals the complete answer key.
- Prints the worksheet using the browser print dialog.
- Supports the browser's **Save as PDF** option.
- Includes print-specific styling for paper output.

</td>
</tr>
</table>

## 🚀 Installation

### 1. Save the file

Save the supplied HTML code as:

```text
index.html
```

A minimal project folder can look like this:

```text
sip-problem-sums/
└── index.html
```

### 2. Open it in a browser

Double-click `index.html`, or open it using Chrome, Edge, Firefox, or another modern browser.

That's it. There are no packages to install and no build step.

## 📘 How to Use

1. **Open the page** in your browser.
2. **Solve the questions** by entering a numeric answer in each input box.
3. Select **Check Answers** to see your score and feedback for each question.
4. Select **Show Solutions** to reveal the correct answer for every problem.
5. Select **New Set (Regenerate)** to shuffle the existing 100 questions into a different order.
6. Select **Print / Save as PDF** to print the worksheet or save it as a PDF.

If you have entered answers, the New Set button asks for confirmation before clearing them.

## 🧮 Question Set

The 100 questions are stored directly in the JavaScript `ORIGINAL` array. Each entry contains the wording of a problem and its expected numeric answer.

The set includes scenarios involving:

- Adding quantities together
- Finding what remains after items are removed
- Equal groups and repeated quantities
- Sharing objects equally
- Basic money and measurement contexts

### How regeneration works

The **New Set** button does not create new problems or change the numbers. It shuffles a copy of the existing list, so the same 100 questions appear in a different order.

## 🖨️ Printing and PDF

1. Click **Print / Save as PDF**.
2. In the browser print dialog, choose a printer or **Save as PDF**.
3. Adjust paper size, margins, and scale if necessary.
4. Print or save the file.

The page includes a print stylesheet to improve paper output. The controls and footer are hidden while printing, and the results panel is configured to display.

## 🛠️ Technologies

| Technology | Role |
|---|---|
| HTML | Page structure, question cards, answer inputs, and results panel |
| CSS | Colors, responsive two-column layout, answer feedback, and print styles |
| JavaScript | Stores the questions, shuffles their order, checks answers, calculates scores, and displays solutions |

## 📱 Responsive Layout

On larger screens, the worksheet uses two columns. At widths of **900 px or less**, it switches to a single-column layout to make questions easier to read on smaller screens.

## ⚠️ Limitations

- The question bank is fixed at 100 problems.
- Regeneration shuffles the question order; it does not generate new problem text or values.
- Scores and answers are not saved to a server or database.
- Refreshing or closing the page loses the current answers.
- The answer checker compares numeric values only; it does not accept written explanations.
- There are no student accounts, teacher dashboard, timer, or persistent progress tracking in the current version.
- The logo image element has an empty `src` in the supplied HTML, so no logo will appear unless an image path is added.

## 💡 Possible Future Improvements

Potential additions for a future version include:

- Difficulty levels or selectable question categories
- A timer for contest practice
- Student name and date fields
- A separate printable answer key
- Score history saved locally
- New randomized question banks
- Optional logo upload or a configurable logo path

These are suggestions only and are not part of the current code.

---

<div align="center">

**Made for simple, offline arithmetic practice**

HTML · CSS · JavaScript

[⬆ Back to top](#-sip-problem-sums--class-2)

</div>
