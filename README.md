# crAPI-
**OWASP API Top 10 (2023) - Detailed Explanation with issue and practical**

**Vulnerable Target – crAPI**

**API 01:2023 — Broken Object Level Authorization (BOLA)**

**🔍 Issue:**

APIs expose object IDs in requests.

Attackers modify object IDs to access unauthorized resources**.**

**🔨 Exploitation :**

First logging in the application and intercept the location end point

![](attachment:f3347b31-1493-4d53-8bea-979b0a8de51e:image1.png)

**And go to the community section for test bola and intercept this request and I copied vehicle id**

![](attachment:a7b99cb3-ba03-43b1-847e-71198e6aef57:image2.png)

**And copied vehicle id change with real vehicle id and leak the information(location) of other user you can see this here this is confirm to bola**

![](attachment:975304db-2952-4810-a057-0e0de3949d7a:image3.png)

**🛑 API 02:2023 —** Broken Authentication

**🔍 Issue:**

Weak authentication allows attackers to bypass login.

Issues include default passwords, no rate limiting, or JWT token flaws**.**

Click on forget password

![](attachment:6db51312-f0dd-4c89-a2b6-bc412a46f965:image4.png)

Enter the email

![](attachment:ecf862f4-5e0f-458a-857b-341493e9c98a:image5.png)

Enter the wrong otp

![](attachment:2a4cbf59-ce0b-4e8f-8c02-a198f9ada787:image6.png)

**and intercept this request**

![](attachment:92ff712c-f5a2-4b01-ab65-5ea08e733f32:image7.png)

**And send to the intruder for otp bruteforce and set the payload**

**Attack type; sniper**

**Otp set ; 0000-9999**

**Start the attack**

![](attachment:70363f46-6aea-4172-95bf-494d65060a78:image8.png)

**One thing always remember every time when you start the attack uncheck the URL-encode**

![](attachment:91f926fb-571d-4256-be6d-54f582885112:image9.png)

Here my attack is fail because of this api using v3 this not vulnerable

![](attachment:9f19ebe9-3510-4ba0-a328-fc545d0ef9a8:image10.png)

And intercept the request again and send to the intruder and change the version v3 to v2

![](attachment:15e3e402-d13b-4421-ab99-b8982dc0cc53:image11.png)

**Here is my attack is successful because of not rate limiting**

**Here allow attackers to bypass login**

![](attachment:282273e6-feff-470a-9395-a96b9f8e6257:image12.png)

**Go the browser and enter the otp**

![](attachment:44a7bc09-50cb-4880-aa43-569916e7856a:image13.png)

**Here You can bruteforce the otp with tool like hsfuzz and ffuf**

![](attachment:2697a590-24bd-4e37-b9ab-29411c19b576:image14.png)

**API 03:2023 — Broken Object Property Level Authorization**

