# Week 3 record

Name: Sairam Boddupally  
Date: 16-10-2026

---

## 1. The finding I chose

- **File:** `src/handlers/directory.js`
- **Line:** 8–11
- **What the tool said about it:** The SQL statement is built by joining pieces of text together. If any of those pieces come from outside the application, the database may read them as part of the SQL command instead of treating them as values.

## 2. What an assistant told me

- **Assistant used:** ChatGPT
- **Its explanation, in my own words:** ChatGPT explained that the search value comes from the browser and is added directly to the SQL query. This could allow a user to change how the query works by entering specially crafted text.
- **One thing it asserted that I had not verified at that point:** I had not yet tested whether specially crafted input would actually change the search results in the running application.

## 3. What the code shows

**Where does the data come from?**

The data comes from `req.query.q` in `src/handlers/directory.js`. This is the search text entered by the user on the directory page.

**What happens to it on the way?**

The code checks whether the search value is a string. It then joins the value directly into the SQL query. The search value is not passed separately using a SQL parameter placeholder.

**Where does it become dangerous?**

The problem occurs in lines 8–11, where `q` is added directly to the SQL statement. The resulting query is passed to `db.prepare(sql).all()`. This allows specially crafted input to change the meaning of the SQL query.

**What stands in the way?**

There is no SQL parameter binding for the search value in this query. The string check only checks the type of input; it does not prevent SQL injection.

## 4. What the running application shows

**Ordinary case**

- **What I entered:** `Engineering`
- **What came back:** The directory displayed zero colleagues and showed the message “No colleagues found.”

**The case I was testing for**

- **What I entered:** `' OR '1'='1`
- **What came back:** The directory displayed three colleagues: Alice Nolan, Bob Keane and Morgan Doyle.
- **How this differs from the ordinary case:** The normal search returned zero colleagues, while the specially crafted input returned three colleagues. This showed that the input changed how the SQL query worked.

## 5. My answer

**Real**

**Why, in two or three sentences.**

I believe this is a real SQL injection vulnerability because the search input is added directly to the SQL query. When I tested the special input, the application returned three colleagues instead of zero. The code and the test results support this conclusion.

**What would change my mind.**

If the query used parameter binding for the search value and the same test treated the input only as search text, I would reconsider my conclusion for that corrected version.

**How far this answer reaches.**

I tested the directory search in the version of Atrium running locally on my computer, using the lab data. My results show that this particular search is vulnerable. I have not tested every query or every part of the application.

## 6. Back to the assistant

- **Did I check it?** Yes. I checked the source code and tested the search input in the running application.
- **Was it right?** Yes. The special input returned three colleagues, which supported the assistant's explanation that the input could change the SQL query's behaviour.

---

## Optional, if you had time

The findings in `src/db/reset.js` and `src/handlers/resources.js` use SQL parameter placeholders, with values supplied separately. The directory search in `src/handlers/directory.js` instead concatenates user input into the SQL query, which is why the three findings do not represent the same situation.