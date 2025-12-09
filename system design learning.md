```markdown
# 15 System Design Case Studies — Simple Explanations

Below is a clean, copy-ready Markdown file summarizing all 15 cases in simple English.

---

## 1. Redis Use Cases  
Redis is like a super-fast countertop for temporary data. Apps use it for caching, queues, sessions, leaderboards, and anything that must respond instantly.

---

## 2. How Stock Exchange Works  
A stock exchange matches buy and sell orders at extreme speed. It must be fair, near-instant, and highly available, even during massive trading spikes.

---

## 3. How Spotify Works  
Spotify stores millions of songs and streams them from the closest server. It also learns your tastes using recommendation models and user behavior data.

---

## 4. How Reddit Works  
Reddit manages millions of posts and comments by caching popular content and ranking posts using algorithms so feeds load fast.

---

## 5. How Twitter Timeline Works  
Twitter pre-builds timelines for each user in the background. When you open the app, your feed appears instantly because it was prepared ahead of time.

---

## 6. How Meta Handles 11.5M Serverless Function Calls/sec  
Meta uses serverless computing that automatically scales. Smart caching, load balancing, and extremely fast cold-starts handle massive demand.

---

## 7. How Uber Finds Nearby Drivers at 1M Requests/sec  
Uber divides the map into small grid cells. When you request a ride, it looks for drivers inside your grid and nearby ones — fast and efficient.

---

## 8. How Google Docs Works  
Google Docs syncs edits instantly using algorithms that merge changes without conflicts, allowing multiple people to edit at the same time.

---

## 9. How Slack Works  
Slack uses WebSockets — always-open connections — to deliver messages instantly across channels, devices, and teams.

---

## 10. How LLMs Like ChatGPT Work  
ChatGPT predicts the next word using giant networks of numbers trained on vast amounts of text. It uses powerful GPUs to compute responses quickly.

---

## 11. How YouTube Supports 2.49B Users With MySQL  
YouTube splits (shards) user data across many MySQL databases and caches aggressively. This lets it handle billions of users without breaking.

---

## 12. How to Scale an App to 10M Users on AWS  
Scaling to millions involves load balancers, auto-scaling groups, caching, CDNs, message queues, and separating services so one component doesn't overload another.

---

## 13. How Bluesky Works  
Bluesky uses decentralized identity. Your account data isn’t locked to one company’s server — anyone can host parts of the network.

---

## 14. How URL Shortener Works  
A short URL is just a unique key mapped to a long link in a database. The system must redirect extremely fast and generate non-colliding keys.

---

## 15. How Apache Kafka Works  
Kafka is a high-speed message conveyor belt. Producers put messages on it, consumers take messages off, all with strong durability and horizontal scaling.

---

**End of File**
```
