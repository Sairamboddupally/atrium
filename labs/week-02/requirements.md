# Week 2 security requirements
Your name: Sairam Boddupally
Date: Oct 3 2026
## 1. What this application is
Atrium is a small internal website for a school team. It has a Directory page with 3 users and a Documents page with 5 files. Users must log in to see them. It runs at localhost:9090 for internal use only.

Where assistant explanation did not match: Nothing found. I checked localhost:9090 and it matches.

## 2. What is worth protecting
| Asset | What it costs if this goes wrong |
| User passwords | Account takeover if seen |
| Session cookies | Hijack without password |
| Private documents | Privacy leak |
| User profile data | Wrong info shown |

## 3. The requirements
1. A user who is not logged in is not allowed to see the Directory or Documents pages.
2. User A is not allowed to see User B's private documents.
3. A regular user is not allowed to change or delete another user's profile.
4. A user is not allowed to stay logged in forever - session must expire.

Which did you write yourself: I wrote 1 and 2 myself. 3 and 4 started as draft from assistant and I rewrote.

## 4. One I rejected or rewrote
- The original sentence: "Nobody is allowed to do anything bad"
- My version: "A user who is not logged in is not allowed to view the Documents page because documents are private"
- Why I changed it: Original was too vague. I made it specific about who, what, and why.

## 5. How somebody would check one of these
Pick one requirement: Requirement 1 - not logged in cannot see Documents.
Steps:
- Sign out, try to go to /documents directly
- What would mean it is met: Redirected to login page
- What would mean it is not met: Documents page shows without login

## Optional, if you had time
My order: 1, 3, 2, 4. 1 is most important because it protects everything. 3 next because profile changes affect others.
