# What Atrium is
Atrium is a small internal website for a school team. It lets staff login, search for colleagues in the directory, view their own profile page, and open shared documents. I logged in as alice.nolan and I saw my own profile and team list.

Note: I asked AI and it said Atrium has admin roles too, but when I logged in I only saw normal user pages, I did not see any admin dashboard.

# Assets and Costs

1. Team Directory with names, emails, phone numbers - Cost: If a old employee still knows a password, he can login and see phone numbers and office location of all staff and call them.

2. Personal Profile Data - Cost: If someone guesses alice.nolan password, he can change her role or phone number and other staff will send private info to wrong place.

3. Private Shared Documents - Cost: A normal user who should not see salary papers can open and download confidential files from documents page.

4. Login Session Cookie - Cost: If user leaves laptop open without logout, next person can use Atrium as that user without password.

# Requirements

R1: Only users who have signed in may view the directory page at /directory. If not signed in and goes to /directory, must go to /login.

R2: A user can only edit his own profile at /profile. If user A tries to save changes to user B profile using POST /api/profile, it must give 403 error.

R3: Only users with role 'staff' can download files from /documents/confidential/. Other roles must get 403 and not get file.

R4: Atrium must logout session after 15 minutes no activity. After 15 min, if user tries to open any page that needs login, it must ask login again.

# Rejected / Rewritten

Original: "Personal data must be protected and secured appropriately."

Rewritten: I changed it to R1 above.

Reason: This original fails Test 1 because "protected" and "appropriately" is not specific, it does not say who cannot see or what page. Fails Test 2 because we cannot check it, no page name given. Fails Test 3 because not about Atrium, no /directory or /login mentioned. My R1 says /directory and /login so we can check it.

# Check for R1

Requirement checked: R1

Steps:
1. Open private window with no login.
2. Go to http://localhost:9090/directory without sign in.
3. See what happens.

Pass: It goes to /login page and team list is not shown.
Fail: It shows team list with names, emails, phone numbers without login.
Account: No account for fail check, and use alice.nolan account for pass check.