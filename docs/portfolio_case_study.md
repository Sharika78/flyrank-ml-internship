# Portfolio Case Study & Framing

## 1. Voice Card
> Direct, honest, grounded, practical, no buzzwords.

---

## 2. Case Study: FlyRank Content Refresh & Decay Prediction

### The Problem
Editorial teams waste massive amounts of time trying to figure out which web pages are losing search traffic. Relying on gut feeling or rigid, blunt rules (like "flag any page with a 20% traffic drop") leads to false alarms, missing seasonal dips, and exhausting manual reviews.

### What I Did & Decided
* **Framed the Task:** Defined this as a binary classification problem instead of an open-ended analysis, splitting pages into those needing an immediate editorial refresh versus stable ones.
* **Protected Against Leakage:** Deliberately designed the target variable while strictly excluding raw future trend signals to prevent data leakage.
* **Aligned with Constraints:** Focused optimization on Precision@50 because editorial teams only have the bandwidth to review top-ranked flagged pages each week.

### What Came of It
Built a clean, reproducible task framing and baseline model pipeline in Python/Pandas that achieved a clear empirical lift (~3x higher Precision@50) compared to naive static rules, giving content teams a reliable, prioritized action list.

---

## 3. Bio & Contact / CTA

### Bio
Hi, I’m Abida Sultana Sharika—a Computer Science student and aspiring Machine Learning Engineer based in Dhaka. I build practical classification models and focus on turning messy data into clean, functional solutions.

### Contact / CTA
* Want to collaborate or look at my code? Check out my GitHub Repository or connect with me on LinkedIn. Let’s build something useful.

---

## 4. Before / After Edit (The Voice Test)

* **Generic AI Line:** 
  > "Leveraging cutting-edge predictive analytics and state-of-the-art machine learning algorithms to maximize organizational synergy and drive disruptive content optimization outcomes."
* **My Edited Version:** 
  > "Using binary classification to flag declining web pages accurately, so editors fix the right content instead of guessing."