This category combines [API3:2019 Excessive Data Exposure](https://owasp.org/API-Security/editions/2019/en/0xa3-excessive-data-exposure/) and [API6:2019 - Mass Assignment](https://owasp.org/API-Security/editions/2019/en/0xa6-mass-assignment/), focusing on the root cause: the lack of or improper authorization validation at the object property level. This leads to information exposure or manipulation by unauthorized parties.

**Exploitation;**

**Go the /shop endpoint here present three products**

![](attachment:c44546f2-ac89-419a-99a2-1df446206a52:image15.png)

**Intercept this endpoint**

![](attachment:1f8b39d2-e130-434e-b211-0e1cf3ecdd7e:image16.png)

**And change this method to POST and come bad request but you can see this below this field is required**

![](attachment:fd0eecf2-dcc9-4d55-a9e0-ec9eee27f65b:image17.png)

**And I fill-ups the required filled with Jason data send to the request and come 200 ok**

![](attachment:60d58477-d580-466c-bed7-45f7d0d73efb:image18.png)

**Retrieve the data with GET method here you can see my item(badminton) is added**

![](attachment:71749689-78a0-4c51-8b22-1f27907095b2:image19.png)

**Here You can see this item is successfully added on web application**

![](attachment:0b086e2b-572a-4255-afcb-86cee533b079:image20.png)

**🛑 API 04:2023 —** Unrestricted Resource Consumption

**🔍 Issue:**

Attackers abuse API requests to overload the system.

API has no rate limits on CPU, memory, or bandwidth usage**.**

**🔨 Exploitation ; go the the order page**

![](attachment:f4c3da6e-72b7-4622-9ec0-c1108a436061:image21.png)

**Intercept the request of order**

![](attachment:6b1f14b9-a760-41df-827e-63959aa0cd3e:image22.png)

**I increase the large limit (1000000) but come same response**

**Hit this endpoint multiple times with high limits (e.g. Burp Intruder) to:**

**Cause DoS**

**Detect if there's rate limiting**

**Observe performance impact**

![](attachment:87231aba-2774-4087-ba9f-b7ebf7113434:image23.png)

**🔒 Secure Fix (for devs):**

Server-side validation

**if limit > 100:**

return {"error": "Limit exceeds maximum allowed (100)"}, 400

🛑 **API 05:2023** — Broken Function Level Authorization

**🔍 Issue**:

Users can access admin functions due to poor role checks.

**🔨 Exploitation** :

Upload the video to click on three dot and change the name of video

![](attachment:b2b101a6-17ca-4274-ab85-63c0e7daff89:image24.png)

**Intercept the request**

![](attachment:866eb10f-c1fb-4a5b-b1ea-01960918536f:image25.png)

**Here I analyse the request using options methods to see which method is allow here.**

![](attachment:64e5f512-1f51-4359-ad12-f6ae700887f2:image26.png)

Here I choose DELETE method but come 404 and u read this message in request below

![](attachment:0289e855-0ee5-4a82-b9e0-c80cab32af06:image27.png)

**Here I change user to admin and video deleted successfully and my attack is successful to BFLA vulnerability**

![](attachment:436596f1-f865-4e52-977d-12fbe5608c70:image28.png)

**🛑 API 06:2023 —** Unrestricted Access to Sensitive Business Flows

**🔍 Issue:**

APIs expose business-critical functions without restrictions.

Attackers abuse account creation, financial transactions, etc**.**

**🔨 Exploitation :**

**Now you're sending all required fields**, and the API accepts it:

- email: attacker{}@mail.com
- password: P@ssw0rd
- name: attacker{}
- number: 123456789{}

The backend API is built using **Spring Boot**, and it’s validating input with annotations like @NotBlank. That’s why you got errors like:

![](attachment:483349a6-69af-47db-b999-00f2416d883c:image29.png)

### ✅ Why is this a vulnerability?

1. **No rate-limiting / CAPTCHA**
    
    ⇒ You can automate user signups without restriction
    
2. **No authentication needed to hit signup endpoint**
    
    ⇒ Anyone can register **multiple fake users**, maybe to:
    
    - Spam the system
    - Fill up the database
    - Use those accounts to perform further attacks
3. **Critical business flow exposed without control**
    
    ⇒ Account creation should have protections in place
    

### 💥 Vulnerability: Unrestricted Access to Sensitive Business Flows

This happens when:

- Business logic flows (like registration, password reset, checkout) are exposed without security measures
- There's no check for abuse

🛑 **API 07:2023** — Server-Side Request Forgery (SSRF)

🔍 **Issue:**

APIs allow users to request external/internal URLs.

Attackers force the server to fetch unauthorized data.

🔨 **Exploitation;**

Go the contact page

![](attachment:ac7aa3e7-e953-4ced-bb85-0a069af5f9b2:image30.png)

![](attachment:d68a4a04-3151-4c03-bd7e-a332bba58d7c:image31.png)

Intercept the request

![](attachment:bf567f00-dc25-4624-b97f-f6d5f707570a:image32.png)

Here you can check the request data send to this type

![](attachment:9f9c9fee-a406-441c-aade-2e32322b1a31:image33.png)

**Here I change the url highlighted in yellow colour and fetch of this url request this is vulnerable to ssrf**

![](attachment:a168ac41-8020-43ee-bab9-fccfe843287a:image34.png)

**SQLI Check there**

**Fetch this endpoint and intercept the burp and send to the repeater**

![](attachment:d20ab180-a1a4-4a53-9717-00ffa94a4267:image35.png)

**I try here sqli and come error this is the first clue of error based sqli**

![](attachment:72a84287-4c8d-4fdb-9031-f1200bccb059:image36.png)

**Here I using no sql payload and this successful you can see this below**

![](attachment:dafdbbdc-c58e-41f9-9910-44ab70c1fe08:image37.png)

**Here I validate the coupon**

![](attachment:917a42c6-2e19-465c-9fa8-5e575263d714:image38.png)

**Work this conform to sqli**

![](attachment:ec82637a-7959-4d34-bd4f-754d28dbb2e5:image39.png)

**Second example of sqli**

**Go to the /workshop/api/shop/apply_coupon endpoint try sql payload and come error again**

![](attachment:8e88dbe9-0b7a-4143-8058-ea9a3d25330c:image40.png)

**Use this payload to see the version you can see this below**

**‘ ; select version ();--**

![](attachment:61c0f48a-90e7-40a7-902f-11bc219f25c0:image41.png)

**See for data base use this payload**

**‘ ; select current_database ();--**

![](attachment:087dab1d-0082-447e-9286-b8df3dfcd9fc:image42.png)

**🛑 API 08:2023 —** Security Misconfiguration

**🔍 Issue:**

API has default credentials, open admin panels, or unnecessary headers.

Attackers exploit misconfigurations to access sensitive info**.**

**🔨 Exploitation Example:**

**# Checking for open API docs & admin panels**

curl -X GET "https://api.example.com/admin"

curl -X GET "https://api.example.com/swagger"

**✅ Fix:**

Disable API documentation in production.

Enforce least privilege access to admin panels.

**🛑 API 09:2023** — Improper Inventory Management

**🔍 Issue:**

APIs expose deprecated/hidden endpoints attackers can abuse.

**🔨 Exploitation Example:**

# Fuzzing for hidden API endpoints

ffuf -w wordlist.txt -u https://api.example.com/FUZZ

**✅ Fix:**

Regularly audit APIs & remove outdated endpoints.

Implement strict API versioning.

**🛑 API 10:2023 —** Unsafe Consumption of APIs

**🔍 Issue:**

API blindly trusts data from third-party APIs.

Attackers inject malicious payloads via external API calls**.**

**🔨 Exploitation Example:**

# An API integrates with an external payment system

curl -X POST "https://api.example.com/payment" -d '{"amount":"100","status":"paid"}'

**✅ Fix:**

Validate & sanitize all third-party API responses.

Implement signature-based verification for external data.
